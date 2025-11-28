# linux-pc-config 💻🐧🔧

[Ansible](https://www.ansible.com/) playbooks to configure a freshly installed [Fedora Linux 42 Workstation](https://fedoraproject.org/workstation/download).

If you want to adapt it to your needs, feel free to [fork it](https://github.com/le-chartreux/linux-pc-config/fork)!

Many tasks are inspired by [devangshekhawat's Fedora-42-Post-Install-Guide](https://github.com/devangshekhawat/Fedora-42-Post-Install-Guide) - thanks for the excellent base!

> [!NOTE]  
> Only tested on my Lenovo ThinkPad X1 Carbon Gen 10 (dual-boot with Windows 11).

## 📑 Table of Contents

- [linux-pc-config 💻🐧🔧](#linux-pc-config-)
  - [📑 Table of Contents](#-table-of-contents)
  - [🐧 Usage](#-usage)
  - [🛠️ Troubleshooting](#️-troubleshooting)
    - [EFI Partition Error](#efi-partition-error)
  - [✋ Manual Steps](#-manual-steps)
    - [🦑 GitHub SSH Key Setup](#-github-ssh-key-setup)
    - [🔄 Reboot](#-reboot)

## 🐧 Usage

1. Clone the repository:

   ```bash
   git clone https://github.com/le-chartreux/linux-pc-config.git
   # Also change the branch if necessary.
   ```

2. Create a virtual environment:

   ```bash
   python -m venv .venv
   source .venv/bin/activate
   pip install .  # pip install -e ".[dev]" for development
   ```

3. Install the needed Ansible plugins:

   ```bash
   ansible-galaxy install -r requirements.yml
   ```

4. Adapt the `vars` on the playbooks (e.g., keyboard device in *keyboard.yml*).

5. Run the full configuration playbook:

   ```bash
   ansible-playbook playbooks/site.yml --ask-become-pass --verbose
   ```

## 🛠️ Troubleshooting

### EFI Partition Error

If you get an error related to */boot/efi* during the `Update devices` task:

- A system update might already be in progress.
- **Solution**: Reboot your machine to let the update finish, then re-run the playbook.

## ✋ Manual Steps

Some steps can't (yet) be automated.
Please perform these manually after the playbook run.

### 🦑 GitHub SSH Key Setup

1. Generate an SSH key:

   ```bash
   ssh-keygen -t ed25519 -C "your-email@example.com"
   ```

2. Copy the public key to your clipboard:

   ```bash
   wl-copy < ~/.ssh/id_ed25519.pub
   ```

3. Add the key to your GitHub account:  
   👉 [GitHub SSH Keys](https://github.com/settings/ssh/new)

### 🔄 Reboot

Finally, restart your computer to apply all system-level changes.
