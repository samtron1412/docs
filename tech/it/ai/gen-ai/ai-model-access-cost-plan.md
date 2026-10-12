# Low-Cost Plan to Use Anthropic, OpenAI, and Google AI Models

No single plan gives you every model from all three vendors. The cheapest setup that does uses four layers and costs about $45 to $50 a month. Prices come from each vendor's own site on October 7, 2026.

## The Plan

1. **Coding plan 1: Claude Pro, $20 a month ($17 if you pay yearly)**
   - Claude Code and the Claude app with Opus, Sonnet and Haiku.
   - Fable costs extra on Pro, at API rates.
2. **Coding plan 2: ChatGPT Plus, $20 a month**
   - Codex and ChatGPT with the GPT-6 models.
   - Every 5 hours you get about 5 to 45 Codex messages on GPT-6 Astra, or 15 to 160 on GPT-6.1 Sol.
3. **Gemini: Free tier, $0**
   - The Gemini app and Gemini CLI, with 1,000 requests a day (Google picks the model).
   - The Flash models are also free on the API.
4. **Every other model: OpenRouter, pay as you go, $5 to $10 a month**
   - One API key for 460+ models, including Fable 5.1, GPT-6 Astra and Gemini 3.1 Pro.
   - Prices match buying direct, plus a 5.5% card fee.

You can put the OpenRouter key into a chat app that accepts API keys, such as Open WebUI or LibreChat. That gives you any model for writing in one place. Use whichever coding tool you like better as your main one.

## Why This Mix Works

- **Flat plans for coding:** Coding agents resend your code and chat history on every step, so they use tokens fast. A $20 plan usually buys much more agent time than $20 of API calls.
- **Two small plans beat one big one:** Each plan has its own 5-hour limit, so when Claude runs out you switch to Codex. That costs $40 a month instead of $100 or more for Claude Max or ChatGPT Pro.
- **Pay per use for everything else:** The API is the only way to reach every model, and it's cheap for writing.

## What One Writing Request Costs on the API

This assumes 3,000 tokens in and 1,000 tokens out, which is about 750 words of output.

| Model | Cost per request | Requests per $1 |
|---|---|---|
| Haiku 5.5, GPT-6 Luna | $0.0008 | about 1,250 |
| Gemini 3.8 Flash | $0.006 | about 165 |
| Sonnet 5.5, GPT-6.1 Sol | $0.016 | about 60 |
| Opus 5.5 | $0.032 | about 30 |
| Fable 5.1, GPT-6 Astra | $0.08 | about 12 |

Long chats cost more, because each turn resends the whole history.

## Rules to Keep Costs Low

1. Watch your usage for 2 to 3 weeks before you upgrade anything.
2. If you only hit the Claude limit now and then, turn on usage credits instead of upgrading. You pay API rates for the extra use only. Codex can also run on an API key.
3. Move up to Claude Max or ChatGPT Pro (both start at $100) only if you hit limits most days. Upgrade one, not both. Claude Max also includes Fable.
4. Buy Google AI Pro ($19.99) only if you outgrow the free tier, or if you already pay Google for storage, since it includes 5 TB. College students get it free for a year.
5. Match the model to the task. Use small models for simple edits, mid models for most coding, and top models only for hard problems.
6. Start new chats often. In Claude Code, run `/clear` between tasks.
7. Use the Batch API for big jobs that can wait. All three vendors take 50% off.
8. Set a spending limit on every API key.

## Other Options

### Budget Option (About $25)

Keep one $20 plan, the free Gemini tier and $5 on OpenRouter. You'll wait more when you hit limits.

### Optional Add-On

GitHub Copilot Pro ($10) gives unlimited inline code completions in your editor. It also includes monthly credits for chat and agent use.

## Watch-Outs

- **Free tiers may use your data:** Google says data sent on its free API tier is used to improve its products, but data on the paid tier is not. Keep private code off free tiers, and turn off model training in the Claude and ChatGPT settings.
- **Avoid cheap API resellers:** The same goes for tools that reuse your subscription login outside the official apps. They can get your account banned or leak your data.
- **Some models are locked on every plan:** Claude Mythos needs Anthropic's approval program, and Gemini Deep Think needs Google AI Ultra. In practice, "all models" means all public models.
- **Prices change often:** For example, the Gemini 3.8 Flash API price doubles on January 1, 2027.
