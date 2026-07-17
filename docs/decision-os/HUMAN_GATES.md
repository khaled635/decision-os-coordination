# Human Gates

## Gate 1 — Approve Execution

شرکت‌کنندگان:

- Human / Decision Owner
- Architect

ورودی‌های لازم:

- Proposal
- Challenge Report
- Architect Response
- مسائل Blocking باقیمانده
- ریسک‌های شناخته‌شده
- معیارهای پذیرش اجرا

خروجی‌های مجاز:

- `APPROVED_FOR_EXECUTION`
- `REVISION_REQUIRED`
- `REJECTED`
- `DEFERRED_FOR_EVIDENCE`

بدون `APPROVED_FOR_EXECUTION`، Executor اجازهٔ اجرای تغییر معماری یا Repository را ندارد.

## Gate 2 — Final Decision

شرکت‌کنندگان:

- Human / Decision Owner
- Architect

ورودی‌های لازم:

- Execution Report
- Review Report
- نتایج تست یا Validation
- انحراف‌های اجرا
- ریسک‌های باقی‌مانده

خروجی‌های مجاز:

- `ACCEPTED`
- `ACCEPTED_WITH_KNOWN_RISKS`
- `REVISION_REQUIRED`
- `REJECTED`

فقط خروجی Gate 2 می‌تواند به‌عنوان تصمیم نهایی در Repository ثبت شود.
