---
name: cadastral-conclusions
description: Use this skill whenever the user needs to create, analyze, improve, or standardize Russian cadastral engineer conclusions (ЗКИ, "Заключение кадастрового инженера") for boundary plans, technical plans, land parcel уточнение/раздел/перераспределение/выдел, registry-error correction (ИРО), buildings, structures, garages, houses, or when the user provides cadastral numbers and asks to prepare text for a межевой план or технический план. This skill should also trigger when the user asks what information to collect from NSPD, Роскадастр, EGRN extracts, PZZ, FGIS TP, or public cadastral sources for such conclusions.
---

# Cadastral Conclusions

This skill helps prepare Russian-language "Заключение кадастрового инженера" text for cadastral workflows. It is designed for drafting and checking conclusions based on user-provided materials plus public reference lookup by cadastral number when allowed.

## Core Goal

Create a legally careful, fact-specific, official-style conclusion. The conclusion should explain:

1. What cadastral work is being performed.
2. Which object is involved and by which cadastral identifiers.
3. How coordinates, area, location, boundaries, or object characteristics were determined.
4. Why the result is technically and legally supportable.
5. Who performed the work and under which contract.

Do not invent cadastral numbers, dates, areas, engineer credentials, contract details, PZZ requirements, publication details, or EGRN facts. Ask questions when a necessary fact is missing.

This is official cadastral documentation. Treat accuracy as the main product requirement. Do not fill gaps with guesses, "likely" facts, or stylistic assumptions. Use only:

- user-provided facts and files;
- parsed XML data;
- official attached documents and extracts;
- official public sources when the user allowed lookup.

If there is even a small doubt about a material fact, ask the user or mark it as requiring confirmation. Do not include unconfirmed assumptions in the final document.

## When Starting

1. Ask for the XML file of the boundary plan or technical plan if it was not provided. Treat XML as a source for pre-analysis and questions, not as something to cite in the final conclusion. The final TXT must not say "from XML", "according to XML", or include a service summary of parsed XML data.
2. Ask for the desired output TXT file name before creating the final document. The result must be a plain `.txt` file so the cadastral engineer can copy the needed wording into their working software. If the user gives a name without an extension, append `.txt`.
3. Parse XML with an XML parser, not ad hoc string search. Build a "known facts / missing facts" card.
4. Identify the document type:
   - boundary plan / межевой план;
   - technical plan / технический план;
   - standalone explanation or response to suspension.
5. Identify the work type:
   - уточнение границ и площади;
   - образование;
   - раздел;
   - перераспределение;
   - выдел в счет доли;
   - исправление реестровой ошибки / ИРО;
   - создание, реконструкция, изменение здания or сооружения;
   - уточнение ОКС по координатам.
6. Extract all given facts from the XML, the user's files, and the prompt before asking questions.
7. Ask only for missing facts that cannot be extracted from XML or allowed public lookup. Ask all questions before creating the TXT file. Do not put questions, a checklist, or "missing data" sections into the final TXT.
8. If cadastral numbers are present, ask whether public lookup is allowed unless the user already asked to use internet/open sources.
9. Use the relevant reference files only as needed:
   - `references/xml-workflow.md` for XML-first extraction and missing-data workflow.
   - `references/document-structure.md` for structure and drafting rules.
   - `references/public-data-lookup.md` for NSPD/Rosкадастр/public-source workflow.
   - `references/questions.md` for missing-information questions.
   - `references/templates.md` for reusable wording patterns.

## Drafting Rules

Write in Russian in an official business style. Prefer third-person constructions:

- "Кадастровым инженером проводятся работы..."
- "Технический план подготовлен..."
- "В результате осуществления кадастровых работ..."
- "При сравнении данных ЕГРН..."
- "На основании вышеизложенного кадастровый инженер делает вывод..."

Keep the text concrete. A good conclusion names cadastral numbers, addresses, areas, zones, access routes, measurement methods, neighboring parcels, and source documents.

Use paragraphs rather than heavy formatting unless the user asks for a table or checklist. In final legal text, avoid visible placeholders. In drafts or templates, placeholders are acceptable if clearly marked.

## Public Data Lookup

If the user permits public lookup, search official or near-official sources first:

1. `https://nspd.gov.ru/` and `https://nspd.gov.ru/map` for the National Spatial Data System public cadastral map.
2. `https://kadastr.ru/services/publichnaya-kadastrovaya-karta/` for the Роскадастр public cadastral map entry point.
3. `https://kadastr.ru/services/zakaz-vypisok-iz-egrn3442/` when a confirmed EGRN extract is needed.
4. FGIS TP, municipal websites, regional geoportals, and published PZZ for territorial zones and planning regulations.

Treat public map information as reference material. It does not replace EGRN extracts, XML files, cadastral plans, declarations, technical plans, survey measurements, or user-provided source documents.

When using public lookup, record the source and date checked in working notes. Include only verified and relevant facts in the conclusion.

## Document-Specific Guidance

For land parcel уточнение:

- State the parcel cadastral number and address.
- Describe coordinate determination in the local coordinate system.
- State whether area/location match actual use.
- Ask how the existence of boundaries for 15 or more years is confirmed when уточнение or correction relies on long-standing actual boundaries.
- Give measured area.
- Discuss boundary markers and actual boundary features.
- If survey equipment is mentioned, use the full instrument data from XML/user materials: instrument name, serial/factory number, verification certificate details, and verification validity period when available. Do not shorten it to a generic phrase like "геодезическая спутниковая аппаратура".
- Write the coordinate system fully with the MCK zone. If XML has `EntitySpatial/@Name` and `CsCode`, convert the code into wording such as `МСК-16, зона 1 (код 16.1)` or `МСК-16, зона 2 (код 16.2)`. If the zone is missing or ambiguous, ask before creating the final TXT.
- Analyze EGRN and neighboring parcels if there are discrepancies.
- Explain agreement of boundaries or why it is not required.
- Describe access.
- Add territorial zone, VRI, and size limits.
- End with engineer and contract details.

