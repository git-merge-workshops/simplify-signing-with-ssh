<h1 align="center">&#129300; Author opinion: Enterprise challenges</h1>

<p align="center">
  <a href="/README.md#mega-prerequisites">&#128227; Prerequisites</a> •  
  <a href="/motivation.md">&#128161; Motivation</a> •  
  <a href="/README.md#school_satchel-exercises">&#127890; Exercises</a> •  
  <a href="/README.md#rocket-beyond">&#128640; Beyond</a> •  
  <a href="/README.md#books-resources">&#128218; Resources</a>
</p>

> **Note**
> Everything here should be taken with a grain of :salt: as purely an opinion of the author.

## Managing trusted keys at scale

This workshop is aimed at getting participants started with SSH code signing.  One of the topics not covered is managing trust for hundreds or thousands of SSH keys across an enterprise as the steps in "[Exercise: Setup workstation](exercises/01-setup-workstation.md)" had participants setup to only trust their own SSH key:

> 4. **Create file containing SSH public key for verifying signers**
> 
>    ```shell
>    awk '{ print $3 " " $1 " " $2 }' ~/.ssh/id_ed25519.pub >> ~/.ssh/allowed_signers
>    ```

Unlike [GPG keyservers][gpg-keyservers], which can be used to distribute GPG keys uploaded by individuals, SSH keys are not distributed the same way.  As Git's SSH code signing is built on top of [`ssh-keygen` allowed signers][man-ssh-keygen-allowedsigners], a different approach to establishing trust is needed: [certificate authorities][ssh-certificate-authority] or CAs.

Using the `cert-authority` option, the principal field of the allowed signers line can take a wildcard entry to trust a larger domain of email addresses using SSH keys signed by the CA:

```
# A certificate authority, trusted for all principals in a domain.
*@example.com cert-authority ssh-ed25519 AAAB4...
```

For enterprises with open source programs, this becomes more difficult, demonstrating opportunity for source control vendors.

## Revoking untrusted keys

GPG has been designed so individuals can [revoke keys from keyservers][gpg-key-revoking], immediately making it untrusted by anyone else using the keyserver.  SSH keys do not have a similar process of revoking untrusted keys or broadcasting information about untrusted keys.

<hr />
<p align="right">
  Next: <a href="/README.md#rocket-beyond">&#128640; Beyond</a>
</p>

[gpg-key-revoking]: https://www.gnupg.org/gph/en/manual/c235.html#AEN304
[gpg-keyservers]: https://www.gnupg.org/gph/en/manual/x457.html
[ssh-certificate-authority]: https://www.ssh.com/academy/pki
[man-ssh-keygen-allowedsigners]: https://man7.org/linux/man-pages/man1/ssh-keygen.1.html#ALLOWED_SIGNERS
