<h1 align="center">&#127890; Exercise: Motivation</h1>

<p align="center">
  Motivation •  
  <a href="setup-workstation.md">Setup workstation</a>
</p>

## Outcomes

> In this exercise, the importance of code signing is explored including:
>
> 1. the nature of the problem
> 1. relevance to broader security concerns

## Nature of the problem

Which of these 2 pull requests would you accept?

<p align="center">
  <img width="1792" alt="Screenshot depicting pull request with unverified changes" src="https://user-images.githubusercontent.com/2089743/187014107-4bb86da3-fd12-4b9f-8877-d518ebfe8dfc.png" />

  <img width="1792" alt="Screenshot depicting pull request with verified changes" src="https://user-images.githubusercontent.com/2089743/187014106-a5ccc564-ecc2-4f62-816d-2f6abd875143.png" />
</p>

Due to the decentralized nature of Git, authenticity can only be established by signing changes, which involves capturing the additional `gpgsig` header information with the [Git objects][git-scm-internals-storage]:

```shell
~/simplify-signing-with-ssh (main) $ git log
commit d7a327072ed28cb660924d903ae7c3c22f6c13d1 (HEAD -> main)
Good "git" signature for andyfeller@github.com with ED25519 key SHA256:cX/wtIPgTMgycKw3xFBE9xkJXM+K+t4KzifsuBKxexo
Merge: 25c3e34 a512451
Author: Andy Feller <andyfeller@github.com>
Date:   Sun Aug 28 13:25:48 2022 -0400

    Merge branch 'main' of github.com:git-merge-workshops/simplify-signing-with-ssh


~/simplify-signing-with-ssh (main) $ git cat-file -p d7a327072ed28cb660924d903ae7c3c22f6c13d1
tree 1a0ea28e98cc913b83a26347cab3e0df98a36ece
parent 25c3e34e22861e7bef8d5f177ea8809d8f547068
parent a5124518546d6680626d806c36085099333fac4c
author Andy Feller <andyfeller@github.com> 1661707548 -0400
committer Andy Feller <andyfeller@github.com> 1661707548 -0400
gpgsig -----BEGIN SSH SIGNATURE-----
 U1NIU0lHAAAAAQAAADMAAAALc3NoLWVkMjU1MTkAAAAgAuowLNeV7cU7+ho4jLGSa61imG
 JnxMf652Yfgxz9rVUAAAADZ2l0AAAAAAAAAAZzaGE1MTIAAABTAAAAC3NzaC1lZDI1NTE5
 AAAAQDHypmlmi0bdrpWD6T5kllYQwSTKcfcQuFog7SuinZ3/tMAAt1zDXba1Ua0KvIigAQ
 nHX5FueI8ze7p0wPKN0gY=
 -----END SSH SIGNATURE-----

Merge branch 'main' of github.com:git-merge-workshops/simplify-signing-with-ssh
```

## Broader security concerns

Our reliance on software and the increasingly complex ways that changes are authored have raised the need to secure our supply chains.

In the May 2021, the White House released the "[Executive Order on Improving the Nation’s Cybersecurity][whitehouse-improving-nations-cybersecurity]" executive order, which contains a section "Enhancing Software Supply Chain Security" stating:

- `4.e.iii`

  > employing automated tools, or comparable processes, to maintain trusted source code supply chains, thereby ensuring the integrity of the code;

- `4.e.vi`

  > maintaining accurate and up-to-date data, provenance (i.e., origin) of software code or components, and controls on internal and third-party software components, tools, and services present in software development processes, and performing audits and enforcement of these controls on a recurring basis;

- `4.e.x`

  > ensuring and attesting, to the extent practicable, to the integrity and provenance of open source software used within any portion of a product.

Expanding existing signing support for [GPG][git-1.7.9-releasenotes] and [X509][git-2.19.0-releasenotes] signing, [Git 2.34][git-2.34-releasenotes] added SSH signing support, which we should lower barriers to improving code authenticity.

<hr />
<p align="right">
  Next: <a href="setup-workstation.md">Setup workstation</a>
</p>

[git-1.7.9-releasenotes]: https://github.com/git/git/blob/master/Documentation/RelNotes/1.7.9.txt
[git-2.19.0-releasenotes]: https://github.com/git/git/blob/master/Documentation/RelNotes/2.19.0.txt
[git-2.34.0-releasenotes]: https://github.com/git/git/blob/master/Documentation/RelNotes/2.34.0.txt
[git-scm-internals-storage]: https://git-scm.com/book/en/v2/Git-Internals-Git-Objects#_object_storage
[whitehouse-improving-nations-cybersecurity]: https://www.whitehouse.gov/briefing-room/presidential-actions/2021/05/12/executive-order-on-improving-the-nations-cybersecurity/
