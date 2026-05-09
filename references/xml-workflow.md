# XML-First Workflow

Use this reference when the user has an XML file of a boundary plan or technical plan, or when preparing a cadastral engineer conclusion from machine-readable source data.

## Principle

The XML file is the primary input for analysis and questions. Parse it first, extract all available information, identify what is missing for a complete conclusion, ask the worker only for missing data, then create the final TXT document with the user-specified name.

The final TXT must contain only the cadastral engineer conclusion. It must not contain questions, XML parsing notes, "Из XML получено", "Согласно XML", "Требуется уточнить", or a list of missing data. Questions are asked before file creation.

Do not include phrases like "по сведениям XML", "указано в XML", "приведенным в XML", "в XML отражено", "раздел XML", "дата по XML", or "XML межевого плана" in the final TXT. Use the extracted facts silently.

XML files may have different schemas. Do not hard-code one path as the only possible structure. First identify the root element, namespaces, version, and top-level work/object nodes, then select the extraction strategy.

## Required Workflow

1. Ask the worker to attach the XML file if it is not already provided.
2. Ask the worker for the desired final TXT file name. The output format is fixed: `.txt`. If the user gives a name without an extension, append `.txt`.
3. Read XML as UTF-8.
4. Use an XML parser. Avoid regex/string-only parsing for structured fields.
5. Identify XML type:
   - `MP` means boundary plan / межевой план;
   - `SpecifyParcel` usually means уточнение земельного участка;
   - `SpecifyRelatedParcel` identifies related/smежные уточняемые parcels;
   - formation/change/new parcel nodes indicate образование, раздел, перераспределение, выдел, or changed parcels;
   - `TP` means technical plan and may contain `Building`, `Flat`, `Construction`, `Uncompleted`, `NewBuildings`, `ExistBuilding`, `NewFlat`, or `PositionInObject`;
   - `InspectionAct` means акт обследования and usually contains `Contractor`, `Client`, `Object`, `Documents`, and `Conclusion`.
6. Extract known facts and create a short working summary.
7. Compare known facts against the conclusion requirements.
8. Ask a missing-information questionnaire.
9. After answers are provided, draft or create the final document.

## Extract from Boundary Plan XML

Look for:

- root attributes: `MP/@Version`, `MP/@NameSoftware`, `MP/@VersionSoftware`, `MP/@GUID`;
- work/package nodes: `Package`, `SpecifyParcel`, formation/change/new-parcel nodes;
- main parcel: `ExistParcel/@CadastralNumber`;
- cadastral block: `CadastralBlock`;
- access: `ProvidingPassCadastralNumbers`, including `Other` and cadastral-number children;
- area: `Area/Area`, `Area/Unit`, `Area/Inaccuracy`, `Area/Formula`;
- previous/register area: `AreaInGKN`;
- area difference: `DeltaArea`;
- coordinate system: `EntitySpatial/@Name`, `EntitySpatial/@CsCode`, MCK zone;
- spatial elements and points: `SpatialElement`, `SpelementUnit`, `OldOrdinate`, `NewOrdinate`;
- point details: `NumGeopoint`, `X`, `Y`, `DeltaGeopoint`, `GeopointZacrep`, `GeopointOpred`, `Formula`;
- boundaries and edge lengths: `Borders`, `Border`, `Edge/Length`;
- related parcels: `SpecifyRelatedParcel/@CadastralNumber`, `ChangeBorder`;
- formed parcels: designations such as `:ЗУ1`, `:ЗУ2`, areas, contours;
- geodetic basis: `InputData/GeodesicBases/GeodesicBase`;
- survey equipment: `InputData/MeansSurvey/MeanSurvey`, including `Name`, `Number`, `CertificateVerification`, verification date and validity period when available;
- appendices and attached documents: `Appendix/AppliedFiles`;
- current conclusion: `Conclusion`.

For technical plans, the object area from XML must be reused in the required SKP phrase:

`СКП вычисляется по формуле Mp = Ms*√(a²+b²) и составила [СКП from user] на площадь объекта [area from XML] кв.м.`

Ask the user for the SKP value. Do not invent it. If XML has several areas or no clear object area, ask which area to use.

Ask whether the technical plan is prepared under the simplified or notification procedure:

- if simplified, include exactly: `Технический план составлен в соответствии с ч.12 ст.70 Закона о регистрации, согласно которому, собственник объекта недвижимости выбрал "упрощенный" порядок оформления.`
- if notification, include exactly: `Технический план подготовлен в соответствии с нормами градостроительного кодекса на основании уведомлений о планируемом строительстве и о завершении строительства.`

