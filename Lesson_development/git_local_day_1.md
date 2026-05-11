# 🎓 Workshop Lesson Plan: Git Basics

**Note:** Instructor comments are marked as `> Instructor Note:` and should help guide the pacing, demonstration strategy, and what to emphasize. Everything else is intended for participants or for use during live demos.

## 🛠️ Preparation (Before Start)

To prepare your terminal for dual-pane command tracking:

```bash
# Main terminal (record command history live)
export PROMPT_COMMAND="history -a; $PROMPT_COMMAND"

# Second terminal (display ongoing history)
tail -f ~/.bash_history

# Clear history if needed
dhistory -c
```

For Windows/WSL setup:

```bash
cd /mnt/c/Users/<your-username>/OneDrive - Delft University of Technology/
export PS1='$ '
```
For mirror a window using ([Ontopreplica](https://github.com/LorenzCK/OnTopReplica))

---

## 📍 Part 1: Getting Started with Git

| Objectives                                                                 | Questions                                      |
|---------------------------------------------------------------------------|-----------------------------------------------|
| Understand the benefits of an automated version control system.           | What is version control and why should I use it? |
| Understand the basics of how automated version control systems work.      |                                               |


### 🧊 Introduction \[10 min]

* Start with [HackMD collaborative notes](https://edu.nl/xhydh) and icebreaker.
* Transition to Git introduction with [slides](https://zenodo.org/records/19603828).
* Use [Mentimeter poll](https://www.menti.com/alx2mugaqr1n) in  presenter mode .

### 🔧 Step 1: Setting Up Git \[6 min]

> Instructor Note: Sometimes Git Bash won't open via shortcut. Direct students to `C:/Git/git-bash.exe` if needed.

Test installation:

```bash
git --version
```

Get help:

```bash
git --help
# or for specific command
git init -h
```

Configure Git (only needed once):

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

Comments:
- Use the email associated with your GitHub, GitLab, Bitbucket, etc., account.

- Ensures commits are linked to your user profile.

- Enables activity tracking, avatars, and contribution graphs.

- If using Git in a university/research group context:

    - Use your institutional email if commits should be traceable to that identity.

### Configure line endings:

```bash
# Windows
git config --global core.autocrlf true
# Mac/Linux
git config --global core.autocrlf input
```

### Check configuration:

```bash
git config --global --list
```

### 📦 Step 2: Creating a Repository \[4 min]

Create and initialize project folder:

```bash
mkdir patients
cd patients
git init
```

Verify repo status:

```bash
ls -a
# Shows .git folder
git status
```

> Instructor Note: Explain that `.git` is the hidden folder tracking everything.
> Do **not** initialize repos inside subfolders—this breaks versioning logic.

---

### 📝 Step 3: Tracking Your First Change \[10 min]

Create a script:

```bash
touch calculate_mean.py
nano calculate_mean.py
```

Add the code:

```python
import numpy as np

def calculate_mean(data):
    mean = np.mean(data)
    return mean
```

Check status:

```bash
git status
```

Track and commit:

```bash
git add calculate_mean.py
# Git may show CRLF warning (safe to ignore)
git commit -m "create script for analysis"
```

> Instructor Note: Explain staging area vs history. Use slides to illustrate the **modify → add → commit** cycle.

---

### 🛠️ Step 4: Making Additional Changes \[5 min]

Add documentation to the script:

```python
""" This function computes the mean of an array.
Input: A one dimensional array
Output: The mean of the array
"""
```

Check and review differences:

```bash
git status
git diff
```

Add and commit the changes:

```bash
git add calculate_mean.py
git diff --staged
git commit -m "add docstring"
```

```bash

git show # it will show by default what was done in the last commit

```
---

### 📁 Step 5: Working with Empty Directories \[4 min]

Git won't track empty directories:

```bash
mkdir treatments
git status
git add treatments
git status  # Still no changes detected
```

Add files to track the folder:

```bash
touch treatments/aspirin.txt treatments/advil.txt
git add treatments/
git commit -m "add some treatments for patients"
ls -R
```

---

### 🚫 Step 6: Ignoring Files \[6 min]

> Instructor note explain why these ignoring files are necessary and not to include into the repository

Simulate a scenario with large/unwanted files:

```bash
mkdir data
touch data/a.dat data/b.dat big-data.zip
```

Create a `.gitignore`:

```bash
nano .gitignore
```

Contents:

```bash
# data files:
big-data.zip
data/
```

Track the ignore file:

```bash
git add .gitignore
git commit -m "Ignoring data files"
git status --ignored
```

---

## 🧪 Hands-On Exercise: Modify, Add, Commit \[15 min]

> Instructor Note: Use breakout groups. Let participants try each step, then show the solution. Each task: 1–2 minutes.

Assignment:

**Create new repository and use the modify-add-commit cycle.**
- Create and initialize a repository called ‘my-repo’
- Create a file ‘research.txt’ with the sentence “Science is awesome”.
- Add and commit the changes. Remember to use a meaningful message.
- Change sentence in ‘research.txt’ to “Science is messy”
Add and commit.
- Create a folder called “raw-data”
- Ignore the raw-data folder and commit it 
- ( bonus) Check your history log – you should have 3 commits. 


Steps:

```bash
mkdir my-repo && cd my-repo
git init
nano research.txt  # Add "Science is awesome"
git add research.txt
git commit -m "add awesome science"

nano research.txt  # Change to "Science is messy"
git add research.txt
git commit -m "change to messy science"

mkdir raw-data
touch .gitignore
nano .gitignore  # Add: raw-data/
git add .gitignore
git commit -m "ignore raw data folder"

git log --oneline --graph
```

---

## 🔍 Part 2: Exploring Git History \[16 min]

### a. View the Log

```bash
git log
git log --oneline
git log --graph
git log > changelog.txt
```

> Instructor Note: Explain paging (Q = quit, / = search, N = next match).

### b. Understanding HEAD

> HEAD is a reference to the most recent commit in the current branch (`main` or `master`).
> As we saw in the previous episode, we can refer to commits by their identifiers. You can refer to the most recent commit of the working directory by using the identifier _HEAD_.
>We’ve been adding small changes at a time to calculate_mean.py, so it’s easy to track our progress by looking, so let’s do that using our HEADs. Before we start, let’s make a change to calculate_mean.py, adding some lines.
> Visualize with https://edu.nl/bvu6x 

### c. Add a Usage Example

```bash
nano calculate_mean.py
```

```python
# Usage:
# data=np.array([0,10,20,30])
# mean=calculate_mean(data)
```

### d. Compare Differences

```bash
git diff HEAD calculate_mean.py
# or previous versions:
git diff HEAD~1 calculate_mean.py
git diff HEAD~3 calculate_mean.py
```

### e. Use Specific Commit IDs

```bash
git log --oneline  # Copy a commit ID
git diff <commit-id> calculate_mean.py
```

### f. Use `git show`

```bash
git show HEAD~2 calculate_mean.py
```
>Explain that git show is used for viewing a commit(history and why something was written) and git diff to compare files.
---

## ⏪ Reverting Changes \[9 min]

> Instructor Note: Let participants follow if they are confident. Otherwise, demo it.

Ensure changes are committed:

```bash
git add calculate_mean.py
git commit -m "add usage"
```

Revert to last commit:

```bash
git restore calculate_mean.py
cat calculate_mean.py
```

Revert to specific commit:

```bash
git log --oneline
git restore -s <commit-id> calculate_mean.py
```

Restore the file to the state of the last commit:

```bash
git restore calculate_mean.py
git add calculate_mean.py
git commit -m "usage message added"
```

> Instructor Note: Wrap up with summary of `git log`, `diff`, `show`, and `restore`

---

✅ End of day one



