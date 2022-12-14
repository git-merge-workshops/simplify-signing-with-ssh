<h1 align="center">&#127890; Exercise: Setup workstation</h1>

<p align="center">
  Setup workstation •  
  <a href="02-sign-verify-commits.md">Signing and verifying commits</a>
</p>

## Outcomes

> In this exercise, the minimal necessary workstation setup for using SSH code signing is covered including:
>
> 1. Checking and installing prerequisites
> 1. Checking and generating sufficiently secure SSH certificates
> 1. Minimal Git configuration for signing and verifying personal changes

## Steps

1. **Confirm minimum versions of prerequisites; otherwise install accordingly**

   ```shell
   git --version
   ssh -V
   ```

   - Git 2.34 or newer
     - [Linux](https://git-scm.com/download/linux)
     - [MacOS](https://git-scm.com/download/mac)
     - [Windows](https://git-scm.com/download/win)
   - OpenSSH 8.0 or newer
     - [Linux](https://www.openssh.com/portable.html)
     - [MacOS](https://formulae.brew.sh/formula/openssh)
     - [Windows](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=gui)

   Afterwards, configure Git with your name and email address if necessary:

   ```shell
   git config --global user.name "Your Name"
   git config --global user.email "your_email@example.com"
   ```

1. **Generate a new SSH key if an existing key does not exist:**

   > **Warning**
   > Using a passphrase is strongly recommended to secure SSH keys.  With SSH signing requiring use of the SSH agent, the SSH agent will ask once for the passphrase, reducing the need to enter it every time while the SSH agent is running.

   ```shell
   ssh-keygen -t ed25519 -C "your_email@example.com"
   chmod 600 ~/.ssh/id_ed25519
   chmod 644 ~/.ssh/id_ed25519.pub
   ```

   > **Note**
   > If you are using a legacy system that doesn't support the Ed25519 algorithm, use 4096-bit RSA keys for this workshop:
   >
   > ```shell
   > ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   > chmod 600 ~/.ssh/id_rsa
   > chmod 644 ~/.ssh/id_rsa.pub
   > ```

1. **Start up SSH agent and add SSH private key**

   ```shell
   eval `ssh-agent`
   ssh-add ~/.ssh/id_ed25519
   ```

1. **Create file containing SSH public key for verifying signers**

   ```shell
   awk '{ print $3 " " $1 " " $2 }' ~/.ssh/id_ed25519.pub >> ~/.ssh/allowed_signers
   ```

   > **Note**
   > This is a simple variant of a `ssh-keygen` allowed signers file for the purposes of the workshop.
   >
   > For information on more advanced variants, see [`ssh-keygen` ALLOWED SIGNERS documentation][man-ssh-keygen-allowedsigners].

1. **Create local repository for workshop purposes**

   ```shell
   git init -b main simplify-signing-with-ssh-workspace
   cd simplify-signing-with-ssh-workspace
   ```

1. **Configure SSH signing and verifying for workshop repository specifically:**

   ```shell
   git config gpg.format ssh
   git config user.signingkey "$(cat ~/.ssh/id_ed25519.pub)"
   git config gpg.ssh.allowedSignersFile ~/.ssh/allowed_signers
   ```

   > **Note**
   > To globally configure SSH signing and verifying, use the `--global` flag:
   >
   > ```shell
   > git config --global gpg.format ssh
   > git config --global user.signingkey "$(cat ~/.ssh/id_ed25519.pub)"
   > git config --global gpg.ssh.allowedSignersFile ~/.ssh/allowed_signers
   > ```

   For more information about these Git configuration options, see [`gpg.ssh.allowedSignersFile`][man-git-config-gpgsshallowedsignersfile], [`user.signingKey`][man-git-config-usersigningkey], [`gpg.format`][man-git-config-gpgformat].

<hr />
<p align="right">
  Next: <a href="02-sign-verify-commits.md">Signing and verifying commits</a>
</p>

[man-git-config-gpgsshallowedsignersfile]: https://git-scm.com/docs/git-config#Documentation/git-config.txt-gpgsshallowedSignersFile
[man-git-config-usersigningkey]: https://git-scm.com/docs/git-config#Documentation/git-config.txt-usersigningKey
[man-git-config-gpgformat]: https://git-scm.com/docs/git-config#Documentation/git-config.txt-gpgformat
[man-ssh-keygen-allowedsigners]: https://man7.org/linux/man-pages/man1/ssh-keygen.1.html#ALLOWED_SIGNERS
