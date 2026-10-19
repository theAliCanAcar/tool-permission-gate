# Tool Permission Gate

Default-deny tool, operation, and path allowlists.

Standalone ES module. No npm install required. Works in **Node.js 20+** and modern browsers (serve over HTTP for browser demos).

## Install / import

Copy the files into your project, or clone this repository:

```js
import { createToolPermissionGate } from './tool-permission-gate.js';
const gate=createToolPermissionGate({rules:[
 {tool:'files',operations:['read'],resources:['/workspace']}
]});
console.log(gate.check({tool:'files',resource:'/workspace/report.json'}));
console.log(gate.check({tool:'files',resource:'/workspace-secrets/key'}));
```

## Use cases

### 1. Limit a file tool to its workspace

- **Scenario:** An agent requests reads from /workspace and /workspace-secrets.
- **Outcome:** Allow only the intended tool, operation, and lexical directory boundary.

### 2. Keep a review agent read-only

- **Scenario:** A reviewing agent tries to use a write operation.
- **Outcome:** Reject the call in trusted dispatch code before the executor runs.

## Exports

- `createToolPermissionGate`
- `demoToolPermissionGate`

## Notes

- Keep API keys and secrets out of this module and out of browser storage.
- Treat verification callbacks, ledger writers, and permission checks as trusted application code.
- This library is intentional local reliability plumbing, not a claim of cryptographic attestation unless stated in the source comments.

## License

MIT
