# Design decisions history

This document records significant decisions, their rationale, and the commits
that implement them.

## Create a dedicated home for review rules

Implementation commit: `84a82dc`.

The repository owner requested a separate `Agent_generated_code_review`
repository linked from AAP Advanced Features as a submodule. Its README will
hold the rules for reviewing AI agent-generated Ansible code so those rules can
be maintained independently of the projects being reviewed.

The initial README reserves that space. The owner requested formulating the
rules after repository creation; no rules or review tooling are introduced by
this setup.
