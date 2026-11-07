# my-microsoft-azure-quantum-learning

One person's notes from learning Q#, Microsoft's language for quantum computing.
The commits are the record of the topics studied, one after another:
superposition, interference, relative phases and entanglement. Only the last
exercise is in the tree today.

## What is here

- `Program.qs` is that exercise, entanglement between two qubits, in the
  namespace `ExploreEntanglement`. `SetQubitState` puts a qubit into the wanted
  state. `TestBellState` is the entry point: it takes `count`, the number of
  repetitions, and `initial`, the starting state of the first qubit, makes a
  Bell state with `H` and `CNOT`, measures both qubits, and returns how many
  times each one read `Zero` and `One`.
- `MicrosoftAzureQuantum.csproj` is the project file. It names
  `Microsoft.Quantum.Sdk` 0.28.277227 and `net6.0`.
- `Pictures/` holds four JPEG images, among them
  `H and CNOT calculations.jpg`.

To run the exercise you need the .NET SDK and the Q# Development Kit. From this
folder:

```shell
dotnet run --count 1000 --initial 1
```

## Working on it

This repository ships no program: it is a single exercise, and `Program.qs` is
not built, run or tested by anything here. `.\recipe.ps1` is still the
repository's whole interface: `.\recipe.ps1 test` runs pytest and ruff over
`.claude`, and `.\recipe.ps1 info` prints the metadata. The other verbs print
`nothing to <verb>`. `CLAUDE.md` holds the rules.

## License

MIT. See [LICENSE](LICENSE).

## Lab requirements

This repository complies with [revision 4.0.0](http://127.0.0.1:3000/igors-lab/software-requirements/src/tag/v4.0.0/BEST_REQUIREMENTS.md) of the lab requirements, except R-02 (#7), R-09 (#8), R-37 (#9), R-41 (#10), R-42 (#11).
