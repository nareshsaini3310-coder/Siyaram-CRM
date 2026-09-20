# Stage A Builder File: Data, Permissions And Privacy

Use with `followup_app_design_prompt.md`.

## Data

Use Room tables for Project, Lead, Colour, Interaction, Visit, Template, and Setting. Canonical phone uniqueness uses the last 10 digits. Duplicate imports update/link the existing Lead. Leads archive instead of hard-delete and remain restorable with their history.

## Permissions

Request staged permissions only after a clear Hinglish explanation. Denied permissions must not stop core CRM work. Excel uses the system file picker and must not request storage permission. The first screen says: `Aapka data sirf aapke phone mein hai.`

## Privacy

Keep data local by default. Stage D broker-to-broker sharing requires explicit consent and DPDP legal review. Respect Android and Play Store call-log restrictions; direct APK distribution is expected unless policy eligibility changes.

## Stage A Acceptance

- Verify Room migration safety.
- Verify archive and restore.
- Verify duplicate phone import.
- Verify permission denial fallback.
- Verify backup/restore keeps linked records.
