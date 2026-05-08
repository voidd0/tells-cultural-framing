# tells-cultural-framing

> Per-language cultural framing files for [tells](https://tells.voiddo.com) — text-first analysis for what people leave unsaid.

This repo holds the 12 per-language framing JSON files that adjust how tells
analyses are produced for users in different cultural contexts. They are
copied here verbatim from the production backend so native speakers and
researchers can review, critique, and contribute corrections.

## Why this exists separately

These files matter more than most people realise. A "manipulation marker"
flagged with American directness in Russian translation lands as a slur. A
family-hierarchy reading appropriate to Sweden lands as parricide in Saudi
Arabia. tells gets these files right because the diaspora users — and the
in-country users — actually correct them when they're wrong.

We split the privacy surface from the business surface. The full prompt
template repo is at [voidd0/tells-prompt-templates](https://github.com/voidd0/tells-prompt-templates).
The cultural-framing files live there too; this repo isolates them to
lower the contribution barrier — you don't need to read 700 lines of
prompt logic to suggest a change to `ru.json`.

## What's in each file

```json
{
  "register_default": "direct-personal | polite-formal | direct-informal",
  "manipulation_terminology_caution": true | false,
  "directness_level": 0.0 - 1.0,
  "family_hierarchy_sensitivity": "moderate | high | very-high",
  "preferred_metaphors": ["literary", "philosophical", ...],
  "avoid_metaphors": ["military-aggressive", ...],
  "informal_pronoun": "ты | du | tu | etc",
  "subtext_reading_native": true | false,
  "rtl": true | false,
  ...
}
```

Each file is consumed at request time by the prompt-construction layer; the
selected language's JSON is appended to the system prompt before the tells
analysis run. There is no inheritance — each file is self-contained.

## Languages — Day 1 launch

12 languages, with three RTL exceptions (AR / HE not in scope for other
voiddo products).

| Code | Language | Personality |
|------|----------|-------------|
| `en` | English | Direct, neutral baseline |
| `de` | German | Direct, formal register sensitivity |
| `fr` | French | Polite, literary metaphors preferred |
| `es` | Spanish | Warm, family-hierarchy moderate |
| `pt_br` | Portuguese (Brazil) | Warm, informal pronouns default |
| `ja` | Japanese | Polite, very-high family hierarchy, indirect |
| `ko` | Korean | Polite, very-high hierarchy, age-aware |
| `it` | Italian | Direct-personal, gestural metaphors |
| `tr` | Turkish | Polite-formal, religious-neutral framing |
| `ru` | Russian | Direct, ты default, subtext-reading native |
| `ar` | Arabic | Polite-formal, MSA, manipulation caution on, RTL |
| `he` | Hebrew | Direct-informal, Israeli register, RTL |

## Contributing

PRs from native speakers are especially welcome. Suggested workflow:

1. Read the file for your language.
2. Identify a framing decision that doesn't match how the language is
   actually used in the contexts tells handles (relational, conflict,
   workplace, public-figure analysis).
3. Open an issue with: language code, current value, proposed value,
   one-paragraph rationale with at least one concrete example of where
   the current value misfires.
4. PR with the change. We merge if at least one other native speaker
   confirms, or — for low-traffic languages — if the rationale is
   compelling enough on its own.

We do not accept PRs that:

- Push the framing toward a specific political stance,
- Push the framing toward a specific religious or sectarian stance,
- Add a new language without first confirming demand via issue,
- Refactor the JSON structure (open an issue first; structure is
  cross-cutting).

## Native QA budget

Post-launch, vøiddo budgets ~$120-200 per language for a paid review by a
native-speaker translator-with-context (not a generic translator). If you
are a native speaker working in linguistics, translation, or cultural
research and would like to be considered for a paid review pass on your
language, email [hi@voiddo.com](mailto:hi@voiddo.com).

## License

MIT — see [LICENSE](LICENSE).

---

Built by [vøiddo](https://voiddo.com/) — a small studio shipping AI-flavoured products, free dev tools, Chrome extensions and weird browser games.
