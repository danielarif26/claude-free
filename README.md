# claude-free

Keep working in Claude Code after your subscription hits its rate limit — for free.

When Anthropic's rate limit stops your session, `claude-free` reroutes Claude Code through [claude-code-router](https://github.com/musistudio/claude-code-router) to the **GitHub Models free tier** (gpt-4.1 / gpt-4o at $0), with a local Ollama model as an optional lane for background tasks. You lose Claude-level quality; you don't lose your afternoon.

## How it works

```
claude code  →  claude-code-router (local proxy)  →  GitHub Models free tier
                                                  →  Ollama (optional, background tasks)
```

The script grabs a fresh GitHub token via `gh auth token` at every launch and writes the router config on the fly, so there is no stored API key and nothing to rotate.

## Requirements

- [Claude Code](https://claude.com/claude-code)
- [GitHub CLI](https://cli.github.com/) — logged in (`gh auth login`)
- claude-code-router: `npm install -g @musistudio/claude-code-router`
- Optional: [Ollama](https://ollama.com/) running locally (used for background tasks if present)

## Install

```bash
curl -fsSL https://raw.githubusercontent.com/danielarif26/claude-free/main/claude-free \
  -o ~/.local/bin/claude-free && chmod +x ~/.local/bin/claude-free
```

(Or clone the repo and copy the script anywhere on your PATH.)

## Use

```bash
claude-free            # instead of `claude`
claude-free --continue # all normal claude args pass through
```

Run it when you're rate-limited, go back to plain `claude` when your window resets.

## Honest limits

- GitHub Models free tier has tight rate limits and small context windows. Fine for keeping momentum on routine work; wrong tool for hard architecture or big refactors.
- No automatic mid-session takeover — when Claude Code hits its limit, the session stops and you relaunch with `claude-free`. Subscription auth can't be hot-swapped.
- Model quality is a step down from Claude. Treat it as a spare tire.

## Author

I'm S M Arifuzzaman — I built claude-free to survive my own rate-limit walls, and [free-seo-stack](https://github.com/danielarif26/free-seo-stack) for the same reason on the SEO side (17 prompts, bring-your-own-key, $0/month). More of my projects are at [smarifuzzaman.online](https://smarifuzzaman.online).

## License

MIT
