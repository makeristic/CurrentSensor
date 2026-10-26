# CurrentSensor discoverability

## Acceptance criteria

- The README identifies the circuit and links the existing editable source and PDF.
- The schematic-only status, missing manufacturing/firmware artefacts and unresolved library dependency are explicit.
- Existing terms are preserved; MIT covers only Michael Cutler's original work.
- The GitHub description and topics match the schematic, without implying tested performance.
- Documentation links and whitespace checks pass; source design files remain unchanged.
- The feature branch is pushed and an open PR records the changes and validation.

## Checklist

- [x] Inspect the schematic, project, PDF, history and existing repository metadata.
- [x] Write the README, scoped MIT licence and generated-state ignore rules.
- [x] Update and verify the GitHub description and topics.
- [x] Validate links and review the complete diff against the default branch.
- [x] Commit, push and open the PR.

## Source audit and correction

- [x] Inspect component mappings, connectivity, library setup and existing documentation against the source.
- [x] Correct reproducible project setup errors and document unresolved circuit work in `docs/code-audit-report.md`.
- [x] Validate the final diff and supported CAD operations, update the existing PR, then merge the verified head.
