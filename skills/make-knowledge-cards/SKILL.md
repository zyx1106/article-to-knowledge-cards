---
name: make-knowledge-cards
description: Convert pasted articles or local Markdown/TXT files into 5-8 source-grounded knowledge cards. Use when the user asks to summarize learning material, extract key knowledge points, make study cards, or turn article/text/Markdown content into concise cards with title, core knowledge, brief explanation, and an example or self-test question. Does not support web scraping, PDF processing, Anki export, or graphical interfaces.
---

# Make Knowledge Cards

## Purpose

Turn user-provided article text or a local `.md`, `.markdown`, or `.txt` file into focused knowledge cards for learning and review.

Each card must contain exactly one important knowledge point and four fields:

1. `Title`
2. `Core Knowledge`
3. `Brief Explanation`
4. `Example or Self-Test`

## Inputs

Accept:

- Article text pasted directly in the conversation.
- A local Markdown or plain text file path supplied by the user.

Decline or ask the user to provide supported input for:

- Web pages or URLs that require fetching.
- PDF files.
- Anki decks, Anki import files, or flashcard app exports.
- Requests to build a graphical interface.

## Workflow

1. Read the source completely before writing cards. If the user provides a local file, inspect it directly.
2. Identify candidate knowledge points that are central to the source, not merely interesting details.
3. Merge duplicates and near-duplicates. Keep the clearest source wording as evidence for the merged idea.
4. Remove unsupported inferences. Do not add facts, examples, definitions, causes, or recommendations that are absent from the source.
5. Select 5-8 cards only when the source supports that many distinct important points. If fewer than 5 are supported, output fewer cards and state briefly that the source does not contain enough distinct material to reach 5.
6. Make every card standalone, concise, and useful for review.

## Card Quality Rules

- Cover one knowledge point per card.
- Prefer concepts, mechanisms, contrasts, conditions, tradeoffs, steps, or implications that the source clearly emphasizes.
- Do not preserve the article order if a clearer learning order exists.
- Delete repeated introductions, transitions, anecdotes, rhetorical flourishes, and redundant examples.
- Treat examples as support for a card, not as separate cards, unless an example teaches a distinct knowledge point by itself.
- Keep explanations short: usually 1-3 sentences.
- Use the source's own examples when available. If there is no example, write a self-test question instead of inventing a new example.
- If the source is ambiguous, phrase the card cautiously and avoid filling gaps.
- If the source is mostly opinion, label claims as the source author's view rather than as universal facts.
- Do not cite line numbers unless the user asks.

## Output Format

Use Markdown. Start with a one-sentence note only when fewer than 5 cards are produced or when there is an input limitation. Then output numbered cards:

```markdown
1. **Title:** ...
   **Core Knowledge:** ...
   **Brief Explanation:** ...
   **Example or Self-Test:** ...
```

Keep the final answer focused on the cards. Do not add a long meta-summary after the cards.

## Handling Weak Sources

If the input is too short, too repetitive, or lacks enough concrete knowledge:

- Output only the supported cards.
- Add a brief note such as: "The source only supports 3 distinct knowledge cards without inventing extra material."
- Do not pad with generic background knowledge.

If the input appears to be a task description rather than article content, ask for the article text or a supported file path.
