# Lookatshow — a unified marketing operating system for AI agents

![Lookatshow: shared context, task, tool, readback, next step](assets/marketing-system.svg)

Give an agent a business task: check advertising spend or compare competitors' offers. **Lookatshow** connects that task to company context, practical tools and a result you can verify. Choose your model; keep the work organised around your business.

Open modules by **Дмитрий Лукашов (Dmitry Lukashov)**. Start with one free tool and a repeatable example before working with your own data.

[Run the example](START-HERE.md) · [Architecture](ARCHITECTURE.md) · [Machine-readable catalog](CATALOG.json) · [Русский](README.ru.md)

<!-- masterclass-20261014 -->
## Free live workshop in Russian — 14 October 2026, 17:00 Moscow

Dmitry Lukashov and Mikhail Puzyrev will cover AI for marketing and business workflows in a live Zoom session with questions. [Programme and optional practice](events/2026-10-14-ai-marketing.md) · [Register by commenting “+” on the Telegram announcement](https://t.me/lookatsoul/169). This invitation applies only to the 14 October session.
<!-- /masterclass-20261014 -->

## Available tools

### Yandex Direct placement audit

[`direct-report-audit`](https://github.com/ilookatshow-gif/direct-report-audit) reads a normalised local CSV/TSV export, adds up placement metrics and calculates CPC/CPA. It lists manual-review candidates with reasons. It doesn't exclude placements, change campaigns or claim savings.

Python 3.9+, standard library only. No advertising account, credentials, network or core purchase required.

[Release v0.1.0](https://github.com/ilookatshow-gif/direct-report-audit/releases/tag/v0.1.0) · [Synthetic input](https://github.com/ilookatshow-gif/direct-report-audit/blob/v0.1.0/examples/synthetic-placements.csv) · [Copyable commands and verified output](START-HERE.md)

The example contains five invented rows and four placements. Two meet the stated review thresholds. They're test data, not a customer outcome.

### Compare competitors' prices, delivery and scope

[`competitor-offer-radar`](https://github.com/ilookatshow-gif/competitor-offer-radar) compares two authorised structured JSON offer snapshots by stable IDs. It reports declared amounts, delivery duration and component changes with the supplied source URLs and capture times. No websites are fetched; commercial judgement stays with you.

[Download verified source ZIP](https://github.com/ilookatshow-gif/competitor-offer-radar/archive/7206178f1f6c7484c6f4463c62fe48d497b398d6.zip) · [Install with Codex or Claude Code](START-HERE.md#radar-current-source) · [Synthetic input for this revision](https://github.com/ilookatshow-gif/competitor-offer-radar/tree/7206178f1f6c7484c6f4463c62fe48d497b398d6/examples)

In the fictional example, the declared sum changes by +25%, delivery by +50%, and interview quantity from two to one. `scope_changed_warning=true` means the package changed: this is not a pure price increase for equivalent work. Python 3.9+, no dependencies or paid core. The 11 October source fix handles Cyrillic output; installation and the synthetic workflow passed four CI environments covering Ubuntu, Windows and macOS. [Exact versions and test results](https://github.com/ilookatshow-gif/competitor-offer-radar/actions/runs/38153820165).

The ZIP is pinned to commit `7206178`; give it to your agent with the START-HERE prompt. This is repaired source, not a new release. Historical [v0.1.0](https://github.com/ilookatshow-gif/competitor-offer-radar/releases/tag/v0.1.0) is unchanged and does not contain the encoding fix. Use the pinned ZIP for a new installation.

The [step-by-step practice with a screenshot](https://lookatshow.ru/practice/sravnenie-offerov-konkurentov-ii/?utm_source=github&utm_medium=open_module&utm_campaign=competitor-offer-radar&utm_content=demo) (in Russian) includes runnable commands, source JSON files and a copyable agent prompt. Its archive belongs to the initial release; start a current installation with the ZIP above. The screenshot shows a separate viewer for actual local output on fictional data, not a built-in module interface.

### Check unfinished activities on Bitrix24 deals

[`bitrix-read-kit`](https://github.com/ilookatshow-gif/bitrix-read-kit) identifies visible in-progress deals with no unfinished CRM activity in a complete read. It separates scheduled, overdue, undated and incomplete activity reads. An absent activity does not prove a lost sale or absent customer agreement.

[Download v0.1.0 ZIP](https://github.com/ilookatshow-gif/bitrix-read-kit/releases/download/v0.1.0/bitrix-read-kit-0.1.0.zip) · [Copyable agent prompt](https://github.com/ilookatshow-gif/bitrix-read-kit/blob/v0.1.0/README.md) · [Synthetic input](https://github.com/ilookatshow-gif/bitrix-read-kit/blob/v0.1.0/examples/synthetic-snapshot.json)

Give the ZIP to your agent, ask it to install into a new local folder and run `doctor` and `demo`. Five fictional deals and three unfinished activities demonstrate the distinctions. Python 3.9+, no paid core or account needed for the demo. A real capture separately requires your private webhook and makes no CRM writes.

Native installation and synthetic checks passed [four CI environments](https://github.com/ilookatshow-gif/bitrix-read-kit/actions/runs/38224428848): Ubuntu, Windows and macOS, with 95 tests per suite (Windows skips one POSIX-only test). This verifies selected environments, not every real portal or agent host.

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

An email tool and further workflow integrations are on the roadmap. The first read-only Bitrix24 tool is available above; planned work is not a supplied integration.

## Use this in your company

[Learn to run and check agent workflows](https://lookatshow.ru/executive?utm_source=github&utm_medium=open_module&utm_campaign=catalog&utm_content=readme_en_learn), or [discuss implementation of one business process](https://lookatshow.ru/ai-implementation/?utm_source=github&utm_medium=open_module&utm_campaign=catalog&utm_content=readme_en_implementation). Training and development are separate services; project scope and support are agreed separately. These pages are in Russian.

Practical AI for business by Dmitry: [Telegram](https://t.me/lookatsoul). A subscription isn't a condition of using a free module.

## FAQ

**Must I buy the core?** No. The released modules work independently under MIT. Training, implementation and third-party services have separate terms.

**Does installation connect live accounts?** No. The current tools read your selected local files. Live integrations need their own access and explicit action scope.

**Can I use another agent?** A host that can run Python commands and read JSON can use the same CLI contract. Codex and Claude Code have supplied instructions; that isn't a claim that every host/version has been tested.

**Are my data local?** The CLI doesn't send data over the network. A cloud agent may see what you give it, including command output. Use synthetic input first and follow your company's data rules.

## License and useful issues

New catalog documentation: [MIT](LICENSE), © 2026 Dmitry Lukashov. Each module has its own LICENSE/NOTICE. Report defects with a version, command and small invented input that reproduces the problem. Don't publish customer reports, contacts or credentials in issues.
