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

## Message Typeهای پایه

- `DECISION_PROPOSAL`
- `CHALLENGE_REQUEST`
- `CHALLENGE_REPORT`
- `ARCHITECT_RESPONSE`
- `HUMAN_COMMENT`
- `HUMAN_DECISION`
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

افزودن فیلدهای جدید به Header در نسخهٔ 1.0 ممنوع است مگر با تصمیم رسمی.
