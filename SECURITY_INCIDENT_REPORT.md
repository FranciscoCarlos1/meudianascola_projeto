# Security Incident Report

## 🚨 Exposed Credential Alert

**Date**: December 11, 2025  
**Severity**: CRITICAL  
**Status**: Mitigated

## Issue Description

A PowerShell command containing an embedded GitHub Personal Access Token (PAT) was identified:

```powershell
git remote set-url origin https://franciscosousa-github:github_pat_11AWJU3UY0...@github.com/...
```

This token was **exposed in the problem statement** and should be considered **compromised**.

## Risk Assessment

**High Risk** - The exposed token:
- ✅ Was NOT committed to the git repository
- ✅ Does NOT appear in git history
- ⚠️ Was visible in the problem statement/issue
- ⚠️ May have been shared or logged elsewhere

## Immediate Actions Required

### 1. Revoke the Exposed Token (URGENT)

**The token `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` must be revoked immediately.**

Steps to revoke:
1. Go to https://github.com/settings/tokens
2. Find the token in the list (it may be named or show creation date)
3. Click "Delete" or "Revoke"
4. Confirm the revocation

### 2. Generate a New Token (if needed)

If you still need a Personal Access Token:
1. Go to https://github.com/settings/tokens
2. Click "Generate new token" → "Generate new token (classic)"
3. Give it a descriptive name (e.g., "Local Development - [Your Computer]")
4. Select only the minimum required scopes (e.g., `repo` for private repositories)
5. Set an expiration date (recommended: 90 days or less)
6. Click "Generate token"
7. **Store it securely** using one of the methods in AUTHENTICATION_GUIDE.md

### 3. Use Secure Authentication

**Never embed credentials in git URLs again.** Instead, use one of these secure methods:

#### Recommended: SSH Keys
```bash
git remote set-url origin git@github.com:FranciscoCarlos1/meudianascola_projeto.git
```

#### Alternative: GitHub CLI
```bash
gh auth login
git remote set-url origin https://github.com/FranciscoCarlos1/meudianascola_projeto.git
```

See [AUTHENTICATION_GUIDE.md](AUTHENTICATION_GUIDE.md) for complete setup instructions.

## Actions Taken

✅ **Verified** no credentials in git repository or history  
✅ **Created** SECURITY.md with security policies  
✅ **Created** AUTHENTICATION_GUIDE.md with secure authentication methods  
✅ **Created** .gitignore to prevent accidental credential commits  
✅ **Updated** README.md with security notices  
✅ **Documented** proper authentication procedures

## Prevention Measures

The following measures are now in place to prevent future incidents:

1. **Security Policy** ([SECURITY.md](SECURITY.md))
   - Clear guidelines on credential handling
   - What to do if credentials are exposed

2. **.gitignore File**
   - Prevents common credential files from being committed
   - Includes .env files, key files, and configuration files

3. **Authentication Guide** ([AUTHENTICATION_GUIDE.md](AUTHENTICATION_GUIDE.md))
   - Step-by-step secure authentication setup
   - Multiple authentication methods documented

4. **Updated README**
   - Security notice prominently displayed
   - Links to security documentation

## Recommendations

1. **Immediate**: Revoke the exposed token
2. **Before next use**: Set up SSH or GitHub CLI authentication
3. **Ongoing**: Review git configuration periodically to ensure no credentials are embedded
4. **Best Practice**: Enable 2FA on your GitHub account if not already enabled
5. **Team Practice**: Share SECURITY.md and AUTHENTICATION_GUIDE.md with all contributors

## Verification Checklist

- [ ] Exposed token has been revoked on GitHub
- [ ] New secure authentication method is configured (SSH/GitHub CLI/Credential Manager)
- [ ] Git remote URL contains no credentials (`git remote -v` to verify)
- [ ] Team members have been notified of security best practices
- [ ] 2FA is enabled on GitHub account

## References

- [GitHub Token Security Best Practices](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github)
- [GitHub's Security Advisories](https://docs.github.com/en/code-security/security-advisories)
- [OWASP Credential Management](https://cheatsheetseries.owasp.org/cheatsheets/Credential_Management_Cheat_Sheet.html)

## Contact

For questions about this incident or security practices, contact the repository maintainer.

---

**Note**: This document should be kept for record-keeping purposes but does not need to be shared publicly if the repository is private.
