# 3. Feasibility Study

This document evaluates the practical viability of developing and deploying **PawPet** across technical, operational, economic, schedule, and legal dimensions.

## 1. Technical Feasibility

- **Technology Stack:**
  - **Frontend:** React with Vite for fast refresh and development.
  - **Backend:** GoLang with gin Web Framework for API server for record management and notification scheduling.
  - **Database:** PostgreSQL with GORM ORM for structured pet records and JSON health histories.
  - **Notifications:** 
    - Email notifications using SendGrid while testing and self-hosted SMTP in production.
    - Telegram notifications using Telegram Bot API.
    - SMS notifications using Twilio in production.
  - **Alert & Data Analysis:** PawPet uses simple rule-based data analysis rather than Artificial Intelligence (AI) or Machine Learning (ML) to identify upcoming or overdue pet-care tasks. The system analyzes stored dates and records, such as vaccination dates, medication schedules, and appointments, using predefined conditions and time intervals. For example, if a vaccination is due within a specified number of days, the system automatically generates an alert. This approach keeps the system lightweight, predictable, explainable, and inexpensive to operate.

- **Feasibility Assessment:** **High.** The underlying technology requirements (CRUD database operations, scheduled cron jobs, notification services) rely on standard, industry-proven stacks with low architectural risk.

## 2. Operational Feasibility

- **User Adoption:** Pet owners prioritize intuitive, low-friction interfaces. The application requires minimal input fields and clear visual cues for overdue tasks.
- **Maintenance & Support:** Simple database schema and modular API services keep operational overhead minimal for maintainers.
- **Feasibility Assessment:** **High.** The system directly addresses common pain points (forgotten vaccinations) with straightforward user interactions.

## 3. Economic Feasibility

- **Development Costs:** Open-source foundation reduces licensing fees to zero.
- **Infrastructure Costs:**
  - Database & Server hosting on standard tier cloud services (e.g., Render, Vercel, Supabase, or AWS free tiers).
  - Transactional notification delivery (SendGrid / Firebase Cloud Messaging) free tier accommodates initial user base.
- **Feasibility Assessment:** **Viable.** Initial development can be completed with minimal budget and scaled as active user count grows.

## 4. Schedule & Resource Feasibility

- **Estimated Development Timeline:** 4 to 6 weeks for core MVP release.
  - Weeks 1–2: Setup, DB Schema & User Authentication.
  - Weeks 3–4: Pet Profiles, Medical Records & File Attachments.
  - Weeks 5–6: Reminder Scheduler Engine, Testing & Deployment.
- **Feasibility Assessment:** **Achievable.** Scope is well-defined and split into discrete milestones.

## 5. Legal & Compliance Feasibility

- **Data Privacy:** Stores user emails and pet records. Complies with basic data privacy guidelines (GDPR / CCPA principles regarding account deletion and record export).
- **Medical Disclaimer:** Explicit user disclaimer stating PawPet is a tracking tool and not a substitute for licensed veterinary diagnosis.
- **Feasibility Assessment:** **Low Risk.** Legal requirements are manageable with standard privacy policy and disclaimers.

## 6. Feasibility Conclusion & Recommendation

**Verdict:** **Proceed to Development.**  
The PawPet project is technically achievable, operationally sound, economically viable, and carries minimal legal risk.
