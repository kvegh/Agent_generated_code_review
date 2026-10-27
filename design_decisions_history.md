# Design decisions history

This document records significant decisions, their rationale, and the commits
that implement them.

## Fix findings in batches before functionality tests and a full review restart

Implementation commit: `057d6f6`.

The owner clarified the order of correction and review: collect findings, fix
multiple findings in a coherent batch, run functionality and regression tests,
and restart the complete review only after functionality passes. Individual
findings and edits do not each trigger an immediate full restart. Failed
functionality tests stay in the diagnosis, fix, and test cycle until they pass.

The final complete AAP end-to-end test remains mandatory in the restarted
review. Targeted functionality checks establish that the correction works but
do not close acceptance. README prose, the process diagram, and the TLDR now
describe the same cycle. Documentation consistency, local links, code fences,
and whitespace checks passed; no executable content or deployed objects changed.

## Define the review requirements and acceptance cycle

Implementation commit: `7264129`.

The owner supplied the review requirements after the initial brainstorming.
The README now combines those requirements with the complete Ansible CoP guide
and the relevant content-development sections of the locally supplied AAP 2.7
Develop guide. Record the exact upstream guide revision and account for every
directive so that automated coverage or a short summary cannot silently replace
the full guide. Use current supported AAP runtime behavior when interpreting
historical examples or conflicting recommendations.

The owner made readability, simplicity, native Ansible, certified collections
wherever possible, idempotency, protected external configuration, PAH content,
speed, AAP execution, and reproducible EEs explicit review criteria. Later
clarifications require the current AAP-provided ansible-core baseline and
resolution of every reported deprecation. Every created project must be
CaCable; this does not mandate repository consolidation. Dedicated custom
collection source repositories are allowed, while consuming projects must not
vendor collection releases.

The owner requires provisioning smoke tests and a complete final AAP
end-to-end test. Corrective changes restart the entire review procedure,
including that final test. Evidence must identify the tested revision and
runtime. Missing access, unavailable tooling, or a failed test leaves functional
acceptance incomplete. Test requirements do not independently authorize
destructive operations or changes to unrelated systems.

Strict linting remains separate from APME. Upstream APME inspection identified
six validator backends and the need to verify actual validator completion;
their deployment and project-specific policy selection remain future setup.
Applicable CIS controls and release-matched Red Hat guidance are included.
OpenSCAP and NIST SSDF are identified as proposed supporting references, not
silently imposed additional frameworks.

The separate TLDR provides a quick entry point. Complex project workflows must
also have a maintained visual overview on GitHub Pages. This documentation-only
change does not review project implementations, install tooling, or launch
runtime tests. Local links, upstream source paths, document structure,
whitespace, and basic sensitive-pattern checks passed. The policy is published
on a review branch rather than changing repository protection settings.

## Create a dedicated home for review rules

Implementation commit: `84a82dc`.

The repository owner requested a separate `Agent_generated_code_review`
repository linked from AAP Advanced Features as a submodule. Its README will
hold the rules for reviewing AI agent-generated Ansible code so those rules can
be maintained independently of the projects being reviewed.

The initial README reserves that space. The owner requested formulating the
rules after repository creation; no rules or review tooling are introduced by
this setup.
