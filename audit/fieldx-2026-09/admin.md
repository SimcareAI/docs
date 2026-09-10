# FieldX admin and general documentation audit

Audited September 10, 2026. Scope: all 20 `fieldx/*.mdx` pages, excluding role subfolders. Live browser evidence came from the supplied sandbox accounts. Source checks used the application repository at commit `a17d9d68e4187dce41d75a804db80f9eac90689c`.

## Findings and page coverage

| Guide | Finding and change | Evidence / visual coverage |
| --- | --- | --- |
| `accessing-fieldx` | Sidebar now groups Field Experience under Site Placement. Account and role are at bottom left, not top left. | Live account menu; `admin-account-role.png` replaces old sidebar screenshot. |
| `fieldx-overview` | Corrected role location and account-menu instructions. Kept the role guide links. | Live student account menu; same annotated role example. |
| `ask-ai` | Updated scope from question-only assistant to reports, files, and reviewed admin actions. Removed outdated report example and universal Drive-export claims. | Live welcome screen; capability catalog and table/report components. Added `admin-ask-ai.png`. |
| `coordinator-ask-ai` | Added current report names, XLSX support, .docx generation, attachment workflow, review cards and approval steps. Corrected claim that Overview's term filter automatically supplies chat scope. Removed unsupported privacy/training assertions from the functional guide. | `admin/ask-ai/capabilities-catalog.ts`, `AskAIChatView.tsx`, `MessageBubble/DataTable.tsx`, `ReportDownloadCard.tsx`; live welcome screen. Added `admin-ask-ai.png`. |
| `building-forms` | Corrected entry path to Assignments → Create Assignment → Form → Build New. | Live modal; `features/forms-reports/components/CreateAssignmentModal.tsx`. Added `admin-create-assignment.png`; retained builder reference image. |
| `canvas-lti-integration` | Clarified that one-time assignments copy, past schedule-emitted reports do not, and template cohorts differ from ordinary cohort links. | `lib/fieldx/lti/route-to-cohort.ts` and `clone-cohort-config.ts`. Added `admin-cohorts.png` at FieldX verification step with explicit caption that it is not a Canvas launch. Canvas itself was not authenticated or exercised. |
| `setting-up-recurring-tasks` | Added daily frequency, backdated assignment review, schedule editing and locked start-date behavior. | `site-reports/assign-reports-modal/create/ReportRepeatOptions.tsx`, `tasks/cohortView/EditScheduleModal.tsx`. Existing recurring settings screenshot retained; no new assignments created to exercise scheduling. |
| `step-0-1-testing-fieldx-with-your-sandbox` | Rewrote unsafe/inaccurate advice to invite, log hours, and submit while read-only. Clarified that ordinary admin changes affect real data and test cohorts are not isolated sandboxes. Updated session to one hour; added supervisor preview alternative. | Live Student View banner and source guards. Added `admin-view-student.png`. |
| `step-0-2-customization-settings` | My Program is now Program Settings. Added Hour Templates sidebar tab, corrected Ended/Inactive term statuses and Clearance Tasks navigation. | Live program sidebar and Terms and Tracks; `ProgramPageClient.tsx`, `AcademicTermsSection.tsx`. Replaced academic settings screenshot with `admin-terms-tracks.png`. Configuration-dependent clearance, pooling and Learning Contract instructions preserved. |
| `step-0-getting-started` | Refreshed header labels and screenshot. Removed absent Todos action. Corrected Off Pace drill-down to table help icon and Cohort filter label. Removed redundant older navigation screenshots. | Live Overview; `TeacherKpiCards.tsx`, `StudentTable.tsx`, `FilterModal.tsx`, `HeaderActions.tsx`. Added `admin-overview.png`. |
| `step-1-adding-managing-faculty-students` | Added Supervisors third tab; Add Student/Add Instructor/Admin controls; Program Settings navigation; direct View as Student button and one-hour lifetime. Corrected supervisor invitation subject and credentials flow; scoped 24-hour cooldown to student resend. Removed obsolete roster screenshots. | Live Members and filtered Maya row; `ProgramMembersView.tsx`, `sendSupervisorInvite.ts`, student/admin nudge routes (cross-checked with supervisor audit). Added `admin-view-student-control.png`. |
| `step-2-managing-established-sites` | Removed unconditional assertion that established sites let students log immediately without approval; clarified request/clearance dependence and that Require approval for established sites takes precedence over auto-approval. Updated Program Settings label. | `sites/site-view/admin/AdminSitesView.tsx`, settings controls. Existing site images retained. Approval/removal actions not performed. |
| `step-3-1-approving-students` | Corrected task entry point (student Tasks button, not clickable KPI), Documents → Application review path, Program Settings → Clearance Tasks entry, and revoke extension from Active, not Past. | `TeacherKpiCards.tsx`, `TaskButton.tsx`, `StudentDetailsModal/tabs/DocumentsTab.tsx`, `TermExtensionModal.tsx`. Existing review screenshot retained; no approval/rejection/extension changes submitted. |
| `step-3-set-up-cohorts` | Corrected Cohort Code/Name and default faculty wording, row-based Open Cohort workflow and archive action. | Live cohort list and Create New Cohort; `TrackModals.tsx`, `lib/constants/trackConstants.ts`, cohort components. Added `admin-cohorts.png` and `admin-create-cohort.png`. |
| `step-4-create-assign-tasks` | Removed internal implementation identifier from template explanation; replaced form-creation screenshot with current modal. | Live Create Assignment and source components. Added `admin-create-assignment.png`. Existing assignment/versioning details retained; no template saves or assignments submitted. |
| `step-5-next-semester-setup` | Updated Program Settings label and row archive wording. Illustrated Add Term and source cohort/Academic Terms selectors. | Live term and create-cohort modal; clone configuration helper confirms existing copy guidance. Added `admin-terms-tracks.png` and `admin-create-cohort.png`. No term, cohort, or membership changes made. |
| `step-6-evaluations-reports-information` | Replaced obsolete report-code table with current catalog names and consolidation mapping. Added population, approval, output formats, sample preview versus full generation, saved configuration and Recent reports workflow. | Live catalog (17 reports); `lib/fieldx/reports/engine/catalog.ts`, `ReportCatalog.tsx`, `ReportConfigModal.tsx`, `ReportRunPreviewModal.tsx`. Added `admin-reports.png`. Report availability remains role/program dependent. |
| `todos` | Corrected current availability: no header Todos control in inspected deployments; source comments out TasksDropdown. Added current Cohorts → View All Tasks alternative. Retained legacy instructions only under an explicit conditional heading, correcting Create Task, optional due date, no priority, recurrence and Complete/Dismiss actions. | Live admin/student/faculty/supervisor headers; `HeaderActions.tsx`, `activity-tasks/*`. Added `admin-cohorts.png` to current alternative workflow. No fabricated Todos screenshot. |
| `view-as-student` | Corrected one-hour lifetime, direct Members row button, same-tab navigation, exit to admin Overview, browser-session scope. Narrowed audit promises to recorded start/end events. | Live preview 59:51 countdown; `view-as-jwt.ts`, `ImpersonationBanner.tsx`, `ImpersonationContext.tsx`, view-as routes. Added `admin-view-student-control.png` and `admin-view-student.png`. |
| `view-as-supervisor` | Corrected same-tab navigation, exit to Overview and browser-session scope; removed unsupported guaranteed timeout audit detail. | Live preview 59:52 countdown; supervisor JWT/banner/context/routes. Added `admin-view-supervisor.png`. |

