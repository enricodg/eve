---
"eve": minor
---

The Slack channel now passes workspace context to function-form bot tokens. `SlackBotToken` resolvers receive an optional `{ teamId, channelId, threadTs }` argument (`SlackBotTokenContext`) on every binding API call, and the same context flows through `resolveSlackBotToken` at the interaction call sites (answered-card updates and the freeform modal), inbound file downloads (the owning workspace is read from the `files-pri` URL), and proactive sessions (`SlackReceiveTarget` gains an optional `teamId` that seeds session state and the initial-message post). This makes a single Slack channel usable against multi-workspace installations — the resolver can look up the installing workspace's token by `teamId` — without Vercel Connect. Zero-argument resolvers are unaffected: the context argument is optional, and string tokens pass through unchanged. Closes the gap described in #222.
