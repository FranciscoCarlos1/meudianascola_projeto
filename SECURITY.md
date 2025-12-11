# Security Policy

## ⚠️ Important: Never Embed Credentials in Git Remote URLs

**DO NOT** use commands like this:
```powershell
git remote set-url origin https://username:TOKEN@github.com/repo.git
```

This is a **critical security vulnerability** because:
- Personal Access Tokens (PATs) are exposed in plain text
- Credentials may be accidentally committed to the repository
- Tokens can appear in git history, logs, and error messages
- Anyone with access to the repository can see and misuse these credentials

## ✅ Recommended Authentication Methods

### Option 1: SSH Keys (Recommended)
1. Generate an SSH key:
   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```
2. Add the SSH key to your GitHub account (Settings → SSH and GPG keys)
3. Use SSH remote URL:
   ```bash
   git remote set-url origin git@github.com:FranciscoCarlos1/meudianascola_projeto.git
   ```

### Option 2: GitHub CLI
1. Install [GitHub CLI](https://cli.github.com/)
2. Authenticate:
   ```bash
   gh auth login
   ```
3. GitHub CLI manages credentials securely

### Option 3: Git Credential Manager
1. Install [Git Credential Manager](https://github.com/git-ecosystem/git-credential-manager)
2. Use HTTPS URL without credentials:
   ```bash
   git remote set-url origin https://github.com/FranciscoCarlos1/meudianascola_projeto.git
   ```
3. Credential manager will prompt for authentication and store it securely

## 🔒 If You've Accidentally Exposed a Token

1. **Immediately revoke the token** on GitHub (Settings → Developer settings → Personal access tokens)
2. Generate a new token
3. Update your local git configuration using one of the secure methods above
4. If the token was committed to git history, consider it compromised permanently

## 📝 Best Practices

- Never commit `.env` files or configuration files with credentials
- Use environment variables for sensitive data
- Add credential files to `.gitignore`
- Regularly rotate access tokens
- Use tokens with minimal required permissions
- Enable two-factor authentication (2FA) on your GitHub account

## Reporting Security Issues

If you discover a security vulnerability, please email the repository maintainer instead of opening a public issue.
