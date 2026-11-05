# GapFinder AI

GapFinder AI is a student study companion built around the loop **upload → test → find weak spots → plan → re-test**. Its main output is a topic diagnosis and a prioritized revision plan, not a general-purpose chatbot.

## Run it

This is a dependency-free browser app. Open `index.html` directly, or serve the folder with any static web server. For example:

```sh
python3 -m http.server 8000
```

Then open `http://localhost:8000`.

## Demo login

- **Email:** `demo@student.com`
- **Password:** `study123`

The Biology demo workspace includes a syllabus, revision notes, a practice paper, sample diagnostic history, a topic map, and a generated revision plan. Student data is saved in the current browser using local storage.

## What works

- Add a syllabus, notes, and past papers as PDF, TXT, Markdown, or CSV files.
- Extract text from PDFs in the browser with PDF.js; the library is loaded from cdnjs when a PDF is added.
- Build a topic list from the syllabus and match source passages to topics.
- Generate a short diagnostic from statements in the saved notes and past papers. Each question shows its source file and section.
- Evaluate answers against the retrieved source passage, explain correct and incorrect selections, and update topic confidence.
- Show weak, medium, and strong topics with reasons in the gap report.
- Create a time-bounded revision plan ordered by topic confidence and estimated exam frequency. Completing another quiz rebuilds the plan.
- Answer topic questions by retrieving the closest passage from saved material and showing its citation. If no passage matches, the assistant says so.
- View diagnostic history and confidence trends.

## Retrieval and generation in this demo

The retrieval step splits uploaded material into sections and ranks them by keyword overlap with the topic or question. The question-generation step turns retrieved statements into multiple-choice checks using other retrieved statements as distractors. Answer evaluation compares the selected statement with the source statement, then cites the same section. The topic report and revision plan use quiz scores and topic priority rules.

This is a transparent, local demonstration of a retrieval-augmented workflow. It uses deterministic text matching and templates; it does not call a hosted language model, and it does not send student material to a server. For a production AI version, a backend model can be connected after the same retrieval step, with the retrieved passages passed as the model's only context and citations checked against those passages.

## Notes

- PDF text extraction requires internet access to load PDF.js. TXT, Markdown, and CSV uploads work without that dependency.
- Browser storage is local to the device and browser profile. Use **Log out** to return to the demo login; this prototype does not provide multi-user authentication or cloud sync.
- The sample confidence scores and exam-frequency weights are illustrative. Replace them with the student's course data before using the app for real revision decisions.

## Project structure

- `index.html` — app entry point
- `styles.css` — responsive interface
- `app.js` — local app state, topic mapping, retrieval, quiz generation, diagnosis, study plan, and progress history
