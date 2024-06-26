# Design goals

*26 Mar 2024: Not completed yet*

- Doesn't change behaviour for git / ssh for non-keycutter keys
- Re-runnable
- Security & Transparency
	- Affordably auditable
    - Bash script that uses standard tools
- Well documented
- Insanely great

## Project Transparency

Recognising that SSH keys shouldn't be trusted to untrusted software, keycutter
has been built with transparency in mind. The goal is to keep it so simple that
ROI should be achieved on first use, even if you take the time to audit the
commands. 

Running `keycutter create` will print each command and request confirmation before running it. 

This can be modified with:

- `--dry-run`:  show commands that will be run but don't run
- `--no-confirm`: Don't request confirmation for every command 
