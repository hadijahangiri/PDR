# Thesis Defense Management System - PRD Summary

## Quick Reference

**Document:** Thesis-Defense-Management-System-PRD.md  
**Date:** January 7, 2026  
**Status:** Complete

## What Was Created

A comprehensive Product Requirements Document (PRD) for a university thesis defense management system based on the Persian/Farsi requirements provided.

## System Overview

A web-based management panel for university administration to:
- Manage professors and students with role-based access
- Track thesis defenses with detailed parameters
- Automatically calculate professor compensation
- Handle financial transfers to professor accounts
- Provide filtering and reporting capabilities

## Key Features

### 1. User Management (3 Roles)
- **Manager/Administrator (مدیریت)** - Full system access
- **Professor (استاد)** - View own records and payments
- **Student (دانشجو)** - View own thesis defense info

### 2. Professor Management
Fields: Name, National ID, Professor Code, Bank Account, Password (auto-set to National ID), Status, Role

### 3. Student Management
Fields: Name, National ID, Password (auto-set to National ID), Status, Role

### 4. University Management
Field: University Name

### 5. Academic Rank Management
Fields: Rank Name, Supervision Percentage (درصد پایش)

### 6. Thesis Defense Management
Complete defense record with:
- Professor selection (active only)
- Student selection (active only)
- University selection
- Defense date (Persian calendar)
- Cooperation type (الف / ب / مدعو)
- Academic rank
- Grade (پایه)
- Thesis type (ارشد / دکتری)
- Unit count (4 / 6)
- Position (راهنما / مشاور / داور / ناظر)
- Participation level (0.5 / 1)
- Postal service status (دارد / ندارد)
- **Auto-calculated compensation amount**

### 7. Comprehensive Table & Filtering
Displays all defense records with filtering on all 16+ columns:
- Professor details (name, national ID, code, bank account)
- Student name
- Faculty workplace
- Defense date
- All thesis defense parameters
- Supervision percentage
- Compensation amount
- Payment status

### 8. Financial Management
- Track pending payments
- Process transfers to professor accounts
- Monitor payment status
- Transaction history

## Document Structure

The PRD includes all required sections:

1. **Overview** - Summary, problem statement, goals
2. **Scope & Out of Scope** - Clear boundaries
3. **User Personas & Use Cases** - 9 detailed use cases
4. **Functional Requirements** - 40 specific requirements (FR-1 to FR-40)
5. **Non-Functional Requirements** - Performance, security, reliability, UX
6. **Integration & API Hints** - 18 API endpoints with specs
7. **Analytics & Success Metrics** - KPIs and measurements
8. **Risks & Open Questions** - 5 risks with mitigation, 12 open questions
9. **Acceptance Criteria** - 43 testable criteria
10. **Technical Architecture** - Recommended tech stack and database schema
11. **Appendix** - Persian-English terminology mapping (34 terms)

## Technical Recommendations

### Suggested Stack
- **Backend:** Python + Django/FastAPI
- **Database:** PostgreSQL 14+
- **Frontend:** React/Vue.js with RTL support
- **Date Handling:** Persian calendar library (persiantools/moment-jalaali)
- **Authentication:** JWT-based
- **UI Framework:** Material-UI or Ant Design (RTL support)

### Key Technical Requirements
- Full Persian/Farsi language support
- Right-to-left (RTL) text direction
- Persian (Jalali/Shamsi) calendar integration
- Secure password hashing (bcrypt)
- Encrypted bank account storage
- Role-based access control
- Comprehensive audit logging
- Automated compensation calculation engine

## Use Cases Covered

1. Create professor account
2. Create student account
3. Define university
4. Define academic rank
5. Create thesis defense record
6. Filter and view thesis defense records
7. Manage financial transfers
8. Professor views personal records
9. Student views thesis defense info

## Key Metrics & KPIs

- **Primary KPI:** 70% reduction in administrative time
- **Financial KPI:** 100% payments processed within 30 days
- **Accuracy KPI:** 99% compensation calculation accuracy
- **Adoption KPI:** 80% professor registration in 6 months
- **System Usage KPI:** 95% of defenses recorded in system

## Important Notes

### Security Considerations
- Bank account numbers encrypted at rest
- Passwords hashed with bcrypt
- National IDs validated and sanitized
- Role-based access enforced
- Audit logs for all financial transactions
- Session timeout after 24 hours

### Compensation Calculation
The system automatically calculates compensation based on multiple factors:
- Cooperation type
- Academic rank & supervision percentage
- Grade level
- Thesis type (Master's/Doctorate)
- Unit count (4/6)
- Position (Supervisor/Advisor/Examiner/Observer)
- Participation level (0.5/1)
- Postal service status

**Note:** Exact calculation formula needs to be defined with stakeholders.

### Persian Calendar Integration
- All dates displayed in Persian (Jalali/Shamsi) calendar
- Date picker for defense date selection
- Support for year boundaries and leap years
- Validation of date ranges

## Next Steps

1. **Review with Stakeholders**
   - University administration
   - IT department
   - Finance department
   - Academic affairs

2. **Define Exact Compensation Formula**
   - Get precise calculation rules
   - Define base rates
   - Clarify multipliers and factors

3. **Answer Open Questions** (12 identified in PRD)
   - Approval workflow
   - Integration requirements
   - Report specifications
   - Permission levels

4. **Technical Planning**
   - Architecture design
   - Database schema finalization
   - API specification
   - Security review

5. **Development Phases**
   - Phase 1: User management & authentication
   - Phase 2: Basic entity management (universities, ranks)
   - Phase 3: Thesis defense records
   - Phase 4: Financial management
   - Phase 5: Reporting & analytics

## Files Created

1. **Thesis-Defense-Management-System-PRD.md** (35KB, 686 lines)
   - Complete PRD document
   - All sections included
   - Ready for stakeholder review

2. **PRD-Summary.md** (this file)
   - Quick reference guide
   - Key highlights
   - Next steps

## Contact & Questions

For questions about this PRD or to request modifications, contact the product team.

---

**Created by:** PRD Generator Agent  
**Date:** January 7, 2026  
**Repository:** hadijahangiri/PDR
