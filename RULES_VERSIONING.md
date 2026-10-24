# Versioning rules

## Rule 1: Version changes with code and documentation

Each user prompt that results in code changes or added documentation must include a project version change.

Use `MAJOR.MINOR.PATCH` (`X.X.X`) versioning:

- **Major:** The first number.
- **Minor:** The second number.
- **Patch:** The third number.

Unless the user explicitly specifies otherwise, increment the patch number once per changing prompt, not once per file or edit. For example, `1.2.3` becomes `1.2.4`.

Requests that only run tests without changing code or adding documentation must not change the project version, as defined in `RULES_TESTS.md`.

## Rule 2: Link versions to Git commits

Every project version must be linked to a specific Git commit.

Every Git commit must have a short, concise message summarizing its changes.

## Rule 3: Maintain a detailed changelog

Every project must contain a `CHANGELOG.md` file. Each version change must include a corresponding changelog entry containing:

- The version number in `MAJOR.MINOR.PATCH` format.
- The associated Git commit, identified by its hash or a version tag that resolves to that commit.
- A detailed description of the changes included in that version.

Use a version tag when the changelog entry is included in the commit it describes, since a commit cannot contain its own final hash. The tag must point to the associated commit.

Keep the newest version entries first. Changelog descriptions must provide more detail than the short commit summary.
