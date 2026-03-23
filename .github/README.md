## systemdz (nuts)

A fork of `systemd` that attempts to nullify quesitonable privacy decisions made in upstream.

The goal of this fork *IS NOT* to replace `systemd`, but to provide the minimum set of changes needed to nullify (nerf) the
privacy concerning features found in `systemd`. We do this by changing `systemd` simply never store the concerning data,
and by making any attemts to read it respond as if it was not set.

To clarify, at the time of this writing, fields like `birth_date` in `systemd` are considered optional. For now, it seemed
viable to create a fully compatible fork of `systemd` that always says the concerning values are not set. Hence `systemdz`.

It's our hope that by creating an intentional fork, developers will be discouraged from requiring that this data is availale.

This fork began as a spin off of https://github.com/systemd/systemd/pull/41179, noting that the `systemd` team refused to
revert the changes that added user birthdays.

**IMPORTANT**: This project will only accept PR's related to its goals! Upstream `systemd` still drives the project. We the
authors are simply trying to fix what we consider mistakes with upstream.


### How to use this

Download, build, and install this fork of `systemd` as usual.

Alternatively, checkout a mainline release of `systemd`, then merge-in the changes made in this reposity.

(TODO: provide examples of the above)


### How the it works

The offending code is wrapped in C style `#ifndef` blocks that check for `DZNUTS`. :squirrel:

The original code is intentionally left "as is". This is to encourage GIT to auto-merge the changes to the original and
not see our changes as conflicts.

Our Meson build scripts also define `DZNUTS`, so the original code is omitted.


### Things this fork changes

- `birth_date` is never stored, read, and otherwise acts the same as `systemd` where its not set


### Future goals

Things to explore:

- updating any package generation scripts to output a new package `systemdz` that once installed evicts and takes over all
responsibilities of providing the `systemd` service.
- set up a PPA to easily switch to `systemdz`
- automerge changes to upstream that don't raise any obvious flags
- evaluate other user data that `systemd` stores, if they are even benifitial to have


### What if future software requires that you have a birth_date set, and that all users be 18+?

We hope this never happens, but if it does then it's _truly unfortunate_ that
[the Y2K bug broke birthdays](https://github.com/mikekasprzak/systemdz/tree/always-return-fake-birthday). :wink:
