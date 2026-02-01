# Quick Reference Guide
# Iranian Flower & Plant Information Platform

**Project Type:** Content Management System  
**Primary Language:** Persian/Farsi (RTL)  
**Target Market:** Iran  
**Version:** 1.0

---

## 🎯 Project Vision

Build **Iran's #1 digital resource** for flower and plant information with professional content management, SEO optimization, and collaborative workflows.

---

## 👥 User Roles & Permissions

| Role | Create Article | Edit Any Article | Approve/Reject | Manage Users | Manage Comments |
|------|---------------|------------------|----------------|--------------|-----------------|
| **Admin** | ✅ (immediate publish) | ✅ (immediate publish) | ✅ | ✅ | ✅ |
| **Writer** | ✅ (needs approval) | ✅ (needs approval) | ❌ | ❌ | ❌ (view only) |
| **Public** | ❌ | ❌ | ❌ | ❌ | ❌ (can submit) |

---

## 🔄 Core Workflows

### Workflow 1: Admin Creates Article
```
Admin → Create Article → Fill Details + SEO → Publish → Live Immediately
```

### Workflow 2: Writer Creates Article
```
Writer → Create Article → Submit for Review → Admin Reviews → Approve/Reject → If Approved: Live
```

### Workflow 3: Writer Edits Existing Article
```
Writer → Edit Article → Submit Revision → Admin Compares → Approve/Reject → If Approved: Changes Applied
```

### Workflow 4: Public Comment
```
Visitor → Read Article → Submit Comment → Pending Moderation → Admin Approves → Comment Visible
```

---

## 🎨 Main Features

### 1. Article Management System
- **CRUD Operations:** Full create, read, update, delete
- **Rich Text Editor:** Formatting, lists, headings, links
- **Image Management:** Multiple images per article
- **Categories:** Flowers, Trees, Shrubs, Herbs, Succulents, etc.
- **Tags:** Both predefined and custom
- **Draft Mode:** Save work in progress

### 2. SEO Optimization
- **Custom URLs:** Persian and Latin slug support
- **Meta Tags:** Title (60 chars), Description (160 chars), Keywords
- **Sitemap:** Auto-generated XML
- **Open Graph:** Social media sharing tags
- **Canonical URLs:** Prevent duplicate content
- **Structured URLs:** `/articles/category/slug` format

### 3. Revision Management
- **Version Control:** Full history of all edits
- **Side-by-Side Comparison:** See original vs. proposed changes
- **Approval Workflow:** Admin approve/reject/request changes
- **Notifications:** Writers notified of decisions
- **Audit Trail:** Who changed what when

### 4. Comment System
- **Public Submission:** Anyone can comment
- **Moderation Queue:** All comments start as "pending"
- **Admin Actions:** Approve, reject, edit, mark as spam
- **Spam Filter:** Basic keyword filtering
- **Comment Count:** Display per article

### 5. User Management
- **Identity Server:** JWT-based authentication
- **Role Assignment:** Admin or Writer
- **Account Operations:** Create, update, deactivate
- **Password Policy:** Strong passwords enforced
- **Login History:** Track user activity

### 6. Search Engine
- **Full-Text Search:** Title, content, tags
- **Persian Support:** Proper tokenization and stemming
- **Relevance Ranking:** Best matches first
- **Filters:** Category, date range, author
- **Autocomplete:** Search suggestions
- **Pagination:** 20 results per page

### 7. Responsive Design
- **Mobile:** 320px - 767px
- **Tablet:** 768px - 1024px  
- **Desktop:** 1025px+
- **RTL Support:** Right-to-left for Persian
- **Touch-Friendly:** 44x44px minimum targets
- **Responsive Images:** Appropriate sizes per device

---

## 🛠️ Technology Stack

### Backend
- **Language:** C# with ASP.NET Core
- **Authentication:** Identity Server (JWT)
- **Database:** SQL Server 2017+
- **ORM:** Entity Framework Core

### Frontend
- **Framework:** Razor Pages or MVC
- **CSS:** Bootstrap 5 or Tailwind CSS (RTL configured)
- **JavaScript:** Vanilla JS or minimal jQuery
- **Rich Editor:** TinyMCE or CKEditor

### Infrastructure
- **Hosting:** Azure App Service or IIS
- **File Storage:** Local FileSystem or Azure Blob
- **Search:** SQL Full-Text Search or Elasticsearch
- **Cache:** Redis (optional for performance)

---

## 📊 Database Schema (High-Level)

### Core Tables
- **Users:** UserId, Username, Email, PasswordHash, Role, IsActive
- **Articles:** ArticleId, Title, Content, Slug, CategoryId, AuthorId, PublishDate, Status
- **ArticleImages:** ImageId, ArticleId, FilePath, AltText, DisplayOrder
- **Categories:** CategoryId, Name, Slug, Description
- **Tags:** TagId, Name
- **ArticleTags:** ArticleId, TagId
- **Revisions:** RevisionId, ArticleId, AuthorId, Content, SubmitDate, Status, ReviewerId
- **Comments:** CommentId, ArticleId, AuthorName, AuthorEmail, Content, Status, SubmitDate
- **SEOMetadata:** ArticleId, MetaTitle, MetaDescription, Keywords, CanonicalUrl

---

## 🔌 API Endpoints (Quick Reference)

