
## Description
Continuous Integration (CI) pipelines are the backbone of our development, but "flaky" tests—tests that exhibit both false positive and false negative outcomes randomly—severely degrade developer velocity and erode trust in the CI system.
Currently, our project relies on GitHub Actions for its CI/CD processes. Manually digging through extensive GitHub Actions logs to identify, categorize, and troubleshoot these flaky failures is a massive, time-consuming burden for maintainers.
This internship aims to solve this by building an intelligent, automated toolchain that monitors our GitHub Actions workflows for flaky behavior and leverages an agentic AI workflow to handle the heavy lifting of analysis. The intern will build a system that automatically extracts failing logs, uses AI agents to reason about the failure (differentiating between infrastructure blips, race conditions, network timeouts, etc.), and surfaces actionable mitigation strategies directly to the maintainers.

## Expected Outcomes
Data Ingestion Pipeline: A mechanism to automatically fetch, filter, and parse flaky CI run data and logs directly from the GitHub Actions API.
Agentic Analysis Engine: An integration with an AI/LLM framework designed to read failure logs, categorize the root cause of the flake, and generate a plain-English analysis.
Mitigation & Reporting: A reporting layer that takes the agent's findings and seamlessly integrates them into the developer workflow (e.g., auto-generating GitHub Issues, compiling weekly flake reports, or posting PR comments with suggested fixes).
Documentation: Comprehensive documentation covering the architecture of the tool, how to deploy it, and how maintainers can tweak the agent's prompts and behaviors.

## Recommended Skills
Proficiency in Python or Go (for scripting and API interactions).
Familiarity with GitHub Actions, CI/CD concepts, and log analysis.
Interest or experience in Generative AI, LLMs, and agentic workflows (prompt engineering, AI tool calling).
Experience with the GitHub API is a strong plus.
Familiarity with Local AI is a plus

## Mentors:
Paul Holzinger @Luap99 
Tim Zhou @timcoding1988 
Mohan Boddu @mohanboddu 

---

IMPORTANT: Please do not spam this issue with comments that you like to participate, the applications are only handled through the LFX program. For specific questions you can reach us on our `#podman-dev:matrix.org` matrix channel. Note, this is a developer focused channel, please avoid spamming it with things not related to our project.

LFX mentorship URL: https://mentorship.lfx.linuxfoundation.org/project/050e89d9-aec2-47ad-9113-3ba41a639d55


