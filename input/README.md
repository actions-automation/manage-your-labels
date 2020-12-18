# Action Input

Once installed and running on the `.github` repo, the action will look for
label configuration in the `manage-your-labels.yml` file stored in the
top-level directory.

This file should have two top-level keys:

## `LABEL_GROUPS`

A set of groups of labels. Each sub-key represents a group; the `DEFAULT` group
will be added to all repositories in the organization, while other (optional)
groups must be manually added to individual repos.

### Labels

Within each group should be a set of labels. Each label should be keyed by its
name, with subkeys for `description` and `color`. Both should be strings.

Here's an example label:

```yml
help wanted:
    description: Extra attention is needed
    color: '008672'
```

#### Renaming labels

Labels may also specify an optional key called `old_names`. This should be a
list containing all old names for the label. If specified, the action will
detect labels with those old names and rename them to the new label.

Consider the following label:

```yml
enhancement:
    description: New feature or request
    color: a2eeef
    old_names:
        - improvement
        - feature
```

With this configuration, any label named either `improvement` or `feature` would
be renamed to `enhancement`.

## `REPOS`

Which label groups should be present on each repository. For example, if the
label groups `DEFAULT`, `Technology`, and `Documentation` have been specified:

```yml
REPOS:
    example:
        - Technology
```

With this configuration, the `example` repo would inherit all labels present in
both the `DEFAULT` and `Technology` groups, while all other repos in the
organization would inherit only the labels present in `DEFAULT`.

An example configuration is provided in [example.yml](example.yml).
