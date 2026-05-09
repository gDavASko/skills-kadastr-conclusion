# cadastral-conclusions skill

Skill for preparing Russian cadastral engineer conclusions (`Заключение кадастрового инженера`, ЗКИ) from cadastral XML files and verified source data.

The skill is intended for:

- boundary plans (`MP`, `GKUZU`): уточнение, образование, раздел, перераспределение, выдел, объединение, исправление реестровой ошибки;
- technical plans (`TP`, `GKUOKS`): buildings, houses, garages, premises, flats, constructions, creation, reconstruction, characteristic changes, coordinate уточнение;
- inspection acts (`InspectionAct`, `act_*`): demolition / termination of existence of buildings or structures.

## What the skill enforces

- XML is used for preliminary parsing and questions, not cited as a source in the final conclusion.
- Missing information is requested from the worker before the final file is created.
- The final result is always a plain `.txt` file.
- The final `.txt` contains only the cadastral engineer conclusion.
- No guesses, assumptions, or unverified data are allowed in official text.
- Public data can be used only from official/publicly accessible reliable sources and only when the user allows lookup.

## Repository layout

```text
.
├── SKILL.md
├── README.md
├── LICENSE
├── .gitignore
└── references/
    ├── document-structure.md
    ├── public-data-lookup.md
    ├── questions.md
    ├── templates.md
    └── xml-workflow.md
```

## Installation

### Codex / Agents local skills

Copy this repository folder into one of your local skills directories.

Common locations on Windows:

```text
C:\Users\<UserName>\.agents\skills\cadastral-conclusions
```

or:

```text
C:\Users\<UserName>\.codex\skills\cadastral-conclusions
```

The installed folder must contain `SKILL.md` at its root:

```text
C:\Users\<UserName>\.agents\skills\cadastral-conclusions\SKILL.md
```

Restart Codex or open a new chat after installation.

## Using With ChatGPT, Claude, And Other AI

For non-Codex tools, use [INSTALL_FOR_OTHER_AI.md](INSTALL_FOR_OTHER_AI.md). It explains how to connect this skill through ChatGPT Projects, Custom GPTs, Claude Projects, ordinary chats, and other AI systems that support instructions and knowledge files.

### From GitHub

Clone the repository:

```powershell
git clone https://github.com/<owner>/<repo>.git cadastral-conclusions
```

Then copy the cloned `cadastral-conclusions` folder to your skills directory.

## Example prompts

```text
Используй cadastral-conclusions. Разбери XML межевого плана, задай вопросы по недостающим данным и после ответов создай TXT-заключение.
```

```text
Подготовь заключение кадастрового инженера по техническому плану. Итоговый файл назови Заключение_гараж.txt.
```

```text
Разбери XML акта обследования и составь список вопросов перед созданием заключения.
```

## Official-document accuracy

This skill is designed for official cadastral documentation. The model must not invent:

- cadastral numbers;
- addresses;
- areas;
- permitted uses / ВРИ;
- territorial zones;
- right holders;
- contract details;
- engineer credentials;
- publication details;
- registry-error reasons;
- legal conclusions.

If a fact is missing or doubtful, the model must ask the user or rely on an official source explicitly allowed by the user.

## Final TXT rules

The final `.txt` must not contain:

- questions to the worker;
- parsing notes;
- phrases like `Из XML получено`, `по сведениям XML`, `указано в XML`, `в XML отражено`;
- a `Требуется уточнить` section;
- geodetic-basis point descriptions;
- raw lists of XML source documents, except PZZ information when legally relevant.

## License

MIT. See [LICENSE](LICENSE).
