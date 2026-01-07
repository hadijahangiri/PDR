# PRD Generator Agent 📋

یک Custom GitHub Copilot Agent برای تولید خودکار اسناد PRD (Product Requirement Document) با کیفیت بالا. 

[English](#english) | [فارسی](#persian)

---

<a name="persian"></a>
## 🇮🇷 راهنمای فارسی

### 📖 معرفی

این Agent یک دستیار هوشمند است که بر اساس ورودی ساختاریافته شما، یک سند PRD کامل و حرفه‌ای تولید می‌کند.  این سند شامل تمام جزئیات لازم برای توسعه‌دهندگان، تیم QA، و ذینفعان است.

### 🚀 نحوه استفاده

#### گام 1: فعال‌سازی Agent

1. در GitHub Copilot Chat (در VS Code، Visual Studio، یا github.com) تایپ کنید: 
   ```
   @workspace
   ```

2. Agent به صورت خودکار از دستورالعمل‌های موجود در `.github/copilot-instructions.md` استفاده خواهد کرد.

#### گام 2: ارائه ورودی

ورودی خود را با فرمت زیر به Agent بدهید:

```
لطفاً یک PRD برای این feature بساز: 

FeatureName: [نام feature]
ProductContext: [محصول/سیستم مربوطه]
Description: [توضیح غیرفنی]
TargetUsers: [کاربران هدف]
MainUseCases: [3 تا 7 سناریو اصلی]
TechStack: [تکنولوژی‌های مورد استفاده]
Constraints: [محدودیت‌ها]
EdgeCases: [موارد خاص]
NonFunctionalNeeds: [نیازمندی‌های غیرعملکردی]
Dependencies: [وابستگی‌ها]
Risks: [ریسک‌های اصلی]
```

#### گام 3: دریافت PRD

Agent یک PRD کامل با ساختار زیر تولید خواهد کرد:

1. **Overview** - خلاصه و اهداف
2. **Scope & Out of Scope** - محدوده کار
3. **User Personas & Use Cases** - کاربران و سناریوها
4. **Functional Requirements** - نیازمندی‌های عملکردی
5. **Non-Functional Requirements** - نیازمندی‌های غیرعملکردی
6. **Integration & API Hints** - پیشنهادات API
7. **Analytics & Success Metrics** - معیارهای موفقیت
8. **Risks & Open Questions** - ریسک‌ها و سوالات
9. **Acceptance Criteria** - معیارهای پذیرش

### 📚 فایل‌های مهم

- **`.github/copilot-instructions. md`** - دستورالعمل‌های agent
- **`templates/prd-template.md`** - قالب خروجی PRD
- **`examples/input-example.md`** - نمونه ورودی کامل
- **`examples/output-example.md`** - نمونه خروجی PRD
- **`Thesis-Defense-Management-System-PRD.md`** - نمونه PRD واقعی برای سیستم مدیریت دفاع پایان‌نامه
- **`PRD-Summary.md`** - خلاصه سریع PRD سیستم مدیریت دفاع پایان‌نامه

### 💡 نکات مهم

✅ **انجام دهید:**
- از فرمت ورودی پیشنهادی استفاده کنید
- تمام فیلدهای مهم را پر کنید
- Use Case‌ها را واضح و مشخص بنویسید
- محدودیت‌ها و ریسک‌ها را صریح ذکر کنید

❌ **انجام ندهید:**
- ورودی‌های خیلی مبهم یا کوتاه ندهید
- بخش‌های مهم را خالی نگذارید
- انتظار جزئیات implementation-level نداشته باشید (PRD سطح بالاست)

### 🔧 رفع مشکلات رایج

#### خطای "Task Creation Failed"

**علت:** Prompt خیلی طولانی یا فرمت نادرست

**راه‌حل:**
1. مطمئن شوید Agent به repository دسترسی دارد
2. از فایل `.github/copilot-instructions. md` استفاده کنید (نه paste مستقیم prompt)
3. ورودی را در قالب ساختاریافته ارائه دهید
4. GitHub Copilot را restart کنید

#### Agent دستورالعمل‌ها را نادیده می‌گیرد

**راه‌حل:**
1. مطمئن شوید فایل `.github/copilot-instructions.md` در root repository است
2. از `@workspace` در Copilot Chat استفاده کنید
3. Repository را refresh کنید

### 🎯 مثال سریع

```
@workspace لطفاً یک PRD برای این feature بساز: 

FeatureName: Two-Factor Authentication
ProductContext: SaaS Authentication System
Description: Add optional 2FA using TOTP authenticator apps
TargetUsers: End users and enterprise customers
MainUseCases: 
1. User enables 2FA for first time
2. User logs in with 2FA
3. User recovers account with recovery codes
TechStack: Python + FastAPI + PostgreSQL
Constraints:  Must be done in 6 weeks, GDPR compliant
EdgeCases:  Lost device, clock drift, expired codes
NonFunctionalNeeds: <200ms validation, audit logging
Dependencies: Email service, existing auth system
Risks: User lockout, poor adoption rate
```

---

<a name="english"></a>
## 🇬🇧 English Guide

### 📖 Introduction

This Agent is an intelligent assistant that generates complete, professional PRD (Product Requirement Document) based on your structured input. The document includes all necessary details for developers, QA teams, and stakeholders.

### 🚀 How to Use

#### Step 1: Activate the Agent

1. In GitHub Copilot Chat (VS Code, Visual Studio, or github.com), type:
   ```
   @workspace
   ```

2. The Agent will automatically use instructions from `.github/copilot-instructions.md`.

#### Step 2: Provide Input

Give your input to the Agent in this format:

```
Please create a PRD for this feature: 

FeatureName: [feature name]
ProductContext: [product/system]
Description: [non-technical explanation]
TargetUsers: [target users]
MainUseCases: [3 to 7 main scenarios]
TechStack: [technologies to use]
Constraints: [limitations]
EdgeCases: [edge cases]
NonFunctionalNeeds: [non-functional requirements]
Dependencies: [dependencies]
Risks: [main risks]
```

#### Step 3: Receive PRD

The Agent will generate a complete PRD with this structure:

1. **Overview** - Summary and goals
2. **Scope & Out of Scope** - Work boundaries
3. **User Personas & Use Cases** - Users and scenarios
4. **Functional Requirements** - Functional requirements
5. **Non-Functional Requirements** - Non-functional requirements
6. **Integration & API Hints** - API suggestions
7. **Analytics & Success Metrics** - Success metrics
8. **Risks & Open Questions** - Risks and questions
9. **Acceptance Criteria** - Acceptance criteria

### 📚 Important Files

- **`.github/copilot-instructions.md`** - Agent instructions
- **`templates/prd-template.md`** - PRD output template
- **`examples/input-example.md`** - Complete input example
- **`examples/output-example.md`** - PRD output example
- **`Thesis-Defense-Management-System-PRD.md`** - Real-world PRD example for Thesis Defense Management System
- **`PRD-Summary.md`** - Quick reference summary of the Thesis Defense Management System PRD

### 💡 Best Practices

✅ **Do:**
- Use the suggested input format
- Fill all important fields
- Write clear and specific use cases
- Explicitly mention constraints and risks

❌ **Don't:**
- Give vague or too-short inputs
- Leave important sections empty
- Expect implementation-level details (PRD is high-level)

### 🔧 Troubleshooting

#### "Task Creation Failed" Error

**Cause:** Prompt too long or incorrect format

**Solution:**
1. Ensure Agent has repository access
2. Use `.github/copilot-instructions.md` file (not direct paste)
3. Provide input in structured format
4. Restart GitHub Copilot

#### Agent Ignores Instructions

**Solution:**
1. Ensure `.github/copilot-instructions.md` is in repository root
2. Use `@workspace` in Copilot Chat
3. Refresh the repository

### 🎯 Quick Example

```
@workspace Please create a PRD for this feature: 

FeatureName: Two-Factor Authentication
ProductContext: SaaS Authentication System
Description: Add optional 2FA using TOTP authenticator apps
TargetUsers:  End users and enterprise customers
MainUseCases:
1. User enables 2FA for first time
2. User logs in with 2FA
3. User recovers account with recovery codes
TechStack: Python + FastAPI + PostgreSQL
Constraints: Must be done in 6 weeks, GDPR compliant
EdgeCases: Lost device, clock drift, expired codes
NonFunctionalNeeds: <200ms validation, audit logging
Dependencies: Email service, existing auth system
Risks: User lockout, poor adoption rate
```

---

## 📞 Support

If you encounter issues or have questions: 
- Check the examples in `/examples` directory
- Review troubleshooting section above
- Open an issue in this repository

---

## 📄 License

[Your License Here]

---

**Made with ❤️ for better product documentation**