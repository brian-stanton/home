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

1. Install git and clone this repo to `~/Documents/code/home`
2. `sudo ./ansible/bootstrap` — ansible, sudo for **your login**, clone there if needed
3. As that same user: `cd ~/Documents/code/home && ./ansible/install linux`
4. Reboot (or log out) and pick the MATE session. i3 is the window manager.
5. Optional: `./ansible/install ssh`, then add the key to GitHub

On a Mac, skip bootstrap. Homebrew and Ansible are installed if they are missing.

### Linux desktop (MATE + i3)

A full Linux run installs this. You do not opt in separately, and you do not
need `DISPLAY` set.

```bash
./ansible/install linux            # everything, including desktop
./ansible/install linux desktop    # only the desktop stack
./ansible/install linux i3         # same tag as desktop
```

That installs `i3`, `ubuntu-mate-desktop`, compton, etc., links
`~/.config/i3` and `~/.config/i3status`, and points MATE at i3.

`HOME_HEADLESS=1` is only for the Docker test image. It skips the MATE `dconf`
session commands (no graphical session in the container). Packages and config
links still run if you asked for `desktop`. Do not set this on a real machine.

### Notes

- Neovim is **built from source** next to this repo (`../neovim`, e.g. `~/Documents/code/neovim` on Linux) and installed to `~/.local` (no sudo). The first run clones `stable`; later runs never overwrite the checkout, then `make` + `make install` from whatever is in that tree. `~/.local/bin` is on PATH via `.zsh_profile`.
- Dotfiles are **linked**, not copied. Edits in `~/.config/nvim` or `~/.tmux.conf` are edits in the repo.
- Tmux: `./ansible/install tmux` installs the binary and links `dotfiles/.tmux.conf`. Prefix is `C-a`. Reload with `prefix r`.
- Alacritty on Mac comes from the official GitHub dmg (Homebrew disabled the cask — Gatekeeper). Linux still builds with cargo.
- Docker is for testing the Ubuntu target: `docker compose -f ansible/docker-compose.yml build`. The image user is your host login (`$USER`), not a hardcoded name. Override with `HOME_USER=...` if needed.
- Resolution in a VM: `xrandr --output Virtual-1 --mode 1920x1080`
