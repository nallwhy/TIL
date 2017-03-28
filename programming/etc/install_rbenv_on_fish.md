## Install rbenv on fish

### Install rbenv via brew
```bash
$ brew install rbenv
```

### Run rbenv init
```bash
$ rbenv init
# Load rbenv automatically by appending
# the following to ~/.config/fish/config.fish:

status --is-interactive; and source (rbenv init -|psub)
```

Add `status --is-interactive; and source (rbenv init -|psub)` to `~/.config/fish/config.fish`.

Finished!
