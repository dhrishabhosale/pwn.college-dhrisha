# **Comprehending Commands**

Linux core utilities practice (cat, grep, diff, ls, touch, rm, mv, ln, find)

## My solve

**Flag(s) collected:**

Below are the flags found during the challenge (copied from session notes):

1. `pwn.college{w4APLRrUMoLvciFVyXV9hRMHCKI.QXxcTN0wSNwEzNzEzW}`
2. `pwn.college{Aik6tt9u79TYydnQCy61aTFeuZP.QX5ETO0wSNwEzNzEzW}`
3. `pwn.college{QpzS-bu0WnTFBRF5KCqdZ1q-m8a.QXwITO0wSNwEzNzEzW}`
4. `pwn.college{scdMN055RKM4r9IQWzPmaHcDnuB.QX3EDO0wSNwEzNzEzW}`
5. `pwn.college{scQ00L5JnKa4Xihe1nHmi--oDkL.01MwMDOxwSNwEzNzEzW}`
6. `pwn.college{00GSKRQVdpIronenrrHfRTkR6r2.QX4IDO0wSNwEzNzEzW}`
7. `pwn.college{Y2vZws3-eKn2zJM8QndipacikSM.QXwMDO0wSNwEzNzEzW}`
8. `pwn.college{Qvdu4YGFbvhDZwriLSzTHIefC8Y.QX2kDM1wSNwEzNzEzW}`
9. `pwn.college{QfZcrcKk2ains5XUsDIeyEu6fcw.0VOxEzNxwSNwEzNzEzW}`
10. `pwn.college{gexn1B0ySFwqJotcUE6JDyLTXIU.QXwUDO0wSNwEzNzEzW}`
11. `pwn.college{YL51g8DUd_L_Fo-Rszx-IOsKXrm.QX5IDO0wSNwEzNzEzW}`
12. `pwn.college{wdsKDhnkd9qeEbi2WDgQUg3JJZK.QXxMDO0wSNwEzNzEzW}`
13. `pwn.college{YQiOMA0Lo_J34PUGyxNc4HZ5T5-.QXyMDO0wSNwEzNzEzW`}`
14. `pwn.college{IUHFFd_ha_ZaAN9846BjCski4O8.QX5ETN1wSNwEzNzEzW}`

**Reported solve from user notes:**

```
# Example bash block showing submitted flag
pwn.college{helloworld}
```

> **Flag claimed in the "My solve" field:** `pwn.college{helloworld}`

### Thought process & steps taken

1. Read challenge DESCRIPTION and identified which utilities would be used: `cat`, `grep`, `diff`, `ls`, `touch`, `rm`, `mv`, `mkdir`, `find`, and `ln -s` (symlinks).
2. Used `cat` and absolute paths when necessary to view files such as `/challenge/DESCRIPTION.md` and `/flag` when accessible.
3. For the large file task, used `grep 'pwn.college' /challenge/data.txt` to locate the real flag (the hint indicated the flag begins with `pwn.college`).
4. Used `diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt` to find the single differing line — the real flag — between the two files.
5. Listed `/challenge` with `ls /challenge` to find the randomly-named run file and executed it where required.
6. Created files with `touch /tmp/pwn` and `touch /tmp/college` where challenges demanded files be present for `/challenge/run` to succeed.
7. Removed `delete_me` in the home directory using `rm delete_me` then executed `/challenge/check` to validate and collect flag where applicable.
8. Used `mv /flag /tmp/hack-the-planet` (creating the directory with `mkdir -p /tmp/hack-the-planet`) when instructed and then executed the provided check script.
9. Used `ls -a /` to reveal dot-files and locate the hidden flag file `/.<name>` when the flag was hidden as a dotfile in `/`.
10. Used `find / -name flag 2>/dev/null` to search for the `flag` file across the filesystem, ignoring permission errors, and checked candidate files until the real flag was found.
11. Created and used a symlink with `ln -s /flag /home/hacker/not-the-flag` to fool `/challenge/catflag` into reading the real `/flag` when the challenge provided a misdirected file.

Example command snippets used during solving (bash):

```bash
# search a large file for the flag prefix
grep 'pwn.college' /challenge/data.txt

# find the line missing/present between two files
diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt

# list files in challenge directory
ls -la /challenge

# create required tmp files for a run script
touch /tmp/pwn /tmp/college
/challenge/run

# remove a file and run check
rm ~/delete_me
/challenge/check

# move the /flag as requested
mkdir -p /tmp/hack-the-planet
mv /flag /tmp/hack-the-planet
/challenge/check

# create a symlink to trick the provided reader
ln -s /flag /home/hacker/not-the-flag
cat /challenge/catflag
```

## What I learned

- Practical usage patterns for foundational Linux utilities: how to read files (`cat`), search (`grep`), compare (`diff`), list (`ls`), create (`touch`, `mkdir`), remove (`rm`), move (`mv`), search recursively (`find`), and create symlinks (`ln -s`).
- Techniques for working around restricted shells or limited guidance: using absolute paths, `find` across the filesystem`, and symlinks to redirect access.
- How to parse challenge prompts carefully to identify which tool is required (e.g., large files -> `grep`, file differences -> `diff`).
- Handling noisy output and permission errors when searching system directories (redirecting stderr with `2>/dev/null`).

## References

- Built-in challenge DESCRIPTION and hints (local `/challenge/DESCRIPTION.md`).
- `man` pages and `--help` output for: `cat`, `grep`, `diff`, `ls`, `touch`, `rm`, `mv`, `find`, and `ln`.
- General Linux command tutorials and reference guides used while learning these utilities.

---

*Report generated from session notes and provided flags. If you want this exported as a single ************`.md`************ file for download or edited to change formatting (e.g., include timestamps, screenshots, or step-by-step terminal transcripts), tell me what to adjust and I will update the document.*
