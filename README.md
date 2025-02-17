# Generating GnuPG keys at Linux

> A GPG (GNU Privacy Guard) is a tool used for IT Professionals with the goal of enhanced authentication and cryptography. It's used for security, privacy and integrity of comunications and file verification.

you can learn more about it at: [gnupg.org](https://gnupg.org/)

_Arguing that you don't care about the right to privacy because you have nothing to hide is no different from saying you don't care about free speech because you have nothing to say. – Edward Snowden_

---

### For generating a gpg key the first command you'll need is:

```
gpg --full-generate-key
```

### After running it, gpg will ask you: 

- What type of encryption key you want to work with

- How many bits long (1024 - 4096)

### You'll be asked for contructing your key identifier by provisioning the following information:

- Expiration date

- Fullname

- Email

- Comment

### Check and confirm the given information

---

### For listing keys run the following command:

```
gpg -k
```

```
gpg -K
```

```
gpg --list-keys
```
 
_PS: If you run the geration command using "sudo", the key will be under sudo administration, so if you try to list withou "sudo", you'll not be able to see it._


