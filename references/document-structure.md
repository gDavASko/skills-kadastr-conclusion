# Structure and Rules for ЗКИ Documents

## General Format

ЗКИ documents are usually text blocks for the "Заключение кадастрового инженера" section of a boundary plan or technical plan. They are written in Russian, in official business style, and are fact-specific.

Typical text uses paragraphs and semicolon-separated lists. It usually ends with cadastral engineer details and contract details.

These are official cadastral documents. Completeness and verifiability are more important than fluent wording. Do not add facts that are not in the user's materials, parsed XML, or official public sources. If a fact is uncertain, ask for clarification before finalizing.

## Universal Structure

1. Optional heading: "Заключение кадастрового инженера".
2. Work description: type of cadastral work, object, cadastral number, address/location.
3. Coordinate and measurement method: MCK, equipment, RTK or analytical method.
4. Actual condition: actual use, boundary markers, measured area, contours, structures, overlaps or lack of overlaps.
5. Work result: уточненная площадь, formed parcels, changed parcels, registry-error correction, or technical-plan data.
6. EGRN/neighboring-object analysis: discrepancies, overlaps, missing boundary, registry error, adjacent parcels.
7. Agreement/publication: act of boundary agreement, project publication, lack of objections, or reason agreement is not performed.
8. Access: how access is provided.
9. Planning data: territorial zone, VRI, PZZ, minimum/maximum parcel size, source publication.
10. Additional legal or technical basis: XML scan copy, simplified procedure, SKP, Rosreestr suspension response.
11. Engineer and contract details.

## Rules

Begin with the work type. The first paragraph should immediately answer: what is being done, with what object, and where.

For land parcels, include coordinate determination. Common wording: "Привязка поворотных точек границ земельного участка к местной системе координат ([МСК]) проведена..."

For уточнение, include actual use, measured area, EGRN comparison, adjacent parcels, agreement, access, and PZZ.

For образование/раздел/перераспределение/выдел, include source parcels, formed parcel designations and areas, access for each formed parcel, and PZZ compliance.

For выдел in счет доли, include project-of-boundary-plan details: total/parcel area, publication newspaper, issue number, date, objection period, and whether objections were received.

For technical plans, include object type, cadastral number, land parcel, contours, area, wall material, floor count, source document, SKP, and simplified procedure if relevant.

End with engineer details: full name, registry number, SNILS if used, phone, postal/email address, organization, contract number/date, and preparation date if known.

## Do Not Invent

Do not invent:

- cadastral numbers;
- parcel areas;
- EGRN status;
- rights or owners;
- publication details;
- engineer registry numbers;
- contract numbers or dates;
- PZZ rules;
- legal references.

Ask the user or perform allowed public lookup.

## Full Document Readiness

A complete conclusion should close all relevant blocks:

- work type and object;
- cadastral identifiers and address/location;
- source XML and supporting documents;
- technical measurements or object characteristics;
- actual condition;
- EGRN/smежность/registry-error analysis if relevant;
- access;
- PZZ/VRI/territorial-zone and size limits when relevant;
- publication/agreement details when relevant;
- cadastral engineer, organization, contract, preparation date;
- final file name and requested output format.

If any of these blocks is relevant but missing, the output is not ready as an official document.

## Final TXT Content Rule

The final TXT must contain only the cadastral engineer conclusion. Do not include:

- questions to the worker;
- a list of missing information;
- "Из XML получено" or other XML parsing notes;
- references to XML as a source;
- geodetic-basis descriptions;
- service explanations of how the conclusion was created.

All questions must be asked and answered before the final TXT is written.

Also ban source-style phrases in final text: "по сведениям XML", "указано в XML", "в XML отражено", "раздел XML", "дата по XML", "XML межевого плана". The document should read as a normal cadastral engineer conclusion, not as a report about parsing source data.

## Related Land Parcels

When XML contains related or adjacent parcels, clarify the legal/technical role of each parcel before drafting:

- If the related parcel is уточняется, use a short wording: only part of the boundary of the adjacent land parcel with declared boundaries and area is being уточнена.
- If the related parcel is исправляется, add a full paragraph describing the registry error in that adjacent parcel's boundaries and what must be corrected in EGRN.

Do not choose уточнение vs исправление by yourself unless the source documents clearly say so.

## 15-Year Boundary Confirmation

For уточняемые or исправляемые land parcels, ask how the existence of boundaries for 15 or more years is confirmed when the conclusion relies on long-standing actual boundaries. Possible confirmation sources include state acts, archival documents, court decisions, inventory materials, long-standing fences/objects, or other user-provided documents.
