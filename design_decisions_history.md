# Design decisions history

This document records significant decisions, their rationale, and the commits
that implement them.

## Balance review effort against benefit and use agents for readability checks

Implementation commit: `e4f4168`.

The owner clarified that review acceptance does not require perfect conformance.
Reviewers may accept low-impact deviations when the effort, added complexity,
or regression risk of correction is disproportionate to the practical benefit.
The dated report must explain each accepted deviation or known limitation,
its impact, the benefit and cost of fixing it, and the reason for acceptance.
Material decisions retain the existing authorization requirements, and mandatory
functionality and final end-to-end evidence must still pass.

The owner also requires explicit functionality-test confirmation in each review
report and a check that project documentation sufficiently describes the actual
supported environment. A KVM-only implementation does not need VMware support
to pass review; its documentation must accurately state the boundary.

Readability and simplicity are assessed by agents rather than requiring human
verification. Additional independent agents may confirm or challenge the
assessment; their scopes, findings, and disagreement resolutions are recorded.
This sets the review method without launching reviews or delegating tasks now.

The README, flowchart, report requirements, and TLDR were aligned. Documentation
consistency, report fields, local links, code fences, and whitespace checks
passed. No executable project content or deployed objects changed.

## Keep a dated completion report with each reviewed project

Implementation commit: `835d2cf`.

The owner requires a `Code_Review_YYYY-MM-DD.md` document in the repository
actually reviewed after findings are fixed and functionality is verified.
Keeping the report with that project makes its scope, fixes, tested revisions,
and acceptance evidence available alongside the maintained code. The existing
requirement for a successful restarted full review and final AAP end-to-end
test remains in force before recording successful completion.

The report must explain conflicting review approaches or guidance: which
requirements contradicted each other, the affected context, the chosen approach,
alternatives, rationale, and verification. Record explicitly when no conflicts
were identified. Sensitive evidence remains outside public code repositories.
The README, process diagram, and TLDR now include this requirement. Documentation
checks passed; no successful review report was created for an unreviewed project.

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
