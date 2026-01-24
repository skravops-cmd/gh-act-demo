1.  **visual mental model (hierarchy)**
2.  **clean structured Markdown document template**
3.  **short explanation of each layer**
4.  **quick-reference checklist**


---

# 🧠 1) Mental Model — “The Roof”

Think of GitHub Actions like this:

```
Event
  ↓
Workflow
  ↓
Workflow Run
  ↓
Jobs
  ↓
Steps
  ↓
Actions
  ↓
Runners
```

And alongside:

```
Artifacts ← produced by Jobs
CI/CD ← types of Workflows
```

This is the “single roof” structure.

---

# 🧩 2) Clean Unified Notes — Template Document

---

## GitHub Actions — Core Concepts

### 1) Events — Triggers

**What they are:**
Events are specific activities that trigger a workflow.

**Examples:**

* `push`
* `pull_request`
* `workflow_dispatch` (manual)
* `schedule` (cron)
* external webhooks

**Where defined:**

```yaml
on:
  push:
    branches: [ "main" ]
```

**Purpose:**
No event → no workflow run.

---

### 2) Workflow — The Automation Definition

**What it is:**
Workflow is an automated process made of one or more jobs.

**Where stored:**
`.github/workflows/<workflow>.yml`

**Contains:**

* Triggers (events)
* Jobs
* Steps

---

### 3) Workflow Run — A Single Execution

**What it is:**
An instance of a workflow running after an event occurs.

**You can see:**

* Job status
* Step logs
* Artifacts

---

### 4) Jobs — Units of Work

**What they are:**
A job is a collection of steps executed on the same runner.

**Properties:**

* Run sequentially inside a job
* Jobs can run in parallel
* Each job has its own runner

**Example:**

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
```

---

### 5) Runners — Execution Environment

**What they are:**
Virtual machines or containers that execute jobs.

**Types:**

* GitHub-hosted runners
* Self-hosted runners

**Example:**

```yaml
runs-on: ubuntu-latest
```

---

### 6) Steps — Tasks Inside a Job

**What they are:**
Steps are individual tasks executed inside a job.

**Two types:**

* Run shell commands
* Use actions

**Example:**

```yaml
steps:
  - run: echo "u can run - u can't hide"
  - uses: actions/checkout@v4
```

---

### 7) Actions — Reusable Building Blocks

**What they are:**
Reusable units of code that perform specific tasks.

**Sources:**

* GitHub Marketplace
* Your own custom actions

**Used as:**

```yaml
- uses: actions/checkout@v4
```

**Rule:**

* All actions run as steps
* Not all steps run actions

---

### 8) Artifacts — Output Files

**What they are:**
Files produced by workflows.

**Examples:**

* Build binaries
* Logs
* Test reports
* Deployment packages

**Used for:**

* Sharing data between jobs
* Download after workflow completes

---

### 9) CI/CD — Workflow Purposes

**CI (Continuous Integration):**

* Build
* Test
* Validate code

**CD (Continuous Deployment):**

* Deploy to servers/cloud
* Release automation

---

## 3) Example Minimal Workflow

```yaml
name: CI

on:
  push:
    branches: ["main"]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
      
      - name: Run script
        run: echo "It's Alive!"
```

---

## 4) One-Page Cheat Sheet

| Concept      | What it does              | Defined in                |
| ------------ | ------------------------- | ------------------------- |
| Event        | Triggers workflow         | `on:`                     |
| Workflow     | Automation definition     | `.github/workflows/*.yml` |
| Workflow Run | Single execution instance | Actions tab               |
| Job          | Group of steps            | `jobs:`                   |
| Runner       | Execution machine         | `runs-on:`                |
| Step         | Individual task           | `steps:`                  |
| Action       | Reusable step logic       | `uses:`                   |
| Artifact     | Output file               | upload/download actions   |

---

# 🧭 6) ADHD-Friendly Tip

When you feel lost, ask:

**“What event triggered what workflow, which started what job, which ran what steps, on which runner, producing what artifacts?”**

If you can answer those six questions — you understand the system.

---

