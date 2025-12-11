# Authentication Guide for meudianascola_projeto

This guide explains how to properly authenticate with GitHub for this repository.

## 🚫 What NOT to Do

**Never use this command or similar ones:**
```powershell
git remote set-url origin https://username:TOKEN@github.com/repo.git
```

This embeds your Personal Access Token directly in the git configuration, which is:
- **Insecure**: Token is stored in plain text
- **Dangerous**: Can be accidentally exposed in logs or commits
- **Against GitHub's security best practices**

## ✅ Proper Setup Methods

### Method 1: SSH (Most Secure - Recommended)

SSH keys provide the most secure authentication without needing to enter passwords.

**Windows (PowerShell):**
```powershell
# Generate SSH key
ssh-keygen -t ed25519 -C "your_email@example.com"

# Start SSH agent
Start-Service ssh-agent

# Add key to SSH agent
ssh-add ~\.ssh\id_ed25519

# Copy public key to clipboard
Get-Content ~\.ssh\id_ed25519.pub | Set-Clipboard
```

**Linux/Mac:**
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your_email@example.com"

# Start SSH agent
eval "$(ssh-agent -s)"

# Add key to SSH agent
ssh-add ~/.ssh/id_ed25519

# Copy public key (Linux)
cat ~/.ssh/id_ed25519.pub | xclip -selection clipboard

# Copy public key (Mac)
pbcopy < ~/.ssh/id_ed25519.pub
```

**Add SSH key to GitHub:**
1. Go to https://github.com/settings/keys
2. Click "New SSH key"
3. Paste your public key
4. Click "Add SSH key"

**Update repository remote:**
```bash
git remote set-url origin git@github.com:FranciscoCarlos1/meudianascola_projeto.git
```

### Method 2: GitHub CLI

GitHub CLI provides a simple, secure authentication method.

**Installation:**
- Windows: `winget install GitHub.cli` or download from https://cli.github.com
- Mac: `brew install gh`
- Linux: See https://github.com/cli/cli/blob/trunk/docs/install_linux.md

**Setup:**
```bash
# Authenticate with GitHub
gh auth login

# Follow the prompts to authenticate via browser

# Repository remote URL can remain as HTTPS
git remote set-url origin https://github.com/FranciscoCarlos1/meudianascola_projeto.git
```

### Method 3: Git Credential Manager

Git Credential Manager securely stores credentials and handles authentication.

**Installation:**
- Included with [Git for Windows](https://git-scm.com/download/win)
- Mac: `brew install git-credential-manager`
- Linux: Download from https://github.com/git-ecosystem/git-credential-manager

**Setup:**
```bash
# Configure credential manager (if not already configured)
git config --global credential.helper manager

# Set repository remote to HTTPS (without credentials)
git remote set-url origin https://github.com/FranciscoCarlos1/meudianascola_projeto.git

# Next time you push/pull, you'll be prompted to authenticate
# Your credentials will be stored securely
```

## 🔍 Verify Your Setup

After setup, verify your authentication works:

```bash
# Check remote URL (should NOT contain credentials)
git remote -v

# Test connection with SSH
ssh -T git@github.com

# Or test by fetching
git fetch origin
```

Your remote URL should look like one of these:
- SSH: `git@github.com:FranciscoCarlos1/meudianascola_projeto.git`
- HTTPS: `https://github.com/FranciscoCarlos1/meudianascola_projeto.git`

**Never** like this:
- ❌ `https://username:token@github.com/...`

## 🆘 Troubleshooting

### "Permission denied (publickey)"
- Your SSH key isn't added to GitHub or SSH agent
- Follow the SSH setup steps above

### "Authentication failed"
- Your credentials expired or are incorrect
- Re-run `gh auth login` or regenerate credentials

### "Could not resolve host"
- Check your internet connection
- Verify the repository URL is correct

## 📚 Additional Resources

- [GitHub SSH Documentation](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- [GitHub CLI Documentation](https://cli.github.com/manual/)
- [Git Credential Manager](https://github.com/git-ecosystem/git-credential-manager)
