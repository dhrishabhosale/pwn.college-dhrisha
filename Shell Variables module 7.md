
type what the challenge asks

## My solve
**Flags collected:**
1. `pwn.college{8CVjctASVRxY9U53urTJwQFrbFV.QX3UTN0wSNwEzNzEzW}`
2. `pwn.college{E_v9xV7wrOIWgi3qozMXNXsQ7r-.QX5UTN0wSNwEzNzEzW}`
3. `pwn.college{wcYV-ZL5uGYH4yf1Yubp2KrIqoo.QXwYTN0wSNwEzNzEzW}`
4. `pwn.college{gVBsEHDhFT5gaF7qU80dtFlwbcO.QXyYTN0wSNwEzNzEzW}`
5. `pwn.college{8gD5zRYDgtJq5_AtintaSwRoM52.QX4UTN0wSNwEzNzEzW}`
6. `pwn.college{APQbCvqj-eTGGbc84-WdOG-Y6X4.QX1cDN1wSNwEzNzEzW}`
7. `pwn.college{8q7J-qErB0IfDtAk4mKXgPVeL2d.QX4cTN0wSNwEzNzEzW}`
8. `pwn.college{kVHkBf3HXLss7_lt0I5aqVcWjPt.QXwIDO0wSNwEzNzEzW}`

Below are the concrete commands and the thought process used to solve each mini-task described in the challenge. Commands are grouped by the concept they exercise.

### 1) Print the FLAG variable (the program itself cannot print it)
Thought: the environment already has a variable named `FLAG`. We just need to expand it.

```bash
# Print FLAG using echo
echo "$FLAG"

# Or using printf (safer for arbitrary content)
printf '%s
' "$FLAG"
```

Expected output: the contents of the `FLAG` variable (one of the `pwn.college{...}` strings).

---

### 2) Set a variable (PWN=COLLEGE) and verify
Thought: assign without spaces. Variable names and values are case-sensitive.

```bash
# Set the variable locally in the shell
PWN=COLLEGE

# Access it
echo "$PWN"
# output: COLLEGE
```

---

### 3) Export PWN so child processes inherit it, but set COLLEGE non-exported
Thought: use `export` for PWN; set COLLEGE without export so it remains unexported.

```bash
# Set COLLEGE locally (not exported)
COLLEGE=PWN

# Set and export PWN so child processes (like /challenge/run) see it
export PWN=COLLEGE

# Verify in the current shell
echo "PWN (shell): $PWN"
echo "COLLEGE (shell): $COLLEGE"

# Show exported env entries (COLLEGE shouldn't appear)
env | grep -E '^PWN=|^COLLEGE=' || true
```

If you run a child shell, only exported variables (PWN) will be visible there; COLLEGE will not.

---

### 4) Invoke /challenge/run with PWN exported and COLLEGE local (not exported)
Thought: ensure PWN is exported and COLLEGE remains local, then run `/challenge/run` — the program will inherit exported env vars.

```bash
# Set non-exported COLLEGE
COLLEGE=PWN

# Export PWN
export PWN=COLLEGE

# Run the command; /challenge/run will see PWN in its environment but not COLLEGE
/challenge/run
```

If the challenge expects `/challenge/run` to react to those variables, exporting PWN is necessary.

---

### 5) Inspect exported variables with env to find FLAG
Thought: `env` lists exported environment variables. FLAG might be exported already.

```bash
# list exported environment variables and look for FLAG
env | grep -i '^FLAG=' || echo "FLAG not exported; try echo \$FLAG"
```

If FLAG is exported, it will show up; otherwise, use `echo $FLAG` from the current shell.

---

### 6) Store command output into a variable (command substitution)
Thought: use `$(...)` to capture output into a variable. Example: read the output of `/challenge/run` into `PWN`.

```bash
# Capture output of a command into variable PWN
PWN="$(/challenge/run)"

# Print to verify
printf 'PWN contains: %s
' "$PWN"
```

This sets `PWN` to whatever `/challenge/run` prints to stdout.

---

### 7) Use read to get user input into PWN
Thought: `read` reads from stdin. Use `-p` for a prompt (interactive) or feed input programmatically.

```bash
# Interactive usage:
read -p "Enter value for PWN: " PWN
echo "You set PWN to: $PWN"

# Non-interactive: echo "COLLEGE" | read PWN won't persist in the parent shell.
# To set PWN from a pipeline in the same shell environment, use command substitution:
PWN="$(printf '%s' "COLLEGE")"
echo "$PWN"
```

Note: A pipeline spawns a subshell in many shells; prefer `PWN="$(...)"` or `read` with redirected input (next section).

---

### 8) Read a file into a variable without using cat (avoid Useless Use of Cat)
Thought: redirect the file into `read` so the shell builtin reads it directly.

```bash
# Read the first token/line of /challenge/read_me into PWN
read PWN < /challenge/read_me

# If you need the entire file including spaces, use:
PWN="$(< /challenge/read_me)"

# Verify
echo "PWN: $PWN"
```

`PWN="$(< /challenge/read_me)"` is the fastest form (Bash-specific) and avoids launching an external command.

---

## What I learned
- How to **access** environment variables (`$VAR`) and how to **assign** them (`VAR=value`) — assignment must have no spaces around `=`.
- Exporting (`export VAR`) passes a variable to child processes; non-exported variables remain local to the shell.
- **Command substitution** `$(command)` captures output into a variable; preferred to backticks because it nests cleanly.
- `read` can accept input from the user or from redirected files — reading from files with `read < file` avoids spawning external processes.
- `env` lists exported variables; useful to confirm what child processes will inherit.
- Small shell optimizations: `PWN="$(<file)"` reads a file into a variable without forking `cat`.
- Pitfalls: pipelines often run in subshells so `read` in a pipeline may not set variables in the parent shell.
