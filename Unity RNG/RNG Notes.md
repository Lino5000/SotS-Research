Most of the RNG of the game makes use of Unity's built-in `UnityEngine.Random` PRNG, which uses the [xorshift128 algorithm](https://en.wikipedia.org/wiki/Xorshift#Example_implementation).

There seem to be two RNG states used:

# 'Standard' RNG
This is the default RNG that is used by the game for various things, such as:
- Angles of character portraits.
- `Flickerer` effect.
- Various other animation randomness.

# Important RNG
For some uses, the game switches out the internal state of the PRNG using the `SaveManager.ImportantRandomStart()` and `SaveManager.ImportantRandomEnd()` methods.

This 'Important RNG' is used for the following things:
- The small amount of randomness involved in conversations; see [[Game Sequence]].
- Every time you start travelling along a road, one call is made to see if a special event will occur. This is approximately equivalent to a 1/3 chance for each dot on the road.
    - If one will occur, 3 more calls are made to see which event it will be, and when in the journey it will be. (see `FlowState.Map` case in `FlowX`)
    - If the event is of the right type and the player chooses to follow it, more calls will occur to choose which card in the deck to replace / copy.

# Breaking the PRNG
To be able to break the xorshift128 algorithm that Unity uses, we first need to understand how it works. Most of the following is drawn directly from the [relevant Wikipedia article](https://en.wikipedia.org/wiki/Xorshift#Example_implementation).

## How does xorshift128 work?
The internal state of this PRNG is a set of four 32-bit unsigned integers, often stored either as an array, or as a single 128-bit value. For this discussion, we will refer to this state as if it were declared as
```rust
state: [u32; 4];
```

Each step of the PRNG returns a 32-bit value, and then mutates the state. The steps are as follows:
1) Save the last element of the state into a temporary `t: u32`.
2) Rotate the elements of the array to the right, so that `state[3]` moves to `state[0]`.
3) Do some in-place XORs of `t` with shifted versions of itself.
4) Replace `state[0]` (which is what `t` started as; it was moved by the rotation) with some more XOR math combining `t` with another part of the state (namely the value of `state[1]` post-rotation, which was in `state[0]`).
5) Return the new `state[0]` value.

In Rust code, we have:
```rust
fn step_rng(state: &mut [u32; 4]) -> u32 {
    // 1) Save element
    let mut t: u32 = state[3];

    // 2) Perform rotation of array
    // Don't bother setting `state[0]` 
    //  because we overwrite it anyway.
    let s: u32 = state[0];
    state[3] = state[2];
    state[2] = state[1];
    state[1] = s;

    // 3) In-place XORs of t
    t = t ^ (t << 11);
    t = t ^ (t >> 8);

    // 4) Combine `t` and `s` to make new `state[0]`.
    state[0] = t ^ s ^ (s >> 19);

    // 5) Return new `state[0]`.
    state[0]
}
```

In order to work with this algorithm more easily, we [[xorshift128 Matrix|re-interpret it]] into a form that we can apply some Linear Algebra to. We also find the [[xorshift128 Inverse|inverse function]] to facilitate moving single steps backward more efficiently in case the matrices are too hard to program.


On top of this, Unity does some extra processing of the output in order to provide various different types of result.
- `Random.value` takes the bottom 23 bits of the output, and divides them by $2^{23}$. This is because it should return a 32-bit float in the interval $[0, 1]$, and $2^{-23}$ is the smallest number greater than 0 that is representable in an IEEE 32-bit float.
- `Random.Range` behaves differently depending on if you want a float or an integer. 
    - For floats, it uses `Random.value` to interpolate between the endpoints of the range.
    - For integers, it takes the output modulo the size of the range, then adds the minimum.

## Breaking - Gathering Information
Since each PRNG step output is also the value of `state[0]`, if we get 4 consecutive raw outputs from the PRNG we know the entire internal state and can then predict the remainder of the sequence completely.

Unfortunately, we don't get raw outputs from the PRNG; we just get the game behaviour that is based on some logical processing of those outputs. So, we need to examine the code more closely to determine which events give us what information about the output at that step.

This information will likely not be exact, instead giving restrictions like 'float output > 0.7' and similar, so we will likely find that we need more than 4 events to fully determine the state.

This information has been collated in [[Game Sequence]].

### Gathering - The shuffles
At the start of each conversation, both decks are shuffled. If we could work out the precise shuffle that occurred (we can't due to duplicates, but we'll deal with that later), how much does that tell us about the RNG state?

Well, the number of RNG calls involved in a single shuffle is precisely 2 less than the number of cards being shuffled. Due to the design of the shuffle algorithm, and the way Unity provides random integers in a range, each of these RNG calls restricts the raw output to a particular congruence class.

Unfortunately, this sort of restriction is very difficult to propagate through the xorshift128 algorithm, so we will likely be reduced to a brute-force search through the possible states. This may still be a feasible method, since we will be working with restrictions on consecutive states, and the algorithm and it's inverse are both very fast functions to compute. On the other hand, there are $2^{128}$ possible states to search through, so we would likely need to work out some particularly effective 
