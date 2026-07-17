# Decision OS — Bootstrap Package v1.0

این بسته نقطهٔ شروع رسمی Decision OS است و برای انتقال دانش اولیه از چت به Repository ایجاد شده است.

## اصل پایه

- تفکر در Conversation انجام می‌شود.
- هماهنگی بین نقش‌ها از طریق Protocol Message انجام می‌شود.
- دانش و تصمیم‌های معتبر در Repository ثبت می‌شوند.

## زبان

- زبان پیش‌فرض تعامل انسانی و محتوای پیام‌ها فارسی است.
- کلیدهای فنی، شناسه‌ها و Enumهای پروتکل انگلیسی باقی می‌مانند.
- مقدار پیش‌فرض `LANGUAGE` برابر `fa` است.

## نقش‌های فعلی

- Human / Decision Owner
- Architect / ChatGPT
- Technical Challenger / Claude
- Executor / Claude Code
- Reviewer

## ترتیب شروع

1. همهٔ نقش‌ها ابتدا این فایل و اسناد پوشهٔ `docs/decision-os` را می‌خوانند.
2. هیچ نقش یا قاعده‌ای نباید از حافظهٔ چت فرض شود.
3. هر تعارض یا ابهام باید گزارش شود و خودسرانه اصلاح نشود.
4. تغییرات معماری فقط با تصمیم Human ثبت می‌شوند.

## اسناد مرجع

- `docs/decision-os/ROLES_AND_AUTHORITY.md`
- `docs/decision-os/INTERACTION_PROTOCOL_v1.0.md`
- `docs/decision-os/PROTOCOL_MESSAGING_STANDARD_v1.0.md`
- `docs/decision-os/HUMAN_GATES.md`
- `docs/decision-os/CONTEXT_DISTRIBUTION.md`
- `docs/decisions/ADR-0009-language-and-presentation-policy.md`
- `docs/decisions/ADR-0010-runtime-architecture-and-repository-roles.md`

## نوع اجرا: Direct Human Execution در برابر Decision OS Workflow

دو نوع متفاوت از فعال‌شدن Executor وجود دارد:

- **Direct Human Execution** — Human مستقیماً و بدون طی‌کردن چرخهٔ کامل Interaction Protocol،
  یک اقدام مشخص و غیرمعماری (مثلاً راه‌اندازی اولیهٔ Repository) را به Executor دستور می‌دهد.
  این حالت جایگزین Human Gate نمی‌شود؛ صرفاً برای اقدام‌هایی است که خودشان یک تصمیم معماری یا
  محصول نیستند.
- **Decision OS Workflow** — هر تغییری که معماری، پروتکل، یا تصمیم محصول را تحت تأثیر قرار
  می‌دهد، باید چرخهٔ کامل `INTERACTION_PROTOCOL_v1.0.md` (Proposal → Challenge → Human Gate 1 →
  Execution → Review → Human Gate 2) را طی کند.

اگر Executor در تشخیص این‌که یک درخواست کدام نوع است تردید داشت، باید طبق اصل توقف‌و‌گزارش در
`docs/decision-os/ROLES_AND_AUTHORITY.md` متوقف شود، نه این‌که خودسرانه تصمیم بگیرد.

## وضعیت

`BOOTSTRAP_ACCEPTED`

این وضعیت خروجی یک Direct Human Execution بود (دستور مستقیم Human برای وارد‌کردن اولیهٔ این
بسته به Repository) — نه خروجی یک چرخهٔ کامل Human Gate 1 / Gate 2. این‌جا صریحاً ثبت می‌شود تا
`BOOTSTRAP_ACCEPTED` به‌اشتباه معادل یک `FINAL_DECISION_RECORD` خوانده نشود.

این بسته صرفاً نسخهٔ پایه است و نباید پیش از آزمون واقعی پیچیده‌تر شود.
