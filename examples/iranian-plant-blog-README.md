# Iranian Flower & Plant Platform - PRD Example

This directory contains a complete Product Requirements Document (PRD) example for a comprehensive flower and plant information platform targeting the Iranian market.

## 📁 Files in This Example

### 1. `iranian-plant-blog-prd.md` (38 KB)
**The Complete PRD** - Full product requirements document in English

This is the main, comprehensive document containing:
- Detailed overview and business goals
- Complete scope definition
- 9 detailed use cases with flows
- 62 functional requirements
- 38 non-functional requirements
- API endpoint specifications
- Success metrics and KPIs
- Risk analysis
- Complete acceptance criteria

**Best for:** Developers, architects, QA teams, project managers

---

### 2. `iranian-plant-blog-prd-summary-fa.md` (15 KB)
**Persian Language Summary** - خلاصه فارسی

A comprehensive summary in Persian (Farsi) with RTL support containing:
- Executive summary (خلاصه اجرایی)
- Key features explanation (ویژگی‌های کلیدی)
- User roles and workflows (نقش‌ها و گردش کار)
- Technical architecture (معماری فنی)
- Success metrics (معیارهای موفقیت)
- Acceptance criteria (معیارهای پذیرش)

**Best for:** Persian-speaking stakeholders, business owners, Iranian team members

---

### 3. `iranian-plant-blog-quick-reference.md` (9.3 KB)
**Quick Reference Guide** - Fast lookup for developers

A concise, scannable reference containing:
- User roles matrix
- Core workflows (visual flow diagrams)
- Feature checklist
- Technology stack
- API endpoints quick reference
- Database schema overview
- Performance targets
- Security requirements
- MVP phase breakdown
- Project timeline estimate

**Best for:** Quick lookups, onboarding new team members, sprint planning

---

## 🎯 Project Overview

**What:** A content management platform to become Iran's primary digital resource for flower and plant information.

**Key Features:**
- Admin panel with full management capabilities
- Writer panel with article creation and editing
- SEO-optimized article system
- Revision approval workflow
- Comment moderation system
- Internal search engine
- Responsive design with RTL support

**Tech Stack:**
- Backend: ASP.NET Core (C#)
- Auth: Identity Server
- Database: SQL Server
- Frontend: Razor Pages/MVC

---

## 📖 How to Use These Documents

### For Project Kickoff
1. Start with `iranian-plant-blog-quick-reference.md` to get the big picture
2. Read `iranian-plant-blog-prd.md` sections 1-3 for context
3. Share `iranian-plant-blog-prd-summary-fa.md` with Persian-speaking stakeholders

### For Development
1. Reference `iranian-plant-blog-prd.md` sections 4-6 for detailed requirements
2. Use `iranian-plant-blog-quick-reference.md` for API and database schema
3. Follow acceptance criteria in section 9 for definition of "done"

### For Sprint Planning
1. Use MVP checklist in quick reference guide
2. Break down functional requirements (FR-1 through FR-62) into user stories
3. Prioritize based on acceptance criteria

### For QA/Testing
1. Use acceptance criteria (section 9) as test scenarios
2. Reference use cases (section 3) for flow testing
3. Check non-functional requirements (section 5) for performance/security tests

---

## 🎓 Learning from This Example

This PRD example demonstrates:

### ✅ Good PRD Practices
- **Clear Structure:** Organized into 9 standard sections
- **Actionable Requirements:** Every FR/NFR is testable
- **Complete Use Cases:** Pre-conditions, post-conditions, flows, error handling
- **Risk Mitigation:** Each risk has concrete mitigation strategies
- **Measurable Success:** Specific KPIs with targets and timelines

### 🎯 Key Takeaways
1. **Personas First:** Define who will use the system before what they'll do
2. **Workflows Matter:** Visual flows help everyone understand the system
3. **Be Specific:** "Fast" is vague; "< 2 seconds" is testable
4. **Consider All Users:** Admin, Writer, and Public all have different needs
5. **RTL is Critical:** For Persian/Arabic languages, RTL isn't optional
6. **SEO from Start:** Built into requirements, not added later
7. **Security by Design:** Security requirements upfront, not retrofitted

### 💡 Reusable Patterns
- **Approval Workflow:** Writer → Pending → Admin Review → Approved/Rejected
- **Comment Moderation:** Submit → Pending → Admin Review → Visible
- **Role-Based Access:** Clearly defined permissions per role
- **Revision System:** Track changes, compare versions, rollback capability
- **Multi-language:** RTL support, proper text handling

---

## 🔄 Using This as a Template

To adapt this example for your own project:

1. **Replace the Domain:** Change "flowers and plants" to your domain
2. **Adjust Roles:** Modify Admin/Writer to match your user types
3. **Customize Features:** Keep/remove/add features as needed
4. **Update Tech Stack:** Change ASP.NET to your preferred stack
5. **Adapt Language:** Change Persian/RTL to your target language

---

## 📊 Project Stats

| Metric | Value |
|--------|-------|
| Total Functional Requirements | 62 |
| Total Non-Functional Requirements | 38 |
| Use Cases Detailed | 9 |
| API Endpoints Specified | 24+ |
| Database Tables (High-Level) | 10+ |
| Estimated Timeline | 13-17 weeks |
| Target KPIs | 8 |

---

## 🤝 Contributing

If you find this example helpful and want to improve it:
1. Fork the repository
2. Make your improvements
3. Submit a pull request
4. Share feedback in issues

---

## 📞 Questions?

- **About the PRD format:** Check `/templates/prd-template.md`
- **About the agent:** See main `README.md`
- **About this example:** Open an issue in the repository

---

## 📝 Version History

- **v1.0** (2026-02-01) - Initial release with full PRD, Persian summary, and quick reference

---

**Created by:** PRD Generator Agent  
**Repository:** [hadijahangiri/PDR](https://github.com/hadijahangiri/PDR)

---

*Use these documents as a reference for creating your own high-quality PRDs!*
