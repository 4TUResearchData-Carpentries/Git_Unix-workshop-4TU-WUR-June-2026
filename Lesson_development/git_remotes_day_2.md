
## 🛰️ Day 2: Working with Remotes and Collaborating on GitHub

### 🧭  — Recap of local Git
### 🧭  — Intro to Remotes
### 🧭  — Push/Pull

> **Instructor Note:** Introduce the idea of remote repositories using slides. Explain what GitHub is, how it connects to local repositories, and why remotes are important for collaboration and backup.

---

### 🌐 Connecting to GitHub \[20 min]

#### a. Create a GitHub Repository

> Ask participants to log into GitHub and create an **empty public repository** named `patients-analysis`.

* Description suggestion: *Analysis of different clinical treatments*

#### b. Connect Local Repo to Remote

##### b0. SSH Setup for GitHub Access (**Technical Break**, 30 min)

> **Instructor Note:** Use slides or a diagram to explain SSH authentication, its benefits over HTTPS, and GitHub’s two-factor authentication requirements.

Steps to generate and configure an SSH key:

```bash
cd ~
ssh-keygen -t ed25519 -C "your_email@example.com"
# Choose default location: ~/.ssh/id_ed25519
```

✅ **Email requirements:**

* The email in this command doesn't need to match your GitHub account.
* Still, using a verified GitHub email is recommended for clarity and organization.

Check generated files:

```bash
ls ~/.ssh/
```

Start the SSH agent and add the key:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

Copy the public key:

```bash
clip < ~/.ssh/id_ed25519.pub  # Windows
# or
cat ~/.ssh/id_ed25519.pub     # For manual copy
```

On GitHub:

* Go to **Settings → SSH and GPG keys → New SSH key**
* Paste the key and name it clearly (e.g., `workshop-laptop`)

Test the SSH connection:

```bash
ssh -T git@github.com
```

🔗 Resources:

* [GitHub SSH Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
* [Troubleshooting SSH](https://docs.github.com/en/authentication/troubleshooting-ssh)

#### b1. Add the Remote and Push

Return to your project folder:

```bash
cd ~/Desktop/patients
```

Link to the remote repository:

```bash
git remote add origin git@github.com:<your-username>/patients-analysis.git
git remote -v
```

Set default branch and push:

```bash
git branch -M main
git push -u origin main
```

To pull future updates:

```bash
git pull origin main
```

> Questions? Clarify remote tracking, default branches, and pushing/pulling.

---

### 🖥️ Optional: Explore GitHub Web GUI

> **Instructor Note:** Quickly tour the GitHub interface: file browser, commit history, branches, issues, pull requests.

---

## ☕ 10:45 - 11:00 – Break

Invite participants to join `workshop-check-in` repo as collaborators before resuming.

---
11:00 - 12:00 
## 🤝 Collaboration Practice: Hands-On Session issues? 

### a. Clone a Shared Repository

> Instructor shares repo URL: `https://github.com/leilaicruz/workshop-checkin`

Clone it locally:

```bash
cd ~/Desktop
git clone git@github.com:leilaicruz/workshop-checkin.git
```

> **Instructor Note:** Now contrast cloning vs forking using the table below.

| Aspect                | 🌀 Cloning                      | 🍴 Forking                               |
| --------------------- | ------------------------------- | ---------------------------------------- |
| **What it does**      | Local copy of existing repo     | Your own copy under your GitHub account  |
| **Who owns the repo** | The original owner              | You (your GitHub username)               |
| **Use case**          | Team projects with write access | Contributing to external/public projects |
| **How to contribute** | Direct push or PRs to original  | PRs from fork to upstream                |
| **Remote origin**     | Points to source repo           | Points to your fork                      |

### b. Make a Check-in Entry

Create a copy of the template and edit it:

```bash
cd workshop-checkin
cp template.md <first-two-letters-name-last-two-digits-phone>.md
nano le71.md
```

> Example name: `le71.md`. Add your name, research field and your ideal job an ideal world.

### c. Collaborative Git Workflow

A typical workflow:

```bash
git pull origin main
git add .
git commit -m "check <your-name> in"
git push origin main
```

> **Note:** This requires that participants have been added as **collaborators**.

---

### 🪄 Optional: Branches and Pull Requests (if time allows)

Create and switch to a new branch:

```bash
git switch -c <your-branch-name>
```

Edit your check-in file, stage, commit, and push:

```bash
git add check-in/<your-id>.md
git commit -m "add check-in info"
git push origin <your-branch-name>
```

> Instructor can then demonstrate how to open a Pull Request (PR) via the GitHub interface.

---

## 🧩 Final Exercise: Working with Issues and PRs

> Instructor Note: Display this on a shared screen or slide.

**demo before assignment**

1. Owner writes an issue about something is not working in the code.
2. Collaborator forks , clone , make a new branch, solve the issue and push it to the fork and create a PR.
3. Owner sees the peer and tries it locally before it can be merged.
   `git fetch origin pull/123/head:pr-123` 123 is the name of the PR
   `git checkout pr-123`
4. Owner goes to the website and merge the PR to main.

- explain visually what happens.

**Assignment:**

1. Write an Issue in your `patients-analysis` repo. Options:

   * Add a multiplication function
   * Improve `calculate_mean` with full documentation
   * Create a `README.md` file

2. Pair up:

   * Clone or fork each other’s repositories. 
   * Create a branch, solve the issue.
   * Open a Pull Request with your changes.

3. Review and integrate PRs if possible.

4. Reflect:

   * What worked well?
   * What was confusing?
   * Did you encounter merge conflicts?
   * How would you improve the process next time?

---

### 🪪 12. Licensing & Citation \[Optional, 5 min]

> Instructor Note: Briefly explain why software licensing matters for reuse and collaboration.

* Share TU Delft software template repo: [https://github.com/manuGil/fair-code](https://github.com/manuGil/fair-code)

Encourage:

* Adding a LICENSE file
* Including CITATION metadata in the repo

---

### ❓ 13. Q\&A

Open floor for questions, clarifications, and sharing experiences.
