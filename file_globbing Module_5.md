# Challenge Name
File Globbing

## Flags found
1) `pwn.college{MMEYUfyls-zzRxnAMWo-jx-rhLZ.QXxIDO0wSNwEzNzEzW}`
2) `pwn.college{QAwnrOzsismdFatmCJJpIaNG1__.QXyIDO0wSNwEzNzEzW}`
3) `pwn.college{IH6ljyn2Z7FWa_jgCUHSokTscq2.QXzIDO0wSNwEzNzEzW}`
4) `pwn.college{wHZc-yF5lDqQC5rISNTRBt-3RRx.QX0IDO0wSNwEzNzEzW}`
5) `pwn.college{kU5EmxBI5KHcOoRjurmA_1rTzuY.0lM3kjNxwSNwEzNzEzW}`
6) `pwn.college{QRkygFlMEh7MW5juTv_MLIpJ5Bk.QX1IDO0wSNwEzNzEzW}`
7) `pwn.college{cqM7gglGV8_1v73s3bBgV3KEmHP.QX2IDO0wSNwEzNzEzW}`
8) `pwn.college{QR8owGzmbLk5N9ePzq5P61-yDI2.0FN0EzNxwSNwEzNzEzW}`
9) `pwn.college{cwzFYHhFx4C94t4kUrYqrXTGR8m.0lN0EzNxwSNwEzNzEzW}`
10) `pwn.college{ITJCs-BttKEZdUEeh1FQ51K2V4w.0VN0EzNxwSNwEzNzEzW}`

## My solve
**Flag:** `pwn.college{helloworld}`

**Solution & thought process**

In this challenge, I practiced different types of shell globbing patterns (`*`, `?`, `[]`, and negations) and applied them step by step to reach the flag.

Steps I took:

1. **Using `*`**
   - Matched multiple files with a single pattern:
     ```bash
     echo file_*
     ```
   - Used it to shorten paths like `/ch*` → `/challenge`.

2. **Using `?`**
   - Replaced a single character in filenames:
     ```bash
     echo file_?
     ```

3. **Using `[]`**
   - Targeted multiple specific files in one command:
     ```bash
     /challenge/run file_[absh]
     ```

4. **Absolute path globbing**
   - Combined globs with full paths:
     ```bash
     /challenge/run /challenge/files/file_[absh]
     ```

5. **Multiple globs**
   - Used more than one `*` in a short pattern to catch files with the letter `p`:
     ```bash
     /challenge/run *p*
     ```

6. **Combining everything**
   - Crafted a single short glob (≤ 6 characters) that expanded into `challenging`, `educational`, and `pwning`.

7. **Negation**
   - Excluded files starting with `p`, `w`, or `n`:
     ```bash
     /challenge/run [!pwn]*
     ```

8. **Tab completion**
   - Used `<TAB>` to complete tricky filenames like:
     ```bash
     cat /challenge/pwn<TAB>
     ```
   - This expanded to the hidden file with the flag.

Final command that revealed the flag looked like:
```bash
pwn.college{helloworld}
```

## What I learned
- `*` = wildcard for zero or more characters.
- `?` = wildcard for exactly one character.
- `[]` = matches one character from a set.
- `[!...]` or `[^...]` = negates the set.
- Globbing expands before command execution.
- Tab completion is safer than manually typing tricky filenames.
- Use `echo <glob>` to preview expansions safely.

## References
- `man bash` (Pattern Matching / Filename Expansion)
- GNU Bash Manual: https://www.gnu.org/software/bash/manual/
- General shell tutorials on wildcard expansion
