<h1 align="center">&#127890; Exercise: Signing and verifying tags</h1>

<p align="center">
  <a href="sign-verify-commits.md">Signing and verifying commits</a> •  
  Signing and verifying tags •  
  <a href="sign-past-commits-tags.md">Signing past commits and tags</a>
</p>

## Steps

1. **Confirm SSH tag signing is setup correctly**

   ```shell
   git tag -s --message="Confirm SSH tag signing setup" v1.0.0
   ```

   Possible responses:

   - ```
     error: cannot run gpg: No such file or directory
     error: gpg failed to sign the data
     error: unable to sign the tag
     The tag message has been left in .git/TAG_EDITMSG
     ```

     :disappointed_relieved: Do not to worry!  This is error is likely due to missing SSH signing configuration from "<a href="setup-workstation.md">Setup workstation</a>".

1. **Confirm SSH tag verifying is setup correctly**

   ```shell
   git tag -v v1.0.0
   ```

   Possible responses:

   - ```
     object 20c2bd4bd781bb767098a65b40b394e74f9f1cce
     type commit
     tag v1.0.0
     tagger Your Name <your_email@example.com> 1661543739 -0400
     
     Confirm SSH tag signing setup
     Good "git" signature for your_email@example.com with ED25519 key SHA256:...
     ```

     :partying_face: Congratulations!  SSH tag verifying setup including SSH agent is good.

   - ```
     error: gpg.ssh.allowedSignersFile needs to be configured and exist for ssh signature verification
     ```

     :disappointed_relieved: Do not to worry!  This is error is likely due to missing SSH signing configuration from "<a href="setup-workstation.md">Setup workstation</a>".

1. **Configure additional SSH tag signing and verifying for workshop repository specifically:**

   ```shell
   git config tag.gpgsign true
   ```

   > *Note*
   > To globally configure SSH signing and verifying, use the `--global` flag:
   >
   > ```shell
   > git config --global tag.gpgsign true
   > ```

   For more information about these Git configuration options, see [`tag.gpgSign`][man-git-config-taggpgsign].

<p align="right">
  Next: <a href="sign-past-commits-tags.md">Signing past commits and tags</a>
</p>

[man-git-config-taggpgsign]: https://git-scm.com/docs/git-config#Documentation/git-config.txt-taggpgSign
