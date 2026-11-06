# Test Cases

There are two kinds of tests in this project:

1. **Automated API tests** in `backend/tests/api.test.js` (39 tests). Run them with `npm test` inside `backend/`. They use the in-memory demo database, so they never touch a real MongoDB.
2. **Manual UI checklist** in `docs/Test_Cases_and_Bug_Log.xlsx` (45 cases with a Bug Log and a Summary sheet). Fill in the Status column as you test the screens in the browser.

## What the automated tests cover
| Area | What is checked |
|---|---|
| Login | Token returned, no password in the response, same 401 message for wrong password and unknown email, bad or missing token rejected, wrong-password limit (429), broken JSON gives 400, unknown route gives 404 |
| Registration | Creates an organization and an owner, ignores a role sent by the client, requires an organization name, rejects weak passwords, bad email and empty body, duplicate email (any letter case) gives 409, new user can log in, user list has no password hashes |
| Projects and roles | Owner and manager can create, employee cannot (403), duplicate key gives 409, validation for name, due date and status, only the owner can delete, unknown id gives 404 |
| Tasks | Creates a task, script text stays plain text, validation for title, due date, priority, assignee and missing project, status moves, employee can move only their own tasks, manager can move any, subtask rules, filtering by priority, delete rules |
| Two organizations | Org B cannot see, open, change or delete org A data, cannot create tasks in org A projects, cannot assign people or add members from another organization, deleting a project in org B leaves org A tasks alone |
| Progress numbers | Project progress and dashboard completion rate for 1 done task out of 4 is 25%, a new organization shows zeros |

## Result
All 39 automated tests pass. The same tests were also run against the original code before the fixes. Many of them failed there (registration crashed, anyone could pick a role, invalid due dates were accepted, tasks could be given to people in other organizations), which is why they were added.

## Not covered yet
- The automated tests run in memory mode only. They have not been run against a real MongoDB.
- The React screens have not been click-tested. Use the manual checklist for that.
- File uploads and comments do not exist in this version.
