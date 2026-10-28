# Triage Labels

The skills speak in terms of five canonical triage roles. This file maps those roles to the actual label strings used in this repo's issue tracker.

| Label in mattpocock/skills | Label in our tracker | Meaning                                  |
| -------------------------- | -------------------- | ---------------------------------------- |
| `needs-triage`             | `needs-triage`       | Maintainer needs to evaluate this issue  |
| `needs-info`               | `needs-info`         | Waiting on reporter for more information |
| `ready-for-agent`         | `ready-for-agent`    | Fully specified, ready for an AFK agent  |
| `ready-for-human`          | `ready-for-human`    | Requires human implementation            |
| `wontfix`                  | `wontfix`            | Will not be actioned                     |

When a skill mentions a role (e.g. "apply the AFK-ready triage label"), use the corresponding label string from this table.

All five labels exist on `eazlong/xiaozhi_server`. `wontfix` was already present as a GitHub default and is reused as the role's label rather than duplicated.

## Wayfinding labels

Used by `/wayfinder` (recorded here so the label vocabulary lives in one place):

| Label                | Meaning                                          |
| -------------------- | ------------------------------------------------ |
| `wayfinder:map`      | The map — one issue holding the route and fog    |
| `wayfinder:research` | Ticket: go find something out                    |
| `wayfinder:prototype`| Ticket: build a throwaway to answer a question   |
| `wayfinder:grilling` | Ticket: interrogate a decision before committing |
| `wayfinder:task`     | Ticket: known work, just do it                   |

Each ticket carries exactly one `wayfinder:<type>` label; the map carries `wayfinder:map`.

Edit the right-hand column to match whatever vocabulary you actually use.