### Authentication
- `POST /api/auth/login` → Login
- `POST /api/auth/logout` → Logout
- `POST /api/auth/refresh` → Refresh token

### Articles
- `GET /api/articles` → List articles
- `GET /api/articles/{id}` → Get single article
- `POST /api/articles` → Create (Admin only)
- `PUT /api/articles/{id}` → Update
- `DELETE /api/articles/{id}` → Delete (Admin only)

### Revisions
- `GET /api/revisions` → List pending revisions
- `GET /api/revisions/{id}` → Get revision details
- `POST /api/revisions/{id}/approve` → Approve (Admin only)
- `POST /api/revisions/{id}/reject` → Reject (Admin only)

### Comments
- `GET /api/articles/{id}/comments` → Get article comments
- `POST /api/comments` → Submit comment
- `PUT /api/comments/{id}/approve` → Approve (Admin only)
- `PUT /api/comments/{id}/reject` → Reject (Admin only)

### Users
- `GET /api/users` → List users (Admin only)
- `POST /api/users` → Create user (Admin only)
- `PUT /api/users/{id}` → Update user (Admin only)

### Search
- `GET /api/search?q={query}` → Search articles

---

## 📈 Performance Targets

| Metric | Target |
|--------|--------|
| Page Load Time | < 2 seconds (95th percentile) |
| Search Response | < 500ms |
| Image Upload | < 5 seconds (5MB files) |
| Concurrent Users | 1,000 without degradation |
| API Response | < 200ms (90th percentile) |

---

## 🔒 Security Requirements

- ✅ HTTPS only (TLS 1.2+)
- ✅ Password hashing (bcrypt)
- ✅ CSRF protection
- ✅ XSS prevention (input sanitization)
- ✅ SQL injection prevention (parameterized queries)
- ✅ Rate limiting (login: 5 per 15 min, comments: 3 per hour)
- ✅ File upload validation (type, size)
- ✅ Security headers (CSP, X-Frame-Options)
- ✅ Audit logging

---

## 📋 MVP Feature Checklist

### Phase 1: Core Platform (Must Have)
- [ ] User authentication & authorization
- [ ] Admin panel with user management
- [ ] Article CRUD operations
- [ ] Rich text editor
- [ ] Image upload
- [ ] Category & tag system
- [ ] Basic SEO fields (slug, meta tags)

### Phase 2: Workflow (Must Have)
- [ ] Revision system for edits
- [ ] Approval workflow
- [ ] Side-by-side comparison
- [ ] Notifications
- [ ] Comment system with moderation

### Phase 3: Discovery (Must Have)
- [ ] Full-text search (Persian)
- [ ] Search filters
- [ ] Pagination
- [ ] Related articles

### Phase 4: Polish (Should Have)
- [ ] Responsive design (all devices)
- [ ] RTL support
- [ ] Performance optimization
- [ ] Caching
- [ ] XML sitemap

### Phase 5: Analytics (Nice to Have)
- [ ] View counts
- [ ] Admin dashboard metrics
- [ ] Writer statistics
- [ ] Search analytics

---

## 🎯 Success Metrics (KPIs)

| KPI | Target | Timeline |
|-----|--------|----------|
| Monthly Active Users | 10,000 | 6 months |
| Published Articles | 500+ | 12 months |
| Revision Approval Rate | 80%+ | Ongoing |
| Page Load Time | < 2s | Launch |
| System Uptime | 99.5%+ | Ongoing |
| Search Success Rate | 50%+ | 3 months |
| Organic Traffic Growth | +20% MoM | Ongoing |

---

## ⚠️ Key Risks

1. **Writer Content Quality** → Mitigation: Strict review process, training
2. **Revision Bottleneck** → Mitigation: Adequate admin staffing, SLA
3. **Persian Search Complexity** → Mitigation: Specialized libraries, testing
4. **Scalability** → Mitigation: Cloud infrastructure, load testing
5. **Security** → Mitigation: OWASP practices, security audit

---

## 📅 Project Timeline Estimate

| Phase | Duration | Description |
|-------|----------|-------------|
| Setup | 1 week | Environment, repo, CI/CD |
| Phase 1 | 3-4 weeks | Core platform & auth |
| Phase 2 | 3-4 weeks | Workflows & moderation |
| Phase 3 | 2-3 weeks | Search & discovery |
| Phase 4 | 2-3 weeks | Responsive & polish |
| Testing | 2 weeks | QA, security, performance |
| **Total** | **13-17 weeks** | *~3-4 months* |

---

## 📚 Documentation Deliverables

- [x] Product Requirements Document (Full)
- [x] Persian Summary (For local stakeholders)
- [x] Quick Reference Guide (This document)
- [ ] Technical Architecture Document
- [ ] API Specification (OpenAPI/Swagger)
- [ ] Database Schema Diagram
- [ ] Admin User Guide
- [ ] Writer User Guide
- [ ] Deployment Runbook

---

## 🔗 Related Documents

- **Full PRD:** `iranian-plant-blog-prd.md`
- **Persian Summary:** `iranian-plant-blog-prd-summary-fa.md`
- **PRD Template:** `../templates/prd-template.md`
- **Example Input:** `input-example.md`

---

**Status:** ✅ Ready for Review  
**Next Step:** Technical architecture planning and team assignment

---

*Last Updated: 2026-02-01*
