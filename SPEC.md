# Software requirements specification: my-microsoft-azure-quantum-learning

Reverse-engineered from commit `92d511e` on 2026-11-18. It describes what the
code does, not what it was meant to do. Documentation hub:
[docs/README.md](docs/README.md).

<!-- jira-sync:start -->
Jira: KAN-116

## Tasks

This list is one ticket in Jira project KAN, [KAN-116](https://igorsvolohovs.atlassian.net/browse/KAN-116). Each line is a checkbox there: tick it in Jira and the sync ticks it here; add a checkbox there and it is appended here. Done items are the features described in section 3; open items are what the project declares but the code does not do yet.

- [x] Qubit preparation (section 3.1) <!-- spec-qubit-preparation -->
- [x] Bell-state experiment (section 3.2) <!-- spec-bell-state-experiment -->
- [x] Build (section 3.3) <!-- spec-build -->
- [x] Repository tooling (section 3.4) <!-- spec-repository-tooling -->
- [ ] Commit `b97ad6e` is titled "pin ruff and pytest", but only ruff's version is (declared, not implemented) <!-- spec-commit-b97ad6e-is-titled-pin-ruff-and-pytest-but-o -->
- [ ] `recipe.ps1 test` runs pytest and ruff over `.claude` (`recipe.ps1:45-53`); (declared, not implemented) <!-- spec-recipe-ps1-test-runs-pytest-and-ruff-over-claude-r -->
- [ ] `Program.qs:34` and `Program.qs:36` carry a commented-out counter line and a (declared, not implemented) <!-- spec-program-qs-34-and-program-qs-36-carry-a-commented- -->

<!-- jira-sync:end -->

## 1. Purpose and scope

The repository holds one Q# exercise that prepares a Bell state on two qubits,
measures it repeatedly and reports the measurement counts (`Program.qs`), plus
photographs of the author's handwritten notes (`Pictures/`).

In scope:

- the Q# program `Program.qs` and its project file `MicrosoftAzureQuantum.csproj`;
- the notes in `Pictures/`;
- the project-specific settings of `recipe.ps1`.

Out of scope:

- the lab tooling shared with repo-quality-template (hooks, Gitea workflows,
  templates), specified by that template;
- the earlier exercises (hello world, superposition, interference, relative
  phases), which exist only in git history (commits `96a22be` to `5f1ce56`);
- running on Azure Quantum hardware or any remote target: no file configures one.

## 2. Context

| Item | Description | Source |
|---|---|---|
| Actor | The author, learning Q#; no other users are named | `README.md:3-6` |
| Toolchain | .NET SDK and the Q# SDK `Microsoft.Quantum.Sdk` 0.28.277227 | `README.md:21`, `MicrosoftAzureQuantum.csproj:1` |
| Runtime | .NET executable, target framework `net6.0` | `MicrosoftAzureQuantum.csproj:4-5` |
| Execution target | Not named in the project; chosen by the SDK when `dotnet run` is used | `MicrosoftAzureQuantum.csproj` |
| External systems | None used by the Q# code | `Program.qs` |
| Repository host | Workflows are written for a Gitea instance (`.gitea/`, `README.md:42` links to one at `127.0.0.1:3000`); this clone's remote is the GitHub repository `IGORSVOLOHOVS/my-microsoft-azure-quantum-learning` | `.gitea/workflows/`, `git remote -v` |

## 3. Functional requirements

### 3.1 Qubit preparation

- **FR-1.** The system shall provide `SetQubitState(desired : Result, target : Qubit)`,
  which measures `target` and applies `X` to it when the measured result differs
  from `desired`.
  Source: `Program.qs:7-11`. Verification: no test.

### 3.2 Bell-state experiment

- **FR-2.** The system shall expose `TestBellState(count : Int, initial : Result) : (Int, Int, Int, Int)`
  as the program entry point.
  Source: `Program.qs:13-14`. Verification: no test.
- **FR-3.** The system shall allocate two qubits `q1`, `q2` once, before the loop.
  Source: `Program.qs:19`. Verification: no test.
- **FR-4.** The system shall, in each of `count` repetitions, set `q1` to `initial`
  and `q2` to `Zero` with `SetQubitState`.
  Source: `Program.qs:20-22`. Verification: no test.
- **FR-5.** The system shall, in each repetition, apply `H` to `q1` and then
  `CNOT` with `q1` as control and `q2` as target.
  Source: `Program.qs:24-25`. Verification: no test.
- **FR-6.** The system shall, in each repetition, measure `q1` and `q2` with `M`
  and add one to a separate counter for each qubit that reads `One`.
  Source: `Program.qs:28-39`. Verification: no test.
- **FR-7.** The system shall set both qubits to `Zero` after the loop, before
  they are released.
  Source: `Program.qs:42-44`. Verification: no test.
- **FR-8.** The system shall emit the message `q1:Zero, One  q2:Zero, One` and
  return `(count - numOnesQ1, numOnesQ1, count - numOnesQ2, numOnesQ2)`.
  Source: `Program.qs:47-49`. Verification: no test.

### 3.3 Build

- **FR-9.** The project shall build as an executable (`OutputType` `Exe`) with
  the Q# SDK `Microsoft.Quantum.Sdk/0.28.277227` for `net6.0`.
  Source: `MicrosoftAzureQuantum.csproj:1-6`. Verification: no test; not built
  for this document.

### 3.4 Repository tooling

- **FR-10.** The repository shall carry the repo-quality-template tooling with
  `recipe.ps1` declaring `$Code = 'mmaq'`, `$Version = '1.0.0'`, no `$App` and
  empty `$Provides`; its `test`, `info` and `clean` verbs act and the other verbs
  print `nothing to <verb>`.
  Source: `recipe.ps1:9-17`, `recipe.ps1:40-73`. Verification: `.\recipe.ps1 info`
  (run 2026-11-18, exit 0).

### 3.5 Declared but not implemented

- Commit `b97ad6e` is titled "pin ruff and pytest", but only ruff's version is
  pinned (`.claude/ruff.toml:2`); `.claude/pytest.ini:1-2` holds no version.
- `recipe.ps1 test` runs pytest and ruff over `.claude` (`recipe.ps1:45-53`);
  `.claude` holds no Python files, so no project code is tested or linted.
- `Program.qs:34` and `Program.qs:36` carry a commented-out counter line and a
  comment that the second counting block could be removed; neither is done.

## 4. Interfaces

### 4.1 Command line of the exercise

| Option | Type | Meaning | Source |
|---|---|---|---|
| `--count` | `Int` | Number of repetitions | `Program.qs:14`, `README.md:25` |
| `--initial` | `Result` | State `q1` is set to before `H` | `Program.qs:14`, `README.md:25` |

The option names are those used in `README.md:25`; the SDK derives them from
the entry-point parameters (inference from the identical names).

### 4.2 Output

| Element | Content | Source |
|---|---|---|
| Message | `q1:Zero, One  q2:Zero, One` | `Program.qs:48` |
| Return value | 4-tuple of `Int`: zeros of `q1`, ones of `q1`, zeros of `q2`, ones of `q2` | `Program.qs:49` |

### 4.3 recipe.ps1

| Verb | Effect | Source |
|---|---|---|
| `test` | sets `core.hooksPath`, runs pytest (exit 5 accepted), `ruff check`, `ruff format` over `.claude` | `recipe.ps1:41-55` |
| `info` | prints Name, Code, Version, Summary | `recipe.ps1:56-62` |
| `clean` | deletes `__pycache__`, `.pytest_cache`, `.ruff_cache` directories | `recipe.ps1:63-68` |
| `build`, `install`, `uninstall`, `run`, `publish` | print `nothing to <verb>` | `recipe.ps1:69-72` |

## 5. Data

- No persistent storage, no input files. State lives in two qubits and two
  mutable counters for one run (`Program.qs:15-19`).
- `Pictures/`: four JPEG files (one 1279x832, three 960x1280), photographs of
  handwritten notes on superposition and interference, the H, Pauli X, Pauli Y
  and CNOT matrices, and a Bell-state calculation; tracked through Git LFS
  (`.gitattributes:10`).

## 6. Non-functional requirements

- **NFR-1.** `.pdf`, `.png`, `.jpg`, `.zip` and `.7z` files shall be stored in
  Git LFS. Source: `.gitattributes:8-12`.
- **NFR-2.** No key shall be committed; `.claude/.env` is gitignored, reversing
  lab requirement R-02. Source: `.gitignore:20-24`, `CLAUDE.md` rule 4.

Line endings (`.gitattributes:1-6`) and the remaining working rules
(`CLAUDE.md`) come unchanged from repo-quality-template and are specified there.

## 7. Constraints and dependencies

| Dependency | Version | Source |
|---|---|---|
| `Microsoft.Quantum.Sdk` | 0.28.277227 | `MicrosoftAzureQuantum.csproj:1` |
| .NET target framework | `net6.0` | `MicrosoftAzureQuantum.csproj:5` |
| Q# namespaces opened | `Microsoft.Quantum.Canon`, `.Intrinsic`, `.Diagnostics`, `.Measurement` | `Program.qs:2-5` |
| ruff (tooling only) | `==0.16.1` | `.claude/ruff.toml:2` |
| pytest (tooling only) | not pinned | `.claude/pytest.ini` |
| PowerShell | for `recipe.ps1`; workflows use `shell: powershell` on a `windows` runner | `.gitea/workflows/test.yaml:9-16` |
| Git LFS | for `Pictures/` | `.gitattributes:10` |

There is no lock file.

## 8. Acceptance

1. With the .NET SDK and Git LFS available, run `dotnet run --count 1000 --initial 1`
   (`README.md:25`). Expect the message of FR-8 and a 4-tuple whose first two
   and last two elements each sum to 1000.
2. Inference from the circuit, to be confirmed by that run: on a noiseless
   simulator the two qubits read equal in every repetition, so elements 1 and 3,
   and 2 and 4, are equal.
3. `.\recipe.ps1 info` prints the metadata of FR-10 and exits 0 (checked
   2026-11-18).
4. `.\recipe.ps1 test` exits 0 (needs pytest and ruff 0.16.1; not run for this
   document).

## 9. Open questions

- Does the project still restore and build with SDK 0.28.277227 and `net6.0`
  on a current machine? Not checked: no .NET SDK on the documenting machine.
- Does this SDK version accept `1` for a `Result` option, as `README.md:25`
  uses, or only `One`? Not checked.
- Which simulator or target runs the program under `dotnet run`? The csproj
  sets no `DefaultSimulator` or `ExecutionTarget` property, so the SDK's default
  applies; which one that is for 0.28.277227 was not checked.
- The repository name mentions Azure Quantum; was submission to an Azure
  Quantum workspace ever intended? Nothing in the tree or in any earlier commit
  (`Program.qs`, the csproj, every README version) configures a workspace or target.
- Why are the earlier exercises kept only in history and not as files?
- What do the exceptions R-37, R-41 and R-42 (`README.md:42`) cover? They are
  tracked in issues `#9`-`#11` on the Gitea instance, not in this repository.
- Does a Gitea runner serve this repository, so that the workflows ever ran?
