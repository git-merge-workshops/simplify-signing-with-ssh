<h1 align="center">&#127890; Exercise: Signing past commits and tags</h1>

<p align="center">
  <a href="04-sign-verify-tags.md">Signing and verifying tags</a> •  
  Signing past commits and tags •  
  <a href="/README.md#rocket-beyond">:rocket: Beyond</a>
</p>

## Outcomes

> In this exercise, the process for signing older commits and tags is covered.

## Steps

1. **Create a simple "foo bar" script**

   ```shell
   cat << 'EOF' > foo.sh
   #! /usr/bin/env bash

   echo "bar"
   EOF

   cat << 'EOF' >> README.md

   ## Foo bar

   Since the `v1.0.0` release, the `foo.sh` script was added, which understandably displays `bar`.
   EOF

   chmod 755 foo.sh
   ./foo.sh
   ```

   resulting in:

   ```
   bar
   ```

1. **Commit "bar" script without signing the commit**

   ```shell
   git add .
   git commit --no-gpg-sign -m "Adding foo script without signing"
   git log
   ```

   should result in something like:

   ```shell
   commit af43f7efe80503b3ebde54c7db85a54e50e3b2d3 (HEAD -> main)
   Author: Andy Feller <andyfeller@github.com>
   Date:   Sat Sep 10 20:05:52 2022 -0400
   
       Adding foo script without signing
   ```

1. **Amend last commit, verifying it is signed**

   ```shell
   git commit --amend --no-edit -S
   git verify-commit -v HEAD
   ```

   should result in something like:

   ```shell
   tree d962e454f8269b75d32c8dfc7ac64b301f6af3ae
   parent 28c46b890121f042e86d7d1c1b58e150b8ac9948
   author Andy Feller <andyfeller@github.com> 1662854752 -0400
   committer Andy Feller <andyfeller@github.com> 1662854795 -0400
   
   Adding foo script without signing
   Good "git" signature for andyfeller@github.com with ED25519 key SHA256:kanlHE9MI77O18EdnFxgEnzc3v1rxJHlW475IbnHdG8
   ```

   > **Note**
   > For signing multiple commits in a branch,
   >
   > ```shell
   > git rebase --exec 'git commit --amend --no-edit -n -S' -i <BRANCH>
   > ```


1. **Create new tag, verifying it is unsigned**

   ```shell
   git tag --no-sign -m "Setup for signing old tags" v1.1.0
   git tag -v v1.1.0
   ```

   should result in something like:

   ```shell
   object 73f57f8ca11bb77cc14a8a0465e2f98b9f76a652
   type commit
   tag v1.1.0
   tagger Andy Feller <andyfeller@github.com> 1662854957 -0400
   
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
   Updated tag 'v1.1.0' (was d12ff7f)
   object d12ff7f288aae53d3d08e710ca95be5cde8fcc4d
   type tag
   tag v1.1.0
   tagger Andy Feller <andyfeller@github.com> 1662854999 -0400
   
   Setup for signing old tags
   Good "git" signature for andyfeller@github.com with ED25519 key SHA256:kanlHE9MI77O18EdnFxgEnzc3v1rxJHlW475IbnHdG8
   ```

## Miscellany

1. **Force pushing might be necessary depending on whether commits and tags were previously pushed** 

1. **Signing old commits or tags might require [setting the `GIT_COMMITTER_DATE` environment variable](https://git-scm.com/docs/git-commit/2.24.0#_date_formats) to preserve historical datetime**

<hr />
<p align="right">
  Next: <a href="/README.md#rocket-beyond">:rocket: Beyond</a>
</p>
