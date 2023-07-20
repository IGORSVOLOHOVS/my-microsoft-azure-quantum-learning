# Exploring Superposition

This repository contains code written in Q# (Q Sharp) for exploring superposition. The code demonstrates the generation of a random bit using the concept of superposition in quantum computing.

## Prerequisites

- [.NET Core SDK](https://dotnet.microsoft.com/download) installed.

## How to Run

To execute the code, follow the steps below:

1. Clone this repository to your local machine.
2. Open a terminal or command prompt and navigate to the cloned repository's directory.
3. Run the following command to execute the code:

```
dotnet run
```

## Code Description

The code is organized into a single Q# namespace called `ExploringSuperposition`. It utilizes the following Q# libraries:

- `Microsoft.Quantum.Canon`: Provides commonly used operations and functions in quantum programming.
- `Microsoft.Quantum.Intrinsic`: Contains fundamental quantum operations and gates.
- `Microsoft.Quantum.Diagnostics`: Offers diagnostics capabilities for quantum programs.
- `Microsoft.Quantum.Measurement`: Provides measurement-related operations.

The main entry point operation is `GenerateRandomBit`, which demonstrates the generation of a random bit using superposition. The code performs the following steps:

1. Initializes a qubit and displays the state of the quantum machine.
2. Applies the Hadamard gate (H) to put the qubit into superposition.
3. Measures the qubit to obtain a random bit and displays the state of the quantum machine.
4. Resets the qubit to its initial state and displays the state of the quantum machine.
5. Returns the random bit as the output.
