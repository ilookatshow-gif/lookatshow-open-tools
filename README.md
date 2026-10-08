# Lookatshow — a unified marketing operating system for AI agents

![Lookatshow: shared context, task, tool, readback, next step](assets/marketing-system.svg)

Give an agent a business task: check advertising spend or compare competitors' offers. **Lookatshow** connects that task to company context, practical tools and a result you can verify. Choose your model; keep the work organised around your business.

Open modules by **Дмитрий Лукашов (Dmitry Lukashov)**. Start with one free tool and a repeatable example before working with your own data.

[Run the example](START-HERE.md) · [Architecture](ARCHITECTURE.md) · [Machine-readable catalog](CATALOG.json) · [Русский](README.ru.md)

## Available now: Yandex Direct placement audit

[`direct-report-audit`](https://github.com/ilookatshow-gif/direct-report-audit) reads a normalised local CSV/TSV export, adds up placement metrics and calculates CPC/CPA. It lists manual-review candidates with reasons. It doesn't exclude placements, change campaigns or claim savings.

Python 3.9+, standard library only. No advertising account, credentials, network or core purchase required.

[Release v0.1.0](https://github.com/ilookatshow-gif/direct-report-audit/releases/tag/v0.1.0) · [Synthetic input](https://github.com/ilookatshow-gif/direct-report-audit/blob/v0.1.0/examples/synthetic-placements.csv) · [Copyable commands and verified output](START-HERE.md)

The example contains five invented rows and four placements. Two meet the stated review thresholds. They're test data, not a customer outcome.

## One working method

| Step | What the agent needs or produces |
|---|---|
| Context | Business facts, sources and action boundaries |
| Task | Selected input and a completion criterion |
| Tools | A command or integration suited to that task |
| Readback | A check against source data, a receipt or the changed object |
| Next step | A decision, an owner and a condition for checking again |

Each open module does a standalone job. The core is a separate delivery that combines context, configuration and workflows. This repository provides the catalog and instructions, not a core installer. See [architecture and component boundaries](ARCHITECTURE.md).

Model independence is an architectural principle. Current open modules are Python CLI tools with companion instructions for Codex and Claude Code. Check other hosts against the example; a CLI tool, a skill and an MCP server are different components.

## Next work

`competitor-offer-radar` is ready locally, not published. It compares two authorised structured offer snapshots; it doesn't scrape websites or rank commercial winners.

CRM and email tools are on the roadmap. Download cards appear only after a checked public release.

## Use this in your company

[Learn to run and check agent workflows](https://lookatshow.ru/executive?utm_source=github&utm_medium=open_module&utm_campaign=catalog&utm_content=readme_en_learn), or [discuss implementation of one business process](https://lookatshow.ru/ai-implementation/?utm_source=github&utm_medium=open_module&utm_campaign=catalog&utm_content=readme_en_implementation). Training and development are separate services; project scope and support are agreed separately. These pages are in Russian.

Practical AI for business by Dmitry: [Telegram](https://t.me/lookatsoul). A subscription isn't a condition of using a free module.

## FAQ

**Must I buy the core?** No. The released module works independently under MIT. Training, implementation and third-party services have separate terms.

**Does installation connect live accounts?** No. The current tool reads your selected local file. Live integrations need their own access and explicit action scope.

**Can I use another agent?** A host that can run Python commands and read JSON can use the same CLI contract. Codex and Claude Code have supplied instructions; that isn't a claim that every host/version has been tested.

**Are my data local?** The CLI doesn't send data over the network. A cloud agent may see what you give it, including command output. Use synthetic input first and follow your company's data rules.

## License and useful issues

New catalog documentation: [MIT](LICENSE), © 2026 Dmitry Lukashov. Each module has its own LICENSE/NOTICE. Report defects with a version, command and small invented input that reproduces the problem. Don't publish customer reports, contacts or credentials in issues.
