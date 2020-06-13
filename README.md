Tools for Jsparagus and SmooshMonkey development

# Setup

 * Clone this repository
 * Add `bin` directory in the clone into your `PATH`
 * Place the `mozilla-central` clone next to the `jsparagus` clone
 * Make sure `origin` remote of `jsparagus` is your fork of [official jsparagus](https://github.com/mozilla-spidermonkey/jsparagus)
 * Make sure `upstream` remote of `jsparagus` is [official jsparagus](https://github.com/mozilla-spidermonkey/jsparagus)
 * Make sure `mozilla-central` is git repository with git-cinnabar to `hg::https://hg.mozilla.org/mozilla-unified`, if you want to push to try with single command

# Workflow

## Build SpiderMonkey with SmooshMonkey enabled, with local clone of jsparaagus

```
cd {path-to-mozilla-central}
smoosh-tools build --local
```

If you want to use optimized build, pass `--opt`.

```
smoosh-tools build --local --opt
```

## Run SpiderMonkey JS shell with SmooshMonkey enabled

```
cd {path-to-mozilla-central}
smoosh-tools run

```

If you want to use optimized build, pass `--opt`.

```
smoosh-tools run --opt
```

## Run tests with SmooshMonkey enabled

```
cd {path-to-mozilla-central}
smoosh-tools jstests
smoosh-tools jit-test
```

If you want to use optimized build, pass `--opt`.

```
smoosh-tools jstests --opt
smoosh-tools jit-test --opt
```

## Push to try with modified jsparagus

Push to try with current local jsparagus and mozilla-central.
(This needs Level 1 Commit Access to hg.mozilla.org, and SSH set up for it)

```
cd {path-to-jsparagus}
# Create a branch {branch-name} for the modification here, if not yet.
# Commit modified files here, if not yet.

cd {path-to-mozilla-central}
# Commit modified files here, if not yet.

smoosh-tools try
```

This does th following:
* create `{branch-name}-generated-branch` branch on jsparagus, with generated files
* push above to jsparagus fork (`origin`)
* push to try with the following commits:
  * update Cargo.toml to refer the above `{branch-name}-generated-branch` branch, and `./mach vendor rust`
  * try syntax `try: -b do -p sm-smoosh-linux64 -u none -t none`  
    (note that SM(smoosh) is tier3 job, that is hidden by default)
* Remove all temporary commits generated above


## Bump jsparagus revision to [`+ref/heads/ci_generated`](https://github.com/mozilla-spidermonkey/jsparagus/wiki/Branch-for-generated-files) HEAD.

```
cd {path-to-mozilla-central}
smoosh-tools cargo o -
./mach vendor rust
# Commit updated/vendored files here.
```

# Commands

See [Commands.md](Commands.md)
