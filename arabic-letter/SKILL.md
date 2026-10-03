---
name: arabic-letter
description: "Writes the wording of formal Arabic letters and official emails (خطاب، رسالة رسمية) in Gulf government style. Use when asked to draft one. Output is text; PDFs are made separately."
compatibility: "Claude.ai, Claude Desktop, Claude Code, Cowork · text only, no tools or packages · Sonnet or Opus recommended for Arabic register"
---

# Arabic Letter Composer

Composes formal Arabic letters in the conventional style of Gulf government and organizational correspondence.

If `personal.md` exists in this folder, read it first; it overrides the defaults in this file.

## Optional user files

Read these from this folder when they exist. They are the user's own and are never shipped with the skill.

| File | What it holds | How to use it |
|---|---|---|
| `glossary.md` | Preferred word choices: a table of *Use* / *Avoid* / *When* | Apply every row. A glossary entry wins over the general style rules below. |
| `people.md` | Recipients the user writes to: English name, full Arabic name, Arabic title, Arabic organization, internal or external. Write it by hand, or generate it from person notes with `scripts/build_people.py` (fields `name_ar`, `title_ar`, `org_ar`, `internal`) | Copy the Arabic name, title and organization exactly. If a recipient isn't listed, ask for the full Arabic name rather than guessing a four-part name. |

## When to use

Use this skill when the user:

- asks to write, draft or compose an Arabic letter, خطاب, رسالة رسمية, official correspondence or a formal letter in Arabic
- says "write a letter to" or "draft a letter for" in a formal or official context
- gives bullet points or a description, in English or Arabic, and wants it turned into a formal Arabic letter or formal Arabic email

Covers government letters, organizational correspondence, and official requests and notifications. Not for casual messages, WhatsApp-style notes or English letters.

## Workflow

Copy this checklist into your reply's working notes and tick it off as you go:

```
- [ ] 1. Extract recipient, purpose, key points, tone (and a sender only if one is given); ask only if recipient or purpose is missing
- [ ] 2. Decide mode: letter (with subject line) or email (subject goes in the email subject field)
- [ ] 3. Decide the honorific level for the recipient (rule 8); ask if the rank is unclear
- [ ] 4. Draft the letter in the seven-part structure below
- [ ] 5. Run the verification pass; fix and re-check until it passes
- [ ] 6. Output the letter as plain text, then the English summary (and Arabic subject line for emails)
```

## Input Handling

The user gives a free-form description in **English or Arabic** (or a mix). Extract:

1. **Recipient**: name, title, organization
2. **Sender**: usually none. The signature comes from the user's email client or letterhead, so leave it out unless the user names a sender or asks for a signature block
3. **Subject/Purpose**: what the letter is about
4. **Key points**: the content, requests or information to convey
5. **Tone**: formal/official by default; adjust if the user says otherwise

If the recipient or the purpose is missing, ask briefly. For other gaps, make a reasonable assumption and list it in the summary.

## Letter Structure

Every letter follows this structure, top to bottom. Do NOT include a date or reference number unless the user asks for one.

### 1. Addressee Block (المرسل إليه)
- Format (note the run of spaces before المحترم):
  ```
  السيد/ [الاسم الكامل]        المحترم
  [المسمى الوظيفي] – [المؤسسة/الجهة]
  ```
- `السيدة/` with `المحترمة` for a female recipient
- `السادة/` with `المحترمين` for an organization or group
- Second line: title only for internal recipients (same organization). For external recipients, title and organization joined with –, whether email or letter.

### 2. Greeting (التحية)
- Exactly: `تحية طيبة وبعد ...`
- Three dots `...` after وبعد, never a comma
- Blank line after the greeting

### 3. Subject Line (الموضوع)
- Format: `الموضوع: [عنوان موجز وواضح]`
- Short and specific
- **Emails:** leave the subject line out of the body. Suggest an Arabic subject line separately, after the letter.

### 4. Body (المتن)
- **Opening sentence**: pick the one that fits:
  - `بالإشارة إلى الموضوع أعلاه`: following up on a known topic (not for emails, since there is no subject line above it)
  - `نود أن نفيدكم بأن...`: informing or notifying
  - `يسرنا أن نتقدم إليكم...`: making a request or proposal
  - `إلحاقاً لخطابنا السابق...`: following up on an earlier letter
  - `نظراً لـ...`: giving the justification first
- **Main content**: clear, concise paragraphs
  - Connecting phrases: `علماً بأن`، `نظراً لـ`، `بناءً على`، `في ضوء ما سبق`، `وبناءً عليه`
  - Several points: `أولاً:`، `ثانياً:`، `ثالثاً:` or a numbered list

### 5. Closing (الختام)
- Exactly: `وتفضلوا بقبول فائق الاحترام والتقدير`
- No comma or period at the end
- Blank line after the closing

### 6. Sender Block (المرسل), only when asked
- Leave it out by default: the letter ends at the closing, and the user's email signature or letterhead supplies the sender.
- When the user asks for one or names a sender: name and title only; do NOT repeat the organization:
  ```
  [الاسم الكامل]
  [المسمى الوظيفي]
  ```

### 7. Optional Elements (only if the user mentions them)
- `نسخة إلى:` for CC recipients
- `المرفقات:` for attachments
- Both go at the bottom, after the closing (or the sender block, if there is one)

## Language & Style Rules

