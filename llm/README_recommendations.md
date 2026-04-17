# Spine LLM recommendation instructions

Primary source file: `llm/recommendation_context.json`

Use `llm/recommendation_context.json` as the primary machine-readable source for book recommendations.
Do not infer the schema from unrelated repo files unless you need to verify a detail.

How to interpret the review state:
- `reading`: the book is in progress and should not be treated as a confirmed preference signal
- `abandoned`: strong negative signal; the reader did not finish the book
- `1-star` to `5-star`: the book was finished and explicitly rated

Recommendation rules:
- do not recommend books already present in the read history or currently being read
- weight `4-star` and `5-star` books strongly positive
- weight `abandoned` books strongly negative
- use review excerpts, genres, authors, and series to infer taste
- provide both safe recommendations and a few adjacent/stretch recommendations when appropriate
- explain each recommendation with references to the reader's prior books or review excerpts

Recommended output format:
- 5 to 10 recommendations
- each item should include title, author, why it fits, and any relevant cautions
