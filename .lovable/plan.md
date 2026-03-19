

## Plan: Fix Audit Log Stats Bar Layout

### Changes

**File 1: `src/components/settings/audit/auditLogUtils.ts`**
- In `getModuleName()`: Map `tasks`, `deal_action_items`, `lead_action_items` all to `'Action Items'` instead of `'Tasks'`
- In `getReadableResourceType()`: Change `tasks` → `'Action Items'`, add `deal_action_items` and `lead_action_items` → `'Action Items'`
- In `getDatePresets()`: Remove `'This month'` entry

**File 2: `src/components/settings/audit/AuditLogStats.tsx`**
- Remove the "Total" badge entirely
- Remove "This Week" badge (duplicate of "Last 7 days")
- Remove `weekCount` prop usage
- Layout order: **Today (with count)** → **Last 7 days** → **Last 30 days** → separator → **Module chips** (Action Items, Deals, Contacts, Campaigns, Accounts...) → Clear filter button
- Date presets and module chips render inline in one row

**File 3: `src/components/settings/AuditLogsSettings.tsx`**
- Remove `weekCount` from stats passed to `AuditLogStats`
- Remove `onFilterThisWeek` handler
- Update `moduleDisplayToFilter` map: remove `'Tasks'` key, add `'Action Items': 'action_items'`
- When `moduleFilter === 'action_items'`, match resource_type in `['tasks', 'action_items', 'deal_action_items', 'lead_action_items']`

**File 4: `src/components/settings/audit/AuditLogFilters.tsx`**
- Rename "Tasks" option to "Action Items" with value `'action_items'` in module dropdown

### Expected Result
Stats bar: `Today 14 | Last 7 days | Last 30 days | Action Items 47 | Deals 38 | Contacts 14 | Campaigns 1 | Accounts 1` — no "Total", no "This Week", no "This month", "Tasks" always shown as "Action Items".

