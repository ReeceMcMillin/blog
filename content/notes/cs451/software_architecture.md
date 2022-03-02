+++
title = "Software Architecture"
date = 2022-02-28
[extra]
mathjax = true
+++

# Software Architecture

> Architecture is what remains when you cannot take away any more things and still understand the system and explain how it works. [Kruchten, 2000]
> 
{% definition(term="Software Architecture") %}
The structure/organization of high-level components in a software system. This includes high-level components and relationships between components.
{% end %}

Software systems have both non-functional and functional requirements. Architecture determines the degree to which non-functional requirements are present.

## Architecture and Design Aren't the Same

Architecture is a *type* of design.

Difference:
- architecture impacts the system as a *whole*.
- User need tends to drive low/mid-level design decisions, while architects must consider the needs of *all* stakeholders.
  - users, acquirers, developers, testers, maintainers, support staff, etc.

## The Process of Software Architecture

1. Identify stakeholders and their needs
2. Identify and prioritize scenarios
3. Look for opportunities to apply architecture styles (patterns)
4. Document the planned architecture
5. Validate the planned architecture

## Documenting Architecture

Different stakeholders are interested in different aspects of the architecture! In most cases, no single document can adequately address the concerns of every stakeholder.

## 4 + 1 View Model of Architecture

- Logical
- Process
- Physical/Deployment
- Development
- \\( + 1 \\)
  - the combination/completeness of the other 4 views