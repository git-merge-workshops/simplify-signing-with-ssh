<h1 align="center">&#127890; Exercise: Setup workstation</h1>

<p align="center">
  <a href="motivation.md">Motivation</a>
  Setup workstation •  
  <a href="sign-verify-commits.md">Signing and verifying commits</a>
</p>

## Steps

1. **Generate a new SSH key if an existing key does not exist:**

   > *Warning*
   > Using a passphrase is strongly recommended to secure SSH keys.  With SSH signing requiring use of the SSH agent, the SSH agent will ask once for the passphrase, reducing the need to enter it every time while the SSH agent is running.

   ```shell
   ssh-keygen -t ed25519 -C "your_email@example.com"
   chmod 600 ~/.ssh/id_ed25519
   chmod 644 ~/.ssh/id_ed25519.pub
   ```

   > *Note*
   > If you are using a legacy system that doesn't support the Ed25519 algorithm, use 4096-bit RSA keys for workshop:
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

   > *Note*
   > This is a simple variant of a `ssh-keygen` allowed signers file for the purposes of the workshop.
   >
   > For information on more advanced variants, see [`ssh-keygen` ALLOWED SIGNERS documentation][man-ssh-keygen-allowedsigners].

1. **Clone the [`git-merge-workshops/simplify-signing-with-ssh`](https://github.com/git-merge-workshops/simplify-signing-with-ssh) repository**

   ```shell
   git clone git@github.com:git-merge-workshops/simplify-signing-with-ssh.git
   cd simplify-signing-with-ssh
   ```

   > *Note*
   > This workshop repository is a template, which GitHub users can use to create a copy within their own account.
   >
   > <img width="920" alt="Screen Shot 2022-08-24 at 4 09 56 PM" src="https://user-images.githubusercontent.com/2089743/186513817-73b33136-0672-4a88-9c93-172404c2490f.png">

1. **Configure SSH signing and verifying for workshop repository specifically:**

   ```shell
   git config gpg.format ssh
   git config user.signingkey "$(cat ~/.ssh/id_ed25519.pub)"
   git config gpg.ssh.allowedSignersFile ~/.ssh/allowed_signers
   ```

   > *Note*
   > To globally configure SSH signing and verifying, use the `--global` flag:
   >
   > ```shell
   > git config --global gpg.format ssh
   > git config --global user.signingkey "$(cat ~/.ssh/id_ed25519.pub)"
   > git config --global gpg.ssh.allowedSignersFile ~/.ssh/allowed_signers
   > ```

   For more information about these Git configuration options, see [`gpg.ssh.allowedSignersFile`][man-git-config-gpgsshallowedsignersfile], [`user.signingKey`][man-git-config-usersigningkey], [`gpg.format`][man-git-config-gpgformat].

<p align="right">
  Next: <a href="sign-verify-commits.md">Signing and verifying commits</a>
</p>

[man-git-config-gpgsshallowedsignersfile]: https://git-scm.com/docs/git-config#Documentation/git-config.txt-gpgsshallowedSignersFile
[man-git-config-usersigningkey]: https://git-scm.com/docs/git-config#Documentation/git-config.txt-usersigningKey
[man-git-config-gpgformat]: https://git-scm.com/docs/git-config#Documentation/git-config.txt-gpgformat
[man-ssh-keygen-allowedsigners]: https://man7.org/linux/man-pages/man1/ssh-keygen.1.html#ALLOWED_SIGNERS