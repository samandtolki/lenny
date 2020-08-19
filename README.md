<p align="center">
  <img width=200px height=200px src="ui/assets/favicon.svg">
  <h3 align="center">( ͡° ͜ʖ ͡°)</h3>
</p>

[![](https://github.com/innereq/lenny/workflows/Continuous%20Integration/badge.svg)](https://github.com/innereq/lenny/actions?query=workflow%3A"Continuous+Integration") [![](https://quay.io/repository/innereq/lenny/status)](https://quay.io/repository/innereq/lenny)

**Lenny** is a fork of a link aggregator — [Lemmy](https://github.com/LemmyNet/lemmy). Sadly, it only exist because of disrespectful behavior of the original author.

To maintain stability, this fork has a little no changes, but:
- the main reason, completely removed “slur filter” — the ugliest way to block words;
- a bit cleaned up UI — removed “sponsors” page and useless right-down panel;
- new default themes — Pleroma, based on themes of the [Pleroma project](https://pleroma.social);
- ~~allowed `<sub>text</sub>` and `<sup>text</sup>` HTML tags as `~text~` and `^text^`~~ upstreamed!;
- a muffin logo (by [MLP Vector Club](https://mlpvector.club)).

# The Lemmy Problem

`static ref SLUR_REGEX: Regex = RegexBuilder::new(r"(fag(g|got|tard)?|maricos?|cock\s?sucker(s|ing)?|\bn(i|1)g(\b|g?(a|er)?(s|z)?)\b|dindu(s?)|mudslime?s?|kikes?|mongoloids?|towel\s*heads?|\bspi(c|k)s?\b|\bchinks?|niglets?|beaners?|\bnips?\b|\bcoons?\b|jungle\s*bunn(y|ies?)|jigg?aboo?s?|\bpakis?\b|rag\s*heads?|gooks?|cunts?|bitch(es|ing|y)?|puss(y|ies?)|twats?|feminazis?|whor(es?|ing)|\bslut(s|t?y)?|\btr(a|@)nn?(y|ies?)|ladyboy(s?)|\b(b|re|r)tard(ed)?s?)").case_insensitive(true).build().unwrap();`

https://github.com/LemmyNet/lemmy/commit/1c0cc78f3f6d191aa384d8702016564625d51269

> We are never going to remove the slur filter completely (or add an option to that effect), because we dont want to make it easy for right-wingers to use Lemmy. We can talk about removing or changing specific words, but in general I dont think there is anything wrong with writing “b*tch” or something like that.

https://github.com/LemmyNet/lemmy/pull/816#issuecomment-644694838

> I’ll have to think about this. Hard-coding it means I don’t have to do a database migration every time someone comes up with a new slur. And putting it in a DB table means someone could very easily remove it by deleting every row of that table, which isn’t good. I want to make it very difficult for racist trolls to use the most updated version of Lemmy.

https://github.com/LemmyNet/lemmy/issues/622#issuecomment-608707278

This is bullshit.

# Development

The easiest way to build this project is using Podman (or Docker).

Take a look at [`shtripok/rust-musl-builder`](https://hub.docker.com/r/shtripok/rust-musl-builder) container. You can use it both in coding process and building production images.

Here is an example how to setup a coding environment:

```bash
git clone https://github.com/innereq/lenny && cd lenny
podman pull shtripok/rust-musl-builder:arm
podman run -it --rm -v ./:/home/rust/src:Z shtripok/rust-musl-builder:arm /bin/bash
cd server && cargo build
```

To build a production container image:

```bash
podman build -t lenny -f ./docker/prod/Dockerfile .
```

To use public container registry:

```bash
podman pull quay.io/innereq/lenny
```