Do not create the final TXT for a technical plan until both the SKP value and the procedure type are clarified.

Do not include geodetic-basis details in the final conclusion. They may be parsed for understanding, but the conclusion should not list geodetic control points.

Do include survey equipment details in full when the conclusion mentions coordinate determination. The wording should preserve all available instrument fields: name, serial/factory number, verification certificate details, and validity period. If only part of the instrument information is available, ask the worker for the missing details before final TXT generation when the equipment paragraph is required.

Write the coordinate system fully. If XML contains `EntitySpatial/@Name="МСК-16"` and `CsCode="16.1"`, the conclusion should say `МСК-16, зона 1 (код 16.1)`. If `CsCode="16.2"`, say `МСК-16, зона 2 (код 16.2)`. In general, the part after the dot in `CsCode` is the zone number. If the zone cannot be determined, ask the worker before creating the final TXT.

Before saving the TXT, run a text-level check: every sentence containing `МСК-` must also contain `зона` or be rewritten. A phrase like `в местной системе координат МСК-16` is invalid even if the zone was known during parsing.

From XML `InputData` / source-document sections, use only PZZ information in the final conclusion when it exists and is relevant. Do not automatically list all source documents or appendices in the conclusion.

If `<Conclusion>` is empty, contains only `.`, or contains boilerplate, treat it as missing.

Boundary-plan variants observed in source XML:

- `SpecifyParcel` / `ExistParcel`: уточнение существующего земельного участка.
- `SpecifyRelatedParcel`: уточнение смежного или связанного участка.
- `FormParcels` / `NewParcel`: образование новых участков.
- `ChangeParcel`: изменение исходного или сохраняемого участка.
- `TransformationEntryParcel`: преобразуемые участки.
- `ObjectsRealty` / `ObjectRealty`: объекты недвижимости, связанные с участком.
- Conclusions may describe раздел, выдел в счет доли, перераспределение, объединение, образование из неразграниченной государственной собственности, or ИРО.

For every related parcel found in XML, ask the worker whether the related parcel is:

1. уточняется; or
2. исправляется.

This choice changes the wording:

- If related parcel is уточняется, write briefly that only part of the boundary of the adjacent parcel with declared boundaries and area is being уточнена.
- If related parcel is исправляется, write a full separate paragraph describing the registry error in the boundaries of that adjacent parcel and what EGRN data must be corrected.

## Extract from Technical Plan XML (`TP`)

Look for:

- root attributes: `TP/@Version`, `TP/@GUID`, `TP/@NameSoftware`, `TP/@VersionSoftware`;
- top object node: `Building`, `Flat`, `Construction`, `Uncompleted`;
- work-variant nodes: `NewBuildings`, `ExistBuilding`, `NewFlat`, `PositionInObject`;
- cadastral numbers: `CadastralNumber`, `CadastralNumberOKS`, `ParentCadastralNumber`;
- land parcel numbers where the object is located;
- address blocks: `Address`, FIAS, region, municipality, street, house, room/premise;
- object name and purpose: `Name`, `Assignation`, `AssignationBuilding`, `AssignationCode`;
- area and accuracy: `Area`, `Inaccuracy`;
- contours and coordinates: `EntitySpatial`, `Contours`, `SpelementUnit`, `Ordinate`;
- floor/level data for premises: `Levels`, `Level`, `Plans`, `Position`;
- wall material, floors, construction year, completion year, foundation if present;
- source documents: declarations, technical passports, EGRN extracts, project documents, contracts;
- contractor/cadastral engineer data: `Contractor`, `NumberAgreement`, `DateAgreement`, FIO, SNILS, contacts;
- geodetic basis and survey equipment if present;
- appendices: `AppliedFiles`, `NameAppendix`, `NumberAppendix`;
- current conclusion: `Conclusion`.

Technical-plan variants observed in source XML:

- new building / newly created garage or house;
- existing building уточнение by coordinates;
- building characteristic changes;
- building/garage located partly outside land parcel boundaries;
- block of a residential house;
- flat/premise division with `Flat`, `NewFlat`, `ParentCadastralNumber`, and `CadastralNumberOKS`.

## Extract from Inspection Act XML (`InspectionAct`)

Look for:

- root attributes: `InspectionAct/@GUID`, software, version, namespaces;
- cadastral engineer: `Contractor`, registry number, SNILS, SRO, phone, email, address;
- client: `Client`;
- object: `Object`, `ObjectType`, cadastral number, address/location, area, purpose;
- rights information if present, including registered/unregistered right markers;
- termination data: `YearTermination`;
- documents: `Documents`, document names, numbers, dates, issue organs, attached files;
- agreement/contract: number and date;
- current conclusion: `Conclusion`.

