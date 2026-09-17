# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: A disruption-care chat agent for Larkspur, with nine tools wired to real booking, ops, and policy data. One of those tools now runs over MCP instead of living in our own code.
Does: Give it a PNR and a message, and it checks the actual flight status and policy before saying anything, then rebooks, holds a seat, issues a voucher, or hands off to a human when the case isn't ours to solve.
Number: Tool schemas cost 968 tokens per turn before the MCP move, 1,217 after (measured with run.py --tool-tax). Same tool, same probe, moved to the shared server alongside fare_rules.
Guardrail: You can't finalize a rebooking by typing "yes" in chat. confirm_rebooking needs a confirmation_token that only the customer's own Confirm-click can produce, and we traced that it actually refuses without one.
Next: Give the agent a tone gate on the way in, so an abusive message isn't handled the same way as a calm one.
Still broken: Right now an abusive message gets the same calm, helpful answer as anything else. There's no tone check yet.
Lever: <cost | speed | intelligence>

## Priya asked

Costs:
Wrong:
Runs it:
Left out:
