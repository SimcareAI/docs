# pg_stat_statements snapshot — prod (teajfjskcdsnctdnpnsy)

Taken 2026-09-25, right before `pg_stat_statements_reset()`. Stats window: 2026-02-12 → 2026-09-25.
Total exec time by role: service_role 391h, authenticated 50h, authenticator 13h, postgres 10h, auth_admin 3h, anon 3h.

Top statements by total exec time (mean_ms is the whole-window average; the hours-summary
pushdown fix landed 2026-09-09, so those averages are mostly pre-fix):

| # | role | calls | mean ms | total h | statement |
|---|------|------:|--------:|--------:|-----------|
| 1 | service_role | 222,808 | 2,702 | 167.2 | rpc fieldx.bulk_placement_hours_summary |
| 2 | service_role | 124,403 | 1,815 | 62.7 | rpc fieldx.bulk_student_hours |
| 3 | service_role | 261,055 | 409 | 29.6 | rpc fieldx.bulk_pre_app_forms |
| 4 | service_role | 22,196 | 3,071 | 18.9 | rpc fieldx.bulk_placement_hours_summary (variant) |
| 5 | service_role | 52,093 | 1,186 | 17.2 | select fieldx.placement_hours_summary (direct view read) |
| 6 | service_role | 41,179 | 1,462 | 16.7 | rpc fieldx.bulk_placement_hours_summary (variant) |
| 7 | service_role | 12,546 | 2,433 | 8.5 | select fieldx.placement_hours_summary (direct view read) |
| 8 | authenticated | 59,150 | 471 | 7.7 | case_templates + case_template_sharing by school_id |
| 9 | service_role | 11,360 | 2,403 | 7.6 | rpc fieldx.bulk_placement_hours_summary (variant) |
| 10 | service_role | 14,590 | 1,838 | 7.5 | rpc fieldx.bulk_student_hours (variant) |
| 11 | service_role | 27,967 | 869 | 6.8 | rpc fieldx.bulk_student_hours (variant) |
| 12 | service_role | 25,355 | 938 | 6.6 | rpc fieldx.search_sites_hybrid |
| 13 | authenticator | 161,150 | 124 | 5.5 | PostgREST schema cache reload (columns) |
| 14 | authenticated | 40,515 | 454 | 5.1 | cases join case_templates |
| 15 | service_role | 7,491 | 2,041 | 4.3 | select fieldx.placement_hours_summary (direct view read) |
| 16 | authenticated | 27,004 | 553 | 4.2 | assignment_submissions join users.role |
| 17 | service_role | 18,772 | 653 | 3.4 | select fieldx.placement_hours_summary (direct view read) |
| 18 | service_role | 138,496 | 76 | 2.9 | rpc fieldx.bulk_pre_app_forms (variant) |
| 19 | authenticated | 17,856 | 587 | 2.9 | case_templates + sharing (variant) |
| 20 | service_role | 492,912,689 | 0.005 | 2.6 | PostgREST set_config per request |

Hot-but-cheap (Natalie's RLS point): `SELECT role FROM users WHERE id = auth.uid()` 153M calls / 1.0h;
`SELECT school_id ...` 154M calls / 0.75h.

Not present at snapshot time: the "Sol Health" WITH query and the `case_data feedback::text LIKE` count
Supabase reported (ad-hoc, evicted — pg_stat_statements.max = 5000).
