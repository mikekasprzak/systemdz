## systemdz (nuts)

An "easy-to-sync-with-upstream" fork of `systemd` that attempts to nullify quesitonable privacy decisions made in upstream.

The goal of this fork *IS NOT* to run a parallel project, but to provide the minimum number of changes needed to nullify or "nerf"
the privacy concerning features of `systemd`. We don't exactly do this not by removing any code or features, but by removing any
attempts to read, write, or store the offending data.

This began as a spin off of https://github.com/systemd/systemd/pull/41179, noting that the `systemd` team refused to revert the
changes that added tracking a user `birth_date`. Notably this change was followed by other date/time related improvements (i.e.
verifying SHA256 hash freshness), so reverting these changes as a whole might not have been the best idea. So instead, the focus
is on stopping the data from being stored, used, and potentially removing any code that gates core features of `systemd` behind
the absense or insufficiency of such data.

**IMPORTANT**: This project will only accept PR's related to its goals! Upstream `systemd` still drives the `systemd` project.
Our goal is to provide a compatible fork that respects user privacy in a straightforward way.


### How to use

Define `DZNUTS` and build the project.

(TODO add instructions, or modify build scripts)


### Things this fork changes

- `birth_date` is never stored, read, and otherwise acts the same as `systemd` where its not set


### Future goals

Things to explore:

- updating any package generation scripts to output a new package `systemdz` that once installed takes over the responsibilities
for the `systemd` package.
- set up a PPA allowing users to seamlessly switch by installing a package
- automerge changes to upstream that don't raise any flags
- evaluate other data that `systemd` stores about users, and unless it provides actual benefit to the user, consider nullifying it
