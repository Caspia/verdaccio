# Caspia fork of Verdaccio

This repository is a fork of https://github.com/verdaccio/verdaccio with some small changes to
better support the needs of using it as an offline NPM repository, particularly with the
[Open Prison Education Project](https://github.com/operepo/ope). The main intent of those changes is to allow setting up verdaccio to never attempt to update a package from a downstream repository. This is useful to setup a verdaccio repository, located online, that will nevertheless work exactly the way that an offline version of the same repository would work.

This README describes the Caspia changes. The README for the upstream project has been renamed here to README-upstream.md

## Forced offline mode

The main added feature is support for a forced offline mode. Normally, if no local cached copy of
the requested version of a module is available in verdaccio, it will check its local information about the missing version.
Frequently that information is available locally (that is, in the verdaccio offline cache) in the package.json
file for the module, that contains information on all available versions of a module. The original verdaccio will
then try to get that version from https://registry.npmjs.org/ (or other appropriate upstream as listed in package.json).
The Caspia version provides the capability to turn that off.

Why do we want to do that? We want to be able to provide a test verdaccio install, that is usable online for example by a class instructior,  that demonstrates exactly how the offline
version will behave, without having verdaccio providing copies of that version that would not be available offline.

This small feature may at some point be introduced to the upstream verdaccio, at which point this fork may be deprecated.

### Usage

The feature adds an option "disableFetch" in the config.yaml file, which defaults to false. To prevent verdaccio from silently
contacting the upstream registry, modify your config.yaml following this example:
```yaml
uplinks:
  npmjs:
    url: https://registry.npmjs.org
    disableFetch: true
```