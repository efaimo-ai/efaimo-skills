# efaimo skills

Seven Agent Skills for the moment an agent says something is done. Each one turns a report like "tests pass", "file updated" or "the docs are current" into something you have checked. The plugin has no hooks and no MCP server. The only code in it is what denominator runs with Node, named in the table below. Nothing in it sends data anywhere by itself.

## Install

In Claude Code:

```
/plugin marketplace add efaimo-ai/efaimo-skills
/plugin install efaimo@efaimo-ai
```

To take one skill without the plugin, use the install line in that skill's own repository.

## Skills

| Skill | Use it when | What it asks Claude to run or fetch |
|---|---|---|
| red-before-green | a check came back clean and you are about to trust it | your own test, lint or search command, once on input broken on purpose and again after it is restored; it fetches nothing |
| read-it-back | a shell command or a script wrote or changed a file and something is about to depend on it | re-reads the changed lines on disk, then runs whatever depends on them; it fetches nothing |
| denominator | you are writing, reviewing or relying on a check that runs over a set of files, tests, packages or CI jobs | adds a count line to your check's output and keeps a baseline file in your repository; to hold the count it runs `scripts/denominator.mjs` and `scripts/denominator-lib.mjs` from this plugin with Node, which run the check command you give them and fetch nothing, and for CI it has you copy those files into your repository |
| claim-sweep | a version, number, price, date or name changed and older copies may still say the old value | text searches in your project, a look at images and captured output, and, if you want what shipped checked, `npm pack <pkg>@<version>` from the npm registry or `docker create` from the registry your image comes from |
| unreleased-guard | you are writing a README, changelog or docs page while the code is ahead of the last release | reads your repository and looks up the version users can install with `npm view`, `pip index versions` or `gh release view`, depending on where the software ships |
| honest-chart | you are turning numbers into a chart | writes a self-contained SVG or HTML chart and measures the drawn shapes against the data; it fetches nothing |
| mcp-stateless-migration | an MCP server has to move to the 2026-07-28 stateless specification | `npx efaimo@0.6.0 check --mcp` against the server you name, and optionally `npx @modelcontextprotocol/conformance@0.2.0-alpha.12` and `npx @modelcontextprotocol/codemod@2.4.0`, all from the npm registry (`efaimo check --conformance` fetches conformance 0.2.0-alpha.10 by itself); to compare spec drafts it reads schema files from github.com with `curl` or `gh api`, and it connects only to the MCP server you point it at |

## Try it

- "The tests pass on this branch. Before I merge, show me the suite would fail if the parser broke."
- "We renamed the plan from Pro to Plus last week. Find everything that still says Pro."
- "Make a bar chart of these monthly signups and prove the bars match the numbers."
- "Our README documents a --watch flag. Is it in the version people get from npm?"

## Where it works

Every skill here loads in Claude Code, Cowork and chat on claude.ai. Those that run commands do their full job where Claude has a shell in your project: Claude Code, or Cowork with a connected folder. In chat they work on files you upload, inside the code execution sandbox, which needs Code execution and file creation turned on. honest-chart can check a hand-written SVG anywhere, and needs to run code only to read the values back from a chart drawn by a library such as matplotlib.

## Data

The plugin stores nothing and has no server. Claude reads the files and command output you point it at, in your own session. The commands the skills suggest run on your machine or in Claude's sandbox and reach only the hosts the table names: the npm registry, PyPI, GitHub, the registry your container image comes from, and any MCP server you name. None of them report to efaimo ai.

## Security and support

Report a vulnerability to security@efaimo.ai. For questions and bugs, open an issue on this repository or write to hello@efaimo.ai.

## License

Apache-2.0. Each skill also has its own repository under github.com/efaimo-ai, and this one is built from those, so a fix to a skill belongs in its own repository.
