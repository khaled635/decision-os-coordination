# ADR-0011 — Evidence-Based Protocol Evolution

- Status: Accepted
- Date: 2026-07-18
- Decision Owner: Human
- Architect: ChatGPT

## Context

در همان روز اول استفادهٔ واقعی از Decision OS، چند نقص مستقل در خودِ پروتکل — نه در محصول — از
طریق اجرای واقعی کشف شد (رجوع به `docs/decision-os/PROCESS_DISCOVERIES.md`، `DISC-0001`). هیچ
سازوکار رسمی برای ثبت این‌گونه یافته‌ها و پیگیری تصمیم دربارهٔ آن‌ها وجود نداشت؛ هر یافته در قالب
یک Task مجزا اصلاح می‌شد، بدون حافظهٔ مشترک بین آن‌ها.

## Decision

1. یافته‌های واقعی دربارهٔ رفتار پروتکل (نه پیشنهادهای نظری) در
   `docs/decision-os/PROCESS_DISCOVERIES.md` ثبت می‌شوند، با ساختار ثابت: Discovery ID، Date،
   Status، Source Type، Evidence Ref، Observed Problem، Root Cause، Recommendation، Resolution.
2. Statusهای مجاز یک Discovery: `OPEN`, `MONITORING`, `ACCEPTED`, `IMPLEMENTED`. این فهرست از
   Statusهای پایهٔ پیام پروتکل (`docs/decision-os/PROTOCOL_MESSAGING_STANDARD_v1.0.md`) جداست —
   یک Discovery رکورد دانش است، نه یک پیام.
3. Source Typeهای مجاز: `PRODUCTION_INCIDENT` (رخداد واقعی حین استفادهٔ واقعی)،
   `SIMULATED_TEST` (سناریوی آزمایشی عمدی).
4. هیچ تغییر پروتکلی نباید صرفاً بر پایهٔ نظر یا حدس اعمال شود؛ هر تغییر باید به یک Evidence Ref
   واقعی (پیام، Commit، یا Interaction مشخص) ارجاع بدهد.

## Explicitly Out of Scope (این دور)

طبق تصمیم تصویب‌شده، موارد زیر عمداً به این دور وارد نشدند:

- Status `EVIDENCE_EXISTS`
- Status `WONT_FIX`
- قانون حداقل دو Interaction برای تبدیل یک یافته به `SIMULATED_TEST` تأییدشده
- Architect Revision به‌عنوان مرحلهٔ رسمی Workflow

## Consequences

- تغییرات پروتکل آینده (مثل یکپارچه‌سازی Statusها در TASK-0001) باید به یک Discovery ارجاع
  بدهند، نه صرفاً به یک درخواست موردی.
- بخشی از مأموریت جاری — بازبینی TASK-0001 و علامت‌گذاری بخش‌های `UNSUPPORTED` با وضعیت
  `DEFERRED` — اجرا **نشد**، چون هیچ Audit یا Evidence Ref مشخصی (کدام بخش‌ها، کدام Audit) در
  Task دریافت نشده بود. طبق اصل همین ADR (بدون Evidence Ref، تغییر پروتکلی اعمال نمی‌شود)، این
  آیتم به Architect بازگردانده شده — رجوع به Execution Report مربوطه.
- حجم مستندات Decision OS رشد می‌کند؛ Discoveryهای بدون پیگیری واقعی باید در آینده بازبینی یا
  بسته شوند (همان‌طور که در Repository خصوصی محصول، اسناد بدون مصرف‌کنندهٔ فعال کاندید حذف‌اند).
