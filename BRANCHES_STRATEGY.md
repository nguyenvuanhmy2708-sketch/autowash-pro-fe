# Git Branches Strategy

## Branch Types

### 1. main
- **Purpose**: Production-ready code
- **Rules**: 
  - Only merge from release/hotfix branches
  - Must pass all CI/CD tests
  - Always tagged with version numbers
- **Usage**: Never commit directly here

### 2. develop
- **Purpose**: Development branch, integration point
- **Rules**:
  - Merge from feature branches via Pull Request
  - Must pass all tests before merge
  - Latest development code
- **Usage**: Base branch for all feature branches

### 3. feature/*
- **Purpose**: New features or enhancements
- **Naming**: `feature/feature-name`
  - Example: `feature/login-page`, `feature/payment-api`
- **Usage**:
  1. Create from `develop`: `git checkout -b feature/my-feature develop`
  2. Work and commit
  3. Push: `git push -u origin feature/my-feature`
  4. Create Pull Request to `develop`
  5. After review/approval, merge to `develop`
  6. Delete branch: `git branch -d feature/my-feature`

### 4. bugfix/*
- **Purpose**: Bug fixes
- **Naming**: `bugfix/bug-description`
  - Example: `bugfix/fix-login-error`, `bugfix/auth-token-expiry`
- **Usage**: Same as feature branches but for bug fixes

### 5. hotfix/*
- **Purpose**: Critical production fixes
- **Naming**: `hotfix/issue-description`
  - Example: `hotfix/payment-gateway-down`
- **Usage**:
  1. Create from `main`: `git checkout -b hotfix/issue main`
  2. Fix and test thoroughly
  3. Merge to both `main` and `develop`
  4. Tag with version
  5. Delete branch

### 6. release/*
- **Purpose**: Prepare release version
- **Naming**: `release/v1.0.0`
- **Usage**:
  1. Create from `develop`: `git checkout -b release/v1.0.0 develop`
  2. Only bug fixes and version bumps
  3. Merge to `main` with version tag
  4. Merge back to `develop`

---

## Workflow Example

```
develop (main work branch)
   ↓
feature/login-page (create your work)
   ↓
commit → commit → commit
   ↓
git push -u origin feature/login-page
   ↓
Create Pull Request on GitHub
   ↓
Code review by teammates
   ↓
Merge to develop
   ↓
Delete feature/login-page
```

---

## Quick Commands

```bash
# Create feature branch
git checkout -b feature/my-feature develop

# Switch to existing branch
git checkout feature/my-feature

# List all branches
git branch -a

# Delete local branch
git branch -d feature/my-feature

# Delete remote branch
git push origin --delete feature/my-feature

# Update your branch with latest develop
git pull origin develop
git rebase develop

# Push your branch
git push

# View branch history
git log --oneline --graph
```

---

## Rules to Follow

✅ **DO:**
- Always create feature branch from `develop`
- Write clear commit messages
- Pull latest before pushing
- Review code before merging
- Delete branches after merge
- Test before creating PR

❌ **DON'T:**
- Don't push directly to `main`
- Don't force push to shared branches
- Don't commit secrets or sensitive data
- Don't merge without testing
- Don't commit large files
