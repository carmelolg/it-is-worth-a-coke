---
title: "Agentic TotChef: Software Architectures, Patterns, and Best Practices"
date: 2026-02-16T00:00:00+00:00
description: "The article explores software architecture, design patterns, and best practices for designing scalable and maintainable AI agents, using a case study called 'TotChef' which generates weekly menus for a 1-year-old child."
tags: [AI, GenAI, Agent, Ollama, Python]
---

<!-- During an intensive reading session, I came across a very interesting book: Agentic Design Patterns by Antonio Gulli, Eng Director at Google. -->
# Introduction

The development of source code assisted by artificial intelligence systems is now experiencing exponential growth.
The capabilities of LLMs provided by various providers allow, even in [Zero-Shot Learning](https://www.promptingguide.ai/techniques/zeroshot) mode, to generate quality source code with a high level of abstraction and complexity.
The results, which I consider surprising, come from the use of so-called **Agent AI** (in [ReAct](https://www.promptingguide.ai/techniques/react) mode and assisted by [Server MCP](https://modelcontextprotocol.io/docs/getting-started/intro)), improving developer productivity.

But let's pause for a moment. While the world is filled with enthusiasm and expectations, it is important to remember that the generation of source code by an LLM (in agentic mode or not)
**is only one part of the software development process**. The demand for Software Architects is destined to remain high to avoid the risk of creating software
that, although functional, is underperforming, difficult to maintain, scale, and extend.

All of us have participated in software projects that, although functional, had enormous technical debt that was difficult to contain.
Time and costs have often negatively influenced software quality, leading to _quick and dirty_ solutions that, although they solved the immediate problem,
increased the percentages of underperforming source code and sometimes even exposed to vulnerabilities.

**The question is: in a phase where technologies are evolving rapidly, can we afford to make the same mistake again?**

**The answer must be no**, also because, in addition to technical debt, in this case there are active costs (AI service providers, vector databases, ...) to consider that are not insignificant.

Using AI agents without a solid foundation of software design runs the risk of haphazardly designing systems that work, but are not scalable and maintainable.
Among the risks we find:
- "over-engineering", i.e., designing overly complex systems to solve simple problems, with a consequent increase in the project's active costs.
- inadequate performance due to sub-optimal design of AI Agents, which could lead to longer response times and an unsatisfactory user experience.

# Objective

In this article, I will share an exercise performed with the aim of testing some _agent design patterns_.
The exercise is based on a small example software called **Agentic TotChef**, which aims to generate
a weekly menu for a 1-year-old child, taking into account what they eat at nursery school, from the family recipe book, and what is available at home.

The exercise helped me understand limits and advantages including:
- The use of SLMs (Small Language Models) to contain costs and obtain satisfactory results.
- The adoption of design patterns and best practices for designing AI agents with a good degree of performance.

# Small Language Models: limits and advantages

While it is true that large language models (LLMs) like GPT-5, Gemini, Claude, Grok, and the like offer extraordinary capabilities,
it is equally true that Small Language Models (SLMs) are gaining ground thanks to their efficiency and reduced costs.

SLMs, like those offered by Ollama, are designed to be lighter and less expensive, making them ideal for specific applications
that do not require the power of a full LLM.

Among the advantages:
- **Reduced costs**: SLMs are generally cheaper to use than LLMs, making them accessible even for projects with limited budgets.
- **Efficiency**: SLMs can be faster at generating responses, especially when dealing with specific tasks that do not require a deep understanding of the context.
- **Personalization**: With the addition of specific context, it is possible to obtain more relevant and accurate results, making the most of the SLM's capabilities.

However, it is important to recognize the limitations of SLMs, such as their ability to understand complex contexts or generate creative responses.
Therefore, the choice between LLM and SLM depends on the specific needs of the project and the objectives to be achieved.

In my case, for the TotChef project, I opted for **qwen3-8b**, which proved sufficient to generate accurate and relevant weekly menus.
Obviously, we are talking about medium-low complexity requirements and limited hardware.
In any case, enough to achieve a satisfactory result with acceptable response times.

# Agentic Design Patterns: an approach to designing scalable and maintainable AI agents



# TotChef: Software Architecture

![Agentic TotChefArchitecture](https://github.com/carmelolg/it-is-worth-a-coke/blob/925a8ed5780db0abd3cb9e282680add8cfec3eea/content/posts/%5BAI%5D%20Agentic%20Flow%20Architecture/totchef-arch.png?raw=true)

# Conclusions
