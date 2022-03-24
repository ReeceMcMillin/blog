+++
title = "Project Planning (Continued)"
date = 2022-02-25
[extra]
mathjax = true
+++

# Scheduling

Most common tool: the [Gantt Chart](https://www.gantt.com/). It shows start and stop types for tasks in a usually recognizable calendar form. It also shows timing of milestones.

{% annotation(context = "example gantt chart") %}
![Gantt Chart](https://www.gantt.com/img/gantt-chart-1.jpg)

{% end %}
# Critical Path Analysis & Float Time

The longest sequence of activities in the network diagram

{{ definition(term="slack") }}

# Order of Events

Question: is it better to:
- assign resources \\(\rightarrow\\) estimate effort \\(\rightarrow\\) schedule
- estimate effort \\(\rightarrow\\) schedule \\(\rightarrow\\) assign resources

{{ definition(term="Resource Leveling") }}

# Planning Methods

- Full-Scale Predictive Planning
- Adaptive Planning
  - develop a course-graned macro plan with high-level goals, milestones, and estimates
  - plan in short iterations using the feedback from completed iterations to improve planning 

# Communications Planning

Communication planning is a process:
- determining the information needs of each stakeholder
- making sure the needed information is created and delivered:
  - to the right people
  - at the right time
  - in the right format

## Creating a Communication Plan

1. Determine the information and communication needs of each stakeholder
2. Determine the source of the needed information
3. Decide on the format and frequency of distribution
4. Create a plan for the free flow of information during the project

{% callout(type="note") %}
Determining the information needs of stakeholders isn't straightforward!
{% end %}

### Sources of Information

Example information stores:
- issues database
- config management system
- process assets database

## Configuration Management

The freedom to change a document is more restricted after the document is baselined.

# Selecting a Methodology

Most software development plans are adaptations from generic plans that fit within a certain software development methodology. For example, a group might choose to use *Extreme Programming* with formal inspections in place of pair programming.
