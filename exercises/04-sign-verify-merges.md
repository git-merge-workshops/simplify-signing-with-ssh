<h1 align="center">&#127890; Exercise: Signing and verifying merges</h1>

<p align="center">
  <a href="03-sign-verify-commits.md">Signing and verifying commits</a>
  Signing and verifying merges •  
  <a href="05-sign-verify-tags.md">Signing and verifying tags</a>
</p>

## Outcomes

> In this exercise, the process for signing and verifying merges is covered including:
>
> 1. Explicitly sign and verify commits
> 1. Troubleshooting problems
> 1. Optional Git configurations to sign and verify all commits

## Steps

> **Note**
> This exercise uses preparation done previously in "[Signing and verifying commits](03-sign-verify-commits.md)".

1. **Checkout the default branch of the repository in preparation for the merge**

   ```shell
   git checkout main
   ```

1. **Merge branch from previous exercise ensuring signatures are verified**

   ```shell
   git merge --verify-signatures exercises-$(whoami) --message "Confirm SSH merge signing setup"
   ```

   Possible results:

   - ```
     Commit 14a73ae has a good GPG signature by andyfeller@github.com
     Merge made by the 'ort' strategy.
     ```

     :partying_face: Congratulations!  SSH merge signing is good.

   - ```
     fatal: Commit 1a18ff8 does not have a GPG signature.
     ```

     :disappointed_relieved: Do not to worry!  This is error is likely due to the last commit being signed.

   For more information about signing merges, see "[`git merge --verify-signatures`][git-merge-verifysignatures]".

1. **Confirm logs show SSH commit sign status**

   ```shell
   git log --show-signature
   ```

   Possible results:

   - ```
     commit 5bd0c89361d4ed6242fc464f9fe80a1b49d80027 (HEAD -> main, origin/main, origin/HEAD)
     Good "git" signature for andyfeller@github.com with ED25519 key SHA256:cX/wtIPgTMgycKw3xFBE9xkJXM+K+t4KzifsuBKxexo
     Merge: f41ed7f 14a73ae
     Author: Andy Feller <andyfeller@github.com>
     Date:   Sun Sep 4 18:13:43 2022 -0400
     
         Confirm SSH merge signing setup
     ```

     :partying_face: Congratulations!  SSH merge verification setup is good.

1. **Configure additional SSH merge signing and verifying for workshop repository specifically:**

   ```shell
   git config merge.verifySignatures true
   ```

   > **Note**
   > To globally configure SSH signing and verifying, use the `--global` flag:
   >
   > ```shell
   > git config --global merge.verifySignatures true
   > ```

   For more information about these Git configuration options, see [`merge.verifySignatures`][git-merge-verifysignatures].
  
<hr />
<p align="right">
  Next: <a href="05-sign-verify-tags.md">Signing and verifying tags</a>
</p>

[git-config-mergeverifysignatures]: https://git-scm.com/docs/git-config#Documentation/git-config.txt-mergeverifySignatures
[git-merge-verifysignatures]: https://git-scm.com/docs/git-merge#Documentation/git-merge.txt---verify-signatures
