# 📘 **Runbook: Adding SSH Keys to GitHub**

## **1. Purpose**

This runbook provides the steps required to generate an SSH key and add it to a GitHub account for secure Git operations (clone, pull, push).

---

## **2. Prerequisites**

* Git installed
* Terminal/Command Line access
* GitHub account
* Access to `~/.ssh` directory
* (Optional) GitHub CLI installed

---

## **3. Summary**

1. Generate SSH key
2. Add key to SSH agent
3. Copy the public key
4. Add key to GitHub
5. Test authentication

---

## **4. Steps**

### **4.1 Step 1 — Check Existing SSH Keys**

```bash
ls ~/.ssh
```

If you see `id_ed25519.pub` or `id_rsa.pub`, you may skip to Step 3.

---

### **4.2 Step 2 — Generate a New SSH Key**

Recommended (ED25519):

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Follow the prompts and press **Enter** to accept defaults.

---

### **4.3 Step 3 — Start SSH Agent and Add the Key**

Start agent:

```bash
eval "$(ssh-agent -s)"
```

Add key to agent:

```bash
ssh-add ~/.ssh/id_ed25519
```

---

### **4.4 Step 4 — Copy Public Key**

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy the entire output (begins with `ssh-ed25519`).

---

### **4.5 Step 5 — Add SSH Key in GitHub**

1. Go to **GitHub → Settings → SSH and GPG Keys**
   URL: [https://github.com/settings/keys](https://github.com/settings/keys)
2. Click **New SSH Key**
3. Add a title (ex: *My MacBook Pro*)
4. Paste the copied public key
5. Click **Add SSH key**

---

### **4.6 Step 6 — Test SSH Connection**

```bash
ssh -T git@github.com
```

Expected output:

```
Hi <username>! You've successfully authenticated...
```

---

## **5. Troubleshooting**

### **Problem: Permission denied (publickey)**

Run:

```bash
chmod 600 ~/.ssh/id_ed25519
chmod 700 ~/.ssh
```

### **Problem: Git still uses HTTPS instead of SSH**

Set SSH remote:

```bash
git remote set-url origin git@github.com:<username>/<repo>.git
```

---

## **6. Validation Checklist**

* [ ] SSH key exists under `~/.ssh`
* [ ] Key is added to `ssh-agent`
* [ ] Key is added to GitHub account
* [ ] SSH authentication test successful
* [ ] Able to clone using SSH URL

---

## **7. Revision History**

| Date       | Author        | Change          |
| ---------- |---------------| --------------- |
| 2025-12-04 | harshavardhan | Initial version |

---
