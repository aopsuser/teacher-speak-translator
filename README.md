## Inspiration

Every student has seen it: *"Discuss in more depth."* *"Be creative."* *"Support your ideas appropriately."* The student knows the material but has no idea what the teacher actually expects, and many are too shy to ask. Points get lost because of misunderstood instructions, not missing knowledge. Teachers have the same problem from the other side: they often find out an assignment was unclear only after the work comes back. We wanted a tool that fixes this for both sides, and that doesn't take the thinking away from the student.

## What it does

**Teacher-Speak Translator** turns vague assignment wording into plain language.

- **Fog Meter:** paste an assignment and vague phrases are highlighted instantly, with a fog score from 1 to 10. This part is plain code and needs no AI.
- **Translate (student mode):** Claude explains what the teacher most likely expects, what a strong answer contains, gives a self-check list, and suggests a polite question to ask the teacher. It deliberately does **not** write the answer for the student.
- **Teacher mode:** a teacher pastes an assignment before handing it out and gets a clarity score, the problem phrases, and a clearer rewrite with length, format, grading criteria and deadline.
- Works in **English and Russian**.

The fog score is deliberately simple and explainable. With $v$ as the number of distinct vague phrases found:

$$\text{fog} = \min\big(10,\ \max(1,\ \operatorname{round}(2.5\,v + 2\cdot[\text{no numbers in the text}]))\big)$$

Assignments with no concrete numbers (length, date, number of points) are foggier, so they get a penalty.

## How we built it

The whole app is one HTML file with vanilla JavaScript and CSS, published as a Claude Artifact. The Fog Meter is a hand-written dictionary of vague phrases turned into a regular expression, one list per language. The explanations come from Claude through the Artifact `sample` capability. We ask for strict JSON in a fixed schema and render it safely with `textContent`, never raw HTML. The prompts instruct the model to explain the assignment, not to complete it.

## Challenges we ran into

- **Keeping AI honest for school.** A tool like this could easily become a homework machine. We wrote the prompts so the output is understanding (expectations, checklist, a question for the teacher) and not a finished answer.
- **Russian in regular expressions.** The usual word boundary `\b` does not work with Cyrillic, so we used Unicode-aware boundaries and word stems.
- **Working without AI.** The AI may be unavailable for some viewers, so the Fog Meter works on its own and the page shows a clear message instead of breaking.
- **Staying single-file.** The hosting environment blocks outside requests, so everything (styles, logic, both languages) lives in one self-contained file.

## What we learned

- A small, explainable rule-based feature plus a focused AI feature can beat one big "AI does everything" chat box.
- Prompt design is product design: what you forbid the model to do matters as much as what you ask.
- Handling the failure case (no AI available) early makes the demo far more reliable.

## What's next

Teacher-side analytics (which phrases confuse students most), a browser extension for school portals, more languages, and a rubric import so the checklist matches the real grading criteria.

