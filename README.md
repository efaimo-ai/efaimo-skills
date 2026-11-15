# efaimo skills

Seven Agent Skills for the moment an agent says something is done. Each one turns a report like "tests pass", "file updated" or "the docs are current" into something you have checked. The plugin has no hooks and no MCP server. It holds instructions only. Nothing in it sends data anywhere by itself.

## Skills

| Skill | Use it when | What it asks Claude to run or fetch |
|---|---|---|
| red-before-green | a check came back clean and you are about to trust it | your own test, lint or search command, once on input broken on purpose and again after it is restored; it fetches nothing |
| read-it-back | a tool reported a write as successful | re-reads the changed lines on disk, then runs whatever depends on them; it fetches nothing |
| denominator | a check passed and you want to know how many things it examined | adds a count line to your check's output and keeps a baseline file in your repository; the optional ratchet tool installs from github.com/efaimo-ai/denominator |
| claim-sweep | a version, number, price, date or name changed and older copies may still say the old value | text searches in your project, a look at images and captured output, and, if you want the published package checked, `npm pack <pkg>@<version>` from the npm registry |
| unreleased-guard | you are writing a README, changelog or docs page while the code is ahead of the last release | reads your repository and looks up the version users can install, for example with `npm view <pkg> version` |
| honest-chart | you are turning numbers into a chart | writes a self-contained SVG or HTML chart and measures the drawn shapes against the data; it fetches nothing |
| mcp-stateless-migration | an MCP server has to move to the 2026-07-28 stateless specification | `npx efaimo check --mcp` against the server you name, and optionally `npx @modelcontextprotocol/conformance` and `npx @modelcontextprotocol/codemod`, all from the npm registry; it reads schema files from github.com when you compare spec drafts, and connects only to the MCP server you point it at |

## Try it

- "The tests pass on this branch. Before I merge, show me the suite would fail if the parser broke."
- "We renamed the plan from Pro to Plus last week. Find everything that still says Pro."
- "Make a bar chart of these monthly signups and prove the bars match the numbers."
- "Our README documents a --watch flag. Is it in the version people get from npm?"

## Where it works

Every skill here loads in Claude Code, Cowork and chat on claude.ai. Those that run commands do their full job where Claude has a shell in your project: Claude Code, or Cowork with a connected folder. In chat they work on files you upload, inside the code execution sandbox, which needs Code execution and file creation turned on. honest-chart works the same everywhere.

## Data

The plugin stores nothing and has no server. Claude reads the files and command output you point it at, in your own session. The commands the skills suggest run on your machine or in Claude's sandbox and reach only the npm registry, github.com and any MCP server you name. None of them report to efaimo ai.

## Security and support

Report a vulnerability to security@efaimo.ai. For questions and bugs, open an issue on this repository or write to hello@efaimo.ai.

## License

Apache-2.0. Each skill also has its own repository under github.com/efaimo-ai, and this one is built from those, so a fix to a skill belongs in its own repository.
