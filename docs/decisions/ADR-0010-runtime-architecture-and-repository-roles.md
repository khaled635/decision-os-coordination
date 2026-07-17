# ADR-0010 — Runtime Architecture Without External Orchestrator؛ نقش Repositoryها

- Status: Accepted
- Date: 2026-07-18
- Decision Owner: Human
- Architect: ChatGPT

## Context

پس از بررسی Architect و Technical Challenger، این پرسش مطرح شد که آیا Decision OS باید از یک
Orchestrator خارجی (مثلاً LangGraph) یا APIهای پولی جداگانه استفاده کند تا هماهنگی بین نقش‌ها
خودکار شود.

Human تصمیم گرفت این وابستگی در این مرحله اضافه نشود، چون معماری فعلی (هماهنگی دستی توسط Human
بین چند مدل، طبق `INTERACTION_PROTOCOL_v1.0.md` بخش Transport Independence) هنوز آزمون واقعی
نشده و افزودن Orchestrator پیش از آن، دقیقاً همان الگوی «معماری‌سازی زودهنگام» است که این پروژه
از آن پرهیز می‌کند (رجوع به `README.md`: «این بسته... نباید پیش از آزمون واقعی پیچیده‌تر شود»).

هم‌زمان، نیاز بود نقش دو Repository که در این تصمیم مطرح شدند — Repository عمومی هماهنگی
(همین ریپو) و Repository خصوصی محصول — صریحاً ثبت شود.

## Decision

1. معماری اجرایی فعلی Decision OS بدون LangGraph، بدون APIهای پولی جداگانه، و بدون هیچ
   Orchestrator خارجی دیگر ادامه پیدا می‌کند.

2. جریان عملی فعلی نقش‌ها:

   ```
   Human
     ↓
   Architect (ChatGPT)
     ↓
   Public Coordination Repository
     ↓
   Technical Challenger (Claude) — در مواردی که Challenge لازم باشد
     ↓
   Human Decision
     ↓
   Executor (Claude Code)
   ```

3. `decision-os-coordination` (این Repository، عمومی) نقش **Control Plane** را دارد: هماهنگی
   نقش‌ها، پروتکل پیام‌رسانی، ADRها، Templateهای رسمی، و اسناد فرآیندی.

4. Repository خصوصی محصول (در حال حاضر: `Decision-intelligence`) نقش **Source of Truth** را
   دارد: تصمیم‌های واقعی محصول (مثل Decision Contract)، لاگ اعتبارسنجی، فرضیه‌های رد‌شده، و کد.

5. LangGraph یا Orchestratorهای دیگر ممکن است در آینده بررسی شوند، اما در نسخهٔ فعلی وابستگی یا
   الزام معماری محسوب نمی‌شوند.

## Consequences

- هماهنگی بین نقش‌ها فعلاً دستی است (Human پیام‌ها را جابه‌جا می‌کند)؛ این هزینه پذیرفته شده تا
  خودِ پروتکل ابتدا با داده‌ی واقعی آزموده شود.
- Repository عمومی نباید حاوی محتوای خصوصی محصول باشد (رجوع به
  `docs/decision-os/CONTEXT_DISTRIBUTION.md` برای مسئولیت تفکیک این مرز).
- افزودن هر Orchestrator در آینده نیازمند یک ADR جدید و طی‌کردن چرخهٔ کامل Interaction Protocol
  است، نه یک تغییر خودسرانهٔ Executor یا Architect.
