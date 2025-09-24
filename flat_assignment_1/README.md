# FLAT Assignment: Finite-State Transducers

This repository contains the solution for the case conversion task using the OpenFST library.

### Problem Statement

The assignment is to build a Finite-State Transducer (FST) that converts all lowercase letters in an input string to their uppercase equivalents.

### Solution Overview

A Finite-State Transducer is an ideal tool for this task because it can perform a simple, character-by-character mapping from a set of input symbols to a set of output symbols. The FST for this problem is simple, consisting of a single state and multiple self-looping transitions.

### FST Implementation Details

The solution is implemented using the OpenFST command-line tools.

#### 1. Symbol Table (`symbols.txt`)

This file maps each character (both lowercase and uppercase letters, as well as special symbols like spaces) to a unique integer. This is a required step for OpenFST, as it works with integer representations of symbols.

#### 2. Case Conversion FST (`case_converter.txt`)

This file defines the FST itself. It has one state (state `0`), which is both the initial and final state. For each lowercase letter, there is a transition with the form `0 0 lowercase_letter uppercase_letter`. For symbols that should remain unchanged, the transition is of the form `0 0 symbol symbol`.

### How to Compile and Run the FST

Assuming OpenFST is installed on a Unix-like system (Linux or macOS), you can replicate this solution by following these steps:

1.  Clone this repository.
2.  Navigate to the project folder in your terminal.
3.  Compile the FST from its text definition:
    ```bash
    fstcompile --isymbols=symbols.txt --osymbols=symbols.txt case_converter.txt > case_converter.fst
    ```
4.  Create and compile a test input string (e.g., "hello world!"):
    ```bash
    # Create the input file
    echo "0 1 h" > test_input.txt
    echo "1 2 e" >> test_input.txt
    echo "2 3 l" >> test_input.txt
    echo "3 4 l" >> test_input.txt
    echo "4 5 o" >> test_input.txt
    echo "5 6 <space>" >> test_input.txt
    echo "6 7 w" >> test_input.txt
    echo "7 8 o" >> test_input.txt
    echo "8 9 r" >> test_input.txt
    echo "9 10 l" >> test_input.txt
    echo "10 11 d" >> test_input.txt
    echo "11 12 <exclamation>" >> test_input.txt
    echo "12" >> test_input.txt
    
    # Compile the input acceptor
    fstcompile --isymbols=symbols.txt --osymbols=symbols.txt --acceptor test_input.txt > test_input.fst
    ```
5.  Run the composition and view the output:
    ```bash
    fstcompose test_input.fst case_converter.fst | fstproject --project_type=output | fstprint --isymbols=symbols.txt --osymbols=symbols.txt
    ```

This process will output the converted string, demonstrating the successful operation of the FST.