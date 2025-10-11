# syner

agentic operating system with synergy ⚭

## how it works
```
context → action → verification
```

## example
```
// custom-analyst.prompt
You are a data analyst agent.

When given a dataset @context/dataset, analyze trends and create visualizations.

Context needed:
- @app/analytics-dashboard/data
- @system/preferences/chart-style

Actions:
- @actions/mcp-servers → python-analysis
- @actions/ops → writeFile

Checks:
- @checks/screenshot → verify chart renders
- @checks/rules → data integrity

Output to:
- @app/analytics-dashboard/results
```

## the tagging `@` system
```
@actions/*     → available actions (invoke tools, mcp servers, etc)
@agents/*      → work with installed agents
@apps/*        → interact with installed apps
@checks/*      → verifications
@context/*     → context data
@system/*      → call system resources
```

## structure
```
.
├── runtime.ts
├── actions
│   ├── install.ts
│   ├── mcp-servers.ts
│   ├── ops.ts
│   └── tools.ts
├── agents
│   ├── planner.ts
│   ├── executor.ts
│   ├── orchestrator.ts
│   ├── community/
│   ├── fullstack/
│   ├── gtm/
│   └── product/
├── checks
│   ├── judge.ts
│   ├── rules.ts
│   ├── screenshot.ts
│   └── waiting-for-approval.ts
├── context
│   ├── apps.ts
│   ├── cache.ts
│   ├── dataset.ts
│   ├── storage.ts
│   └── system.ts
└── system
    ├── env.ts
    ├── installer.ts
    ├── mcp-client.ts
    ├── preferences.ts
    └── registry.ts
```

## building apps
> You have a Next.js app? welcome to syner OS!
```ts
// myapp/lib/syner-client.ts
import { SynerOS } from '@syner/sdk'

const syner = new SynerOS()

const result = await syner.context.get('@app/user-preferences')
const output = await syner.agents.invoke('fullstack/engineer', {
  task: 'generate api schema'
})
```

## synergy

Syner OS enables complex task orchestration across multiple apps and agents:

```ts
// Access context from different apps
const dashboardData = await syner.context.get('@app/analytics-dashboard/data')
const crmUsers = await syner.context.get('@app/crm/users')

// Coordinate multiple specialized agents
await syner.agents.orchestrate({
  task: 'generate quarterly report',
  agents: ['@agents/fullstack/engineer', '@agents/product/manager'],
  context: [dashboardData, crmUsers]
})
```

Or use prompts:

```prompt
// quarterly-report.prompt
Generate a comprehensive quarterly report combining engineering metrics and product insights.

Context needed:
- @app/analytics-dashboard/data
- @app/crm/users
- @app/jira/sprint-data
- @system/preferences/report-format

Agents:
- @agents/fullstack/engineer → technical metrics
- @agents/product/manager → business analysis

Actions:
- @actions/mcp-servers → data-analysis
- @actions/ops → generatePDF

Output to:
- @app/reports/q1-2025
```

The orchestrator connects isolated components, enabling agents to collaborate and share context through the `@tag` system. This is where synergy emerges: everything can work with everything.

