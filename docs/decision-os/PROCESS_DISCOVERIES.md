# Process Discoveries

## هدف

ثبت متمرکز یافته‌های **واقعی** (نه فرضی) دربارهٔ نحوهٔ عملکرد واقعی پروتکل Decision OS — طبق اصل
Evidence-Based Protocol Evolution (رجوع به
`docs/decisions/ADR-0011-evidence-based-protocol-evolution.md`). هر بار که اجرای واقعی پروتکل
چیزی را آشکار کند که در اسناد پیش‌بینی نشده بود، همین‌جا ثبت می‌شود — به‌جای پراکنده‌شدن در
Commit Messageها یا Protocol Messageهای مجزا.

## ساختار هر Discovery

هر ورودی این فیلدها را دارد:

- **Discovery ID** — قالب `DISC-<sequence>` (مثلاً `DISC-0001`)
- **Date**
- **Status** — یکی از: `OPEN`, `MONITORING`, `ACCEPTED`, `IMPLEMENTED`
- **Source Type** — یکی از: `PRODUCTION_INCIDENT`, `SIMULATED_TEST`
- **Evidence Ref** — ارجاع مشخص به پیام/Commit/Interaction که این یافته از آن آمده
- **Observed Problem**
- **Root Cause**
- **Recommendation**
- **Resolution**

این فهرست Statusها و Source Typeها مستقل از `Statusهای پایه` پیام پروتکل
(`docs/decision-os/PROTOCOL_MESSAGING_STANDARD_v1.0.md`) است — یک Discovery رکورد دانش است، نه
یک پیام.

## Discoveries

### DISC-0001 — نیاز به فرآیند مستندسازی مبتنی‌بر‌شواهد برای تکامل پروتکل

- **Date:** 2026-07-18
- **Status:** `IMPLEMENTED`
- **Source Type:** `PRODUCTION_INCIDENT`
- **Evidence Ref:**
  1. `INTR-2026-07-18-LANGGRAPH-ALIGNMENT`، Round 1 — پیامی با `MESSAGE_TYPE: EXECUTION_REQUEST`
     (نوعی خارج از فهرست رسمی) و `STATUS: OPEN` (نه `APPROVED_FOR_EXECUTION`)، بدون
     `MESSAGE_ID`/`INTERACTION_ID`/`ROUND`/`AUTHORITY` — رجوع به `MSG-EXEC-REPORT-001`.
  2. همان تعامل — ناسازگاری `ROLE_ACKNOWLEDGEMENT` (از `BOOTSTRAP_INSTRUCTION_FOR_CLAUDE.md`)
     با فهرست رسمی Message Typeها — رجوع به `MSG-EXEC-REPORT-002`، Commit `743353e`.
  3. `INTR-2026-07-18-TASK-0001` — ناسازگاری چندجانبهٔ فهرست پایهٔ `STATUS` با
     `HUMAN_GATES.md`، `ROLES_AND_AUTHORITY.md`، و `EXECUTION_REPORT_TEMPLATE.md` — رجوع به
     `MSG-TASK-0001-003`، Commit `e00f2a7`.
- **Observed Problem:** در همان روز اول استفادهٔ واقعی از Decision OS، چند نقص مستقل و واقعی در
  خودِ پروتکل کشف شد — همه از طریق اجرای واقعی پیام‌ها، نه بازبینی نظری از پیش.
- **Root Cause:** اسناد اولیهٔ Bootstrap یک‌باره و بدون بازخورد اجرای واقعی نوشته شده بودند؛ هیچ
  سازوکار متمرکزی برای ثبت الگوهای تکرارشونده وجود نداشت — هر یافته در قالب یک Task جداگانه
  اصلاح می‌شد، بدون حافظهٔ مشترک بین آن‌ها.
- **Recommendation:** ایجاد همین سند به‌عنوان محل ثبت متمرکز، و پذیرفتن این اصل که هیچ تغییر
  پروتکلی صرفاً بر پایهٔ نظر یا حدس اعمال نشود — هرکدام باید به یک Evidence Ref واقعی ارجاع بدهد.
- **Resolution:** `IMPLEMENTED` — همین سند و
  `docs/decisions/ADR-0011-evidence-based-protocol-evolution.md` نتیجهٔ مستقیم این Discovery‌اند.
