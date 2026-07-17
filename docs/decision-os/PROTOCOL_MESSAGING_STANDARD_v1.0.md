# Protocol Messaging Standard v1.0

## انواع محتوا

### Conversation

گفت‌وگوی عادی برای فکرکردن.

- تصمیم رسمی نیست.
- Header پروتکل ندارد.
- الزاماً در Repository ثبت نمی‌شود.

### Protocol Message

پیام رسمی بین نقش‌ها.

- Header استاندارد دارد.
- بخشی از یک Interaction است.
- قابل ثبت و پردازش است.

### Human Comment

نظر Human که هنوز تصمیم الزام‌آور نیست.

### Human Decision

تصمیم صریح و الزام‌آور Human.

## سیاست زبان

- کلیدهای فنی و Enumها انگلیسی هستند.
- بدنه با زبان اعلام‌شده در `LANGUAGE` نوشته می‌شود.
- مقدار پیش‌فرض پروژه `LANGUAGE: fa` است.

## Header اجباری

```text
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Decision OS Protocol Message
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

LANGUAGE:
fa

MESSAGE_ID:
<unique-message-id>

INTERACTION_ID:
<stable-interaction-id>

ROUND:
<number>

MESSAGE_TYPE:
<enum>

STATUS:
<enum>

FROM:
<role>

TO:
<role>

ACTION_REQUIRED:
<requested-action>

AUTHORITY:
<authority-level>

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Footer اجباری

```text
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
END OF MESSAGE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## قواعد شناسه‌ها

- هر پاسخ یک `MESSAGE_ID` جدید دارد.
- همهٔ پیام‌های یک بحث، `INTERACTION_ID` یکسان دارند.
- `ROUND` با هر دور Challenge افزایش می‌یابد.
- هیچ Agentی نباید شناسهٔ پیام قبلی را بازنویسی کند.

### قرارداد موقت تولید شناسه

قرارداد زیر **سبک و موقت** است — هیچ Registry مرکزی یا سازوکار تضمین‌کنندهٔ یکتایی ندارد؛ فقط
برای خوانایی و کاهش تصادم دستی است. تغییر یا جایگزینی آن در آینده نیازمند تصمیم رسمی نیست، چون
خودِ این بخش جایگزین‌شدنی و غیرالزام‌آور اعلام شده است.

- `INTERACTION_ID`: قالب `INTR-<YYYY-MM-DD>-<topic-slug>`. فقط یک‌بار، توسط فرستندهٔ اولین پیام
  یک تعامل ساخته می‌شود و تا پایان همان تعامل ثابت می‌ماند.
- `MESSAGE_ID`: قالب `MSG-<ROLE_ABBR>-<TYPE_ABBR>-<sequence>` — مثلاً `MSG-EXEC-REPORT-001`.
  `ROLE_ABBR` نمونه: `HUMAN`, `ARCH`, `CHAL`, `EXEC`. `TYPE_ABBR` نمونه: `TASK`, `REPORT`,
  `PROPOSAL`. `sequence` عددی افزایشی سه‌رقمی، مستقل برای هر `INTERACTION_ID`.

## Message Typeهای پایه

- `DECISION_PROPOSAL`
- `CHALLENGE_REQUEST`
- `CHALLENGE_REPORT`
- `ARCHITECT_RESPONSE`
- `HUMAN_COMMENT`
- `HUMAN_DECISION`
- `ROLE_ACKNOWLEDGEMENT`
- `EXECUTION_TASK`
- `EXECUTION_REPORT`
- `REVIEW_REQUEST`
- `REVIEW_REPORT`
- `FINAL_DECISION_RECORD`

## Statusهای پایه

- `OPEN`
- `IN_REVIEW`
- `BLOCKED`
- `APPROVED_FOR_EXECUTION`
- `EXECUTED`
- `ACCEPTED`
- `ACCEPTED_WITH_KNOWN_RISKS`
- `REJECTED`
- `CLOSED`
- `REVISION_REQUIRED`
- `DEFERRED_FOR_EVIDENCE`
- `PARTIALLY_EXECUTED`
- `FAILED`

این ۱۳ مقدار، فهرست کامل و یکپارچهٔ `STATUS` برای Header پروتکل است. چهار مقدار آخر پیش‌تر در
`docs/decision-os/HUMAN_GATES.md` (خروجی Gate 1 و Gate 2)، `docs/decision-os/ROLES_AND_AUTHORITY.md`
(وضعیت‌های پیشنهادی Reviewer)، و `.decision-os/templates/EXECUTION_REPORT_TEMPLATE.md` (بخش
Final Status) استفاده می‌شدند بدون این‌که در این فهرست پایه ثبت شده باشند — این افزودن صرفاً
همان مقادیر از پیش در‌حال‌استفاده را یکپارچه می‌کند و هیچ مقدار موجودی را حذف یا تغییرنام نمی‌دهد.

### فیلدهای مشابه که عمداً جدا از `STATUS` هستند

دو مورد زیر شبیه `STATUS` به‌نظر می‌رسند اما مفهوم متفاوتی دارند و نباید با آن یکی گرفته شوند:

- **`Final Verdict`** در `.decision-os/templates/CHALLENGE_REPORT_TEMPLATE.md`
  (`ACCEPTABLE`, `ACCEPTABLE_WITH_CHANGES`, `REQUIRES_RED_DESIGN`, `BLOCKED_PENDING_EVIDENCE`) —
  قضاوت Technical Challenger دربارهٔ کیفیت Proposal است، نه وضعیت چرخهٔ‌عمر یک پیام. هیچ‌کدام از
  این چهار مقدار به فهرست `STATUS`های پایه اضافه نشدند.
- **`BOOTSTRAP_ACCEPTED`** در `README.md` — طبق توضیح همان بخش، خروجی یک Direct Human Execution
  است، نه خروجی یک `HUMAN_GATES.md` Gate یا معادل `FINAL_DECISION_RECORD`.

افزودن فیلدهای جدید به Header در نسخهٔ 1.0 ممنوع است مگر با تصمیم رسمی.
