
# GitHub Multi-Account Setup (Windows)

This repository documents the steps to configure and manage multiple GitHub accounts (e.g., Company A and Company B) on a single Windows machine using SSH.

---

## 🔧 Setup Instructions

### 1. Generate SSH Keys

```bash
# For Company A
ssh-keygen -t ed25519 -C "you@companya.com" -f ~/.ssh/id_ed25519_companya

# For Company B
ssh-keygen -t ed25519 -C "you@companyb.com" -f ~/.ssh/id_ed25519_companyb
````

---

### 2. Add SSH Keys to Agent

```bash
# Start ssh-agent
eval "$(ssh-agent -s)"

# Add private keys
ssh-add ~/.ssh/id_ed25519_companya
ssh-add ~/.ssh/id_ed25519_companyb
```

---

### 3. Add Public Keys to GitHub

Copy and paste the public key content into your GitHub settings:

```bash
cat ~/.ssh/id_ed25519_companya.pub
cat ~/.ssh/id_ed25519_companyb.pub
```

* Go to each GitHub account → **Settings → SSH and GPG Keys** → **New SSH key**

---

### 4. Configure SSH Config

Edit your SSH config file (`~/.ssh/config`) as follows:

```ssh
# Company A
Host github-companya
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_companya

# Company B
Host github-companyb
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_companyb
```

---

### 5. Clone Repos with Custom Host

```bash
# For Company A
git clone git@github-companya:CompanyA/repo-name.git

# For Company B
git clone git@github-companyb:CompanyB/repo-name.git
```

---

### 6. Set Git User Identity per Repository

```bash
# Inside Company A project
git config user.name "Your Name A"
git config user.email "you@companya.com"

# Inside Company B project
git config user.name "Your Name B"
git config user.email "you@companyb.com"
```

---

## ✅ Result

* Seamless switching between accounts
* No credential conflict
* Clear SSH routing via `~/.ssh/config`

---

## 📂 Example Directory Structure

```
C:/Projects
├── company-a/
│   └── repo-a (uses github-companya)
└── company-b/
    └── repo-b (uses github-companyb)
```

---

## 🧠 Tip

Use different terminal profiles or aliases (like PowerShell profiles) to quickly navigate and work under each identity.

---

## 📜 License

MIT License

```
