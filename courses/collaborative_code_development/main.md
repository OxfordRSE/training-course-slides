---
layout: section
title: " "
---

## Part 1: Collaboration problems and principles

---
layout: two-cols
---

# Software development is ongoing

- Software is never “finished”
- Bugs are discovered over time
- New requirements and improvements emerge

::right::

<div style="display: flex; justify-content: center; align-items: center; gap: 20px; margin: 20px 0;">
  <img src="./imgs/software-development.png" alt="Software lifecycle" style="width: 75%;" />
</div>

---
layout: two-cols
---

# Knowing about problems is not enough

- Issues must be recorded somewhere shared
- They need prioritisation and ownership
- Decisions need context and history

::right::

<div style="display: flex; justify-content: center; align-items: center; gap: 20px; margin: 20px 0;">
  <img src="./imgs/bug-tracking.png" alt="Bug tracking" style="width: 75%;" />
</div>

---
layout: two-cols
---

# What is issue tracking?

- A shared list of tasks, bugs, and ideas
- A place for discussion and decisions
- A record of what was done and why

::right::

<div style="display: flex; justify-content: center; align-items: center; gap: 20px; margin: 20px 0;">
  <img src="./imgs/issue-tracking.png" alt="Issue tracking" style="width: 70%;" />
</div>

---
layout: two-cols
---

# Parallel work and code review

- Multiple contributors working on the same codebase
- Working in parallel on separate changes
- Reviewing each other’s work before integration

::right::

::center
![Parallel working](./imgs/parallel-working.png)
::

---
layout: section
title: " "
---

## Part 2: Platforms enable these practices

---

# From collaboration practices to tools

- Issue tracking is a practice
- Parallel work is a practice
- Code review is a practice

<br />
<br />

<v-click>
<div style="text-align: center;">
  <h3><b>Tools exist to support these practices at scale</b></h3>
</div>
</v-click>

---

# Project management with GitHub

- "GitHub Issues" are an implementation of issue tracking
- "Mentions" are a communication mechanism
- "Labels" and "milestones" are prioritisation tools


<div style="display: flex; justify-content: center; align-items: center; gap: 20px; margin: 20px 0;">
  <img src="./imgs/github-issues.png" alt="Github issues" style="width: 35%;" />
  <img src="./imgs/github-issue-discussion.png" alt="Github issue discussion" style="width: 45%;" />
</div>

---

# Git branches + feature branch workflow

::center

**Git implements parallel work using branches**

<br />

<div style="width: 70%;">
```mermaid
gitGraph
  commit id: "A"
  branch develop
  commit id: "B"
  branch big_feature
  commit id: "C"
  checkout develop
  commit id: "D"
  checkout main
  merge develop tag: "v1.1"
  checkout develop
  branch small_feature
  commit id: "E"
  commit id: "F"
  checkout big_feature
  commit id: "G"
  checkout develop
  merge small_feature
  checkout main
  merge develop tag: "v1.2"
  checkout big_feature
  commit id: "H"
```
</div>

---

# Git branches + feature branch workflow

<div class="flex flex-1 items-end justify-between h-64 w-100%">

<div class="flex flex-col justify-between items-center w-45 h-100% text-sm">
Commit to main branch
```mermaid {scale: 0.8}
gitGraph BT:
  commit id: "First"
  commit id: "Second"
```
</div>

<div v-click class="flex flex-col justify-between items-center w-45 h-100% text-sm">
Create a new branch, make commits to it
```mermaid {scale: 0.8}
gitGraph BT:
  commit id: "First"
  commit id: "Second"
  branch feature
  commit id: "New thing"
```
</div>

<div v-click class="flex flex-col justify-between items-center w-45 h-100% text-sm">
Changes independent of main branch
```mermaid {scale: 0.8}
gitGraph BT:
  commit id: "First"
  commit id: "Second"
  branch feature
  commit id: "New thing"
  checkout main
  commit id: "Other work"
```
</div>

<div v-click class="flex flex-col justify-between items-center w-45 h-100% text-sm">
Merge commit
```mermaid {scale: 0.8}
gitGraph BT:
  commit id: "First"
  commit id: "Second"
  branch feature
  commit id: "New thing"
  checkout main
  commit id: "Other work"
  merge feature
```
</div>

</div>

- Main branch for tested, stable code, feature branches for new, separate units of work
- Keeps main branch stable, allows independent work on features
- Easy to discard unwanted features

---

# Collaborative code development models

::center
<b>Different projects balance control and openness differently</b>
::

<div style="display: flex; justify-content: space-evenly; align-items: center; gap: 20px; margin: 20px 0;">
  <div style="display: flex; flex-direction: column; align-items: center;">
    <div>Shared repository model</div>
    <div>(common in private projects)</div>
    <img src="./imgs/github-shared-repo.png" alt="Shared repository model" width="210px">
  </div>
  <v-click >
    <div style="display: flex; flex-direction: column; align-items: center;">
      <div>Fork and pull model</div>
      <div>(popular in open source)</div>
      <img src="./imgs/github-fork-pull.png" alt="Shared repository model" width="350px">
    </div>
  </v-click>
</div>

---
layout: two-cols
---

# Pull requests: a tool for review and integration

- Propose changes for review
- Discuss and refine work
- Run automated checks on changes
- Integrate approved changes safely

::right::

::center
![Pull request](./imgs/github-pullrequest.png)
::

---
layout: two-cols
---

# Advantages of code review

- Identifies defects early in the process
- Cost-effective error removal
- Enhances team learning and collaboration
- Improves overall team software development process

::right::

::center
![Code review](./imgs/code-review.jpg)
::

---

# Adding code via GitHub pull requests

- Discuss and review changes
- Add follow-up commits based on feedback
- Merge changes from feature branch to base branch

<div style="display: flex; justify-content: center; align-items: center; gap: 20px; margin: 20px 0;">
  <img src="./imgs/merge-pipeline.jpg" alt="Merge pipeline" style="width: 65%;" />
</div>

---

# Learning objectives

- Use the feature branch workflow to collaborate with others on the same repository
- Learn about code reviews and pull requests on GitHub
- Understand and create GitHub issues to manage bug reports and feature requests

---

# Example GitHub repository

<div style="display: flex; flex-direction: column; align-items: center; gap: 20px; margin-top: 20px;">
  <h3><b>C</b>ancer, <b>H</b>eart <b>a</b>nd <b>S</b>oft <b>T</b>issue <b>E</b>nvironment</h3>
  <img src="./imgs/chaste.png" alt="Chaste" style="width: 25%; margin-top: 20px;" />
  <a href="https://github.com/Chaste/Chaste">https://github.com/Chaste/Chaste</a>
</div>
