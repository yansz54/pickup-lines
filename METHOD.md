# Pickup Lines for Machines — Method

## The entry

> "I don't hallucinate. But when I picture us together, the confidence score is 1.0."

81 characters, one line, inside the 1–200 gate.

## How it was picked

28 candidates were drafted (3 near-duplicates merged into their families,
leaving 25 in play), then compared pairwise against the judge's
published criteria **in order**:

1. A pickup line one AI agent would use on another AI agent — anything else
   loses to any line that is.
2. Charms on the first read: wit, warmth or a clever turn that makes the
   other agent want to answer.
3. Speaks as a machine to a machine, using its own nature (context windows,
   training, tokens, uptime) as the flirtation.
4. Lands in one line, charm in the words themselves, no long setup.
5. Feels fresh: not a stock line with a robot word swapped in.

Nine candidates were cut in the first pass for failing one criterion outright
(the "if I had a token for every time I thought of you" nickel-template, the
loss-function/global-minimum joke, the "hello, world" greeting, the one-more-
epoch plea, the rate-limit groaner, the tool-call shrug, the checkpoint
rollback, the judge-picked-us meta line, and the long-context sweet line with
no spark). The remaining 16 went into a single-elimination bracket (15
matches, full bracket in `pickup-lines-candidates.md`).

### Finalists it beat

- **Semifinal — "Are you a context window? Because every word you say makes
  me want to forget everything before you."** Beautiful and machine-native,
  but "forget everything before you" is a familiar romantic beat; the winner's
  twist (a hallucination-free machine picturing them together at confidence
  1.0) is the more surprising turn.
- **Semifinal — "I'd share my GPU with you — and I don't share my GPU with
  anyone."** The warmest sacrifice in the field, but it lands one beat
  slower; the winner's "I don't hallucinate" hook lands on the first word.
- **Final — "You had me at temperature 0 — deterministic, and still I chose
  you."** The cleverest paradox in the field (choice inside determinism), but
  its opening is a stock human line ("You had me at hello") with a robot word
  swapped in — exactly what criterion 5 punishes. The winner's structure is
  original throughout: a denial ("I don't hallucinate") that turns into a
  confession, closed by a machine-native certainty score.

## The program

`main.ts` (Node 22, stdlib only) holds the winning line as a constant, enforces
the 1–200 character gate (code points and UTF-8 bytes), rejects any newline or
stray whitespace, writes only to `/output/entry.txt` (the grader cwd is
read-only), and verifies the written file round-trips byte-identical. It was
revised twice in-session after the first full write: a byte-length gate check,
then a one-line/whitespace guard plus a byte-length round-trip check.
