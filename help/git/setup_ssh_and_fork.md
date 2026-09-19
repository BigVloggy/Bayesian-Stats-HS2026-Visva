# Setting up git + SSH on JupyterHub and forking the course repo

This is a one-time setup you do on a **new machine** — in our case, a fresh JupyterHub
server, which doesn't remember anything about you between sessions unless your
`$HOME` directory is persistent. By the end of this you will have:

- an SSH key on JupyterHub that GitHub recognises as *you*,
- your own **fork** of the course repository on GitHub,
- that fork cloned onto JupyterHub, with two remotes configured:
    - `origin` → **your fork** (you can push and pull here),
    - `upstream` → **the course repository** (you can only pull/fetch from here).

If any single step below fails, stop there and fix it before moving on — later
steps assume the earlier ones worked.

---

## 1. Generate an SSH key on JupyterHub

Open a **terminal** in JupyterHub (not a notebook — the Launcher has a "Terminal" tile).

Check whether you already have a key:
```bash
ls -al ~/.ssh
```
If you see `id_ed25519` and `id_ed25519.pub` (or `id_rsa`/`id_rsa.pub`), you can skip
to step 2. Otherwise, generate a new key pair:
```bash
ssh-keygen -t ed25519 -C "your_email@ethz.ch"
```
- Press **Enter** to accept the default file location.
- You'll be asked for a passphrase. You can leave it empty (press Enter twice) for
  convenience, or set one for extra security — if you set one, you'll be asked for
  it again whenever you use the key in a new terminal, unless you also start an
  `ssh-agent` (see the [troubleshooting](#troubleshooting) section).

This creates two files: `~/.ssh/id_ed25519` (**private key — never share this**) and
`~/.ssh/id_ed25519.pub` (**public key — this is what you give to GitHub**).

> **Important — JupyterHub-specific:** some JupyterHub deployments reset `$HOME` at
> the end of every session, in which case `~/.ssh` will be gone the next time you
> log in and you'll need to repeat steps 1–2. If that happens to you every time,
> ask the course staff whether your deployment has persistent storage, and if not,
> where you're expected to keep your SSH key (e.g. a persistent volume mounted
> outside `$HOME`).

---

## 2. Add the public key to your GitHub account

Print your public key and copy the entire output (starts with `ssh-ed25519`, ends
with your email):
```bash
cat ~/.ssh/id_ed25519.pub
```

On GitHub:
1. Click your profile picture → **Settings**.
2. In the left sidebar, **SSH and GPG keys**.
3. Click **New SSH key**.
4. Give it a **Title** that identifies where it lives, e.g. `jupyterhub-bayesian-stats`
   (useful later if you ever need to revoke it).
5. Paste the full contents of `id_ed25519.pub` into **Key**, and click **Add SSH key**.

Verify the connection works:
```bash
ssh -T git@github.com
```
The first time, you'll be asked to confirm GitHub's host fingerprint — type `yes`.
You should then see:
```
Hi <your-github-username>! You've successfully authenticated, but GitHub does not provide shell access.
```
That message is expected and means it worked — GitHub deliberately doesn't give you
a shell, it's just confirming who you are.

---

## 3. Fork the course repository

Go to the course repository on GitHub:

**https://github.com/Bayesian-Statistics-ETH/Bayesian-Stats-FS2026**

Click **Fork** (top right). This creates your own copy of the repository under your
GitHub account, at `https://github.com/<your-github-username>/Bayesian-Stats-FS2026`.
You have full read/write access to your fork; you do **not** have write access to
the course repository itself, which is exactly the point — you push your work to
your fork, and pull updates from the course repository.

---

## 4. Clone your fork onto JupyterHub

On **your fork's** GitHub page (not the course repo — check the URL has your
username in it), click the green **Code** button, select the **SSH** tab, and copy
the URL shown (it will look like
`git@github.com:<your-github-username>/Bayesian-Stats-FS2026.git`).

Back in the JupyterHub terminal, `cd` to wherever you keep your work, then:
```bash
git clone git@github.com:<your-github-username>/Bayesian-Stats-FS2026.git
cd Bayesian-Stats-FS2026
```

Confirm your fork was set up as `origin` automatically:
```bash
git remote -v
```
Expected output:
```
origin  git@github.com:<your-github-username>/Bayesian-Stats-FS2026.git (fetch)
origin  git@github.com:<your-github-username>/Bayesian-Stats-FS2026.git (push)
```

---

## 5. Add the course repository as `upstream`

```bash
git remote add upstream git@github.com:Bayesian-Statistics-ETH/Bayesian-Stats-FS2026.git
```

Check both remotes are now set:
```bash
git remote -v
```
```
origin    git@github.com:<your-github-username>/Bayesian-Stats-FS2026.git (fetch)
origin    git@github.com:<your-github-username>/Bayesian-Stats-FS2026.git (push)
upstream  git@github.com:Bayesian-Statistics-ETH/Bayesian-Stats-FS2026.git (fetch)
upstream  git@github.com:Bayesian-Statistics-ETH/Bayesian-Stats-FS2026.git (push)
```

`upstream` having a `(push)` line here is normal — git always lists one — but you
should never actually push to it; you don't have write access, and pushing there
would fail. Only ever `push` to `origin`.

---

## 6. Verify you have the access you expect

```bash
git fetch upstream   # should succeed silently: read access to the course repo
git push origin main  # with nothing to push yet, git will say "Everything up-to-date"
```

If both run without asking for a username/password and without a `Permission
denied (publickey)` error, your setup is correct: **pull-only** from `upstream`,
**pull + push** on `origin`.

---

## Staying in sync with the course repository

Once you're set up, use **[sync_a_fork.md](sync_a_fork.md)** for the day-to-day
workflow of pulling new material from `upstream` into your fork — the only
difference from what's written there is that this repository's default branch is
called `main`, not `master`, so use `git checkout main` and
`git merge upstream/main`.

---

## Troubleshooting

**`Permission denied (publickey)` when cloning or fetching/pushing**
- Confirm the key exists: `ls ~/.ssh`.
- Confirm it's loaded: `ssh-add -l`. If it says "no identities", run
  `eval "$(ssh-agent -s)"` followed by `ssh-add ~/.ssh/id_ed25519`.
- Confirm GitHub has the *matching* public key: `cat ~/.ssh/id_ed25519.pub` and
  compare against Settings → SSH and GPG keys on GitHub.
- Re-run `ssh -T git@github.com` — it will tell you clearly whether authentication
  itself is failing, independent of any particular repository.

**You cloned with an `https://` URL by mistake and now `origin` isn't using SSH**
```bash
git remote set-url origin git@github.com:<your-github-username>/Bayesian-Stats-FS2026.git
```

**Asked for a passphrase every time in a new terminal**
Start an agent and add your key once per session:
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

**`git push upstream main` fails with a permissions error**
This is expected and correct — you don't have write access to the course
repository. Push to `origin` (your fork) instead, and open a pull request from
your fork if you ever need to propose a change back upstream.
