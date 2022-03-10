+++
title = "Risk Management"
date = 2022-03-07
[extra]
mathjax=true
+++

# Analyzing Risks

- **Risks** are potential problems that have not (or may not) arrive
- **Problems** are issues that have materialized and may compromise the project

{% definition(term="Project Management") %}
The process of minimizing typical project risks.
{% end %}

1. Identify Risks
	- Risks can be project, product, or business risks
2. Analyze Risks

## Styles of Analysis

### Quantitative
$$\text{risk exposure} = \mathcal{P}(\text{risk}) \cdot \text{expected loss}$$

|        Risk         | Probability |  Loss   | Risk Exposure |
| :-----------------: | :---------: | :-----: | :-----------: |
|   devs unfamiliar   |     80%     | 5 weeks |    4 weeks    |
| design not scalable |     10%     | $40,000 |    $4,000     |

### Qualitative

Assign a heuristic risk level (categorical)

Which is better, qualitative or quantitative?

- People may relate better to qualitative
- Quantitative may give a false sense of precision
- Qualitative will have a common unit of measure

## Estimation Techniques

1. Expert Opinion
2. Cost Modeling
3. Simulation

# Prioritize Risks

# Other Considerations

1. Catastrophic Events
2. Compound Risks
3. Confidence in Estimates
4. Risk Response
	- Action Plans
	  - Avoidance
	  - Risk Transfer
    	  - transfer responsibility to someone else (think insurance industry)
	  - Mitigation
	  - Buying Information
    	  - spend time gathering more information
	- Contingency Plans
       - Risk Acceptance
5. Monitor and Evaluate Changing Risks
6. Risk Response Plan

$$
\text{Risk Reduction} = \frac{\text{Risk Estimate Before} - \text{Risk Estimate After}}{\text{Reduction Cost}}
$$