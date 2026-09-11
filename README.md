<!-- UPcode fork notice -- keep this at the top; see the Licence section at the end. -->

> ## About this fork
>
> This is a fork of [ReCodEx/isolate](https://github.com/ReCodEx/isolate) (itself a fork of
> [ioi/isolate](https://github.com/ioi/isolate)), maintained by the **Department of Computer
> Science, Faculty of Science, Palacký University Olomouc** as part of **UPcode** — the
> department's deployment of ReCodEx, adapted to its needs.
>
> Not affiliated with, nor endorsed by, the ReCodEx Team or the Isolate authors.
>
> **Branches**
>
> | Branch   | What it is                                                              |
> | -------- | ----------------------------------------------------------------------- |
> | `master` | Untouched mirror of `ReCodEx/isolate`. Nothing of ours is committed here. |
> | `upcode` | Our integration branch, and the default. Changes from upstream live here. |
>
> **Licence: this repository is GPL-2.0-or-later**, unlike the rest of the UPcode stack, which is
> MIT. Isolate is © Martin Mareš and Bernard Blackham; see `LICENSE`, which is unchanged and must
> stay that way. Files we modify carry a note saying so and when, as GPLv2 §2(a) asks of anyone who
> passes the result on. Running a service on it is not distribution and triggers no obligation;
> handing the binary or a container image to somebody else does.
>
> **Why it is forked at all:** the vendored Isolate 1.8.1 supports only cgroup **v1**, and current
> Linux distributions default to cgroup v2's unified hierarchy — on which `isolate --cg` refuses to
> run and no submitted code can be evaluated. Work on that happens here.

isolate
=======

Isolate is a sandbox built to safely run untrusted executables,
offering them a limited-access environment and preventing them from
affecting the host system. It takes advantage of features specific to
the Linux kernel, like namespaces and control groups.

Isolate was developed by Martin Mareš (<mj@ucw.cz>) and Bernard Blackham
(<bernard@blackham.com.au>), who still maintain it. Several other people
contributed patches for features and bug fixes (see Git history for a list).
Thanks!

Originally, Isolate was a part of the [Moe Contest Environment](http://www.ucw.cz/moe/),
but it evolved to a separate project used by different
contest systems, most prominently [CMS](https://github.com/cms-dev/cms).
It now lives at [GitHub](https://github.com/ioi/isolate),
where you can submit bug reports and feature requests.

If you are interested in more details, please read Martin's
and Bernard's [paper](http://mj.ucw.cz/papers/isolate.pdf) presented
at the IOI Conference. Also, Isolate's [manual page](http://www.ucw.cz/moe/isolate.1.html)
is available online.

To compile Isolate, you need the headers for the libcap library
(usually available in a libcap-dev package).

You may need `a2x` (found in [AsciiDoc](http://www.methods.co.nz/asciidoc/a2x.1.html)) for building manual.
But if you only want the isolate binary, you can just run `make isolate`
