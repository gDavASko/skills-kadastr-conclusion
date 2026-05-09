# Public Data Lookup for Cadastral Conclusions

Use this workflow when the user provides cadastral numbers and allows public lookup, or explicitly asks to search NSPD, Роскадастр, FGIS TP, PZZ, or public cadastral sources.

## Source Priority

1. `https://nspd.gov.ru/` and `https://nspd.gov.ru/map`
   - Public cadastral map on the National Spatial Data System.
   - Use for object lookup, map context, layers, zones, and visual access/smежность checks.

2. `https://kadastr.ru/services/publichnaya-kadastrovaya-karta/`
   - Роскадастр public cadastral map service page.
   - Use as official entry point and for confirming public-map purpose.

3. `https://kadastr.ru/services/zakaz-vypisok-iz-egrn3442/`
   - Use when the task requires an EGRN extract or legally stronger confirmation.

4. FGIS TP, municipal websites, regional geoportals, published PZZ documents.
   - Use for territorial zones, VRI rules, minimum/maximum parcel sizes, and approval document details.

5. Other sites.
   - Use only as hints. Do not rely on them as authoritative sources in final legal text.

## What to Search by Cadastral Number

- object type: land parcel, building, structure, ONS, ENK;
- address or location;
- area;
- category of land;
- permitted use / VRI;
- status;
- cadastral quarter;
- cadastral value if relevant;
- contours and map location;
- nearby parcels and visible adjacency;
- ZOUIT, territorial zones, settlement/municipal boundaries;
- possible access via roads, common-use land, adjacent parcels, or source parcel.

## Workflow

1. Normalize the cadastral number: trim spaces, check format `00:00:000000:000`.
2. Search NSPD/public cadastral map by cadastral number.
3. If found, record in notes:
   - source;
   - date checked;
   - cadastral number;
   - object type;
   - address/location;
   - area;
   - category;
   - VRI;
   - status;
   - visible zones or adjacent objects relevant to the conclusion.
4. Turn on relevant layers: parcels, buildings/structures, cadastral quarters, ZOUIT, territorial zones, municipal/settlement boundaries, base map or satellite layer.
5. Check access visually, but phrase it cautiously unless confirmed by documents.
6. For PZZ, identify the municipality and search official published PZZ. Use NSPD zone layers as a clue, not as the only basis for legal-size limits.
7. If the object is not found, do not conclude that it does not exist. Ask for an EGRN extract, cadastral plan, XML, screenshot, or additional identifier.
8. If public data conflicts with user documents, prefer user-provided official documents and ask for clarification.

## Safe Use in Final Text

You may use public data to support:

- address/location;
- area and VRI when consistent with source documents;
- cadastral quarter;
- possible adjacent cadastral numbers;
- territorial zone hints;
- ZOUIT presence;
- preliminary access analysis.

Do not use public lookup alone to:

- identify or assert owners/right holders;
- assert encumbrances as legally confirmed;
- prove a registry error;
- replace field measurements;
- determine exact coordinates;
- invent formed parcel areas or boundary-point data.

## Suggested Caveat

When internet lookup materially influenced the draft, keep this working caveat available:

"Сведения из публичных источников использованы как справочные и подлежат сверке с выпиской ЕГРН и исходными материалами кадастровых работ."

Do not overload the final conclusion with URLs unless the source is part of the legal basis, such as PZZ or FGIS TP publication details.
