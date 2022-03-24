+++
title = "Project Planning"
date = 2022-02-23
[extra]
mathjax = true
+++

# Predictive Planning

Predictive planning is an option if:
- requirements are well-understood and stable
- a suitable software design has been identified and validated
- programmers are comfortable with the implementation technologies
- the team's productivity is estimable

Adaptive Planning is better suited to new product development and exploratory-type projects with uncertainty

{{ definition(term="Planning Horizon") }}

# Work Breakdown Structure (WBS)

Creating a WBS is a systematic way of identifying the tasks needed to complete a project. It provides a hierarchical decomposition of the work, and can be presented in graphical or outline form.

{% callout(type="info") %}
Creating a WBS is a systematic way of identifying the tasks needed to complete a project. It provides a hierarchical decomposition of the work, and can be presented in graphical or outline form.Creating a WBS is a systematic way of identifying the tasks needed to complete a project. It provides a hierarchical decomposition of the work, and can be presented in graphical or outline form.Creating a WBS is a systematic way of identifying the tasks needed to complete a project. It provides a hierarchical decomposition of the work, and can be presented in graphical or outline form.
{% end %}

Two types of tasks:
- summary
- detailed elemental tasks (aka *work packages*)
    - tasks description
    - owner
    - schedule start/stop dates
    - estimated effort
    - expected output/deliverable
      - optional completion/acceptance criteria
    - staff and material resources needed to complete the task

# Task Dependencies

Before you can schedule tasks, you have to know the predecessor and successor relationships between tasks.

{% callout(type="warning") %}
uh oh!
{% end %}

- Finish to Start
  - Task \\(A\\) must finish before task \\(B\\) can start.
- Finish to Finish
  - Task \\(A\\) must finish before task \\(B\\) can finish.
  - Common with work that's largely sequential, but can also benefit from feedback fromd ownstream activities.
  - Examples:
    - requirements must be finished before project plan can be finished.
    - drywall must be complete before painting can finish.
- Start to Start
  - Task \\(B\\) can't start until task \\(A\\) starts.

{% aside(title="hey") %}
oops aside!
{% end %}

{% callout(type="note") %}
note 4 l8r
{% end %}

# Estimation

- Effort and duration estimates are made for each task
- After scheduling, these estimates are rolled up (bottom-up estimation) into overall estimates for project cost and duration
- There are several estimation techniques that may be used
  - analogy
  - algorithm models
  - expert opinion

[Continued here!](@/notes/cs451/project_planning_continued.md)