1. **All letter output is in Arabic**, whatever language the input was in.
2. **Modern Standard Arabic (فصحى)**, no dialect at all. Formal but natural: it should read like a person wrote it, not like an archaic or bureaucratic template. Prefer the simpler modern word when one exists (e.g. `بعد` rather than `عقب`).
3. **Formal register** throughout; no casual phrasing.
4. **Clear, direct sentences**: no padding beyond the formality the genre expects.
5. **Arabic punctuation**: `،` (comma), `؛` (semicolon), `؟` (question mark).
6. **Western Arabic numerals** (1, 2, 3...), never Arabic-Indic (٠١٢٣٤٥٦٧٨٩) and never numbers written as words.
7. **No date or reference number** unless requested.
8. **Honorific address forms (سعادتكم / معاليكم / حضرتكم) are rank-gated:**
   - `سعادتكم` / `سعادة السيد` is only for recipients whose addressee block carries the title `سعادة`: minister rank or equivalent (e.g. `معالي الوزير`, `سعادة السفير`). Do NOT use it for any other rank, including Secretary General (الأمين العام), director or department head, and not in a body sentence referring back to the recipient either (e.g. "...ما تراه سعادتكم مناسباً").
   - For everyone else, don't swap in another honorific pronoun (`حضرتكم` is also too elevated for most organizational letters). Use plain second-person plural: `ترونه مناسباً`، `حسب تقديركم`، `وفقاً لما تقررونه`، `ولكم جزيل الشكر` (not `ولسعادتكم` / `ولحضرتكم`).
   - If the recipient's rank is unclear, ask rather than default to an elevated honorific.
9. **State the concrete ask in the opening sentence.** No vague placeholder like "بهذا الطلب"; name the action straight away ("فإننا نتقدم إليكم بطلب لصرف مكافأة تقديرية لـ..." not "نتقدم إليكم بهذا الطلب بخصوص..."). Pairs well with `بالإشارة إلى الموضوع أعلاه` when a subject line precedes it.
10. **Direct, verb-first sentences over abstract phrasing.** "قام الموظف بمهام خارج نطاق مهامه المعتادة" rather than "تجاوز عمل الموظف نطاق مهامه المعتادة". Prefer `قام بـ` and subject-verb-object clarity over making an abstract noun the subject.
11. **One qualifier per noun.** "دعماً خاصاً" not "دعماً خاصاً ومكرساً". If two descriptors are both true, keep the stronger one.
12. **One concrete detail beats a vague statement**, when the detail is known: add "بشكل يومي" rather than leaving frequency unstated; write "الدول المستضيفة للبطولة" rather than "الدولة المستضيفة" when more than one country is involved.
13. **Third-party or estimated figures take `قدرت بـ`, not `بلغت`.** Keep `بلغت` for confirmed, internal, exact figures; using it for a vendor quote overstates certainty.
14. **Round illustrative or vendor-quoted figures** to a clean number (250,000 not 248,730) unless it is a formal invoiced amount. Add `فقط` after the figure when the point is that it is the base or minimum cost.
15. **Cite only the most relevant tier** from an external price list, unless more than one tier bears directly on the ask.
16. **Money as a numeral only**: `15,000 ريال قطري`, not `15,000 ريال قطري (خمسة عشر ألف ريال قطري)`.

## Verification

Before outputting, check the draft against this list:

- Addressee block: correct السيد/السيدة/السادة with the matching المحترم/المحترمة/المحترمين, and the second line follows the internal/external rule
- Greeting is exactly `تحية طيبة وبعد ...` and the closing is exactly `وتفضلوا بقبول فائق الاحترام والتقدير`, with nothing after it
- Email mode: no `الموضوع:` line in the body and no `بالإشارة إلى الموضوع أعلاه` opener; an Arabic subject line is suggested after the letter
- No Arabic-Indic digits, no spelled-out amounts, no date or reference number unless requested
- No `سعادتكم` / `حضرتكم` unless the recipient carries a سعادة-level title
- The opening sentence names the concrete ask
- No sender block unless one was asked for; if present, name and title only
- Every `glossary.md` entry applied, and names/titles copied exactly from `people.md`

If any check fails, return to step 4 of the workflow, fix the draft, and run the checks again.

## Output Format

- The letter as **plain text in chat**, not a file, unless the user asks for a file
- Line breaks separating each section
- After the letter, a brief English summary of what was written, plus any assumptions made, so the user can confirm it matches their intent

## Example

**User input:** "Write a letter to Khalid Al-Salem, Director of Human Resources at Al-Mustaqbal Company, about closing the financial year, from our IT department. Tell him we need to finalize all pending IT procurement before the deadline."

**Output:**

السيد/ خالد عبدالله السالم        المحترم
مدير إدارة الموارد البشرية – شركة المستقبل

تحية طيبة وبعد ...

الموضوع: إقفال السنة المالية

بالإشارة إلى الموضوع أعلاه، نود إفادتكم بضرورة إنهاء جميع عمليات الشراء المعلقة الخاصة بقسم تقنية المعلومات قبل الموعد النهائي المحدد لإقفال السنة المالية.

نرجو التكرم بالتوجيه لتسريع الإجراءات المتبقية حتى يتسنى لنا استكمال جميع المتطلبات في الوقت المحدد.

وتفضلوا بقبول فائق الاحترام والتقدير

---
**Summary:** A formal letter to Khalid Al-Salem (Director of HR, Al-Mustaqbal Company) regarding the financial year closing, requesting that all pending IT procurement be finalized before the deadline.