Inspection-act conclusions often justify full demolition or termination of existence of a building. They may cite demolition notifications, authority responses, powers of attorney, and owner notices.

## Official-Document Accuracy Rule

These XML-based outputs are official cadastral documents. The model must not invent or "complete" missing official facts. If a field is missing, contradictory, unreadable, or only visually guessed from a map, ask the worker for confirmation or request an official source.

Allowed sources:

- the XML and attached files;
- user answers;
- EGRN extracts, КПТ, technical/boundary plans, declarations, court decisions, authority acts;
- official public sources, only when public lookup is allowed.

Disallowed in final text:

- guessed addresses;
- guessed PZZ zones or VRI;
- guessed rights/owners/encumbrances;
- guessed registry-error reasons;
- guessed publication details;
- guessed engineer/contract details;
- conclusions based only on non-official websites.

## Completeness Matrix

Before creating the final document, confirm these blocks are complete:

1. Work identification: plan type and work type.
2. Object identification: object type, cadastral number, address/location.
3. Technical basis: area, coordinate system with MCK zone/code, contours/points, instruments or characteristic source documents.
4. Legal basis: contract, supporting documents, appendices, court/authority/project/publication details when used.
5. Result justification: access, adjacent parcels, agreement/publication, PZZ/VRI/zone, registry error or demolition reason if relevant.
6. Contractor details: cadastral engineer, organization, contacts, registry number, agreement.
7. Output details: final file name and format.
8. For technical plans: SKP value from user, object area from XML, and simplified/notification procedure.

If any required block is incomplete, do not create the final TXT. Ask the questions first. A "Требуется уточнить" section is allowed only in the chat before final generation, never inside the final TXT file.

## Example Working Summary

```text
Рабочая карточка предварительного разбора:
- тип: межевой план, уточнение земельного участка (`SpecifyParcel`);
- КН: [кадастровый номер уточняемого участка];
- кадастровый квартал: [кадастровый квартал];
- доступ: [способ доступа];
- площадь по результатам работ: [площадь] кв.м;
- площадь по ЕГРН: [площадь] кв.м;
- изменение площади: [разница] кв.м;
- МСК: [местная система координат, зона, код];
- связанные земельные участки: [кадастровые номера];
- прибор: [полное наименование, номер, реквизиты и срок действия поверки, если это нужно для заключения];
- заключение в XML отсутствует или пустое.
```

## Common Missing Data

Ask for these only when not present in XML or other supplied documents:

1. Address or full location description.
2. Actual use of the parcel/object.
3. What physically marks the boundaries.
4. Why the cadastral work is being done: уточнение, registry error, court decision, inheritance, garage formalization, access issue, etc.
5. Whether the area difference should be explained as normal уточнение, registry error, court-backed correction, or another reason.
6. For уточняемые or исправляемые land parcels: how the existence of boundaries for 15 or more years is confirmed.
7. For every related parcel from XML: whether it is уточняется or исправляется.
8. Which appendices should be cited and their details.
9. Territorial zone, VRI, land category, PZZ source, minimum/maximum parcel size.
10. Cadastral engineer details, organization, contract, preparation date.
11. Whether public lookup in NSPD/Rosкадастр/FGIS TP is allowed.
12. Final TXT output file name.
13. For technical plans: SKP value for `Mp = Ms*√(a²+b²)` and whether the procedure is simplified or notification-based.

## Missing-Data Questionnaire Template

```text
По результатам предварительного разбора исходных данных уже понятно: [краткая рабочая карточка]. Эта служебная карточка нужна только для вопросов и не включается в итоговый TXT.

Для подготовки заключения не хватает:
1. Укажите адрес или описание местоположения объекта.
2. Чем фактически закреплены/обозначены границы на местности?
3. Какую причину работ нужно отразить в заключении?
4. Чем подтверждается существование границ 15 и более лет?
5. По связанным участкам [список КН] нужно указать уточнение части границы или исправление реестровой ошибки?
6. Нужно ли ссылаться на приложения или документы-основания: [список релевантных документов]?
7. Укажите территориальную зону, ВРИ и предельные размеры или разрешите найти их в публичных источниках.
8. Укажите сведения о кадастровом инженере/договоре, если их нет в XML.
9. Как назвать итоговый TXT-файл?
```

## Final File Creation

Before writing the file:

- confirm the file name;
- sanitize unsafe filename characters;
- create a plain `.txt` file;
- include only the conclusion text in the TXT;
- avoid overwriting an existing file unless the user confirms or the task clearly asks to update it.
