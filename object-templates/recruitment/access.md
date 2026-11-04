# Recruitment Suite Access

Access is granted through teams. Candidate and vacancy records are sensitive
and are scoped to recruitment work, hiring decisions, and approved management.

## Object access

| Team | Candidate | New Candidate | Qualified Candidate | Employee | Alumni | Vacancy | Match (draft) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| General employee | No access | No access | No access | Read own employment context only | No default access | No access | No access |
| Recruitment | Full access | Full access | Full access | Read/update recruitment handoff fields | Read limited history | Full access | Full access |
| HR | Full access | Full access | Full access | Full access | Full access | Read | Full access |
| Sales | No default access | No default access | No default access | No default access | No default access | Read only when commercially relevant | No default access |
| Marketing | Read approved non-sensitive fields | Read approved source fields | No default access | No access | No access | Read published vacancies | Read approved attribution fields only |
| Hiring managers | Read assigned candidates | Read/update assigned candidates | Read/update assigned candidates | Read hiring handoff fields | No default access | Read/create/update assigned vacancies | Read/update assigned Matches and approved fields only |
| Management | Full access | Full access | Full access | Full access | Full access | Full access | Full access |

## Sensitive data

Recruitment and HR control access to candidate contact details, evaluation
notes, interview information, and hiring decisions. Marketing and hiring
managers receive only the fields needed for their assigned work.

## Match draft

The Match column is a proposed policy for [Match](match.md), not a statement
of deployed permissions. Linked properties require source-data authorization
as well as Match access. Marketing access to attribution must not grant contact,
qualification, or notes access. Match is not public.
