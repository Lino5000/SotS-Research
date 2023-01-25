In order to properly [[RNG Notes#Breaking the PRNG|break the RNG for Signs]], we need to be able to work more freely with the steps that the xorshift128 algorithm produces.

By re-interpreting the state as a 128-dimensional vector over the finite field $\text{GF}(2)$ (Integers modulo 2), we can find that a single step of this algorithm is in fact a linear transformation.

Using a computer algebra system (I used Magma because it was developed at USyd and so is the one I was taught), we can construct and examine the matrix that encodes this linear transformation. You can see the logs of these magma sessions [[2-1-2023.log|here]] and [[14-01-2023.log|here]], and the resulting utilities library [[xorshift128-tools.txt|here]].

This Matrix allows us to quickly jump forward and backward in the RNG sequence, but it isn't particularly useful for initially determining the state, mostly due to the nature of the restrictions that are provided by gameplay. For that we will likely perform a brute-force search using the faster [[xorshift128 Inverse|inverse function]].

