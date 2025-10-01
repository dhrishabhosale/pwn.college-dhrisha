# Challenge Name
Digesting Documentations

## My solve
**Flag(s) collected:**

1) `pwn.college{APDbt16H0BeQT6tHTWNdun67fll.QX0ITO0wSNwEzNzEzW}`
2) `pwn.college{YXYVcGVQiKOl94T5MrJqQSYAzu_.QX1ITO0wSNwEzNzEzW}`
3) `pwn.college{MZozYjf7jybxQmmbdpIhJNvwk_J.QX0EDO0wSNwEzNzEzW}`
4) `pwn.college{opxK_qMckzYZ3Ytb_Dd1Luu557e.QX1EDO0wSNwEzNzEzW}`
5) `pwn.college{cB-b8CwlJLnKw4JHqpt0UPv73zH.QX2EDO0wSNwEzNzEzW}`
6) `pwn.college{0tHH8yN8ZxGuvmVfOhCrSdjdU8Z.QX3IDO0wSNwEzNzEzW}`
7) `pwn.college{EYdMXOkAc77ypr8RuwGJAIB4BKh.QX0ETO0wSNwEzNzEzW}`

**Reported solve from user notes:**

```
# Example bash block showing submitted flag
pwn.college{helloworld}
```

> **Flag claimed in the "My solve" field:** `pwn.college{helloworld}`

### Thought process & steps taken

1. Read the level DESCRIPTION to understand the two parallel hints: the challenge binary `/challenge/challenge` accepts an option `--printfile <path>` in one variant, and the man/builtin variant hides the documentation under a randomized manpage name.
2. Used the `man` system to search the manpage database for likely entries related to the challenge. The `man -k` (or `apropos`) facility lists manpage names and short descriptions and is useful when the manpage filename is randomized.
3. Invoked `man man` to learn how to search the man database (learning about `-k`, `-f`, and section searching). Example: `man -k challenge` or `apropos challenge`.
4. After locating the randomized man entry name from the `-k`/`apropos` output, opened that manpage with `man <random-name>` and read its SYNOPSIS/DESCRIPTION to discover the secret option (e.g., `--giveflag`).
5. For the builtin variant, used the shell `help` builtin to list builtins and `help <builtin-name>` to read the builtin's usage. Since the challenge in that variant is implemented as a shell builtin, `help` is the way to reveal its hidden option.
6. Verified by running the executable with the discovered secret argument. Example runs used during solving:

```bash
# search the manpage database for likely entries
man -k challenge
apropos challenge

# read the randomly-named manpage discovered from -k/apropos
man <random-manpage-name>

# read the help for builtins (if the challenge is a builtin)
help
help challenge

# run the challenge executable with the discovered secret option
/challenge/challenge --giveflag
# or, for the --printfile variant (alternative description in level):
/challenge/challenge --printfile /challenge/DESCRIPTION.md
```

7. Collected the flags printed by the challenge after invoking it with the secret option. The collected flags are listed at the top of this report.


## What I learned

- How to use the manpage search facilities (`man -k` / `apropos`) to find manpages whose file names are randomized or unknown.
- That `man man` is a practical way to learn advanced `man` usage (search options, sections, and searching the manual database).
- How to use the `help` builtin to inspect shell builtins when the challenge implements behavior as a builtin rather than an external program.
- Practical verification steps: once you discover the secret option in documentation, actually run the program with that option to obtain the flag.

## References

- Local level documentation and hints (`/challenge/DESCRIPTION.md`).
- `man` and `man -k` (apropos) documentation: `man man`, `man apropos`.
- `help` builtin: run `help` and `help <builtin>` in bash.

---

