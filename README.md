# linux-pc-config 💻🐧🔧

[Ansible](https://www.ansible.com/) playbooks to configure a freshly installed [Fedora Linux 43 Workstation](https://fedoraproject.org/workstation/download).

If you want to adapt it to your needs, feel free to [fork it](https://github.com/le-chartreux/linux-pc-config/fork)!

Many tasks are inspired by [devangshekhawat's Fedora-43-Post-Install-Guide](https://github.com/devangshekhawat/Fedora-43-Post-Install-Guide) - thanks for the excellent base!

> [!NOTE]  
> Tested only on my Lenovo ThinkPad X1 Carbon Gen 10. Should work with a dual-boot setup alongside Windows 11 (it was working before I stopped dual-booting).

## 📑 Table of Contents

- [linux-pc-config 💻🐧🔧](#linux-pc-config-)
  - [📑 Table of Contents](#-table-of-contents)
  - [🐧 Usage](#-usage)
  - [🛠️ Troubleshooting](#️-troubleshooting)
    - [💿 EFI Partition Error](#-efi-partition-error)
  - [✋ Manual Steps](#-manual-steps)
    - [🦑 GitHub SSH Key](#-github-ssh-key)
  - [🧪 For Development](#-for-development)
    - [📝 TODOs](#-todos)

## 🐧 Usage

1. [Set up your GitHub SSH key](#-github-ssh-key) to enable cloning via SSH.

2. Clone the repository:

   ```bash
   git clone git@github.com:le-chartreux/linux-pc-config.git
   cd linux-pc-config/
   # Also change the branch if necessary.
   ```

3. Create a virtual environment:

   ```bash
   python -m venv .venv
   source .venv/bin/activate
   pip install .
   ```

4. Run the full configuration playbook:

   ```bash
   ansible-playbook playbooks/site.yml --ask-become-pass --verbose
   ```

5. Restart your computer to apply all system-level changes.

6. Do the [manual steps](#-manual-steps) you haven't done yet.

## 🛠️ Troubleshooting

### 💿 EFI Partition Error

If you get an error related to */boot/efi* during the `Update devices` task:

- A system update might already be in progress.
- **Solution**: Reboot your machine to let the update finish, then re-run the playbook.

## ✋ Manual Steps

Some steps aren’t automated because they either can’t be or would be too invasive.

### 🦑 GitHub SSH Key

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

## 🧪 For Development

Set up a development environment:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -e ".[dev]"
```

### 📝 TODOs

- Cargo setup.
- Tmux config (or zellij?): persistency & fancy.
