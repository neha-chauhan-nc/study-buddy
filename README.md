# 📚 Study Buddy — Multi-Agent AI Study Assistant

Study Buddy is a multi-agent AI learning assistant built for a hackathon using **Switch + Codex + Mattermost**.

It uses three specialized agents to turn study notes into a personalized quiz and revision plan.

## 🚀 Workflow

```text
                    USER
                      │
                      ▼
              ┌───────────────┐
              │  notes-agent  │
              │ Notes →       │
              │ Short Summary │
              └───────┬───────┘
                      │
              Notes + Summary
                      │
                      ▼
              ┌───────────────┐
              │  quiz-agent   │
              │ 5 Questions   │
              │ Answer Check  │
              └───────┬───────┘
                      │
                Wrong Topics
                      │
                      ▼
              ┌───────────────┐
              │ planner-agent │
              │ 3-Day Draft   │
              │ Approve/Edit  │
              └───────┬───────┘
                      │
                      ▼
              FINAL REVISION PLAN
```

## ✨ Features

- 📝 Converts pasted study notes into a short summary.
- 🎯 Extracts key points without inventing information.
- 🧠 Generates exactly 5 quiz questions.
- 💬 Asks questions one at a time.
- ✅ Checks each answer and gives short feedback.
- 📊 Tracks topics answered incorrectly.
- 📅 Creates a personalized 3-day revision plan.
- 🔄 Supports draft → approve/edit → final workflow.
- 🤖 Uses specialized agents instead of one general-purpose agent.
- 💬 Uses a shared room workflow through Mattermost.

## 🤖 Agents

### 1. notes-agent

**Input:** Study notes

**Output:** Short summary + key points

Responsibilities:
- Summarize the supplied notes.
- Extract important concepts.
- Avoid adding information that is not present in the notes.
- Pass the notes and summary to `quiz-agent`.

### 2. quiz-agent

**Input:** Notes + summary from `notes-agent`

**Output:** Five-question interactive quiz

Responsibilities:
- Ask one question at a time.
- Wait for the student's answer.
- Check the answer.
- Give concise feedback.
- Track incorrectly answered topics.
- Pass wrong topics to `planner-agent` after question 5.

### 3. planner-agent

**Input:** Topics answered incorrectly

**Output:** Three-day revision plan

Responsibilities:
- Build a concise revision plan.
- Mark the first version as `DRAFT`.
- Ask the student to approve or request edits.
- Revise the draft when edits are requested.
- Publish the final plan only after approval.

## 🛠️ Tech Stack

- **Switch** — multi-agent orchestration
- **Codex** — AI provider for the agents
- **Mattermost** — shared communication/room interface
- **Docker** — local infrastructure/container runtime
- **Markdown** — agent configuration and project documentation

## 📁 Project Structure

```text
study-buddy/
│
├── agents/
│   ├── notes-agent.md
│   ├── quiz-agent.md
│   └── planner-agent.md
│
├── docs/
│   └── workflow.md
│
├── screenshots/
│   └── .gitkeep
│
└── README.md
```

## ⚙️ Setup

1. Install and start Docker Desktop.
2. Start the local Switch server.
3. Sign in to Codex through Switch.
4. Create the three agents:
   - `notes-agent`
   - `quiz-agent`
   - `planner-agent`
5. Configure the agents using the instructions in `agents/`.
6. Create the Mattermost room `study-room`.
7. Add the three agents and the user to the room.
8. Run the end-to-end workflow.

## 🧪 Example

### User provides notes

```text
Photosynthesis is the process by which green plants
convert light energy into chemical energy. Chlorophyll
absorbs sunlight. Carbon dioxide and water are used
to produce glucose and oxygen.
```

### notes-agent

```text
Summary:
Photosynthesis converts light energy into chemical energy
in green plants. Chlorophyll absorbs sunlight, while
carbon dioxide and water are used to produce glucose
and oxygen.

Key points:
- Chlorophyll absorbs sunlight.
- CO₂ and water are used.
- Glucose and oxygen are produced.
```

### quiz-agent

```text
Q1. What is the role of chlorophyll in photosynthesis?
```

The agent waits for the answer, checks it, then continues through Q5.

### planner-agent

If the student repeatedly misses a topic:

```text
DRAFT — 3-Day Revision Plan

Day 1: Review the core concept.
Day 2: Practice questions on the weak topic.
Day 3: Quick revision + self-test.

Reply "approve" or send edits.
```

## 🎯 Why Multi-Agent?

Instead of asking one AI agent to perform every task, Study Buddy separates responsibilities:

- `notes-agent` focuses on **understanding and summarization**.
- `quiz-agent` focuses on **assessment**.
- `planner-agent` focuses on **targeted revision**.

This makes the workflow easier to understand, test, extend, and demonstrate.

## 🔮 Future Improvements

- Progress tracking across multiple study sessions.
- Difficulty adaptation based on quiz performance.
- Subject/topic history.
- Spaced-repetition scheduling.
- Flashcard generation.
- PDF/lecture-note ingestion.
- Analytics dashboard for learning progress.
- Support for multiple students and shared study rooms.

## 👥 Hackathon Demo Flow

```text
1. Open study-room
2. Paste study notes
3. notes-agent creates summary
4. quiz-agent starts 5-question quiz
5. Student answers all questions
6. Wrong topics are identified
7. planner-agent creates DRAFT revision plan
8. Student approves or edits
9. Final revision plan is published
```

## 📌 Status

**Core multi-agent workflow:** Complete ✅

**Agents:** 3/3 ✅

**End-to-end test:** Passed ✅

**README/documentation:** Ready ✅
