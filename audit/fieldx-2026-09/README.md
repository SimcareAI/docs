# FieldX documentation audit — September 10, 2026

Reviewed all 36 FieldX guides using the current application, its local implementation, and the documentation repository. Updated all 36 guides and added 31 PNG screenshots with red arrows. All 18 guides that previously had no image now have a relevant screenshot. Existing detailed images remain where no replacement was needed.

## Review records

- [Student guides](student.md): nine guides, 12 new annotated images.
- [Faculty and site supervisor guides](faculty-supervisor.md): seven guides, eight new annotated images.
- [Administrator and shared guides](admin.md): 20 guides, 11 new annotated images.

The original application captures are retained in the application workspace under `artifacts/fieldx-student-screenshots` and `artifacts/fieldx-docs-audit/raw`. New documentation assets live in `images/fieldx/audit`. Each role report records source evidence, image targets, exact annotation prompts, and verification limits.

## Main corrections

- Replaced outdated menus and report names, and separated downloadable reports from reports that collect signatures.
- Corrected faculty progress metrics and navigation that had described the supervisor interface.
- Updated cohort creation, template copying, recurring assignments, and program settings navigation.
- Clarified configuration-dependent site approval, student signatures, long-hour warnings, clearance, and profile requirements.
- Updated notes visibility and supervisor credential access. Removed unsupported blanket privacy claims.
- Documented the current absence of the Todos header button, with current cohort-task alternatives and conditional legacy instructions.
- Corrected View As sessions to one hour, same-tab navigation, and browser-session scope.
- Replaced missing screenshot assets and added captions and descriptive alt text.
- Repaired three invalid section links found in a review using Mintlify's slug function.
- Removed a nonexistent duplicate Canvas navigation entry and closed a missing changelog `Update` tag that blocked validation.

## Verification

Authenticated the supplied student, teacher, and admin sandbox accounts and navigated their FieldX pages through computer use. The optional supervisor login failed; supervisor screens were inspected through the administrator's read-only View As feature. Screenshots retain that banner and their captions explain the context. No signatures, invitations, messages, hour entries, profile changes, or program settings were submitted.

The local application source was consulted at checkout `a17d9d68e`, with live UI labels taking precedence when the source and deployed screen differed. Source inspection supports conditional flows that were not activated just to obtain a screenshot.

Validation includes Mintlify's full build and broken-link checks, every FieldX image reference, all navigation paths, PNG file headers, `git diff --check`, and internal section-link review. Representative student, faculty, supervisor, and admin pages were inspected in a local Mintlify browser preview.

## Remaining limits and product observations

- Canvas-side setup was not performed. That guide's screenshot illustrates the FieldX verification step; existing Canvas video instructions remain. No LMS linkage was created.
- First-time registration, required-profile blocking, all clearance variants, and final form/report submissions were not executed. The role reports distinguish these from live observations.
- Two sandbox report detail views displayed totals that did not reconcile with their category totals. The screenshots preserve the displayed data; no application calculations were changed. Review those records before using their numbers as examples.
- Built-in imagegen added the arrows. It resampled some screenshots and fonts; the relevant controls, labels, and visible data were visually checked. Originals remain available. These images are not byte-identical overlays.
- Changes are prepared for review in a documentation PR and are not published by this audit.
