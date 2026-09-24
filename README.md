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

  ## Level 6 → Level 7
**Goal:** The password is stored somewhere on the server and has all the following properties: owned by user `bandit7`, owned by group `bandit6`, and is 33 bytes in size.

**Command used:**find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
**What I learned:**
- `find /` searches the entire filesystem from root.
- `-user` and `-group` filter results by file owner and group.
- `-size 33c` filters by exact size in bytes.
- `2>/dev/null` redirects error messages (like "permission denied") to `/dev/null`, hiding them so only real results show on screen.

## Level 7 → Level 8
**Goal:** The password is stored in `data.txt`, next to the word `millionth`.

**Command used:**grep "millionth" data.txt
**What I learned:** `find` only locates files by name or attributes, it doesn't look inside file contents. To search for a specific word inside a file, `grep` is the right tool.

## Level 8 → Level 9
**Goal:** The password is stored in `data.txt` and is the only line of text that occurs only once.

**Command used:**sort data.txt | uniq -u
**What I learned:**
- `sort` arranges all lines of a file into alphabetic order, so duplicate lines end up next to each other.
- `|` (pipe) passes the output of one command directly into the next command as input.
- `uniq -u` removes duplicate lines that are next to each other. The `-u` flag makes it show only lines that appear exactly once in the whole file.

## Level 9 → Level 10
**Goal:** The password is stored in `data.txt`, as one of the few human-readable strings, preceded by several `=` characters.

**Command used:**strings data.txt | grep '='
**What I learned:** `strings` pulls out and displays only the human-readable text from a file, filtering out binary/garbage data.

## Level 10 → Level 11
**Goal:** Decode the password stored in `data.txt`, which is Base64-encoded text.

**Command used:**base64 -d data.txt
**What I learned:** Base64 is an encoding scheme, not encryption. The `-d` flag decodes the Base64 representation back into plain text.

## Level 11 → Level 12
**Goal:** The password is stored in `data.txt`, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions (ROT13).

**Command used:**cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
**What I learned:**
- `tr` (translate) maps and replaces characters from one set to another.
- `'A-Za-z'` is the input character set: uppercase A-Z followed by lowercase a-z.
- `'N-ZA-Mn-za-m'` is the output set, shifted by 13 places (e.g. A→N, N→A).


