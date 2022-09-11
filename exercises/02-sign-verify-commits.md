<h1 align="center">&#127890; Exercise: Signing and verifying commits</h1>

<p align="center">
  <a href="01-setup-workstation.md">Setup workstation</a> •  
  Signing and verifying commits •  
  <a href="03-sign-verify-merges.md">Signing and verifying merges</a>
</p>

Signing commits is where participants begin gaining experience.

As the previous exercise was focused on workstation setup, this exercise has additional content intended to help troubleshoot possible errors that might arise.

## Outcomes

> In this exercise, the process for signing and verifying commits is covered including:
>
> 1. Explicitly sign and verify commits
> 1. Troubleshooting problems
> 1. Optional Git configurations to sign and verify all commits

## Steps

1. **Create workspace repository README explaining its purpose and the exercise we are on**

   ```shell
   cat << 'EOF' > README.md
   # My git-merge-workshops/simplify-signing-with-ssh workspace

   This repository is my workspace for experimenting with SSH signing keys as a part of [git-merge-workshops/simplify-signing-with-ssh](https://github.com/git-merge-workshops/simplify-signing-with-ssh) where I experimented with the following exercises:

   1. [Setup workstation](https://github.com/git-merge-workshops/simplify-signing-with-ssh/blob/main/exercises/01-setup-workstation.md)
   1. [Signing and verifying commits](https://github.com/git-merge-workshops/simplify-signing-with-ssh/blob/main/exercises/02-sign-verify-commits.md)
   1. [Signing and verifying merges](https://github.com/git-merge-workshops/simplify-signing-with-ssh/blob/main/exercises/03-sign-verify-merges.md)
   1. [Signing and verifying tags](https://github.com/git-merge-workshops/simplify-signing-with-ssh/blob/main/exercises/04-sign-verify-tags.md)
   1. [Signing past commits and tags](https://github.com/git-merge-workshops/simplify-signing-with-ssh/blob/main/exercises/05-sign-past-commits-tags.md)

   EOF
   ```

1. **Confirm SSH commit signing is setup correctly**

   ```shell
   git add .
   git commit -S -m "Initialize workspace repository README"
   ```

   <img alt="Git tree after commiting initial commit with README" src="assets/02-post-init.png" width="600" height="394" />

   Possible results:

   - ```
     [main (root-commit) 1451203] Initialize workspace repository README
      1 file changed, 10 insertions(+)
      create mode 100644 README.md
     ```

     :partying_face: Congratulations!  SSH signing setup including SSH agent is good.

   - ```
     error: Load key "/var/folders/xb/svzskj1x77x3qsmwx1d84nqc0000gn/T//.git_signing_key_tmpW0EAyi": invalid format?
     ```

     :disappointed_relieved: Do not to worry!  This is error is likely due to:

     1. SSH agent being stopped
     1. SSH private key not being added
     1. mismatch between SSH private and public keys

   For more information about signing commits, see "[`git commit -S`][git-commit-sign]".

1. **Verify SSH commit is signed and trusted**

   ```shell
   git verify-commit -v HEAD
   ```

   resulting in:

   ```shell
   tree 8a370608ce603f2dd863efff4f7cc2401c75d829
   author Andy Feller <andyfeller@github.com> 1662853747 -0400
   committer Andy Feller <andyfeller@github.com> 1662853747 -0400
   
   Initialize workspace repository README
   Good "git" signature for andyfeller@github.com with ED25519 key SHA256:kanlHE9MI77O18EdnFxgEnzc3v1rxJHlW475IbnHdG8
   ```

   For more information about verifying commits, see "[`git verify-commit`][git-verify-commit]".

1. **Confirm logs show SSH commit sign status**

   ```shell
   git log --show-signature
   ```

   Possible results:

   - ```
     Good "git" signature for andyfeller@github.com with ED25519 key SHA256:kanlHE9MI77O18EdnFxgEnzc3v1rxJHlW475IbnHdG8
     ```

     :partying_face: Congratulations!  SSH commit verifying setup including SSH agent is good.

   - ```
     error: gpg.ssh.allowedSignersFile needs to be configured and exist for ssh signature verification
     ```

     :disappointed_relieved: Do not to worry!  This is error is likely due to missing `gpg.ssh.allowedSignersFile` configuration above.

   - ```
     Good "git" signature for andyfeller@github.com with ED25519 key SHA256:kanlHE9MI77O18EdnFxgEnzc3v1rxJHlW475IbnHdG8
     /path/to/.ssh/allowed_signers:1: invalid key^M
     sig_find_principals: sshsig_get_principal: key not found^M
     No principal matched.
     ```

     :disappointed_relieved: Do not to worry!  This is error is likely due to format of `gpg.ssh.allowedSignersFile` file as SSH public keys cannot be copied as-is into the file.

   For more information about signatures in logs, see "[`git log --show-signature`][git-log-showsignature]".

1. **Configure additional SSH commit signing and verifying for workshop repository specifically:**

   ```shell
   git config commit.gpgsign true
   git config log.showSignature true
   ```

   > **Note**
   > To globally configure SSH signing and verifying, use the `--global` flag:
   >
   > ```shell
   > git config --global commit.gpgsign true
   > git config --global log.showSignature true
   > ```

   For more information about these Git configuration options, see [`commit.gpgSign`][git-config-commitgpgsign], [`log.showSignature`][git-config-logshowsignature].

## End of exercise

At the end of this exercise, the repository should look like:
  
<img alt="Git tree at the end of the exercise" src="assets/02-end.png" width="600" height="394" />

<hr />
<p align="right">
  Next: <a href="03-sign-verify-merges.md">Signing and verifying merges</a>
</p>

[git-config-commitgpgsign]: https://git-scm.com/docs/git-config#Documentation/git-config.txt-commitgpgSign
[git-config-logshowsignature]: https://git-scm.com/docs/git-config#Documentation/git-config.txt-logshowSignature
[git-commit-sign]: https://git-scm.com/docs/git-commit#Documentation/git-commit.txt--Sltkeyidgt
[git-verify-commit]: https://git-scm.com/docs/git-verify-commit
[git-log-showsignature]: https://git-scm.com/docs/git-log#Documentation/git-log.txt---show-signature
