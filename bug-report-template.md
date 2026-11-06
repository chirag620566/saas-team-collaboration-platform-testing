# Bug Report Template

**Bug ID:** BUG-001  
**Severity:** Critical | High | Medium | Low  
**Assigned Module:** Frontend (Member 2) | Backend (Member 3) | Database (Member 4)  
**Status:** Open | Fixed | Verified  

---

### Description
Brief summary of the issue encountered.

### Steps to Reproduce
1. Navigate to `/login`
2. Submit valid credentials
3. Drag a task card to another column

### Expected Behavior
Card smoothly transitions to target column and persists via `PATCH /api/tasks/:id/status`.

### Actual Behavior
Card does not update or gives 500 error.

### Environment
- OS: Windows 11
- Node.js: v20+
- Browser: Chrome / Edge
