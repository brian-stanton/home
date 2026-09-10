Provision this machine from the repo root. Do not run the playbook with `sudo`;
tasks escalate on their own.

```bash
./ansible/install              # everything for this OS
./ansible/install neovim       # just neovim + its config
./ansible/install mac neovim   # require macOS
./ansible/install linux git    # require Ubuntu/Debian
./ansible/install --list
./ansible/install --check neovim
```

`./install` is the same command. Targets are `mac` and `linux`. If you omit the
target, Ansible uses the machine you are on (`Darwin` or `Debian`).

### First boot (bare Ubuntu)

1. Install git and clone this repo
2. `sudo ./ansible/bootstrap` — ansible, user `abf`, clone to `~/home`
3. As `abf`: `git submodule update --init --recursive`
4. `./ansible/install linux`
5. Optional: `./ansible/install ssh`, then add the key to GitHub

On a Mac, skip bootstrap. Homebrew and Ansible are installed if they are missing.

### Notes

- Neovim is **built from source** on both targets at `~/personal/code/neovim` and installed to `~/.local` (no sudo). The first run clones `stable`; later runs never overwrite the checkout, then `make` + `make install` from whatever is in that tree. `~/.local/bin` is on PATH via `.zsh_profile`.
- Dotfiles are **linked**, not copied. Edits in `~/.config/nvim` or `~/.tmux.conf` are edits in the repo.
- Tmux: `./ansible/install tmux` installs the binary and links `dotfiles/.tmux.conf`. Prefix is `C-a`. Reload with `prefix r`.
- Alacritty on Mac comes from the official GitHub dmg (Homebrew disabled the cask — Gatekeeper). Linux still builds with cargo.
- Linux desktop bits (MATE, i3, `xset`) skip themselves when `DISPLAY` is unset or `HOME_HEADLESS=1`.
- Docker is for testing the Ubuntu target: `docker compose -f ansible/docker-compose.yml build`
- Resolution in a VM: `xrandr --output Virtual-1 --mode 1920x1080`
