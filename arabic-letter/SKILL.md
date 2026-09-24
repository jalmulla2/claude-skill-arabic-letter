---
name: arabic-letter
description: "Compose formal Arabic letters and official correspondence following standard Arabic letter structure. Use this skill whenever the user asks to write, draft, or compose an Arabic letter, خطاب, رسالة رسمية, official correspondence, formal letter in Arabic, or mentions \"write a letter to\" or \"draft a letter for\" in the context of formal/official communication. Also trigger when the user provides bullet points or a description (in English or Arabic) and wants it turned into a formal Arabic letter. Covers government letters, organizational correspondence, and official requests/notifications."
---

# Arabic Letter Composer

Compose formal Arabic letters in the conventional style of Gulf government and organizational correspondence.

## Input Handling

The user will provide input as a free-form description in **English or Arabic** (or a mix of both). Extract the following from their input:

1. **Recipient** — name, title, organization
2. **Sender** — name, title (user specifies each time)
3. **Subject/Purpose** — what the letter is about
4. **Key points** — the main content/requests/information to convey
5. **Tone** — default is formal/official; adjust if user indicates otherwise

If critical information is missing (recipient or purpose), ask the user briefly. For other missing details, make reasonable assumptions and note them.

## Letter Structure

Every letter must follow this exact structure, top to bottom. Do NOT include a date or reference number unless the user explicitly requests one.

### 1. Addressee Block (المرسل إليه)
- Format — note the spacing (multiple spaces before المحترم):
  ```
  السيد/ [الاسم الكامل]        المحترم
  [المسمى الوظيفي] – [المؤسسة/الجهة]
  ```
- Use `السيدة/` for female recipients, with `المحترمة`
- Use `السادة/` for addressing an organization or group, with `المحترمين`
- Second line is the title only for internal recipients (same organization). For external recipients, include title and organization joined with –, whether email or letter.

### 2. Greeting (التحية)
- Exactly: `تحية طيبة وبعد ...`
- Always use three dots `...` after وبعد, NOT a comma
- Leave a blank line after the greeting

### 3. Subject Line (الموضوع)
- Format: `الموضوع: [عنوان موجز وواضح]`
- Keep it short and specific
- **For emails:** OMIT the subject line from the letter body entirely — it will go in the email subject field instead. Suggest an appropriate Arabic subject line separately after the letter.

### 4. Body (المتن)
- **Opening sentence** — vary based on context. Choose the most appropriate:
  - `بالإشارة إلى الموضوع أعلاه` — when following up on a known topic (avoid this opener for emails since there is no subject line above to reference)
  - `نود أن نفيدكم بأن...` — when informing/notifying
  - `يسرنا أن نتقدم إليكم...` — when making a request or proposal
  - `إلحاقاً لخطابنا السابق...` — when following up on a previous letter
  - `نظراً لـ...` — when providing justification upfront
- **Main content**: clear, concise paragraphs
  - Use formal Modern Standard Arabic (فصحى)
  - Avoid colloquial expressions entirely
  - Use proper connecting phrases: `علماً بأن`، `نظراً لـ`، `بناءً على`، `في ضوء ما سبق`، `وبناءً عليه`
  - For multiple points, use `أولاً:`، `ثانياً:`، `ثالثاً:` or a numbered list

### 5. Closing (الختام)
- Exactly: `وتفضلوا بقبول فائق الاحترام والتقدير`
- No comma or period at the end
- Leave a blank line after the closing

### 6. Sender Block (المرسل)
- Format (name and title only — do NOT repeat the organization):
  ```
  [الاسم الكامل]
  [المسمى الوظيفي]
  ```

### 7. Optional Elements (only if user mentions them)
- **نسخة إلى:** — list CC recipients
- **المرفقات:** — list attachments
- Place these at the bottom after the sender block

## Language & Style Rules

