# Code review requirements: TLDR

The full requirements are in [README.md](README.md). Read the complete
[Ansible CoP guide](https://redhat-cop.github.io/automation-good-practices/)
and apply every directive, recording evidence or a justified disposition.
This overview does not replace either document.

- **Correct behavior:** define the required outcome and preserve it during cleanup.
- **AAP baseline:** use the current AAP-provided ansible-core in the selected
  supported EE. Verify the actual runtime and record immutable image/dependency
  versions. Resolve all reported deprecations; keep warnings enabled.
- **Readability and simplicity:** clear names and flow, small coherent units,
  straightforward expressions, and no overengineering or code-density goals.
  Keep comments short; explain the reason, goal, and solution.
- **Native Ansible:** prefer suitable native modules/roles over URI calls and
  external scripts. MCP calls are acceptable. Explain necessary alternatives.
- **Certified content:** use certified collections wherever possible. Explain
  validated, community, and custom alternatives when certified content cannot
  meet the need.
- **Idempotency:** avoid non-idempotent operations where possible; verify repeat
  execution, actual state, accurate change reporting, and recovery.
- **Security:** keep credentials and all sensitive environment values outside
  reusable code. Use AAP credentials, approved secret managers, or a separate
  private Vault-encrypted secrets repository. Protect output and temporary data;
  preserve TLS, least privilege, targeting, and ownership boundaries.
- **PAH:** source collection releases from private automation hub. Declare exact
  versions; do not vendor installed/downloaded collections in project Git repos.
  Justified custom collections may have dedicated source repositories.
- **EEs:** use AAP-provided EEs where possible. Custom EEs need a justified
  `execution-environment.yml`, dependencies, build/publish instructions, runtime
  inspection, and reproducible AAP registration.
- **CaC:** every created project must be CaCable, with reproducible AAP objects,
  relationships, protected inputs, and verified restoration. No repository
  consolidation is implied.
- **Speed:** measure timings, reduce redundant work, and use safe batching and
  parallelism. Retain required integrity and completion checks.
- **Quality checks:** run `ansible-lint --profile production --strict`, syntax
  checks against the AAP baseline, APME, and appropriate supporting-language
  checks. Record which APME validators actually completed. Missing checks leave
  acceptance incomplete; explain narrow exceptions.
- **Security references:** use release-matched Red Hat development/security
  guidance and applicable CIS controls. Select benchmark/profile explicitly.
  OpenSCAP and NIST SSDF are proposed supporting references where relevant.
- **Tests:** create smoke tests after provisioning; verify behavior, idempotency,
  relevant failure/recovery cases, and supported scenarios.
- **Final test:** always finish functional acceptance with the complete AAP
  end-to-end test. Fix findings in batches; multiple findings may be corrected
  in one run. After the batch, run functionality and regression tests, fixing
  and retesting until they pass. Then restart the **whole review procedure**,
  including the complete final end-to-end test.
- **Documentation:** keep the README, decision history, and TLDR current. Complex
  workflows need a maintained visual process overview on GitHub Pages.
- **Review report:** after a successful review, create `Code_Review_YYYY-MM-DD.md`
  in the reviewed repository and link it from that project's README. Record
  findings/fixes, tested revisions, coverage and test results, and any conflicting
  review guidance, the chosen approach, and the reason for that choice.

Review → collect findings → fix a batch → functionality tests → restart the
full review → final full AAP end-to-end test → write the report in the reviewed
repository and accept the exact tested revision.
Failed functionality tests stay in the fix-and-test cycle until they pass.
Do not restart the complete review after each individual finding or edit.

Review requirements do not authorize destructive tests or unrelated environment
changes. Sensitive evidence stays outside public repositories. No project has
been reviewed merely by publishing these rules.
