## systemdz (nuts)

An "easy-to-sync-with-upstream" fork of `systemd` that attempts to nullify quesitonable privacy decisions made in upstream.

The goal of this fork *IS NOT* to run a parallel project, but to provide a minimum number of changes needed to nullify or "nerf"
the privacy concerning features of `systemd`. We don't do this by removing features, but by removing the data and making any
attempts to read, write, or store data fail.

This began as a spin off of https://github.com/systemd/systemd/pull/41179, noting that the `systemd` team refused to revert the
changes that added tracking user birthdays. Its worth mentioning some other date/time improvement were made to `systemd`
after these changes were merged (i.e. SHA256 hashes now check freshness), so original proposal of reverting the changes isn't
exactly viable anymore.

The focus of this fork is to instead stop the data from being stored or used, and if it happens, removing any code that blocks
any core features of `systemd` that are gated behind the absense or insufficiency of user data (things like 18+ only).

**IMPORTANT**: This project will only accept PR's related to its goals! Upstream `systemd` still drives the `systemd` project.
Our goal is to provide a drop-in-replacement that better respects user privacy in a straightforward-to-merge way.


### How to use this

Download, build, and install this fork of `systemd` as usual.

Alternatively, checkout a mainline release of `systemd`, then merge-in the changes made in this reposity.

(TODO: provide examples of the above)


### How the it works

The offending code is wrapped in c `#ifdef` blocks that check for `DZNUTS`. :wink:

The original code is left in "as is". GIT should be see this, and auto-merge any changes, as they should only apply to
the original code. If all goes well, no conflicts will trigger. If it doesn't, then a fix might be needed. Partial PR's
that correct this are welcome.


### Things this fork changes

- `birth_date` is never stored, read, and otherwise acts the same as `systemd` where its not set


### Future goals

Things to explore:

- updating any package generation scripts to output a new package `systemdz` that once installed takes over the responsibilities
for the `systemd` package.
- set up a PPA allowing users to seamlessly switch by installing a package
- automerge changes to upstream that don't raise any flags
- evaluate other data that `systemd` stores about users, and unless it provides actual benefit to the user, consider nullifying them
