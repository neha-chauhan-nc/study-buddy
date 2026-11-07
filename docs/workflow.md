# Study Buddy Workflow

## End-to-End Flow

1. The student joins `study-room`.
2. The student pastes study notes.
3. `notes-agent` summarizes the notes and extracts key points.
4. `notes-agent` hands the notes and summary to `quiz-agent`.
5. `quiz-agent` asks five questions, one at a time.
6. The student answers each question.
7. `quiz-agent` checks every answer and gives concise feedback.
8. After Q5, `quiz-agent` identifies incorrect topics.
9. `quiz-agent` hands those topics to `planner-agent`.
10. `planner-agent` creates a `DRAFT` three-day revision plan.
11. The student replies `approve` or gives edits.
12. `planner-agent` revises or finalizes the plan.

## Agent Handoffs

```text
notes-agent
     │
     │ notes + summary
     ▼
quiz-agent
     │
     │ incorrect topics
     ▼
planner-agent
     │
     │ draft → approval/edit
     ▼
final revision plan
```

## Testing Checklist

- [x] Switch local server starts successfully
- [x] Docker is running
- [x] Codex is connected
- [x] notes-agent created
- [x] quiz-agent created
- [x] planner-agent created
- [x] study-room created
- [x] End-to-end workflow tested
- [ ] Capture final screenshots
- [ ] Add screenshots to `screenshots/`
- [ ] Push project to GitHub
