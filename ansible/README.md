
1. Install ansible and grab repository. `ansible/install` has the script for this, but it won't be present with new image
2. Generate ssh keys with ssh2.yml playbook and update github, `ansible-playbook ssh2.yml`
3. `git pull` to retrieve dotfiles
4. make sure you've opened the MATE desktop, not gnome; `sudo ansible-playbook local.yml`

