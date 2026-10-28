# D&S ERP Portal (prototype)

A lighter front end on top of Microsoft Dynamics 365 Business Central (BC). The goal is to let light users work without a full BC licence (KSh 250,000 a year each).

**Status:** working prototype on **sample data**. It is not connected to BC yet, so every write to BC is simulated.

## What's in it
- **Sign-in and roles:** approver, sales engineer, service engineer, sales manager and portal admin. Admins edit users and a role-by-permission grid.
- **Counter:** barcode scan, kits and fast movers. Quotes and orders with line discounts.
- **Customers:** ledger, statements with overdue amounts by age, and purchase history.
- **Items:** stock by branch, incoming stock with arrival dates, and cost and margin for the roles allowed to see them.
- **Jobs:** job requisitions. **Warranty:** claims with an automatic eligibility check.
- **Self-service:** petty cash, floats, purchase requests and requests for quotation. **Approvals.**
- **BC sync:**
  - Every write goes through a send queue with retries, an outage mode and reconciliation.
  - A document shows "In BC" only after BC accepts it.
- Audit log, notifications, Ctrl+K search, and settings for theme, accent, density and motion.

## Business rules
| Rule | Threshold |
|---|---|
| Line discount needs a manager | > 10% |
| Order over the customer's credit limit | Held for a manager |
| Petty cash needs a manager | > KSh 10,000 |
| Float needs a manager | > KSh 50,000 |
| Job requisition needs approval | > KSh 50,000 |
| Warranty cover | 12 months from the invoice date |
| BC send retries before alerting | 3 |

## Run it
It is a single self-contained `index.html`: open it in a browser, or serve the folder with any static server. Data is stored in the browser's localStorage. Use **Reset sample data** in the account menu to start again.

## Next steps
1. Connect to a BC sandbox through the BC APIs (needs credentials from the digital team).
2. Swap the simulated sync queue for real API calls with idempotency keys.
3. Replace the demo sign-in with company single sign-on (Entra ID).
