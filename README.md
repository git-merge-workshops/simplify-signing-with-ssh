<p align="center">
  <img width="150" height="150" src="https://ghicons.github.com/assets/images/blue/png/Security.png" />
</p>

<h1 align="center">Simplify signing Git commits and tags with SSH keys</h1>
<h5 align="center">@andyfeller</h3>

<p align="center">
  <a href="#mega-prerequisites">&#128227; Prerequisites</a> •  
  <a href="motivation.md">&#128161; Motivation</a> •  
  <a href="#school_satchel-exercises">&#127890; Exercises</a> •  
  <a href="#rocket-beyond">&#128640; Beyond</a> •  
  <a href="#books-resources">&#128218; Resources</a>
</p>

> In this workshop, participants learn how to secure Git commits using [the new OpenSSH feature](https://github.blog/changelog/2022-08-23-ssh-commit-verification-now-supported/).  This is an alternative to the traditional method of using GPG and maintaining keys which can be somewhat cumbersome. 

## :mega: Prerequisites
- Git 2.34 or newer
  - [Linux](https://git-scm.com/download/linux)
  - [MacOS](https://git-scm.com/download/mac)
  - [Windows](https://git-scm.com/download/win)
- OpenSSH 8.0 or newer
  - [Linux](https://www.openssh.com/portable.html)
  - [MacOS](https://formulae.brew.sh/formula/openssh)
  - [Windows](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=gui)

## :school_satchel: Exercises 
1. [Setup workstation](exercises/01-setup-workstation.md)
1. [Signing and verifying commits](exercises/02-sign-verify-commits.md)
1. [Signing and verifying merges](exercises/03-sign-verify-merges.md)
1. [Signing and verifying tags](exercises/04-sign-verify-tags.md)
1. [Signing past commits and tags](exercises/05-sign-past-commits-tags.md)

## :rocket: Beyond
1. [:thinking: Author opinion: Enterprise challenges](enterprise-challenges.md)
1. [:coin: `bitcoin/bitcoin` verify-commits][bitcoin-verify-commits]
   > **Tooling for verification of PGP signed commits**
   >
   > This is an incomplete work in progress, but currently includes a pre-push hook script (`pre-push-hook.sh`) for maintainers to ensure that their own commits are PGP signed (nearly always merge commits), as well as a Python 3 script to verify commits against a trusted keys list.
1. 🎉 Vendor support
   - **GitHub**: [GA August 23rd 2002][vendor-support-github]
   - **GitLab**: [In progress #343879][vendor-support-gitlab]
   - **BitBucket**: [In progress BCLOUD-3166][vendor-support-bitbucket]
1. [:key: 1password "Sign your Git commits with 1Password"][1password-git-signing]
   > We’re excited to announce that 1Password now allows you to set up and use SSH keys to sign Git commits. And with GitHub supporting SSH key signing as well, you can get that verified badge next to your username in seconds. No GPG keys required.
1. [:computer: andyfeller/gh-ssh-allowed-signers][andyfeller/gh-ssh-allowed-signers]
   > A `gh` extension to generate SSH allowed users file from GitHub users' signing keys.

## :books: Resources
- Git commands used for signing and verifying
  - [`git commit`][git-commit-sign]
  - [`git merge`][git-merge-sign]
  - [`git tag`][git-tag-sign]
  - [`git verify commit`][git-verify-commit]
  - [`git verify tag`][git-verify-tag]
- [Git 2.34.0 release notes][git-2.34.0-releasenotes]

## :sparkles: Thanks

This effort couldn't have happened without the support from many people, so thank you to the following who helped throughout the creation of this workshop:

[![@ppremk](https://avatars.githubusercontent.com/ppremk?s=80)](https://github.com/ppremk)
[![@leereilly](https://avatars.githubusercontent.com/leereilly?s=80)](https://github.com/leereilly)
[![@bval](https://avatars.githubusercontent.com/bval?s=80)](https://github.com/bval)
[![@aaronkowall](https://avatars.githubusercontent.com/aaronkowall?s=80)](https://github.com/aaronkowall)
[![@bestra](https://avatars.githubusercontent.com/bestra?s=80)](https://github.com/bestra)
[![@apdarr](https://avatars.githubusercontent.com/apdarr?s=80)](https://github.com/apdarr)
[![@evgenyrahman](https://avatars.githubusercontent.com/evgenyrahman?s=80)](https://github.com/evgenyrahman)
[![@vcsjones](https://avatars.githubusercontent.com/vcsjones?s=80)](https://github.com/vcsjones)
[![@ashishkeshan](https://avatars.githubusercontent.com/ashishkeshan?s=80)](https://github.com/ashishkeshan)
[![@lumaxis](https://avatars.githubusercontent.com/lumaxis?s=80)](https://github.com/lumaxis)
[![@milemons](https://avatars.githubusercontent.com/milemons?s=80)](https://github.com/milemons)
[![@abelberhane](https://avatars.githubusercontent.com/abelberhane?s=80)](https://github.com/abelberhane)
[![@katiem0](https://avatars.githubusercontent.com/katiem0?s=80)](https://github.com/katiem0)
[![@kevfoste](https://avatars.githubusercontent.com/kevfoste?s=80)](https://github.com/kevfoste)
[![@allthedoll](https://avatars.githubusercontent.com/allthedoll?s=80)](https://github.com/allthedoll)

[bitcoin-verify-commits]: https://github.com/bitcoin/bitcoin/tree/master/contrib/verify-commits
[git-2.34.0-releasenotes]: https://github.com/git/git/blob/master/Documentation/RelNotes/2.34.0.txt
[git-commit-sign]: https://git-scm.com/docs/git-commit#Documentation/git-commit.txt--Sltkeyidgt
[git-config-gpgsshallowedSignersFile]: https://git-scm.com/docs/git-config#Documentation/git-config.txt-gpgsshallowedSignersFile
[git-merge-sign]: https://git-scm.com/docs/git-merge#Documentation/git-merge.txt--Sltkeyidgt
[git-tag-sign]: https://git-scm.com/docs/git-tag#Documentation/git-tag.txt--s
[git-verify-commit]: https://git-scm.com/docs/git-verify-commit
[git-verify-tag]: https://git-scm.com/docs/git-verify-tag
[1password-git-signing]: https://blog.1password.com/git-commit-signing/
[vendor-support-github]: https://github.blog/changelog/2022-08-23-ssh-commit-verification-now-supported/
[vendor-support-gitlab]: https://gitlab.com/gitlab-org/gitlab/-/issues/343879
[vendor-support-bitbucket]: https://jira.atlassian.com/browse/BCLOUD-3166
[andyfeller/gh-ssh-allowed-signers]: https://github.com/andyfeller/gh-ssh-allowed-signers
