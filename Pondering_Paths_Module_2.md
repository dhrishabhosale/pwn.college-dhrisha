# Pondering_Paths_Module_2

## Challenge Name
**PONDERING PATH** — explores Linux filesystem paths, cwd, `.`/`..`, and shell expansion.

---

## My Solve

**Flags:**

1. `pwn.college{QLMGshMYifcU-hN_V72e9fwGbw2.QX4cTO0wSNwEzNzEzW}`  
2. `pwn.college{8P9LDOg_mLQaDxhXCvSdeaZdEtZ.QX1QTN0wSNwEzNzEzW}`  
3. `pwn.college{cSQgiN6b6NAJUAMlOWc9s1nCG5O.QX2QTN0wSNwEzNzEzW}`  
4. `pwn.college{A9Q6wqWIsChSD9jcEn5Grt5xkn2.QX3QTN0wSNwEzNzEzW}`  
5. `pwn.college{EGaRhEzmDrXdMQ1GHfeekMCHIpn.QX4QTN0wSNwEzNzEzW}`  
6. `pwn.college{kaypIjDJ_7c-AQEiAhf5dN95ttQ.QX5QTN0wSNwEzNzEzW}`  
7. `pwn.college{MJ1YXrnBE5MVx945eh13HTmFd6n.QXwUTN0wSNwEzNzEzW}`  
8. `pwn.college{gdfYwfO3Sbj-InxQnCUlF8EK7QR.QXxUTN0wSNwEzNzEzW}`  
9. `pwn.college{EInC-UUj9nrKZbAYrsrQs0iRTpc.QXzMDO0wSNwEzNzEzW}`  

---

### Thought Process & Commands

The challenge required:

- Running `/challenge/run` using its **absolute path**.  
- Being in a specific **current working directory** (printed by the program).  
- For the flag-write task: providing an **argument** that expands into an absolute path in the home directory, with the pre-expansion argument ≤ 3 characters.

Steps taken:

```bash
# 1. Run once to see what cwd is required
/challenge/run

# 2. cd into the directory it specifies (example: /challenge)
cd /challenge
pwd

# 3. Run again from required cwd, using absolute path
/challenge/run

# 4. Write flag to a file in home using short pre-expansion argument
/challenge/run ~/f

# 5. Verify flag
cat ~/f
```

Key notes:
- **Naked name (`run`) fails** because Linux doesn’t search the current directory for executables. Must use `/challenge/run` or `./run`.  
- `.` and `..` can be used in paths to explicitly refer to current and parent directories.  
- Shell expands `~` to `/home/hacker`, so `~/f` (3 characters) becomes `/home/hacker/f`.  

---

## What I Learned

- Difference between **absolute** (`/challenge/run`) and **relative** (`./run`) paths.  
- Why Linux does **not** execute binaries from cwd without `./` — a safety feature.  
- Special path components: `.` (current directory), `..` (parent directory).  
- Shell tilde (`~`) expansion happens before arguments are passed to programs.  
- Constraints can be bypassed cleverly with expansion rules (e.g., `~/f` → `/home/hacker/f`).  

---

## References

- pwn.college: Pondering Path module (internal material)  
- Linux man pages: `cd`, `pwd`, `bash(1)`  
- General shell behavior with `.`/`..` and tilde expansion  
