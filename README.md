<!-- UPcode fork notice -- keep this at the top; see the Licence section at the end. -->

> ## About this fork
>
> This is a fork of [ioi/isolate](https://github.com/ioi/isolate), maintained by the **Department of
> Computer Science, Faculty of Science, Palacký University Olomouc** as part of **UPcode** — the
> department's deployment of ReCodEx, adapted to its needs.
>
> Not affiliated with, nor endorsed by, the ReCodEx Team or the Isolate authors.
>
> **Branches**
>
> | Branch   | What it is                                                                    |
> | -------- | ----------------------------------------------------------------------------- |
> | `master` | Untouched mirror of `ReCodEx/isolate`, which is Isolate **1.8.1** plus their patches. |
> | `upcode` | Our integration branch, and the default. Isolate **2.7** as released by `ioi`. |
>
> **Why the two branches are different software, not different revisions.** `ReCodEx/isolate`
> carries Isolate 1.8.1, which supports only cgroup **v1**; current Linux distributions — and
> Docker Desktop, which is how this is developed — default to cgroup **v2**, on which
> `isolate --cg` refuses to run and no submitted code is evaluated at all. Isolate 2.x is the
> mirror image: it *requires* v2. So `upcode` is not 1.8.1 with a patch, it is 2.7.
>
> **Nothing of ReCodEx's own was lost in the move**, which is why this was a version change rather
> than a port. Their fork carried eight patches; every one is either upstream in 2.7 or moot — most
> notably the loopback bring-up they wrote themselves against `ioi/isolate` issue #106, which 2.x
> now does natively (`isolate.c`, and the man page's `--share-net` section). See
> `docs/plans/001-cgroup-v2-local-evaluation.md` in `upcode-deploy` for the table.
>
> **Licence: this repository is GPL-2.0-or-later**, unlike the rest of the UPcode stack, which is
> MIT. Isolate is © Martin Mareš and Bernard Blackham; see `LICENSE`, which is unchanged and must
> stay that way. Files we modify carry a note saying so and when, as GPLv2 §2(a) asks of anyone who
> passes the result on. Running a service on it is not distribution and triggers no obligation;
> handing the binary or a container image to somebody else does.

isolate
=======

Isolate is a sandbox built to safely run untrusted executables, like
programs submitted by competitors in a programming contest. Isolate
gives them a limited-access environment, preventing them from affecting
the host system. It takes advantage of features specific to the Linux
kernel, like namespaces and control groups.

Isolate was developed by Martin Mareš (<mj@ucw.cz>) and Bernard Blackham
(<bernard@blackham.com.au>) and still maintained by the former author.
Several other people contributed patches for features and bug fixes
(see Git history for a list). Thanks!

Originally, Isolate was a part of the [Moe Contest Environment](http://www.ucw.cz/moe/),
but it evolved to a separate project used by different
contest systems, most prominently [CMS](https://github.com/cms-dev/cms).
It now lives at [GitHub](https://github.com/ioi/isolate),
where you can submit bug reports and feature requests.

If you are interested in more details, please read Martin's and Bernard's
papers on [Isolate's design](https://mj.ucw.cz/papers/isolate.pdf) and
[grading system security](https://mj.ucw.cz/papers/secgrad.pdf) published
in the Olympiads in Informatics journal.
Also, Isolate's [manual page](http://www.ucw.cz/isolate/isolate.1.html)
is available online.

## Installing Isolate

To compile Isolate, you need:

  - pkg-config

  - headers for the libcap library (usually available in a libcap-dev package)

  - headers for the libseccomp library (libseccomp-dev)

  - headers for the libsystemd library (libsystemd-dev package) for compilation
    of isolate-cg-keeper

You may need `a2x` (found in [AsciiDoc](https://asciidoc-py.github.io/a2x.1.html)) for building manual.
But if you only want the isolate binary, you can just run `make isolate`

Recommended system setup is described in sections INSTALLATION and REPRODUCIBILITY
of the manual page.

## Debian packages

Isolate is also available as packages for stable Debian Linux and last two LTS
releases of Ubuntu, all on the amd64 architecture. To use them, create
`/etc/apt/sources.list.d/isolate.sources` with the following contents:

    Types: deb
    URIs: http://www.ucw.cz/isolate/debian/
    Suites: trixie-isolate
    Components: main
    Architectures: amd64
    Signed-By: /etc/apt/keyrings/isolate.asc

You also need to install the repository's public key:

    curl https://www.ucw.cz/isolate/debian/signing-key.asc >/etc/apt/keyrings/isolate.asc

Then invoke:

    apt update && apt install isolate

There are experimental packages for the arm64 architecture, too.
