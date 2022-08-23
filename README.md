<h1 align="center">Simplify signing Git commits and tags with SSH keys</h1>
<h5 align="center">@andyfeller</h3>

<p align="center">
  <a href="#mega-prerequisites">Prerequisites</a> •  
  <a href="#schoolsatchel-exercises">Exercises</a> •  
  <a href="#books-resources">Resources</a>
</p>

> In this workshop, participants learn how to secure Git commits using the new OpenSSH feature.
>
> This is an alternative to the traditional method of using GPG and maintaining keys which can be somewhat cumbersome. 

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
1. [_"Would you accept this pull request?"_](exercises/would-you-accept-pr.md)
1. [Setup workstation](exercises/setup-workstation.md)
1. [Signing and verifying commits](exercises/sign-verify-commits.md)
1. [Signing and verifying tags](exercises/sign-verify-tags.md)
1. [Verifying commits as part of CI](exercises/verify-ci.md)
1. [Adoption challenges](exercises/adoption-challenges.md)

## :books: Resources
- Git commands used for signing and verifying
  - [`git commit`][git-commit-sign]
  - [`git merge`][git-merge-sign]
  - [`git tag`][git-tag-sign]
  - [`git verify commit`][git-verify-commit]
  - [`git verify tag`][git-verify-tag]
- [Git 2.34.0 changelog][git-changelog-2.34.0]

[git-changelog-2.34.0]: https://lore.kernel.org/git/xmqq8rxpgwki.fsf@gitster.g/
[git-commit-sign]: https://git-scm.com/docs/git-commit#Documentation/git-commit.txt--Sltkeyidgt
[git-config-gpgsshallowedSignersFile]: https://git-scm.com/docs/git-config#Documentation/git-config.txt-gpgsshallowedSignersFile
[git-merge-sign]: https://git-scm.com/docs/git-merge#Documentation/git-merge.txt--Sltkeyidgt
[git-tag-sign]: https://git-scm.com/docs/git-tag#Documentation/git-tag.txt--s
[git-verify-commit]: https://git-scm.com/docs/git-verify-commit
[git-verify-tag]: https://git-scm.com/docs/git-verify-tag