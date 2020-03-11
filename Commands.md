# Commands

## `gen`

Used in jsparagus clone of fork.

Create a remote (`origin`) branch with generated files added.
The remote branch will be named `{current_branch_name}-generated-branch`.
This can be used by `update-jsparagus-reference` command.

```
smoosh-tools gen
```

:warning: This pushes forcibly. Commits for previous push will be removed.

## `ci_generated_head`

Used in jsparagus clone.

Get the SHA of the HEAD of [`+ref/heads/ci_generated`](https://github.com/mozilla-spidermonkey/jsparagus/wiki/Branch-for-generated-files).

`mozilla-spidermonkey/jsparagus` should be added to remote with `upstream` name.

```
ci_generated_head
```

## `cargo`

Used in mozilla-central clone.

Change jsparagus reference in js/src/frontend/smoosh/Cargo.toml.

### Use local jsparagus clone

Put `jsparagus` directory next to `mozilla-central`.

```
smoosh-tools cargo l
```

### Use forked jsparagus branch on GitHub

First, create a branch with generated files with `push-to-generated-branch` command.

```
smoosh-tools cargo f GITHUB_USER_NAME BRANCH_NAME
```

where `BRANCH_NAME` is `*-generated-branch`

### Use official jsparagus on GitHub

```
smoosh-tools cargo o
```

### Update revision for official jsparagus on GitHub

```
smoosh-tools cargo o SHA
```

where `SHA` is the commit in [`+ref/ci_generated/master`](https://github.com/mozilla-spidermonkey/jsparagus/wiki/Branch-for-generated-files).

### Update revision for official jsparagus on GitHub to ci-generated/master HEAD

This uses `get-ci-generated-head` internally.

```
smoosh-tools cargo o -
```

## `try`

Push to try with current local jsparagus and mozilla-central.

```
smoosh-tools try
```
