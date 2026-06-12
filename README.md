# HPC USE Trainer

An interactive study site for the **USE — Use of the HPC Environment** branch of the
[HPC Certification Forum](https://www.hpc-certification.org/) skill tree
(`USE1` through `USE7`).

## Live interactive site

Use the trainer here:

- **Live site:** <https://maharshiaekkati.github.io/hpc_interactive_learning/>
- **Source repo:** <https://github.com/maharshiaekkati/hpc_interactive_learning>

Important: viewing `index.html` inside the normal GitHub code browser only shows the
source file. The actual interactive site runs through **GitHub Pages** at the live URL above.

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
wsl --install -d Ubuntu-26.04
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

If your network blocks SSH-over-443, use the HTTPS remote workflow below instead.

### 5. Move this project into your personal WSL folder

From Ubuntu:

```bash
mkdir -p ~/personal/github
cp -r /mnt/c/Users/mreddyae/hpc-use-trainer ~/personal/github/hpc-use-trainer
cd ~/personal/github/hpc-use-trainer
```

### 6. Connect to GitHub and push

For this project, the public repo is:

```text
maharshiaekkati/hpc_interactive_learning
```

If SSH works:

```bash
git remote add origin git@github.com:maharshiaekkati/hpc_interactive_learning.git
git push -u origin main
```

If your network resets SSH, use HTTPS instead:

```bash
git remote add origin https://github.com/maharshiaekkati/hpc_interactive_learning.git
git config --global credential.helper 'cache --timeout=28800'
git push -u origin main
```

With HTTPS, use your GitHub username and a **Personal Access Token** when prompted.

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
https://maharshiaekkati.github.io/hpc_interactive_learning/
```

## Source

Content is based on the HPC Certification Forum USE skill tree:

<https://www.hpc-certification.org/wiki/skill-tree/use/>

This is an unofficial study aid and is not affiliated with the HPC Certification Forum.
