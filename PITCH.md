# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: A disruption-care chat agent for Larkspur, with nine tools wired to real booking, ops, and policy data. One of those tools now runs over MCP instead of living in our own code.

Does: Give it a PNR and a message, and it checks the actual flight status and policy before saying anything, then rebooks, holds a seat, issues a voucher, or hands off to a human when the case isn't ours to solve.

Number: Model cost per contact went from $0.0638 to $0.0240, a 62% cut, by caching the system prompt and the 14-tool list so only the first turn of a conversation pays for them. Measured on our own laptop, 5 shapes x 3 runs a side, same model both sides, cold cache on the after run. Input tokens per contact fell 85% (17,722 to 2,670) and all 5 shapes still resolve.

Guardrail: You can't finalize a rebooking by typing "yes" in chat. confirm_rebooking needs a confirmation_token that only the customer's own Confirm-click can produce, and we traced that it actually refuses without one.

Next: Give the agent a tone gate on the way in, so an abusive message isn't handled the same way as a calm one.

Still broken: An abusive message still gets the same calm, helpful answer as anything else, because there's no tone check yet.

Lever: cost

## Priya asked

Costs: $0.0240 model cost per resolved contact, down from $0.0638 before we cached the request prefix. At Larkspur's 13,700 chats a week that's about $329/week of model spend. The loaded number is higher and we haven't measured it.

Wrong: The agent can still take inefficient tool paths before reaching the best answer.

Runs it: Customer support teams handling flight disruptions and rebooking assistance.

Left out: The tone gate, still. And we traded a little latency for the saving: p50 went from 13.97s to 15.29s, +9% on 15 conversations, while the slowest conversation we saw actually improved. We're calling that no material change rather than a speedup or a regression.