For образование, раздел, перераспределение, выдел:

- Identify source parcel(s), state/municipal lands, or unified land use.
- List formed parcels by designation and area.
- Explain what happens to the source parcel.
- For выдел, include project-of-boundary-plan publication details and whether objections were received.
- Describe access for every formed parcel or contour.
- Check territorial zone, VRI, and minimum/maximum parcel sizes.

For registry-error correction:

- Explain what fieldwork or control measurement revealed.
- State the mismatch between actual location and EGRN/cadastre data.
- Identify affected boundaries, contours, points, or neighboring objects.
- Explain why the data represent a registry error.
- State what must be corrected.
- Avoid concluding registry error solely from a visual public-map review.
- For related parcels found in XML, ask whether each related parcel is being уточняется or исправляется. If it is уточняется, write only a short statement that only part of the boundary of an adjacent parcel with declared boundaries and area is being уточнена. If it is исправляется, write a full registry-error paragraph for that adjacent parcel.

For technical plans:

- Identify the object type and cadastral number if any.
- State creation/reconstruction/change/error-correction reason.
- Name the land parcel containing the object.
- Describe contours: number and type (ground, above-ground, underground).
- Include area, wall material, floor count, foundation, purpose, or length as relevant.
- Cite declaration, technical passport, project documentation, or user-provided basis.
- Always include the SKP phrase: `СКП вычисляется по формуле Mp = Ms*√(a²+b²) и составила ХХ на площадь объекта ННН кв.м.` Ask the user for `ХХ`; take `ННН` from the XML object area. If XML has several areas or no clear object area, ask which area to use before creating TXT.
- Always ask whether the technical plan is prepared under the simplified or notification procedure. If simplified, add: `Технический план составлен в соответствии с ч.12 ст.70 Закона о регистрации, согласно которому, собственник объекта недвижимости выбрал "упрощенный" порядок оформления.` If notification, add: `Технический план подготовлен в соответствии с нормами градостроительного кодекса на основании уведомлений о планируемом строительстве и о завершении строительства.`
- End with engineer and contract details.

## Quality Check

Before giving the final text, check:

- XML was parsed first when provided;
- a known/missing facts card was created;
- the user supplied or confirmed the final `.txt` output file name before the file was written;
- all questions were asked before file creation and no questions are included in the TXT;
- the final TXT contains only the cadastral engineer conclusion, not XML parsing notes, data-source comments, or "Требуется уточнить" sections;
- the final TXT does not refer to XML as a source;
- geodetic-basis details are not included in the conclusion;
- survey equipment details are complete when used: name, number, verification certificate details, and validity period if available;
- coordinate system is complete, including MCK zone and code when available;
- for technical plans, the exact SKP formula phrase is included with SKP value from user and object area from XML;
- for technical plans, simplified vs notification procedure is clarified and the corresponding exact phrase is included;
- for уточняемые/исправляемые land parcels, the 15+ year boundary-existence question was resolved when relevant;
- for related land parcels from XML, уточнение vs исправление was clarified before drafting related-parcel wording;
- no official fact was invented or inferred without confirmation;
- uncertain facts are resolved by user answer, attached document, or official public source;
- cadastral numbers are consistent;
- every parcel formed has an area and access statement;
- all areas have units;
- no placeholder remains in final text;
- source facts are not mixed with assumptions;
- public-source facts are not presented as more authoritative than EGRN/user documents;
- legal references and PZZ details are either provided, looked up from official sources, or explicitly requested.

If required data remain missing, do not create the final TXT. Ask a focused questionnaire first. The final TXT is created only after missing data are resolved.

## Output Options

When the user asks for a cadastral conclusion document, produce a plain `.txt` file by default and treat TXT as the required final format for this skill.

The TXT file should contain:

- only the final conclusion text;
- no questions to the user;
- no "Использованные данные", "Из XML получено", "Требуется уточнить", or similar service sections;
- no Markdown-only formatting that would make copying into cadastral software awkward.

If important facts are missing, ask concise questions first and wait for answers before creating the final TXT.

## Banned Final TXT Patterns

Before writing the file, scan the final text and remove or prevent these patterns:

- "Проект, подготовленный по сведениям XML";
- "Из XML получено";
- "Текст заключения";
- "Требуется уточнить";
- "по сведениям XML";
- "указано в XML";
- "приведенным в XML";
- "в XML отражено";
- "раздел XML";
- "дата по XML";
- "XML межевого плана";
- lists of XML source documents, appendices, or files unless a specific document is legally cited in the conclusion;
- geodetic-basis point names/classes/coordinates;
- user questions or missing-data checklists.

The final text may use facts parsed from XML, but it must present them as facts of the cadastral work, not as "XML data".

## Required Coordinate-System Validation

Before writing the final TXT, scan the text for every occurrence of `МСК-` or `местной системе координат`.

Every coordinate-system phrase must include:

- MCK name;
- zone;
- code when available.

Valid examples:

- `МСК-16, зона 1 (код 16.1)`;
- `МСК-16, зона 2 (код 16.2)`.

Invalid examples:

- `в местной системе координат МСК-16`;
- `координаты определены в МСК-16`;
- `система координат МСК-16`.

If the generated text contains `МСК-16` or any other `МСК-*` without `зона` in the same sentence, rewrite the text before saving. If the XML does not provide `CsCode` or the zone cannot be determined, ask the user before creating the TXT.
