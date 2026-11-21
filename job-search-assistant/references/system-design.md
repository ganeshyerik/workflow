# Build plan and access map

## Suggested system

Build in stages rather than trying to automate every job board at once.

### Stage 1: Career evidence and resume repair

- Keep a master career profile as structured facts: roles/dates, scope, technologies actually used, project examples, verified metrics, certifications, and approved personal details.
- Store each fact with a source and verification status (confirmed, needs confirmation, not for use).
- Produce a clean ATS-friendly master resume and a distinct target resume per role family (for example, senior backend/platform and engineering lead, if those match the candidate's goals).
- Validate PDF text extraction and visual rendering; keep an editable source (DOCX or equivalent) alongside exported PDF.

### Stage 2: Search and shortlist

- Use saved searches, company career pages, and job-board notifications or official APIs where available. Prefer job links the candidate can open and apply to directly.
- Parse the description into must-haves, preferred skills, scope/seniority, domain, location, compensation if listed, and application questions.
- Rank by constraints and evidence-backed fit. Surface a small shortlist with reasons and gaps, not a stream of raw postings.
- Track every role in a local spreadsheet or simple database to avoid duplicate applications and enable funnel analysis.

### Stage 3: Tailor and prepare

- Generate a role-specific resume and cover letter from verified facts; report which facts were emphasized and which requirements remain unsupported.
- Generate suggested application answers from an approved answer bank. Ask the candidate whenever an answer is missing or sensitive.
- Save a preview packet and wait for the candidate to approve submission.

### Stage 4: Apply, communicate, and follow up

- Start with user-in-the-loop applications: open the employer application page, prefill only where permitted, then let the candidate inspect and submit.
- Keep recruiter emails as drafts. Approval should show the exact recipient, message, attachments, and destination before sending.
- Ingest replies only if the candidate explicitly connects an inbox and selects the permitted access. For an initial design, use send-only or draft-only access; inbox read access is optional and broader.
- Add calendar access only if the candidate wants interview holds/invitations managed. Start read-only and require approval to create, accept, or modify events.

## Access and plugin recommendations

1. **No connector required for the first MVP.** Use the resume, job links, a local tracker, and user approval. This avoids granting broad account access before the workflow proves useful.
2. **Email:** connect Gmail or Outlook only for drafting/sending recruiter communication. Prefer draft or send capability with the narrowest permissions available. Do not grant mailbox-wide read/delete access just to send a message.
3. **Calendar:** connect Google Calendar or Outlook Calendar only when interview scheduling becomes a real need; read availability first, request approval for event changes.
4. **Job sources:** use official job alerts, company career pages, or supported APIs. LinkedIn, Indeed, and ATS sites have differing terms and anti-bot controls; do not scrape behind login or automate around CAPTCHA/rate limits. Install a connector only if it officially supports the specific read or write action needed.
5. **LLM/API key (if building a standalone app):** keep the key in a server-side secret store, never in browser code or a resume file. Send only the minimum resume/job text needed, set retention deliberately, and allow deletion/export of the profile.

## Example architecture

- **Profile store:** encrypted local database or private cloud database for verified facts, preferences, and answer bank.
- **Ingestion:** user-pasted URL or approved job feed; extract page text without bypassing access controls.
- **Matcher:** deterministic hard filters plus an explainable fit score; model output is advisory.
- **Document generator:** DOCX template + PDF export; include a claim-to-source audit so every bullet maps to career evidence.
- **Workflow engine:** states such as Found → Reviewed → Tailoring → Ready for approval → Submitted → Replied → Interview.
- **Integrations:** separate least-privilege adapters for mail, calendar, and job feeds.
- **Audit trail:** record when a resume version was generated, what was submitted, and who approved the action.

## Resume-specific improvements to verify

- Resolve 12+ years on the resume versus 13 years stated by the candidate; calculate from verified start/end months.
- Confirm that every metric (200K+ daily applications, 99.95% availability, 10K requests/second, percentage improvements, user/adoption counts) is accurate, attributable, and explainable.
- Prioritize senior backend/platform/cloud leadership roles unless the candidate confirms a different goal. Current skills span several job families and can dilute positioning.
- Separate hands-on engineering from architecture/mentoring scope. Add team size, design ownership, production scale, budget/cost impact, and decision-making scope only where facts support it.
- Confirm exact titles, employment dates, project naming/permission to disclose, certifications and current status. Clarify the odd migration phrase in the Deloitte entry and any wording the PDF extraction mangles.
- Consider reducing the long technology inventory to core, recent, defensible skills; move older or occasional tools out of the headline skill groups.
- Quantify the 3-year search period with role targets, application/interview counts, and where the funnel stalls. If the resume is not getting interviews, improve role targeting and evidence/positioning before increasing application volume.

## Initial search target

- Location: Hyderabad.
- Compensation priority: maximize total compensation, prioritizing meaningful bonus and publicly traded stock/RSUs in addition to high fixed pay. Retain ₹45 LPA as the minimum fixed-pay goal; compare offers by fixed pay, target/guaranteed variable, equity grant and vesting schedule, and benefits as separate components. Verify compensation with the recruiter because current postings frequently omit it.
- Notice period: 60 days.
- Role scope: senior software engineer, staff/associate staff, IC, tech lead, manager, or architect are all acceptable to the candidate.
- Search these as distinct role families and tailor a separate application version for each. Prioritize senior/staff backend/platform/cloud IC, technical lead, and architect roles from the resume evidence. The candidate has juniors reporting to them but has not conducted performance reviews; present this as technical leadership/mentoring, not full people-management responsibility. Include engineering manager roles only when job expectations match verified scope; do not imply performance-management experience.
- Do not silently broaden beyond Hyderabad or lower the ₹45 LPA goal. If few roles meet the filter, show near-matches separately and ask before changing constraints.

## Candidate-confirmed technical evidence to validate and phrase

- The candidate describes building scalable applications and handling applications at about 4K TPS using Redis caching and a NoSQL database for aggregated reports. They describe storing/reusing those reports in NoSQL to reduce RAM pressure rather than relying on cache alone. Confirm the exact architecture and whether 4K TPS is sustained, peak, or a benchmark before writing a resume bullet.
- For availability/reliability, the candidate cites FMEA, resilient configurations, and testing. Ask for the system's availability/SLO, incident or failure reduction, and a concrete example before retaining the resume's 99.95% availability or 30% reliability-improvement figures.
- Reconcile the existing resume's ~10K req/s statement with the candidate's 4K TPS description. They may refer to different systems or measurement types; do not combine or substitute without confirmation.

## Information needed to personalize the automation

- Target titles and whether individual contributor, tech lead, architect, or engineering manager is preferred.
- Target countries/cities, remote/hybrid/on-site preferences, and relocation/visa constraints.
- Compensation range, notice period, and any industries/companies to include or exclude.
- Job sources and accounts to connect, if any; desired applications per week.
- Whether the candidate wants all applications to remain approval-gated (recommended initially) and what types of routine follow-up may be sent after per-action approval.
- Verified career details and a source/editable resume. Do not provide passwords or one-time codes; connect accounts through official OAuth permission screens.

