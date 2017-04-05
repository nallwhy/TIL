## How To SSH Run Multiple Command On Remote Machine And Exit Safely

https://www.cyberciti.biz/faq/linux-unix-osx-bsd-ssh-run-command-on-remote-machine-server/

```bash
$ ssh bar@foo "command1 && command2"

# OR

ssh bar@foo << HERE
  command1
  command2
HERE
```

See also

```bash
A; B    # Run A and then B, regardless of success of A
A && B  # Run B if A succeeded
A || B  # Run B if A failed
A &     # Run A in background.
```