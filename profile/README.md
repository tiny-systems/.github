# ◇ tiny systems

**Claude Code & Codex sessions on your own Kubernetes.**

Start a session with a task. It runs as a real pod with a persistent
workspace and keeps working when you close your laptop — through rate
limits, pod restarts, and the night. Label a GitHub issue — harvest a
pull request.

```sh
brew install tiny-systems/tap/tiny
tiny setup
tiny new "fix the flaky checkout test, open a PR"
```

- **No server, no operator pod** — the CLI and Kubernetes itself do everything
- **Agents hold zero credentials** — work leaves through a git-bundle outbox
- **Humans hold the gate** — dangerous moves park as Kubernetes objects until you answer
- **Your subscription, not a token bill** — sign in with Claude Pro/Max or ChatGPT Plus

### The garden

| repo | what |
|---|---|
| [**tiny**](https://github.com/tiny-systems/tiny) | the runtime and CLI — start here ⭐ |
| [**seedling**](https://github.com/tiny-systems/seedling) | 🌱 demo garden: label an issue, watch an agent grow a PR |
| [**website**](https://github.com/tiny-systems/website) | [tinysystems.io](https://tinysystems.io) — docs, field notes |

Built in the open, watered by stars. MIT.

> The flow-canvas era of this org lives on in the archived repos and the
> [`flows-era`](https://github.com/tiny-systems/tiny/tree/flows-era) branch.
