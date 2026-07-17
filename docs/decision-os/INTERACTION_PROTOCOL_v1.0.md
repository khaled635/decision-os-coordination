# Interaction Protocol v1.0

## هدف

تعریف نحوهٔ همکاری چندمرحله‌ای Human، Architect، Technical Challenger، Executor و Reviewer، مستقل از روش انتقال پیام.

این پروتکل Transport را تعریف نمی‌کند. انتقال پیام می‌تواند فعلاً دستی و بعداً خودکار باشد.

## چرخهٔ اصلی

1. Human مسئله، هدف یا محدودیت را مطرح می‌کند.
2. Architect مسئله را تحلیل و یک Proposal آماده می‌کند.
3. Technical Challenger Proposal را نقد می‌کند.
4. Architect به نقد پاسخ می‌دهد یا Proposal را اصلاح می‌کند.
5. در صورت نیاز، دورهای Challenge تکرار می‌شوند.
6. Human Gate 1 دربارهٔ اجازهٔ اجرا تصمیم می‌گیرد.
7. Executor فقط نسخهٔ تأییدشده را اجرا می‌کند.
8. Executor یک Execution Report ارائه می‌دهد.
9. Reviewer خروجی را با تصمیم و معیارها تطبیق می‌دهد.
10. Human Gate 2 نتیجهٔ نهایی را می‌پذیرد، رد می‌کند یا برای اصلاح بازمی‌گرداند.
11. تصمیم و دانش نهایی در Repository ثبت می‌شود.

## قواعد دورهای Challenge

- هر دور دارای `INTERACTION_ID` ثابت و `ROUND` افزایشی است.
- هر پیام دارای `MESSAGE_ID` مستقل است.
- Challenger باید مسائل را به `BLOCKING` و `NON_BLOCKING` تقسیم کند.
- Architect باید برای هر مسئله یکی از پاسخ‌های زیر را بدهد:
  - `ACCEPT`
  - `REJECT_WITH_REASON`
  - `DEFER`
  - `REQUEST_EVIDENCE`
- اختلاف حل‌نشده‌ای که روی اجرا اثر اساسی دارد به Human ارجاع می‌شود.

## شرایط توقف Challenge

Challenge زمانی متوقف می‌شود که یکی از موارد زیر رخ دهد:

- هیچ مسئلهٔ `BLOCKING` باز نمانده باشد.
- Human ادامهٔ بحث را متوقف و تصمیم بگیرد.
- شواهد کافی وجود نداشته باشد و تصمیم به Validation واقعی موکول شود.
- مشخص شود Proposal باید از نو طراحی شود.

## Transport Independence

پروتکل به ابزار انتقال وابسته نیست.

امروز:
- Human پیام‌ها را بین مدل‌ها جابه‌جا می‌کند.

آینده:
- Orchestrator پیام‌ها را مسیریابی می‌کند.

ساختار، شناسه‌ها و قواعد پیام نباید با تغییر Transport عوض شوند.

## ثبت آثار

موارد زیر باید در Repository قابل ثبت باشند:

- Proposal تأییدشده
- Challenge Report
- Architect Response
- Human Decision
- Execution Task
- Execution Report
- Review Report
- Final Decision Record
