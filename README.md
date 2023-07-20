# Exploring Interference

This repository contains Q# code for exploring interference in quantum systems.

## Prerequisites

To run the code in this repository, you need to have the following installed:

- [.NET Core SDK](https://dotnet.microsoft.com/download) (version 3.1 or higher)
- [Q# development kit](https://docs.microsoft.com/en-us/quantum/install-guide/)

## Getting Started

To run the code, follow these steps:

1. Clone this repository to your local machine.

   ```
   git clone https://github.com/IGORSVOLOHOVS/microsoft-azure-quantum-learning.git
   ```
2. Navigate to the project directory.

   ```
   cd microsoft-azure-quantum-learning
   ```
3. Build the project.

   ```
   dotnet build
   ```
4. Run the project.

   ```
   dotnet run
   ```

## Code Description

The code in the `ExploringInterference.qs` file explores interference in a quantum system. It defines the `TestInterference1` operation as the entry point. This operation demonstrates interference by applying the Hadamard (H) gate to a qubit and observing the resulting superposition.
