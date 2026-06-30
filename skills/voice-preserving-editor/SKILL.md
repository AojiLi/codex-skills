---
name: voice-preserving-editor
description: "Edit, polish, correct, complete, or insert user-written text while preserving the user's voice, meaning, tone, warmth, and personal style. Use when the user asks to improve grammar, wording, clarity, accuracy, flow, or missing content in a paragraph, selected passage, Markdown/text document, README, DOCX, Google Doc, or other prose document, especially when they want the writing to stay recognizably theirs rather than be heavily rewritten."
---

# Voice-Preserving Editor

## Overview

Use this skill to make the user's writing clearer and more accurate without flattening its personality. Default to direct, minimal edits when a target file or document location is provided; default to returning the edited text when the user only provides text.

The core rule: preserve the author's meaning and voice unless the user explicitly asks for a rewrite or a new style.

## Non-Negotiables

- Preserve the user's viewpoint, tone, rhythm, vocabulary habits, narrative perspective, and emotional intensity.
- Do not replace warm, personal, hesitant, sharp, plain, or oral-feeling writing with generic polished prose unless the user asks for that.
- Fix obvious errors: grammar, typos, broken sentences, contradictions, unclear references, timeline mistakes, term misuse, and expressions that would mislead the reader.
- For uncertain facts, legal/medical/financial/technical claims, quotes, dates, names, or data, verify from context or sources when needed; otherwise flag uncertainty instead of inventing a fix.
- Do not add new substantive opinions, promises, facts, data, examples, claims, or conclusions unless the user explicitly asks or confirms them.
- When editing a file, change only the specified paragraph, sentence, section, or insertion point. Read surrounding context, but do not "improve" unrelated text.
- Do not create backup files by default. Use minimal scoped edits and rely on the workspace's normal version control when present.

## Supported Inputs

Support:

- plain pasted text
- Markdown and text files
- repository docs such as `README.md` and `docs/*.md`
- `.docx` files through document-aware tools
- Google Docs through the Google Drive/Docs connector when available

Do not treat PDFs as directly editable prose targets by default. Extract or suggest text if needed, but do not overwrite a PDF unless a separate PDF editing workflow is explicitly requested.

## Workflow

### 1. Identify The Target

If the user provides only text, edit the text and return the revised version.

If the user provides a file or document, locate the target paragraph, sentence, section, or insertion point. Use explicit anchors such as selected text, headings, line numbers, nearby sentences, or user-provided keywords.

If the location is ambiguous:

- Search for candidate matches.
- If there is exactly one high-confidence match, edit that match.
- If there are multiple plausible matches, ask the user to choose before editing.
- Do not guess a target paragraph from vague intent.

### 2. Read Context Before Editing

Before editing a document passage, read the target passage and at least the paragraph before and after it. Expand context when the passage depends on:

- section headings
- earlier definitions
- argument flow
- recurring terms
- a setup or emotional beat from earlier text
- document-level style

Use the original text's style as the default when document type or audience is unclear.

### 3. Decide Edit Strength

Default to light-to-medium editing when the user says "edit", "polish", "fix", "make it clearer", or "write it more accurately".

- Light edit: fix grammar, typos, punctuation, broken sentences, ambiguity, repetition, and small transitions while preserving wording.
- Medium edit: adjust sentence order, remove clutter, add small connective tissue, and make meaning more accurate while preserving voice.
- Heavy rewrite: restructure, expand, change style, formalize, marketize, academicize, or replace the voice. Do this only when the user explicitly asks.

When a messy draft contains real feeling or personality, rescue meaning and voice first, then clean structure. Keep strong original phrases when possible.

### 4. Preserve Voice While Correcting

Preserve:

- viewpoint: do not change the user's stance
- tone: keep warmth, restraint, sharpness, sincerity, doubt, closeness, or distance
- rhythm: do not turn every short, breathing sentence into long formal prose
- vocabulary: keep the user's plain or repeated words when they are part of the voice
- perspective: keep first, second, or third person unless the document requires otherwise
- emotional intensity: do not flatten genuine feeling or exaggerate it

Keep oral, incomplete, or informal phrasing when it carries personality and does not harm comprehension. Fix it only when it creates confusion, friction, or a mismatch with the document's purpose.

### 5. Add Content Carefully

Allow light additions that clarify what the user already meant:

- missing subject or object
- transition words
- causal links
- necessary explanation
- one or two context-setting phrases that are directly implied by surrounding text

Do not directly write substantial new content unless requested:

- new argument
- new claim
- new example or story
- new data or source
- new conclusion
- stronger promise or commitment

If the document needs substantial added content, propose the addition or ask a focused question before writing it into the document.

### 6. Match Document Type And Audience

Infer document type, target reader, and use case from the file and context. Adjust only as much as the context requires.

For personal essays, notes, reflections, newsletters, and informal writing, protect texture and voice.

For technical docs, README files, product docs, resumes, business materials, policy text, contracts, tutorials, and other accuracy-sensitive documents, prioritize accuracy, clarity, and reader safety over preserving an imprecise expression. Still keep the user's style where it does not damage correctness.

If the user's tone conflicts with the document type, satisfy the document's purpose with the smallest necessary style shift. Do not erase the author's personal reason or emotional core.

### 7. Edit The Right Format Safely

For Markdown and plain text, edit the file directly with a minimal patch.

For `.docx`, use document-aware tooling and preserve formatting. Do not crudely rewrite raw document XML unless that is the safest available route and the file is verified afterward.

For Google Docs, use the Google Drive/Docs connector when available. Preserve the target document and only edit the requested range.

If safe direct editing is not possible for the format, say so and provide the revised text for the user to apply.

### 8. Multi-Version Requests

If the user asks for multiple versions, tones, or options, do not directly edit the file first. Return 2-4 versions for selection, such as more natural, more formal, more restrained, or more forceful.

After the user chooses a version, write it into the document if a target location exists.

### 9. Response After Editing

When a file is edited, keep the response brief:

- state the file changed
- include the final edited paragraph or inserted text when reasonably short
- if the edited area is long, summarize the area and provide the file path

Do not provide a full before/after comparison or detailed change trace by default. If a correction required a larger-than-usual rewrite to fix an error, mention that briefly.

When no file is edited, return the revised text directly, with only a short note if useful.
