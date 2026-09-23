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

## Level 3 → Level 4
**Goal:** Find the password in a hidden file inside the `inhere` directory.

**Commands used:* cd inhere
ls -la
cat ./<hidden filename>
**What I learned:** `cd` changes directory. `ls -la` lists all files, including hidden ones (dotfiles), which don't show up with a plain `ls`.

## Level 4 → Level 5
**Goal:** Find the password stored in the only human-readable file inside the `inhere` directory.

**Commands used:**cd inhere
cat ./<filename>

**What I learned:** Same `cat` approach as before, but this level adds a filtering step: several files exist in the directory, and only one is actually human-readable text rather than binary data. Checking file types (e.g. with `file ./*`) helps spot the right one quickly.

## Level 5 → Level 6
**Goal:** Locate a file in the `inhere` directory that is human-readable, exactly 1033 bytes in size, and not executable.

**Command used:** find ~/inhere -size 1033c

**What I learned:**
- `find` searches recursively through a folder.
- `~/inhere` gives the full path to search inside.
- `-size 1033c` filters by exact size, where `c` means bytes.
