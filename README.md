# Johnson Trotter algorithm

Each permutation in the [Johnson Trotter algorithm](https://en.wikipedia.org/wiki/Steinhaus%E2%80%93Johnson%E2%80%93Trotter_algorithm) differs from the previous one by swapping two adjacent elements of the sequence.

The main benefit of this is that it can calculate and return one permutation at a time, instead of requiring all permutations to be found at once.

This means that you can analyse the permutations it creates one at a time, which in turn means that you can stop calculating more permutations when you are done, which in turn means that you can analyse lists of any size without causing a stack overflow.

The `Step` type represents the next permutation, if there is one.

```
type Step a
    = Done
    | Next (State a) (List a)
```

`State` is an opaque type, so to create the first `Step` you have to call `first`.

The `next` function returns the next `Step` in the sequence. It requires a `State`, which `getState` returns. The `getPermutation` helper function returns the permutation.

```elm
    JohnsonTrotter.first [ "a", "b", "c" ]
        |> JohnsonTrotter.getState
        |> Maybe.map JohnsonTrotter.next
        |> Maybe.andThen JohnsonTrotter.getPermutation
    -- [ "a", "c", "b" ]
```
