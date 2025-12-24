# Example Input for PRD Generator

Use this format when requesting a PRD from the agent:

---

**FeatureName:** Two-Factor Authentication (2FA)

**ProductContext:** SaaS Web Application - User Authentication System

**Description:** Add an optional two-factor authentication layer to enhance account security. Users can enable 2FA using authenticator apps (like Google Authenticator or Authy) that generate time-based one-time passwords (TOTP).

**TargetUsers:** 
- End users who want to secure their accounts
- Enterprise customers who require enhanced security
- System administrators managing user accounts

**MainUseCases:**
1. User enables 2FA on their account for the first time
2. User logs in with username/password and then enters 2FA code
3. User disables 2FA (with proper verification)
4. User loses access to their 2FA device and needs recovery
5. Admin views which users have 2FA enabled
6. User generates backup recovery codes

**TechStack:** 
- Backend: Python 3.11 + FastAPI
- Database: PostgreSQL 15
- Frontend: React 18 + TypeScript
- Authentication: JWT tokens
- 2FA Library: pyotp (Python TOTP library)

**Constraints:**
- Must be implemented within 3 sprints (6 weeks)
- Must work with existing JWT-based authentication system
- Cannot break existing login flows for users without 2FA
- Must comply with GDPR for storing user security data
- Recovery codes must be securely hashed

**EdgeCases:**
- User tries to enable 2FA but QR code fails to scan
- User enters valid password but 2FA code expires during entry
- User has 2FA enabled but loses their device
- System clock drift causes TOTP validation issues
- User tries to reuse an old 2FA code
- Account lockout after multiple failed 2FA attempts

**NonFunctionalNeeds:**
- **Performance:** 2FA validation must complete within 200ms
- **Security:** Recovery codes must be hashed with bcrypt; QR codes should expire after 10 minutes
- **Observability:** Log all 2FA enable/disable events and failed attempts
- **Scalability:** Must handle 10,000 concurrent 2FA validations
- **Usability:** Setup process should take less than 2 minutes

**Dependencies:**
- Existing User Authentication Service (v2.3)
- Email Service for sending recovery codes
- Audit Logging Service

**Risks:**
- Users may lose access to their accounts if they lose both their device and recovery codes
- Increased support burden for account recovery requests
- Potential user friction if 2FA setup is too complex
- Time estimation might be tight given existing team capacity