# syner

agentic operating system in typescript

## how it works
```
context → action → verification → synergy (we are here)
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
- @actions/mcp-client → python-analysis
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
├── actions
│   ├── mcp-client.ts
│   ├── ops.ts
│   └── tools.ts
├── agents
│   ├── orchestrator.ts
│   ├── community/
│   ├── engineering/
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
    ├── collaboration.ts
    ├── env.ts
    ├── mcp-server.ts
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
const output = await syner.agents.invoke('engineering/fullstack', {
  task: 'generate api schema'
})
```

