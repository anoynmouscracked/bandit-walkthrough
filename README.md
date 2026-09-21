# bandit-walkthrough
Concepts and commands I learned from OverTheWire Bandit, no passwords or full solutions 

## Level 0 → Level 1
**Goal:** Read the password stored in the `readme` file

**Command used:** cat ./readme
**What I learned:** `cat` (concatenate) outputs the raw text content of a file directly to standard output

## Level 1 → Level 2
**Goal:** Read the password from a file named `-`, located in the home directory.

**Command used:** cat ./-
**What I learned:** A plain `cat -` can behave oddly because `-` is often read as an option flag. Prefixing it with `./` tells the shell to treat it as a filename in the current directory instead.

## Level 2 → Level 3
**Goal:** Read the password from a file name `--spaces in the filename--` located in home directory

**Command used:**  cat ./--spaces in the filename--
