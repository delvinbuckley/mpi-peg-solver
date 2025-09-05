# mpi-peg-solver

A parallel peg solitaire puzzle solver written in C++ using MPI.

## Overview

This project solves peg solitaire puzzles by distributing board configurations across MPI processes. Each client process determines whether a puzzle is solvable using a depth-first search. Results are collected by the main server process.

## File Descriptions

- `main.cc` — Runs the MPI program. Handles setup, distributes puzzles, and collects results.  
- `game.h` / `game.cc` — Defines the board, valid moves, and solving logic using DFS.  
- `utilities.h` / `utilities.cc` — Includes helper functions like timing and safe file I/O.

## Build Instructions

To compile with `mpicxx`:

```bash
mpicxx main.cc game.cc utilities.cc -o solver
## How to Run (Local)

```bash
mpirun -np 4 ./solver input.dat output.dat
```

- `input.dat`: Input puzzle(s)  
- `output.dat`: Output results

## Running on HPC (SLURM)

To compile and run on a cluster with SLURM:

```bash
mpicxx main.cc game.cc utilities.cc -o solver
```

Then create a job script (`jobscript.sh`):

```bash
#!/bin/bash
#SBATCH --job-name=pegsolver
#SBATCH --ntasks=4
#SBATCH --time=00:05:00
#SBATCH --output=job_output.txt

mpirun -np 4 ./solver input.dat output.dat
```

Submit the job:

```bash
sbatch jobscript.sh
```

## License

MIT License
