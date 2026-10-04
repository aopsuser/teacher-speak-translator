# Teacher-Speak Translator

> **From teacher to human.**

Paste a vague assignment ("Discuss in more depth", "Be creative") and find out what the teacher actually expects.

Built for the **CSC Back-to-School Hackathon**.

**Live demo:** https://claude.ai/artifact/R83B4F6MtiGsUD3pegXKbQ

![Teacher-Speak Translator](thumbnail.png)

## The problem

Students lose points not because they don't know the material, but because they don't understand what the assignment asks for. Many are too shy to ask the teacher. Teachers face the same problem from the other side: they usually learn an assignment was unclear only after the work comes back.

## Features

- **Fog Meter** (student mode): vague phrases are highlighted instantly and the assignment gets a fog score from 1 to 10. Rule-based, no AI involved.
- **Translate** (student mode): Claude explains what the teacher most likely expects, what a strong answer contains, a self-check list, and a polite question to ask the teacher. It does **not** write the answer for the student.
- **Teacher mode**: a clarity score, the problem phrases, and a clearer rewrite with length, format, grading criteria and deadline.
- **English and Russian** interface and output.

### How the fog score works

With `v` = number of distinct vague phrases found:

```
fog = clamp(round(2.5 * v + (text has no numbers ? 2 : 0)), 1, 10)
```

Vague phrases come from a hand-written dictionary (one list per language) compiled into a Unicode-aware regular expression. Assignments with no concrete numbers (length, date, points) get a penalty.

## Tech stack

- HTML, CSS, vanilla JavaScript in a single file
- Claude, via the Claude Artifact `sample` capability (Translate and Teacher mode)
- No frameworks, no external APIs, no datasets, no stored user data

## Running it

The app is one file: `teacher-speak-translator.html`.

- **Hosted version (recommended):** open the demo link above. The AI features run inside Claude Artifacts and ask for permission on first use.
- **Locally:** open the HTML file in a browser. The Fog Meter and the language switch work. The AI buttons need the Claude Artifact runtime (`window.claude`), so outside Claude they show a "AI is unavailable" message instead of breaking.

## Repository contents

| File | Description |
| --- | --- |
| `teacher-speak-translator.html` | The whole app |
| `thumbnail.png` | Project thumbnail |
| `README.md` | This file |

## AI use disclosure

We used Claude to brainstorm and choose the idea, to write the first version of the code and prompts, and to draft the project text. At runtime the app uses Claude for the Translate and Teacher mode features. The Fog Meter and its scoring are plain code. The prompts instruct the model to explain assignments, never to complete them.

## Team

- Amangeldi Beibarys

## Ideas for the future

Teacher-side analytics on which phrases confuse students most, a browser extension for school portals, more languages, and rubric import so the checklist matches real grading criteria.
