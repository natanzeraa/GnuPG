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
 
_PS: If you run the geration command using "sudo", the key will be under sudo administration, so if you try to list without "sudo", you'll not be able to see it._

---

### GPG keys are your identity when it comes to communication. 

If for some reason your key/identity is stolen, anyone who has your private GPG key can impersonate you as the owner. In this case, the person with your key can read your emails, authenticate at any services you might be using, etc.

There is when the Certificates comes in.

Basicly certificates can be revoked by its owner, so in the cenario above, the way to stop the attacker is by revoking the certificate.

So for generating the revocation certificate, run the following command:

```
gpg --output revocation.crt --gen-revoke <gpg-email-given-at-generation>
```

_In some cases you might have lots of keys generated, then it's not advised to use email for revocation. Instead use the key ID._

To find the key ID run the following command:

```
gpg --fingerprint
```
The output should be something similar to this:

```
pub   rsa2048 2018-05-02 [SC] [expires: 2025-05-02]
      89A9 3BC2 65F0 F772 6240  C2A6 0D9B 9E0D 2B76 2142
uid           [ultimate] John Doe <john.doe@example.com>
sub   rsa2048 2018-05-02 [E] [expires: 2025-05-02]

```

The part of the key that represents your ID are the last 16 characters or the 4 last sections:

```
0D9B 9E0D 2B76 2142
```

This way you wont have problems due to conflicting key emails when revoking certs.

```
gpg --ouput revocation.crt --gen-revoke 0D9B9E0D2B762142
```

Now you'll be asked for confirming the creation of the cert.

Next gpg asks for selecting a reason for the revoke cert creation, choose one and confirm.

GPG will now ask for some description. This part is optional, so the decision is upon you.

Confirm it, and it's done. The revoking cert is generated, and now you have just added an extra security layer to your GPG keys.

If you wish to see it at your terminal, type:

```
cat revocation.crt
```

---

### Exporting GnuPG public key

Imagine that you want to share your public key, so people can reach you under an encrypted comunication

To do that you can export your public key and share it with whoever you want

```
gpg --export --armor <KEY-ID> > <any-name-you-want>.txt
```

Now check out your exported public key

```
cat <public-key-name>.txt
```

---

### Exporting GnuPG Private Key

If you want to export your private key the process is pretty much the same

```
gpg --export-secret-keys --armor <KEY-ID> > <any-name-you-want>.txt
```

_PS: NEVER SHARE YOUR PRIVATE KEY WITH ANYONE, because this is the key that decripts all the comunication that comes in. Make sure to keep it safe!_

---

### Simetric Encrypting GPG Private Key

You can also encrypt your private key running the command:

```
gpg --symetric <your-private-key>.txt
```

The output generated will be _<your-private-key.txt.gpg>_.

You'll need to provide a password for protecting the file. This same password will be asked when needed in future decryption attempts.

_PS: Make sure to keep this key safe!_

---

### Decrypting GnuPG Private Key with Simetric Encrypted Private Key

Now you have the private key encrypted and wants to decrypt the _.gpg_ key, and for that you can run:

```
gpg --output <any-name-you-want-for-the-output>.txt -d <your-encrypted-gpg-private-key-file>.gpg
```

You can check the output:

```
cat <decrypted-private-key>.txt
```

---








