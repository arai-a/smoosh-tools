Tools for Jsparagus and SmooshMonkey development

# Setup

 * Clone this repository
 * Add `bin` directory in the clone into your `PATH`
 * Place the `mozilla-central` clone next to the `jsparagus` clone
 * Make sure `origin` remote of `jsparagus` is your fork of [official jsparagus](https://github.com/mozilla-spidermonkey/jsparagus)
 * Make sure `upstream` remote of `jsparagus` is [official jsparagus](https://github.com/mozilla-spidermonkey/jsparagus)

# Workflow

## Start development with local clone of jsparagus

Update `jsparagus` reference to local clone, and update vendored crates.

```
cd {path-to-mozilla-central}
update-jsparagus-reference l
./mach vendor rust
```

## Before commit

Revert the change from above, and update vendored crates.

```
cd {path-to-mozilla-central}
update-jsparagus-reference o
./mach vendor rust
```

## Push to try with modified jsparagus

Create a remote branch with generated files.

```
cd {path-to-jsparagus}
# Create a branch {branch-name} for the modification here, if not yet.
# Commit modified files here, if not yet.
push-to-generated-branch
```

Update `jsparagus` reference to the branch created above.

```
cd {path-to-mozilla-central}
update-jsparagus-reference f GITHUB_USER_NAME BRANCH_NAME
./mach vendor rust
# Commit vendored files here.
# Push to try here.
```

where `BRANCH_NAME` is `{branch-name}-generated-branch`

## Bump jsparagus revision to [`+ref/ci_generated/master`](https://github.com/mozilla-spidermonkey/jsparagus/wiki/Branch-for-generated-files) HEAD.

```
update-jsparagus-reference o -
./mach vendor rust
# Commit vendored files here.
```

# Commands

See [Commands.md](Commands.md)
