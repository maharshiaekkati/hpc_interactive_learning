<<<<<<< HEAD
# HPC USE Trainer

An interactive study site for the **USE — Use of the HPC Environment** branch of the
[HPC Certification Forum](https://www.hpc-certification.org/) skill tree
(`USE1` through `USE7`).

The app is intentionally simple:

- `index.html` is the full site
- no framework, no build step, no CDN dependencies
- browser `localStorage` keeps each person's study progress private on their own device
- the site can be published to GitHub Pages or run in Docker

## What's improved

Each module now includes more than just a short blurb and quiz:

- learning outcomes
- a pre-quiz **study lesson**
- a realistic HPC scenario
- common mistakes
- guided practice ideas
- command cheatsheet
- quiz with instant feedback

## Best folder layout to keep personal work separate

Use this split:

- **Windows / Cursor / VS / GitLab work:** keep using your work area, such as
  `C:\Users\mreddyae\OneDrive - AlticeUSA\development`
- **WSL personal / GitHub projects:** keep personal repos only in the Linux filesystem, for example:

```bash
~/personal/github/hpc-use-trainer
```

That gives you three benefits:

1. your personal SSH keys stay inside WSL
2. your GitHub identity stays separate from Windows GitLab credentials
3. git performance is usually better in the WSL filesystem than under `/mnt/c/...`

## Local run options

### Option 1: just open it

Open `index.html` in any browser.

### Option 2: run with Docker

From the project directory:

```bash
docker compose up --build
```

Then open:

```text
http://localhost:8080
```

## WSL + personal GitHub setup

If you want this project to live in WSL and publish to your personal GitHub while your
Windows environment stays work-only:

### 1. Install Ubuntu in WSL

Run in Windows PowerShell:

```powershell
wsl --install -d Ubuntu-24.04
```

Then launch Ubuntu and install git:

```bash
sudo apt update
sudo apt -y install git
```

### 2. Set your personal git identity inside WSL

```bash
git config --global user.name  "Your Personal Name"
git config --global user.email "your-personal-email@example.com"
```

### 3. Create a dedicated personal SSH key inside WSL

```bash
mkdir -p ~/.ssh && chmod 700 ~/.ssh
ssh-keygen -t ed25519 -C "personal-github" -f ~/.ssh/id_ed25519_personal
```

Add this to `~/.ssh/config`:

```sshconfig
Host github.com
    HostName ssh.github.com
    User git
    Port 443
    IdentityFile ~/.ssh/id_ed25519_personal
    IdentitiesOnly yes
```

Lock down the config:

```bash
chmod 600 ~/.ssh/config
```

Print the public key:

```bash
cat ~/.ssh/id_ed25519_personal.pub
```

Then add that public key on **github.com** under:

`Settings -> SSH and GPG keys -> New SSH key`

### 4. Test GitHub SSH from WSL

```bash
ssh -T git@github.com
```

You should get a successful authentication message from GitHub.

### 5. Move this project into your personal WSL folder

From Ubuntu:

```bash
mkdir -p ~/personal/github
cp -r /mnt/c/Users/mreddyae/hpc-use-trainer ~/personal/github/hpc-use-trainer
cd ~/personal/github/hpc-use-trainer
```

### 6. Create the GitHub repo and push

Create an empty public repo on github.com named `hpc-use-trainer`, then:

```bash
git remote add origin git@github.com:YOUR_GITHUB_USERNAME/hpc-use-trainer.git
git push -u origin main
```

### 7. Publish with GitHub Pages

In the repo:

- `Settings`
- `Pages`
- `Build and deployment`
- `Source: Deploy from a branch`
- `Branch: main`
- `Folder: / (root)`

Your site will be available at:

```text
https://YOUR_GITHUB_USERNAME.github.io/hpc-use-trainer/
```

## Source

Content is based on the HPC Certification Forum USE skill tree:

<https://www.hpc-certification.org/wiki/skill-tree/use/>

This is an unofficial study aid and is not affiliated with the HPC Certification Forum.
=======
# hpc_interactive_learning
This is created to provide High-Performance Computing (HPC) interactive learning path for all the system engineers
>>>>>>> 2ffb93cc0781357b42a9b04b34db5a82b4d6cf9b
