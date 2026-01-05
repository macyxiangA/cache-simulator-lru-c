# Cache Simulator (LRU) in C

This project implements a configurable cache simulator in C.  
It models a set-associative cache with an LRU (Least Recently Used) replacement policy and reports cache hits, misses, and evictions while replaying memory access traces.

The simulator is designed to help analyze how cache parameters and access patterns affect performance.

## Features

- Set-associative cache model
- LRU replacement policy
- Configurable cache parameters:
  - Number of set index bits (s)
  - Number of lines per set (E)
  - Number of block offset bits (b)
- Supports memory access types:
  - Load (L)
  - Store (S)
  - Modify (M = load + store)
- Ignores instruction fetches
- Outputs hit, miss, and eviction statistics

## Project Structure

- csim.c  
  Core cache simulator implementation

- Makefile  
  Build rules for compiling the simulator

- traces/  
  Sample memory access trace files used for testing

- test-csim  
  Optional testing utility or script

- .csim_results  
  Output file generated after each simulation run

## Build Instructions

To compile the cache simulator:

    make

This produces an executable named:

    csim

To clean build artifacts:

    make clean

## Usage

The simulator accepts command-line arguments to configure the cache and specify a trace file.

Basic usage:

    ./csim -s <s> -E <E> -b <b> -t <tracefile>

Arguments:

- -s <num>  
  Number of set index bits

- -E <num>  
  Number of cache lines per set

- -b <num>  
  Number of block offset bits

- -t <file>  
  Path to the memory trace file

Optional flags:

- -v  
  Verbose mode (prints each memory access)

- -h  
  Print usage help

## Example Commands

Direct-mapped cache:

    ./csim -s 4 -E 1 -b 4 -t traces/trace1

2-way set associative cache with verbose output:

    ./csim -v -s 8 -E 2 -b 4 -t traces/trace2

## Output

After execution, the simulator prints statistics to standard output in the format:

    hits:<H> misses:<M> evictions:<E>

It also writes the same values to a file named:

    .csim_results

This file contains:

    <hits> <misses> <evictions>

## Implementation Notes

- Cache lines store:
  - Valid bit
  - Tag
  - Last-used timestamp (for LRU tracking)
- LRU is implemented using a global access counter updated on every memory access
- Modify (M) operations are treated as two accesses:
  - One load
  - One store

## System Requirements

- 64-bit x86-64 system
- GCC compiler with math library support

## License

This project is provided for educational and experimental purposes.
