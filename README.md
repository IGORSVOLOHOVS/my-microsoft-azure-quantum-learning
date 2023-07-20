
# Explore entanglement

This repository contains Q# (Q Sharp) code for Explore entanglement in quantum systems.

## Code Description

The `ExploreEntanglement` namespace contains the following Q# operations:

### SetQubitState

```Q#
operation SetQubitState(desired : Result, target : Qubit) : Unit {
    if desired != M(target) {
        X(target);
    }
}
```

This operation sets the state of a target qubit to the desired state, where the desired state is specified as a `Result` (either `Zero` or `One`). If the current state of the qubit does not match the desired state, the X gate is applied to the qubit.

### TestBellState

```Q#
operation TestBellState(count : Int, initial : Result) : (Int, Int, Int, Int) {
    // ...
}
```

This operation tests the Bell state by measuring a pair of qubits repeatedly. The `count` parameter specifies the number of measurements to be performed, and the `initial` parameter specifies the initial state of the first qubit. The operation returns a tuple `(numZerosQ1, numOnesQ1, numZerosQ2, numOnesQ2)` representing the number of `Zero` and `One` measurements obtained for each qubit.

## Running the Code

To run the code, execute the following command:

```shell
dotnet run --count 1000 --initial 1
```

This command will run the `TestBellState` operation with a count of 1000 measurements and an initial state of `One` for the first qubit.

Feel free to modify the command-line arguments (`--count` and `--initial`) according to your requirements.
