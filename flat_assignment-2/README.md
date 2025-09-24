### Assignment 2: Digit-to-Word Converter

This part of the assignment focuses on building a Finite-State Transducer that converts a string of digits into their corresponding English words.

#### Solution Overview

The FST for this task uses a network of states and epsilon ($\epsilon$) transitions to map a single input symbol (a digit) to a sequence of output symbols (the letters of a word). Each digit has its own path in the FST that spells out its word.

#### Files

All files for this assignment are located in the `flat_assignment_3/` folder:
* `symbols.txt`: The symbol table for all digits and letters.
* `digit_to_word.txt`: The FST definition with multi-state transitions for each word.
* `test_input.txt`: A sample input string to demonstrate the FST.

#### How to Compile and Run

To run this FST, navigate to the `flat_assignment_3/` directory and use the following commands:
```bash
# Compile the FST definition
fstcompile --isymbols=symbols.txt --osymbols=symbols.txt digit_to_word.txt > digit_to_word.fst

# Compile the test input string
fstcompile --isymbols=symbols.txt --osymbols=symbols.txt --acceptor test_input.txt > test_input.fst

# Run the transducer and view the output
fstcompose test_input.fst digit_to_word.fst | fstproject --project_type=output | fstprint --isymbols=symbols.txt --osymbols=symbols.txt