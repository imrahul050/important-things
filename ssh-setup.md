# Dayal GitLab SSH Setup – Quick Reference

**GitLab Server:**

```bash
192.168.0.7
```

## 1. Check existing SSH keys

SSH keys are normally stored here:

```bash
~/.ssh/
```

Check:

```bash
ls -la ~/.ssh/
```

Example:

```text
id_ed25519_gitlab_dayal
id_ed25519_gitlab_dayal.pub
config
```

* `id_ed25519_gitlab_dayal` → **Private key** — never share
* `id_ed25519_gitlab_dayal.pub` → **Public key** — add this to GitLab
* `config` → SSH configuration

Check the public key:

```bash
cat ~/.ssh/id_ed25519_gitlab_dayal.pub
```

---

## 2. If SSH key does NOT exist, create one

Create an Ed25519 key:

```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

When asked:

```text
Enter file in which to save the key:
```

Give it a specific name, for example:

```text
/home/rahul5/.ssh/id_ed25519_gitlab_dayal
```

Then press Enter for the default location or set a passphrase if required.

This creates:

```text
~/.ssh/id_ed25519_gitlab_dayal
~/.ssh/id_ed25519_gitlab_dayal.pub
```

---

## 3. Add public key to GitLab

Copy the public key:

```bash
cat ~/.ssh/id_ed25519_gitlab_dayal.pub
```

Then go to:

**GitLab → Profile → Edit profile → Access → SSH keys → Add new key**

Paste the **`.pub` key**.

⚠️ Never paste/share:

```text
id_ed25519_gitlab_dayal
```

Only the `.pub` file goes into GitLab.

---

## 4. Configure SSH

Edit:

```bash
nano ~/.ssh/config
```

Add:

```text
Host dayal-gitlab
    HostName 192.168.0.7
    User git
    IdentityFile ~/.ssh/id_ed25519_gitlab_dayal
    IdentitiesOnly yes
```

⚠️ Don't use:

```text
Host http://192.168.0.7/
HostName http://192.168.0.7/
```

Use only:

```text
HostName 192.168.0.7
```

---

## 5. Test GitLab connection

Direct connection:

```bash
ssh -T git@192.168.0.7
```

Using alias:

```bash
ssh -T dayal-gitlab
```

Expected:

```text
Welcome to GitLab, @rahul5!
```

---

## 6. Check which SSH key is being used

```bash
ssh -vT git@192.168.0.7
```

Look for:

```text
Offering public key: /home/rahul5/.ssh/id_ed25519_gitlab_dayal
Server accepts key
```

Short command:

```bash
ssh -vT git@192.168.0.7 2>&1 | grep -E "Offering public key|Server accepts key"
```

---

## 7. Check SSH config

```bash
ssh -G dayal-gitlab | grep -E "hostname|user|identityfile"
```

Expected:

```text
hostname 192.168.0.7
user git
identityfile /home/rahul5/.ssh/id_ed25519_gitlab_dayal
```

---

## 8. Check Git remote

Inside your project:

```bash
git remote -v
```

Example:

```text
origin  git@192.168.0.7:group/sathi.git
```

You can use the SSH alias:

```bash
git remote set-url origin git@dayal-gitlab:group/sathi.git
```

Then:

```bash
git fetch
```

---

## Important SSH Rules

| Item                | Meaning                    |
| ------------------- | -------------------------- |
| `~/.ssh/`           | Location of SSH keys       |
| `.pub`              | Public key → add to GitLab |
| No `.pub`           | Private key → keep secret  |
| `~/.ssh/config`     | SSH configuration          |
| `IdentityFile`      | Path to private key        |
| `Host dayal-gitlab` | Local SSH alias            |
| `192.168.0.7`       | Dayal GitLab server        |

**Quick flow:**

```text
Check ~/.ssh/
      ↓
Key exists?
   ↓ YES              ↓ NO
Use existing       ssh-keygen
   ↓                  ↓
Copy .pub        Copy .pub
   ↓                  ↓
Add to GitLab ←───────┘
      ↓
Configure ~/.ssh/config
      ↓
ssh -T dayal-gitlab
      ↓
Welcome to GitLab
```
