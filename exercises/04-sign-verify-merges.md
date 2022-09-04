<h1 align="center">&#127890; Exercise: Signing and verifying commits</h1>

<p align="center">
  <a href="03-sign-verify-commits.md">Signing and verifying commits</a>
  Signing and verifying merges •  
  <a href="05-sign-verify-tags.md">Signing and verifying tags</a>
</p>

## Outcomes

> In this exercise, the process for signing and verifying commits is covered including:
>
> 1. Explicitly sign and verify commits
> 1. Troubleshooting problems
> 1. Optional Git configurations to sign and verify all commits

## Steps

1. **Confirm SSH commit signing is setup correctly**

   ```shell
   git commit -S --allow-empty --message="Confirm SSH commit signing setup"
   ```

   Possible results:

   - ```
     [main f425cff] Confirm SSH commit signing setup
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
   git verify-commit -v HEAD^
   ```

   ```shell
   tree 0ef02896bdd7ac3eeabf688e6a6de47e9656c4a6
   parent f425cff419cf75ae9689cbe7de4d0281549d53e3
   author Andy Feller <andyfeller@github.com> 1661482122 -0400
   committer Andy Feller <andyfeller@github.com> 1661482122 -0400
   
   Confirm SSH signing setup
   Good "git" signature for andyfeller@github.com with ED25519 key SHA256:kanlHE9MI77O18EdnFxgEnzc3v1rxJHlW475IbnHdG8
   ```

   For more information about verifying commits, see "[`git verify-commit`][git-verify-commit]".

1. **Confirm logs show SSH commit sign status**

   ```shell
   git log --show-signature
   ```

   Possible results:

   - ```
     Good "git" signature for your_email@example.com with ED25519 key SHA256:...
     ```

     :partying_face: Congratulations!  SSH commit verifying setup including SSH agent is good.

   - ```
     error: gpg.ssh.allowedSignersFile needs to be configured and exist for ssh signature verification
     ```

     :disappointed_relieved: Do not to worry!  This is error is likely due to missing `gpg.ssh.allowedSignersFile` configuration above.

   - ```
     Good "git" signature with ED25519 key SHA256:...
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
  
<hr />
<p align="right">
  Next: <a href="05-sign-verify-tags.md">Signing and verifying tags</a>
</p>

[git-config-commitgpgsign]: https://git-scm.com/docs/git-config#Documentation/git-config.txt-commitgpgSign
[git-config-logshowsignature]: https://git-scm.com/docs/git-config#Documentation/git-config.txt-logshowSignature
[git-verify-commit]: https://git-scm.com/docs/git-verify-commit
[git-log-showsignature]: https://git-scm.com/docs/git-log#Documentation/git-log.txt---show-signature