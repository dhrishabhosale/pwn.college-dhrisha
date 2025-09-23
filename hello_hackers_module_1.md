# HELLO HACKERS MODULE 1

# Challenge Name
Intro to the Command Line — `hello` & History

## My solve
**Flags:**
1. `pwn.college{EakfNJ-qvndhB83ULknMq6Gs5Ry.QX3YjM1wSNwEzNzEzW}`
2. `pwn.college{wvFZPq3zOU85wF32sxNion8dXZK.QX4YjM1wSNwEzNzEzW}`
3. `pwn.college{kjeG7Wl5m3pdT17NcgfZ6z22X0N.0lNzEzNxwSNwEzNzEzW}`

**Solve & thought process**

This set of levels teaches three core ideas: running a command, running a command with an argument, and retrieving a value from shell history. I solved them in order.

### Level 1 — run `hello`
The challenge states that running the `hello` program prints the flag. I confirmed the environment (prompt) then ran:

```bash
# Level 1
hello
# -> prints flag: pwn.college{EakfNJ-qvndhB83ULknMq6Gs5Ry.QX3YjM1wSNwEzNzEzW}
```

**Thoughts:** Keep case sensitivity in mind (`hello` must be lowercase). The prompt `hacker@dojo:~$` tells you username/host/privilege but isn’t required to get the flag.

### Level 2 — run `hello` with the single argument `hackers`
This level expects one argument. Using the lesson about arguments, I passed `hackers` to the `hello` program:

```bash
# Level 2
hello hackers
# -> prints flag: pwn.college{wvFZPq3zOU85wF32sxNion8dXZK.QX4YjM1wSNwEzNzEzW}
```

**Thoughts:** Don’t use `echo` here — the challenge program `hello` processes the argument. Quotes are not necessary because the argument is a single word.

### Level 3 — retrieve the flag from shell history
This level injected the flag into the shell history. I used the arrow keys and history commands to retrieve it.

```bash
# Level 3: scroll history with Up Arrow until the injected entry appears,
# or run:
history
# identify the relevant entry number N, then:
!N
# The displayed/ran command revealed the flag:
# pwn.college{kjeG7Wl5m3pdT17NcgfZ6z22X0N.0lNzEzNxwSNwEzNzEzW}
```

**Thoughts:** Arrow keys are the fastest way. `history` + `!N` is helpful if you need to re-run the exact command. The shell stores past commands, and the challenge used that fact to hide the flag in the history.

**Complete example session (concise):**

```bash
whoami
hello
hello hackers
history
# find the history line that contains the flag, then either read/copy it or:
!<line_number>
```

## What I learned
- The shell prompt shows contextual info: `username@hostname:cwd$` (`$` = normal user).  
- Commands are parsed as the first word (command) and subsequent words as arguments.  
- Linux commands are **case-sensitive**.  
- `hello` is a challenge program used here — run it exactly as required to get flags.  
- Shell history is saved and navigable with Up/Down arrows, and can be listed with `history` and re-run with `!N`.  
- Small, targeted commands (`whoami`, `echo`) are useful for environment checks.

## References
- pwn.college DOJO challenge text and in-environment prompts.  
- Bash basics: `whoami`, `echo`, `history`, `!N`.  
- Shell navigation: Up/Down arrow to scroll history.

