
1. Install git and grab repository
2. Run `ansible/install`
3. Generate ssh keys with ssh2.yml playbook and update github, `ansible-playbook ssh2.yml`
4. `git submodule update --init --recursive` to retrieve dotfiles
5. Make sure you've opened the MATE desktop, not gnome; `sudo ansible-playbook linux.yml` or `sudo ansible-playbook mac.yml`; note the username in the .yml files

### Notes
- the Dockerfile is for testing. It mainly does what `ansible/install` does, then needs some adjusting like skipping the i3 tasks in `ansible/tasks/core-setup.yml` to avoid playbook failures. Not gonna document all the cases there
- remember: `xrandr --output Virtual-1 --mode 1920x1080` for resolution changes, as an example; `xrandr --listmonitors` for monitor info

