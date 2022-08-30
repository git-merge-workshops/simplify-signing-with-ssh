<h1 align="center">&#127890; Exercise: Signing past commits and tags</h1>

<p align="center">
  <a href="sign-verify-tags.md">Signing and verifying tags</a> •  
  Signing past commits and tags •  
  <a href="/README.md#rocket-beyond">:rocket: Beyond</a>
</p>

## Outcomes

> In this exercise, the process for signing older commits and tags is covered.

## Steps

1. **Create new commit, verifying it is unsigned**

   ```shell
   date > sign-past-commits-tags.exercise

   git add sign-past-commits-tags.exercise
   git commit --no-gpg-sign --message="Setup for signing old commits"

   git log --show-signature
   ```

   should result in something like:

   ```shell
   Author: Andrew Feller <andrew.feller@gmail.com>
   Date:   Tue Aug 30 19:09:59 2022 -0400

       Setup for signing old commits
   ```

1. **Amend last commit, verifying it is signed**

   ```shell
   git commit --amend --no-edit -S

   git log --show-signature
   ```

   should result in something like:

   ```shell
   Good "git" signature for andrew.feller@gmail.com with ED25519 key SHA256:cX/wtIPgTMgycKw3xFBE9xkJXM+K+t4KzifsuBKxexo
   Author: Andrew Feller <andrew.feller@gmail.com>
   Date:   Tue Aug 30 19:24:11 2022 -0400

       Setup for signing old commits
   ```

   > **Note**
   > For signing multiple commits in a branch,
   >
   > ```shell
   > git rebase --exec 'git commit --amend --no-edit -n -S' -i <BRANCH>
   > ```


1. **Create new tag, verifying it is unsigned**

   ```shell
   git tag --no-sign --message="Setup for signing old tags" v1.1.0
   git tag -v v1.1.0
   ```

   should result in something like:

   ```shell
   object c943063376a07d7e0d0a2de0a8037e35b1616ce6
   type commit
   tag v1.1.0
   tagger Andrew Feller <andrew.feller@gmail.com> 1661902600 -0400

   Setup for signing old tags
   error: no signature found
   ```

1. **Retag last tag, verifying it is signed**

   ```shell
   git tag v1.1.0 v1.1.0 -f -s
   git tag -v v1.1.0
   ```

   should result in something like:

   ```shell
   hint: You have created a nested tag. The object referred to by your new tag is
   hint: already a tag. If you meant to tag the object that it points to, use:
   hint:
   hint:   git tag -f v1.1.0 v1.1.0^{}
   hint: Disable this message with "git config advice.nestedTag false"
   Updated tag 'v1.1.0' (was c91e5fb)
   ```

   and

   ```shell
   Good "git" signature for andrew.feller@gmail.com with ED25519 key SHA256:cX/wtIPgTMgycKw3xFBE9xkJXM+K+t4KzifsuBKxexo
   object c91e5fb7cc54be438808cce6c91f31b26434e565
   type tag
   tag v1.1.0
   tagger Andrew Feller <andrew.feller@gmail.com> 1661902772 -0400

   Setup for signing old tags
   ```

## Miscellany

1. **Force pushing possibly necessary depending on whether commits and tags were previously pushed**

1. **Signing old commits or tags might require setting `GIT_COMMITTER_DATE` to preserve historical date**

## Congratulations

<p align="center">
  <img alt="Congratulations, exercises complete!" src="https://octodex.github.com/images/welcometocat.png" width="400" height="400" />

  Congratulations, exercises complete!
</p>

<hr />
<p align="right">
  Next: <a href="/README.md#rocket-beyond">:rocket: Beyond</a>
</p>
