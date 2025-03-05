
1. Install ansible and grab repository. `ansible/install` has the script for this
2. Generate ssh keys with ssh2.yml playbook and update github, `ansible-playbook ssh2.yml`
3. `git submodule update --init --recursive` to retrieve dotfiles
4. make sure you've opened the MATE desktop, not gnome; `sudo ansible-playbook linux.yml` or `sudo ansible-playbook mac.yml`

### Notes
- the Dockerfile is for testing. It mainly does what `ansible/install` does, then needs some adjusting like skipping the i3 tasks in `ansible/tasks/core-setup.yml` to avoid playbook failures. Not gonna document all the cases there