1. **All letter output is in Arabic** — regardless of whether the user's input was in English or Arabic
2. Use **Modern Standard Arabic (فصحى)** — no dialect whatsoever
3. Maintain **formal register** throughout — avoid casual phrasing
4. Keep sentences **clear and direct** — avoid unnecessary verbosity while maintaining expected formality
5. Use proper Arabic punctuation: `،` (comma), `؛` (semicolon), `؟` (question mark)
6. Use **Western Arabic numerals** (1, 2, 3, 4, 5...) — do NOT use Arabic-Indic numerals (٠١٢٣٤٥٦٧٨٩) or English words for numbers
7. Do NOT include date or reference number unless explicitly requested
8. **Honorific address forms (سعادتكم / معاليكم / حضرتكم) — rank-gated:**
   - `سعادتكم` / `سعادة السيد` is reserved for recipients whose addressee block carries the title `سعادة` — typically minister-rank or equivalent (e.g. `معالي الوزير`, `سعادة السفير`). Do NOT use it for any other rank, including Secretary General (الأمين العام), director, or department head — even in a body sentence referring back to the recipient (e.g. "...ما تراه سعادتكم مناسباً").
   - For recipients without a سعادة-level title, do not substitute another honorific pronoun either (`حضرتكم` is also too elevated for most organizational correspondence) — default to plain second-person plural phrasing instead: `ترونه مناسباً`, `حسب تقديركم`, `وفقاً لما تقررونه`, `ولكم جزيل الشكر` (not `ولسعادتكم`/`ولحضرتكم`).
   - When in doubt about the recipient's rank, ask the user rather than defaulting to an elevated honorific.
9. **State the concrete ask in the opening sentence.** Don't open with a vague placeholder like "بهذا الطلب" — name the specific action being requested right away (e.g. "فإننا نتقدم إليكم بطلب لصرف مكافأة تقديرية لـ..." not "نتقدم إليكم بهذا الطلب بخصوص..."). Pairs well with `بالإشارة إلى الموضوع أعلاه` as the opener when a subject line precedes it.
10. **Prefer direct, verb-first sentence construction over abstract/literary phrasing.** E.g. "قام الموظف بمهام خارج نطاق مهامه المعتادة" rather than "تجاوز عمل الموظف نطاق مهامه المعتادة". Favor `قام بـ` / subject-verb-object clarity over indirect constructions that make an abstract noun the grammatical subject.
11. **One qualifier per noun — don't stack adjectives.** "دعماً خاصاً" not "دعماً خاصاً ومكرساً". If two descriptors are both true, prefer cutting to the stronger one over listing both.
12. **Favor one concrete, specific detail over a vague general statement, when the detail is known.** E.g. add "بشكل يومي" rather than leaving frequency/scope unstated; write "الدول المستضيفة للبطولة" rather than the vaguer "الدولة المستضيفة" if more than one country is involved.
13. **Figures sourced from a third party or estimate: say `قدرت بـ` (estimated at), not `بلغت` (amounted to/totaled).** Reserve `بلغت` for confirmed, internal, exact figures — using it for a vendor quote overstates certainty.
14. **Round comparative/vendor-quoted figures to a clean order of magnitude** (e.g. 250,000 not 248,730) rather than quoting an exact line-item total, when the number is illustrative rather than a formal invoiced amount. Add `فقط` after the figure when the point is that this is the base/minimum cost.
15. **Cite only the single most relevant tier from an external source, not every pricing option**, unless more than one tier is directly relevant to the specific ask being made.
16. **State monetary amounts as a numeral only** — do not add the spelled-out Arabic words in parentheses after the numeral (e.g. `15,000 ريال قطري`, not `15,000 ريال قطري (خمسة عشر ألف ريال قطري)`).

## Output Format

- Output the letter as **plain text in chat** (not a file)
- Use line breaks to clearly separate each section
- After the letter, add a brief note (in English) summarizing what was written, so the user can verify the content matches their intent

## Example

**User input:** "Write a letter to Khalid Al-Salem, Director of Human Resources at Al-Mustaqbal Company, about closing the financial year. I'm Ahmed Al-Hassan, Head of IT. Tell him we need to finalize all pending IT procurement before the deadline."

**Output:**

السيد/ خالد عبدالله السالم        المحترم
مدير إدارة الموارد البشرية – شركة المستقبل

تحية طيبة وبعد ...

الموضوع: إقفال السنة المالية

بالإشارة إلى الموضوع أعلاه، نود إفادتكم بضرورة إنهاء جميع عمليات الشراء المعلقة الخاصة بقسم تقنية المعلومات قبل الموعد النهائي المحدد لإقفال السنة المالية.

نرجو التكرم بالتوجيه لتسريع الإجراءات المتبقية حتى يتسنى لنا استكمال جميع المتطلبات في الوقت المحدد.

وتفضلوا بقبول فائق الاحترام والتقدير

أحمد علي الحسن
رئيس قسم تقنية المعلومات

---
**Summary:** A formal letter to Khalid Al-Salem (Director of HR, Al-Mustaqbal Company) regarding the financial year closing, requesting that all pending IT procurement be finalized before the deadline.
