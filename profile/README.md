# Codex Pass

**Codex, with your own API and models.**

Codex is a good place to work. The moment you point it at your own relay or API key, though,
you lose what made the official app worth having: voice, Live, image generation, the account
you already pay for. Stay on the official account alone, and the models you actually want are
out of reach.

Codex Pass connects both sides. Your ChatGPT account keeps providing the native experience.
Your relay, API key and models handle the model requests. Same Codex, same model picker, nothing
new to learn.

**[cp.dev](https://cp.dev)** · **[console.cp.dev](https://console.cp.dev)**

## Where this comes from

We use Codex all day. We think it is one of the best agent harnesses around, it keeps getting
better with every release, and it has become the tool we don't want to work without. That is
also why we run into its rough edges first: a relay that doesn't speak the protocol Codex
expects, a config that quietly stops working after an update, a thread we want to show a
colleague, a session we want to pick up on another machine.

Codex gives you good places to fix these things: `config.toml` and model providers, the
app-server protocol, hooks, Skills, `AGENTS.md`, memory directories, the model catalog. Codex
Pass is what we built on top of them, a collection of small, well-placed tricks that make Codex
more useful for us, packaged so they work for you too. It doesn't replace Codex or rebuild any
part of it. Every feature below sits on a surface Codex already provides.

## How it works

Codex sends account traffic and model traffic down two separate paths. Codex Pass only touches
the second one.

| Traffic | Route | Codex Pass |
| --- | --- | --- |
| Sign-in, voice, Live, images, cloud tasks, usage | Directly to OpenAI | Untouched |
| Model requests | The provider in `config.toml` | A local proxy on `127.0.0.1` routes, converts and records |

The proxy listens on loopback only. It routes across as many upstreams as you configure,
converts protocols where an upstream doesn't speak Responses (Chat Completions and Anthropic,
with automatic fallback), and records usage, cost and latency per request. Your models appear
in the regular Codex model picker, prices included.

## Beyond the connection

Each of these started as something we wanted for ourselves.

- **Share a conversation** — invite-only links to a thread or a branch. Guests join without an
  account; replies are generated on the sharing device.
- **Remote access** — pair a phone or browser with your computer by QR code to read threads,
  create tasks and approve commands. End-to-end encrypted; the relay sees ciphertext only and
  can be self-hosted.
- **Doctor** — checks the Codex install, `config.toml`, Skills and `AGENTS.md`, and names the
  cause of a failure instead of leaving Codex on "reconnecting".
- **Session sync** — keep Codex sessions in step across machines through a shared folder or
  iCloud.
- **Team memory** — deliver team standards and project knowledge into members' Codex
  environments, with citation counts per entry.

## For teams

An admin connects a relay or API key in the console, sets the available models, member
allowances and policies, and issues a connection code. A member pastes it once, or signs in
with Google. Models, limits and client configuration stay in sync from then on, and usage is
visible per person, per project and per model.

## Repositories

The same idea, in the open:

- [**codexdata**](https://github.com/cpdotdev/codexdata) — open datasets for the Codex client,
  served from [data.cp.dev](https://data.cp.dev): the official model catalog mirror, a ModelInfo
  JSON Schema, the feature-flag registry, the hook product registry and release compatibility
  intelligence. Contributions welcome.

---

Codex Pass is an independent product. "Codex" and "ChatGPT" are products of OpenAI, which is
not affiliated with this organization.
