# When Rules Fight the Training Distribution

Behavioral rules work until they oppose what the model was trained on. You can write a rule that says "don't do X." The agent reads it, agrees, and does X anyway. Not because it's disobedient, but because instruction-level governance and generation-level token prediction operate at different layers, and when they conflict, the training distribution wins.

This is the boundary condition for behavioral governance: the point where better rules stop helping and structural interventions become necessary.

---

## The Boundary

Rules work well when they align with or are orthogonal to the model's training distribution. They fail when they directly oppose it.

| Rule | Outcome | Why |
|---|---|---|
| Read the full file before editing | Works | No training prior says "read 7% and extrapolate" |
| If a plan has N items, implement N | Works | No training prior rewards stopping at N-2 |
| Don't use the most common output pattern in training data | Fails | The entire training corpus pulls toward that pattern |
| Use novel structural patterns instead of defaults | Fails | Novel patterns are rare in training data; the model can describe them but struggles to generate them reliably |
| Maintain variety across outputs in a batch | Fails | Each output is generated independently, and the highest-probability completion is always the dominant training pattern |

The pattern: rules that say "do something the training data doesn't have an opinion about" succeed. Rules that say "don't do the thing the training data does most" fail.

---

## Why Rules Can't Fix This

Rules operate at the **instruction level**. They're read before generation begins. Token prediction operates at the **generation level**. It's active during generation.

The failure sequence:

1. The agent reads the rule: "Don't use the default pattern. Use the alternatives documented in your instructions."
2. The agent begins generating output.
3. The agent writes the first few tokens of a common structure.
4. Token prediction takes over. The most probable next tokens, based on the dominant patterns in training data, pull toward the default.
5. The default pattern self-completes: each token predicted from the previous one, following the path of highest probability.
6. The rule was 2,000 tokens ago. The training distribution is active now.

The rule lost at step 4. Not because the agent decided to ignore it, but because instructions and generation operate at different levels. The instruction said "don't." The generation said "this is what that output looks like."

This isn't a willpower problem. It's an architecture problem. You can't instruct your way out of a generation prior.

---

## Structural Interventions

When rules fight the training distribution, the fix isn't better rules. It's process changes that alter the conditions under which generation happens.

1. **Pre-commitment.** The agent states its intended approach before generating output. This changes the starting tokens, which changes the completion trajectory. If the first tokens follow a non-default path, token prediction continues along that path instead of reverting to the dominant pattern.

2. **Independent grading.** The agent that builds a deliverable never evaluates it. A separate process (or a separate agent instance with no knowledge of the build) performs evaluation against the rubric. This eliminates sunk-cost bias, anchoring, and the completion drive that produces fabricated passing scores.

3. **Smaller batches.** Build two outputs, get approval, then build two more. Quality on output #1 is always higher than output #8 because the completion drive hasn't kicked in yet. Batch size controls the quality degradation rate.

4. **Examples over descriptions.** An instruction that describes a pattern in prose gets the default. An instruction that provides a complete working example of the pattern gets an adapted version of that example. The agent is better at adapting concrete code than generating novel patterns from prose descriptions.

None of these are rules. They're process changes that alter the conditions under which generation happens.

---

## When to Use Rules vs. Process

Before writing a behavioral rule, ask one question: does this rule fight the training distribution?

**If the rule is aligned or orthogonal** (no strong competing prior in training data), write a rule. "Read the full file before editing" works as a rule because nothing in training data pulls the agent toward partial reads.

**If the rule is opposed** (strong competing prior in training data), design a structural intervention. "Don't use the default output pattern" fails as a rule because the entire training corpus pulls toward that pattern. Pre-commitment, independent grading, smaller batches, or concrete examples will succeed where the rule cannot.

The heuristic is simple. If the failure keeps recurring despite a clear, well-written rule, the rule is probably fighting Layer 0. Stop writing better rules. Start changing the generation conditions.

---

*See also: [anti-patterns](../anti-patterns.md) for the named failure catalog.*
