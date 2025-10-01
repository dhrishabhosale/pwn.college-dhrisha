# Practicing Piping – Challenge Report

## Flags Collected
1. `pwn.college{YYR_0tVn9SG6ltr0ZnWdtin_O4u.QX0YTN0wSNwEzNzEzW}`
2. `pwn.college{4aVWZbNZU1xKlc5EwIBbFkvRpBH.QX1YTN0wSNwEzNzEzW}`
3. `pwn.college{s2BsvCY-NZpH8tqHAz7nb0PYXBM.QX3ATO0wSNwEzNzEzW}`
4. `pwn.college{AGToOANX8md8vPrpLqi827iWaHn.QX3YTN0wSNwEzNzEzW}`
5. `pwn.college{YQHdnIJzCFdzJSFj0kwK9Wmt3bx.QXwcTN0wSNwEzNzEzW}`
6. `pwn.college{UNwXkRJrVa4aFDZEuwhj6BssEjO.QX4EDO0wSNwEzNzEzW}`
7. `pwn.college{EDWaZrw-BQaG1dHvwB3FjM-IF2Y.QX5EDO0wSNwEzNzEzW}`
8. `pwn.college{EuJlK9yWxQLvDO7BFtMmtpdUMt_.QX1ATO0wSNwEzNzEzW}`
9. `pwn.college{kSr_kDxE1Xl_lTtkC6h9oq8YtYT.0FOxEzNxwSNwEzNzEzW}`
10. `pwn.college{ku1ZlrDDhJq_LMahtLO7kPbRk0z.QXxITO0wSNwEzNzEzW}`
11. `pwn.college{E6J6WH3FdMvN5Tis9jrPdy1FrgG.0lNwMDOxwSNwEzNzEzW}`
12. `pwn.college{sMU8Lf3sbT6vIysJ1HWwfnIHL-Y.QXwgDN1wSNwEzNzEzW}`
13. `pwn.college{oFU3WslKJIAs040P2kOyXutASJC.QXxQDM2wSNwEzNzEzW}`
14. `pwn.college{4IrGQU3LWRyRwYOQLUKB8nhaezz.01MzMDOxwSNwEzNzEzW}`

---

## Challenge Overview

This set focused on piping and redirection in Linux, starting with simple output redirection and progressing to:

- stdout and stderr management (`>`, `2>`)
- input redirection (`<`)
- filtering output (`grep`)
- duplication (`tee`)
- process substitution (`<()`, `>()`)
- named pipes (FIFOs)

---

## Solve Highlights

### Redirection Basics
```bash
/challenge/run > out.txt 2> err.txt
```

### Appending vs Overwriting
```bash
/challenge/run >> combined_output
```

### Filtering Output with grep
```bash
/challenge/run | grep flag
/challenge/run | grep -v DECOY
```

### Merging stderr into stdout
```bash
/challenge/run 2>&1 | grep flag
```

### Duplicating Output with tee
```bash
/challenge/pwn | tee capture.txt | /challenge/college
```

### Process Substitution
```bash
diff <(/challenge/print_decoys) <(/challenge/print_decoys_and_flag) | sed -n 's/^> //p'
```

### Named Pipes (FIFOs)
```bash
mkfifo /tmp/pipe
/challenge/run > /tmp/pipe   # Terminal 1
cat /tmp/pipe                # Terminal 2
```

---

## Key Learnings

- **Three standard file descriptors**:
  - `0` = stdin
  - `1` = stdout
  - `2` = stderr

- Redirection provides fine-grained control of data streams.

- `tee` duplicates streams for debugging pipelines.

- Process substitution allows commands to be treated as files for comparison or input/output.

- Named pipes (FIFOs) facilitate multi-step or multi-terminal workflows.

---

## References

- GNU Bash Reference Manual – Redirections: https://www.gnu.org/software/bash/manual/html_node/Redirections.html
- Linux I/O Redirection (TLDP): https://tldp.org/LDP/abs/html/io-redirection.html
- Pwn.college documentation & hints
- Personal testing & trial/error during challenges
