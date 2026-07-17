# Context Distribution

## هدف

تعریف این‌که Context (فایل، سند، یا اطلاعات پس‌زمینه) چگونه بین نقش‌ها/Agentهای Decision OS
منتقل می‌شود، و مرز مسئولیت هرکدام در قبال آن چیست. این سند مکمل
`docs/decision-os/INTERACTION_PROTOCOL_v1.0.md` است و Transport پیام‌های پروتکل را تغییر
نمی‌دهد.

## روش انتقال Context

- روش پیش‌فرض: **Raw GitHub URL** (مثلاً آدرس `raw.githubusercontent.com/...` به یک فایل مشخص
  در این Repository). این روش امروز دستی توسط Human انجام می‌شود، طبق Transport Independence در
  `INTERACTION_PROTOCOL_v1.0.md`.
- برای تعامل‌هایی که به چند فایل هم‌زمان نیاز دارند، از **Context Manifest** استفاده می‌شود
  (رجوع به `.decision-os/templates/CONTEXT_MANIFEST_TEMPLATE.md`).
- استفاده از Context Manifest اجباری نیست؛ فقط وقتی توصیه می‌شود که فهرست‌کردن فایل‌ها مستقیماً
  در بدنهٔ Protocol Message خوانایی را کاهش دهد.

## محدودیت مسئولیت Agent

- هر Agent فقط مسئول Context‌ای است که **صریحاً** در پیام یا Context Manifest به او داده شده.
- هیچ Agentی نباید فرض کند به فایل‌های دیگر این Repository، یا به Repository دیگری، دسترسی
  ضمنی دارد.
- هیچ Agentی نباید محتوای Context را از حافظهٔ مکالمات قبلی فرض کند — دقیقاً همان اصل «هیچ نقش
  یا قاعده‌ای نباید از حافظهٔ چت فرض شود» در `README.md`، اینجا برای داده هم تعمیم داده می‌شود.

## مسئولیت Human دربارهٔ مرز اطلاعات عمومی و خصوصی

- Human تنها مرجع تشخیص این است که کدام اطلاعات مجاز به قرارگرفتن در Repository عمومی
  (`decision-os-coordination`) هستند و کدام باید فقط در Repository خصوصی محصول بمانند
  (رجوع به `docs/decisions/ADR-0010-runtime-architecture-and-repository-roles.md`).
- هیچ Agentی — از جمله Executor — نباید محتوای Repository خصوصی محصول را بدون تصریح Human در
  Repository عمومی کپی، خلاصه، یا ارجاع‌پذیر کند.
- اگر یک Agent در انجام یک مأموریت به Context‌ای نیاز داشت که برایش فراهم نشده، باید طبق اصل
  توقف‌و‌گزارش (`docs/decision-os/ROLES_AND_AUTHORITY.md`، بخش «اصل اختیار») متوقف شود و آن را
  به‌عنوان یک Unresolved Item گزارش کند، نه این‌که حدس بزند.
