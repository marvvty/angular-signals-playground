# Angular Signals Playground

See how Angular signals actually work: a live dependency graph, step-by-step playback and the internal state of every node.

> **Status: early development.** There is no public demo yet. The first release (MVP) is planned for early 2027.

## Why

Most explanations of signals stop at `signal`, `computed` and `effect` as black boxes. This playground opens the box:
it instruments Angular's own reactive primitives (`@angular/core/primitives/signals`) and shows what happens inside
when you read, write and recompute.

## Planned features

- **Dependency graph:** signals, computeds and effects as nodes, with edges that update live (including conditional dependencies).
- **Step-by-step playback:** play, pause and step forward or back through every reactive event: read, write, mark dirty, recompute, "checked and skipped", effect run.
- **Node inspector:** value, version, dirty flag and dependencies of any node at any step.
- **Plain-English explanations** for each step, so the push/pull model makes sense from a single example.

### Built-in scenarios

- Basic chain: `signal` → `computed` → `effect`
- Diamond dependency (glitch-free evaluation)
- Conditional dependencies (edges that change)
- Same value written, no recomputation
- `untracked`
- `linkedSignal`
- Effect batching (several `set` calls, one effect run)

## Roadmap

- [ ] Instrumentation core: full event stream of the reactive system
- [ ] Live dependency graph
- [ ] Step-by-step playback with explanations
- [ ] Built-in scenarios
- [ ] **MVP:** public demo
- [ ] Code editor: write your own examples
- [ ] Advanced APIs: `resource`, `httpResource`, `input`/`model`, `toSignal`/`toObservable`, Signal Forms
- [ ] "Guess" mode: predict which nodes go dirty before each step
- [ ] Sharing and embedding: scenario state in the URL, iframe embed mode
- [ ] Signals vs RxJS side-by-side

## Development

Requirements: Node.js 24 LTS and npm.

```bash
npm install
npm start          # dev server at http://localhost:4200
```

| Command             | What it does                        |
| ------------------- | ----------------------------------- |
| `npm start`         | Run the dev server                  |
| `npm run build`     | Production build into `dist/`       |
| `npm test`          | Unit tests (Vitest)                 |
| `npm run lint`      | ESLint for TypeScript and templates |
| `npm run stylelint` | Stylelint for SCSS                  |
| `npm run format`    | Format everything with Prettier     |

A pre-commit hook (Husky + lint-staged) lints and formats staged files automatically.

### A note on internals

The playground relies on Angular's internal signal primitives, which are not a public API and can change between
minor versions. The Angular version is pinned on purpose and updated deliberately, with the instrumentation tests
run after every upgrade.

## Contributing

The project is in its early stage and the core is still taking shape. Issues with ideas and feedback are welcome now.
Contribution guidelines will follow after the MVP.

## License

[MIT](LICENSE)
