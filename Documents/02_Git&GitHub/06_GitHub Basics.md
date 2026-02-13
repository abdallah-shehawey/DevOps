# 📘 GitHub – Full Basics & Practical Guide (Not Git)

> This guide covers **GitHub only** (remote repositories, collaboration, organizations, PRs, permissions, .gitignore, README best practices).  
> It assumes you already know **Git basics** (init, add, commit, branches, merge, rebase).

---

## ❓ Why GitHub?

GitHub is a **cloud platform** for hosting Git repositories and enabling collaboration.

**Use cases:**

- **Personal storage:** Keep your projects backed up online and accessible from anywhere.

- **Multi-developer collaboration:** Multiple developers can work on the same codebase.

- **Contributions & open-source:** Contribute to public projects, submit fixes and features.

- **Code review:** Pull Requests enable discussion and review before merging.

- **Issues & project management:** Track bugs, features, and tasks.

- **CI/CD integrations:** Automate testing and deployments.

---

## 🌐 GitHub Repositories (Remote)

### Create a new repo locally and connect to GitHub

```bash
echo "# git_playground" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/USERNAME/git_playground.git
git push -u origin main
```

### Connect an existing local repo to GitHub

```bash
git remote add origin https://github.com/USERNAME/git_playground.git
git branch -M main
git push -u origin main
```

### Explanation

```bash
git branch -M main
```

- `-M` forcefully renames the current branch to **main** (instead of `master` or any other name).

```bash
git remote add origin https://github.com/USERNAME/repo.git
```

- `remote`: connect your local repo to a remote repo on GitHub.

- `origin`: a **shortcut name** for the remote URL (you can name it anything, but `origin` is the convention).

```bash
git push -u origin main
```

- `push`: upload your commits to GitHub.

- `origin`: remote name (URL shortcut).

- `main`: target branch on GitHub.

- `-u` (upstream): sets the default remote/branch so next time you can use `git push` only.

---

## 🔐 Authentication & Common Error (403)

You might see:

```text
remote: Permission to USER/repo.git denied.
fatal: unable to access 'https://github.com/USER/repo.git/': 403
```

**Why this happens:**

- You’re not authenticated.

- You don’t have permission on that repo.

- You’re using HTTPS without a Personal Access Token (PAT).

**Fix (Recommended):**

- Use **GitHub Personal Access Token (PAT)** instead of password.

- Or use **SSH keys** and push via SSH URL:

```bash
git remote set-url origin git@github.com:USERNAME/repo.git
```

---

## 🌿 Remote Branches & Tracking

List all branches (local + remote-tracking):

```bash
git branch -a
```

List remote-tracking branches only:

```bash
git branch -r
```

### Fetch vs Pull

```bash
git fetch origin
```

- Updates **remote-tracking branches** only.

- Does **not** change your local working branch.

```bash
git pull origin main
```

- `pull` = `fetch` + `merge`

- Updates your local branch with remote changes.

---

## 🧹 Deleting Remote Branches

Delete locally:

```bash
git branch -D branchname
```

Delete on GitHub (remote):

```bash
git push origin --delete branchname
```

> Note: `--delete` removes the branch from the **remote repository**.

---

## 📥 Cloning a Repository

```bash
git clone https://github.com/USERNAME/repo.git
```

This downloads the repo and automatically sets:

- `origin` remote

- default upstream branch

---

## 🍴 Fork & Pull Request (PR)

### Fork

- A **fork** is your personal copy of someone else’s repository on your GitHub account.

- Used when you **don’t have write access** to the original repo.

### Typical Fork Workflow

1. Fork the repo on GitHub.

2. Clone your fork:

```bash
git clone https://github.com/YOUR_USERNAME/repo.git
```

1. Add upstream (original repo):

```bash
git remote add upstream https://github.com/ORIGINAL_OWNER/repo.git
```

1. Create a feature branch:

```bash
git switch -c feature-x
```

1. Push changes to your fork:

```bash
git push origin feature-x
```

1. Open a **Pull Request** from your fork → original repo.

### Pull Request (PR)

- A PR is a **request to merge your changes** into another branch/repo.

- Enables:

  - Code review

  - Discussion

  - CI checks before merge

---

## 🏢 GitHub Organizations

Organizations are used to manage **teams, permissions, and repositories** for companies, teams, or communities.

### Benefits

- Centralized repo ownership

- Role-based access control

- Teams for managing permissions

- Better security & auditing

- Scales well for large teams

### Roles & Permissions

#### 👤 Members

- Part of the organization.

- Can be assigned to teams.

- Permissions depend on team/repo access.

#### 🤝 Outside Collaborators

- Not organization members.

- Granted access to **specific repositories only**.

- Useful for contractors or external contributors.

#### 👥 Teams

- Group members into teams (e.g., Backend, Frontend, DevOps).

- Assign permissions to teams instead of individuals:

  - **Read**: view code

  - **Triage**: manage issues/PRs

  - **Write**: push to repo

  - **Maintain**: manage repo settings (limited)

  - **Admin**: full control

### Permissions Scope

Permissions can be applied at:

- Organization level

- Team level

- Repository level

This gives fine-grained control over:

- Who can push

- Who can review

- Who can manage settings

---

## 🚫 .gitignore (Secrets & Private Files)

Use `.gitignore` to prevent sensitive or unnecessary files from being pushed:

**Examples:**

- API keys

- Secret tokens

- Environment files

- Build artifacts

- IDE configs

Example `.gitignore`:

```gitignore
.env
*.key
*.pem
node_modules/
build/
dist/
```

> ⚠️ Never push secrets to GitHub. If you did, rotate the key immediately.

---

## 📝 README Files on GitHub

### Repository README

- Explains:

  - What the project does

  - How to install

  - How to run

  - How to contribute

  - License

### GitHub Profile README

Create a repo named exactly like your username:

```
USERNAME/USERNAME
```

Your `README.md` will appear on your GitHub profile.

You can use profile README generators to quickly scaffold sections like bio, skills, stats, badges, and featured projects.

---

## 🔒 Best Practices

- Use SSH or PAT for authentication

- Protect `main` branch (require PRs)

- Use meaningful PR titles & descriptions

- Review code before merging

- Keep secrets out of repos

- Use Issues for tracking work

---

## ✅ Summary

- GitHub is for **hosting, collaboration, and code review**.

- Use **push/pull/fetch** to sync with remote.

- Use **fork + PR** when you don’t have write access.

- Use **organizations & teams** for scalable permission management.

- Protect secrets with **.gitignore**.

- Write a clear **README** for every repo.

---

**End of GitHub Guide 🚀**
