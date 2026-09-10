# Faculty and site supervisor documentation audit — September 10, 2026

All seven pages in this audit started without screenshots. Current source was inspected in `soma-lab-v2`; live screens were captured through computer use by the root agent. No cohort enrollment, profile save, report denial, signature, invitation, or email was submitted for this audit.

## Page inventory

| Guide | Outdated or missing content addressed | Screenshot |
| --- | --- | --- |
| `fieldx/faculty/step-1-joining-cohorts.mdx` | Added explicit Open Cohort → My Tasks navigation and removed claim that students must be cleared before appearing; updated sender guidance. Live Join Code / Join Course labels match existing instructions. | `faculty-join-cohort.png` |
| `fieldx/faculty/step-2-viewing-student-progress.mdx` | Replaced supervisor document KPI cards with faculty Students Off Pace / Average Completion / Pending Tasks; corrected Cohorts task navigation, removed supervisor-only My Profile instructions, documented external signer prompts and term-dependent empty metrics. | `faculty-overview.png` |
| `fieldx/faculty/step-3-signing-off-on-hours.mdx` | Corrected report dialog location, zero-hours guidance, configurable long-entry notices, denial confirmation, signing status meaning, email wording and unsupported fixed weekly digest day. | `faculty-hours-report.png` |
| `fieldx/site/step-1-getting-started.mdx` | Corrected welcome email/credentials flow, optional vs required profile prompt, report status meaning, zero-hour rules, comment visibility, long-entry notice, digest timing. | `supervisor-overview.png`, `supervisor-tasks.png` |
| `fieldx/site/step-2-viewing-student-progress.mdx` | Corrected role-specific Completed meaning, zero-hour rules, configurable long-entry notice, denial confirmation and resubmission path; retained read-only Students scope. | `supervisor-students.png` |
| `fieldx/site/step-3-signing-off-on-hours.mdx` | Corrected role-specific completion vs finalized PDF, zero-hour rules, configurable long-entry notices, email signing labels and digest timing. | `supervisor-hours-report.png` |
| `fieldx/site/step-4-my-profile.mdx` | Replaced fixed single-license list with multi-select credentials; added Hide Email from Site; corrected Saved feedback, partial save, optional prompt suppression, required CTA, and disabled Students tab. | `supervisor-profile.png` |

## Evidence

Source paths below are relative to the application repository:

- `app/components/field-exp/teacher-overview/TeacherKpiCards.tsx` — three faculty metrics and empty-term dashes.
- `app/components/field-exp/teacher-overview/TeacherOverview.tsx` and `hooks.ts` — term/filter/search controls and roster sorting.
- `app/(pages)/field-exp/faculty/FacultyFieldExpClient.tsx` — faculty Overview, Cohorts, Sites, Run Report navigation.
- `app/components/field-exp/TrackModals.tsx`, `app/lib/constants/trackConstants.ts` and `app/api/tracks/join/route.ts` — instructor Join Code / Join Course and case-sensitive 8-character code matching.
- `app/components/field-exp/tasks/TeacherActionItemsView.tsx` — cohort My Tasks / Assignments / Members / Settings and task states.
- `app/components/field-exp/teacher-overview/ExternalSignerTasksButton.tsx` — Overview signature prompt for externally assigned forms.
- `app/components/action-items/ActionItemPanel.tsx` and `ActionItemInfo.tsx` — resolved report-total zero-hours gate, View Logs / Sign & Approve, denial confirmation.
- `app/lib/fieldx/long-log-entry-setting.ts` — configurable inclusive long-entry threshold, 2-hour default, optional notice.
- `app/lib/utils/report-status-utils.ts` and `app/components/field-exp/supervisor/SupervisorActionItemsView.tsx` — supervisor reports complete after the supervisor signs; faculty progress and form status are classified separately. Opening the signature modal does not establish completion.
- `app/components/field-exp/supervisor/SupervisorOverview.tsx` and `SupervisorStudentTasksTable.tsx` — supervisor KPI definitions and task-based student list.
- `app/(pages)/field-exp/supervisor/SupervisorFieldExpClient.tsx` — supervisor tab names/order and required-profile gate.
- `app/components/field-exp/supervisor/SupervisorProfileTab.tsx`, `SupervisorProfilePromptModal.tsx`, `app/contexts/SupervisorProfileContext.tsx` and `app/lib/constants/supervisor-license-types.ts` — current credential fields, multi-select, optional prompt vs program requirements, Complete My Profile CTA, partial save, Saved feedback and Hide Email from Site.
- `app/lib/comments/visibility.ts` — internal comment visibility includes supervisors, faculty, and admins.
- `app/lib/email/sendSupervisorInvite.ts` and `app/api/field-exp/PreApplicationTasks/addSupervisor/html.ts` — initial invitation sender/subject and credentials with normal sign-in URL. Current template does not render the old magic-link argument.
- `app/lib/email/sendClassInvitationEmail.ts` and `sendSignatureReminderEmail.ts` — default SimCare sender. Deployment can override general notification sender through configuration.