## Screenshot provenance

Raw captures are in the application workspace's `artifacts/fieldx-docs-audit/raw/`. Final documentation assets are under `images/fieldx/audit/`:

- `admin-account-role.png` — student account-menu example; Field Experience navigation and role label.
- `admin-ask-ai.png` — Ask AI tab, capability guide, plus menu.
- `admin-cohorts.png` — Cohorts navigation and View All Tasks.
- `admin-create-assignment.png` — Form tab and Build New.
- `admin-create-cohort.png` — Copy from existing cohort and Academic Terms.
- `admin-overview.png` — Cohorts and Program Settings.
- `admin-reports.png` — catalog search, Preview, Run report.
- `admin-terms-tracks.png` — Terms and Tracks and Add Term.
- `admin-view-student-control.png` — Students and View as Student.
- `admin-view-student.png` — Read-only and Exit Student View.
- `admin-view-supervisor.png` — Read-only and Exit Supervisor View.

Arrows were added with the built-in image editing tool. Each original capture and final annotated output was visually inspected; rejected overview/cohort variants were replaced to avoid obscured fields or ambiguous target arrows. Raw screenshots remain separate from annotated assets. Generated images may have been resampled by the image service.

All eight root guides that initially had no static picture now contain a relevant annotated screenshot. Some images intentionally serve more than one guide. Captions distinguish a supporting FieldX screenshot from an external Canvas workflow and a current formal-task workflow from the unavailable Todos panel.

## Limits and verification

- External Canvas authentication, launch, linking, course copying, and live enrollment were not performed. The Loom walkthrough remains, and relevant FieldX behavior was checked against implementation.
- No live forms, invitations, assignments, approvals, reminders, new terms, site changes, or archive actions were submitted as part of this admin audit.
- Read-only mode was entered and exited in the supplied test environment. The one-hour timer was observed, not waited out. No attempt was made to prove every write endpoint's guard by mutating student data.
- Program-specific settings were not changed merely to make hidden features appear.
- Full-site MDX and internal-link validation is performed by the parent task after integrating parallel changes. This agent checked local image references and reviewed root-guide changes.
