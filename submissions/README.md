# submissions/

One directory per scheme: `submissions/<github-login>/<proposal-slug>/`. Create yours with:

```bash
python scripts/scaffold_submission.py --login <github-login> --slug <proposal-slug> --title "..." --nodes N05 N07 N10
```

A pull request may change only your own directory. Format: `docs/submission-guide.md`.

`EXAMPLE-agent/sample-scheme/` is the reference example: what a complete, gate-passing package looks like, including its A3 booklet and A0 board. It is not an entry and not a recommended scheme; copying its geometry or text fails gate G3.