## Live verification and limits

Faculty was inspected under the supplied teacher sandbox account. Captures cover Overview, Cohorts, the instructor join dialog, cohort My Tasks, and a pending Weekly Hours Log report. Live labels show **Run Report** (singular).

The provided site-supervisor credentials failed on one login attempt. Supervisor Overview, Tasks, an hours report, Students, and Professional Profile were then inspected through the admin's supported read-only **View as Supervisor** flow for Marcus Thompson. The orange read-only banner is retained in all five annotated screenshots, and captions identify this context. First-login prompt behavior and profile-save validation are source-reviewed only; no credentials, profile, or role were changed.

Email delivery, invitation acceptance, signing completion, denial, resubmission, weekly scheduling, and custom program-required fields were not exercised. The fixed Saturday schedule was removed because it cannot be verified in this repository. Conditional features were retained as conditional.

The captured faculty Weekly Hours Log has a live discrepancy: top Total Hours is 1.0 while category totals sum to 4h. The supervisor report also shows 17.0 total hours while its category total reads 25h 55m. The annotations preserve both captures as observed and point only to review/sign controls. This is an application/data observation, not a documentation calculation.

## Screenshot preparation

The imagegen skill and built-in image tool were used for red arrows. Original captures remain under `artifacts/fieldx-docs-audit/raw` in the application workspace. Annotated project assets are saved under `images/fieldx/audit` in the docs repository. Generated outputs were visually inspected for text, context, and arrow targets; no values or UI controls were intentionally changed.

Prompt set: precise-object-edit instructional screenshots; add exactly two medium red arrows with solid triangular heads; preserve all labels, values, icons, framing, and layout; add no extra labels. Faculty targets: More filters and Tasks; Join Code and Join Course; View Logs and Sign & Approve.

Supervisor arrow targets: Tasks / My Profile; Pending / Get Started; View Logs / Sign & Approve; Calendar / student selector; CV upload / License Type. Eight distinct annotated assets were added across the seven guides.

## Verification

- All seven assigned guides contain a screenshot Frame with descriptive caption and alt text.
- All image references in these guides resolve to nonempty local assets.
- `git diff --check` passes for these MDX files and this audit report.
- Live screenshot labels and arrow targets were visually reviewed. No first-login, profile-save, email-delivery, or signature-state mutation was attempted.
- Site-wide Mintlify preview and broken-link validation are delegated to the root agent's integration check.

## Targeted privacy and anchor review

- Removed the blanket claim that profiles are visible only to supervisors and Program Admins. `app/api/field-exp/admin/supervisor-profiles/route.ts` also grants teachers/faculty with an active membership in a connected program access to core credentials, including CV paths and licenses. Core credentials are global profile data, not limited to fields a program requires. `app/api/field-exp/admin/supervisor-documents/route.ts` separately exposes the CV to authorized staff roles.
- Limited the program-specific privacy statement to custom questions/answers. The profile API's `loadCustomFieldGroups` scopes answers to the viewer's active admin/teacher programs and deliberately retains groups after detachment. The supervisor roster/export/report paths scope custom answers by program ID.
- `app/api/sites/[siteId]/route.ts` returns supervisor name/email for site selection and honors Hide Email from Site; it does not return CV/core credential fields. The guide no longer makes a blanket public-visibility promise.
- Checked all seven MDX files for local and cross-page fragment URLs, and all repository MDX files for incoming fragment links to those seven guides: none found. No heading-anchor links require repair.
