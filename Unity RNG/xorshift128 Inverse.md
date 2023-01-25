The xorshift128 algorithm is centred around this step function:
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

We can use this to [[xorshift128 Matrix|construct a matrix]] and find it's inverse, which allows us to step backwards as far as we want. However, Matrix multiplication is not the fastest, and working with matrices over fields other than $\R$ is rarely an option in linear algebra libraries.

As such, we want to determine the inverse function of `step_rng`, in the hopes that it will make a brute-force search through possible states a bit faster.

# The Inverse
The only step that takes some work to reverse is step 3, and it turns out to be the exact same calculations in the opposite order. This is because the shift-and-xor operation is a nilpotent linear transformation (it is its own inverse), and when inverting a sequence of linear transformations, you perform each individual inverse in the reverse order.

As such, the entire reversed state-step is:
```rust
fn step_back(state: &mut [u32; 4]) {
    // Undo step 4
    let s: u32 = state[1];
    let mut t: u32 = state[0] ^ s ^ (s >> 19);

    // Undo step 3
    t = t ^ (t >> 8);
    t = t ^ (t << 11);

    // Undo Rotate
    state[0] = state[1];
    state[1] = state[2];
    state[2] = state[3];
    state[3] = t;
}
```