
## Entanglement between two qubits

This repository contains Q# (Q Sharp) code for exploring entanglement in quantum computing.

### Prerequisites

To run the code in this repository, you need to have the following installed:

- .NET Core SDK
- Q# Development Kit

### Usage

To run the code and execute the `TestBellState` operation, follow these steps:

1. Clone this repository to your local machine.
2. Open a terminal or command prompt and navigate to the repository's directory.
3. Run the following command:

   ```shell
   dotnet run --count 1000 --initial 1
   ```

   This will execute the `TestBellState` operation with a count of 1000 and an initial state of 1.
4. Observe the output, which will display the number of |0> and |1> states for qubits q1 and q2.

### Code Explanation

The `ExploreEntanglement` namespace contains the following operations:

- `SetQubitState`: Sets the state of a target qubit to the desired state (either |0> or |1>).
- `TestBellState`: Tests the entanglement of two qubits by creating a Bell state and measuring the qubits. The operation takes two parameters: `count` (the number of times to repeat the experiment) and `initial` (the initial state of the qubits).

