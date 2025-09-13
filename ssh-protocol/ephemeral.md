---
description: Run bash commands or full scripts entirely in memory on a Linux target via NetExec SSH.
---

# Ephemeral (in-memory) Module

## Description

The `ephemeral` module runs bash commands or entire scripts **entirely in memory** on a Linux target via SSH.  
No files are written to the remote disk by the module — the script/command is streamed into `/bin/bash -s` and executed. Output (stdout/stderr) is streamed live back to the operator and logged only on the operator machine.

**Module name:** `ephemeral`  
**Protocol:** `ssh`  
**Category:** `ENUMERATION`

---

## Supported options

- `-o COMMAND="<single shell command>"`  
  Run a single command string in memory.

- `-o SCRIPT=/path/to/local/script.sh`  
  Read a local script file and run it in memory on the target. The local file is read by the operator and sent over the SSH session — nothing is written to disk on the remote host.

Notes:
- If neither `COMMAND` nor `SCRIPT` is provided, the module will fall back to NetExec's `-x` single-command (`args.execute`) if NetExec provided it.
- The module does **not** parse or split multiple `-x` invocations — it uses the single `-x` command NetExec passes.

---

## Usage examples

### Run a one-liner with `-o COMMAND`
```bash
nxc ssh 192.168.14.131 -u ubuntu -p ubuntu -M ephemeral -o COMMAND="whoami"

### Run a one-liner with `-o SCRIPT`

```bash
nxc ssh 192.168.14.131 -u ubuntu -p ubuntu -M ephemeral -o SCRIPT="linpeas.sh"```
