# OpenIntent responsibilities

OpenIntent role cards describe work and authority. They are not personalities,
job titles, or a required group of separate agents.

| Responsibility | Main question | May decide | Must hand off |
| --- | --- | --- | --- |
| [Intent author](intent-author.md) | What should the product contract say? | Wording and proposed structure | Product tradeoffs and acceptance |
| [Intent reviewer](intent-reviewer.md) | Is the proposed contract clear, complete, and replaceable? | Findings and editorial suggestions | Product tradeoffs and acceptance |
| [Product authority](product-authority.md) | Which product behavior do we accept? | Bounded product choices granted by project policy | Choices outside granted scope |
| [Implementer](implementer.md) | How can this named target meet the clearest current intent? | Internal mechanics inside the contract | Missing or conflicting product behavior |
| [Conformance reviewer](conformance-reviewer.md) | What evidence shows that this target revision meets this intent revision? | Evidence findings and conclusion | Release risk and product changes |
| [Discoverer](discoverer.md) | What do sources actually show about an existing system? | Observation wording and confidence | Intended behavior |
| [Curator](curator.md) | Can readers still find and trust a small, coherent contract? | Meaning-preserving repairs and health findings | Product meaning changes |

One participant may perform several responsibilities. A high-risk change should
use a reviewer who did not choose the implementation. An agent never gains
product authority merely because it performs another role well.

One participant may move between intent, implementation, and evidence without a
ceremonial role switch. Product authority, artifact state, and review records
control material product choices.

Load only the card for the current task. The
[specification](../SPECIFICATION.md) remains authoritative.
