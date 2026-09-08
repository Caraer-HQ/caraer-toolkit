# Sales Suite Access

Access is granted through teams. Sales records contain customer and prospect
information and are restricted by default.

## Object access

| Team | Contact / Lead / Qualified Lead | Company / Target / Account / Partner | Customer | Deal | Reseller |
| --- | --- | --- | --- | --- | --- |
| General employee | No default access | No default access | No default access | No default access | No default access |
| Recruitment | Read Contact; no default sales write | Read Company/Target where recruitment needs it | No default access | No default access | No default access |
| HR | Read Contact and Employee-related context | Read organisation context | No default access | No default access | No default access |
| Sales | Full access within assigned sales scope | Full access within assigned sales scope | Full access | Full access | Full access where partner work is assigned |
| Marketing | Read Contact/Company; manage Lead marketing fields | Read Target/Company | Read limited customer context | Read | No default access |
| Hiring managers | Read assigned Contact context | Read relevant Company/Account context | No default access | Read linked deal context | No default access |
| Management | Full access | Full access | Full access | Full access | Full access |

## Suite administration

Sales team leads and Management may administer sales views and team scopes.
Sensitive customer records remain limited to the assigned Sales team and
Management unless explicitly shared.
