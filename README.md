## ExploringSuperposition

This repository contains Q# code for exploring superpositions of qubit registers. The code demonstrates the generation of a random number using a uniform superposition of qubits.

### Prerequisites

- [.NET Core SDK](https://dotnet.microsoft.com/download) (version 3.1 or later)
- [Q# development environment](https://docs.microsoft.com/en-us/quantum/quickstarts/install-sdk) (including the Q# compiler)

### Code Explanation

The code in the `ExploringSuperposition` namespace demonstrates the generation of a random number using a uniform superposition of qubits. The qubit register consists of three qubits, resulting in eight possible basis states.

The arbitrary three-qubit state can be expressed as:

```
|ψ⟩ = a0|000⟩ + a1|001⟩ + a2|010⟩ + a3|011⟩ + a4|100⟩ + a5|101⟩ + a6|110⟩ + a7|111⟩
```

Here, `ai` represents complex numbers that satisfy the condition `∑|ai|^2 = 1`.

The code applies a Hadamard gate to each qubit to create a uniform superposition. The resulting superposition state is then measured, collapsing it to a basis state. The collapsed state is converted to an integer value, representing the generated random number.

### Usage

To run the code, use the following command in the terminal:

```
dotnet run
```
