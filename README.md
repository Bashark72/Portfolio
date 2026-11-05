# Bashar Kassum — AI Projects Portfolio

I build LLM-based agents, automations and integrations that real teams use every day: intake pipelines, RAG assistants, WhatsApp bots, and internal tools that take manual work off people's plates.

Stack I work in: Claude API, OpenAI API, Model Context Protocol (MCP), n8n, Make, Python, Next.js, Supabase, Docker.

Each project below has its own folder with a full write-up (problem → what I built → stack → result), an architecture diagram and screenshots or a demo.

---

## Projects

### 1. AI Invoice Intake for SAP Business One
**Status:** in development, tested on a first customer's real invoices, with an SAP integrator partner · **Role:** sole developer, end to end

Supplier invoices arrive as Hebrew PDFs and someone types them into SAP by hand. This multi-tenant SaaS extracts the invoice data with Claude, validates it the way an accountant would, matches the supplier to the company's SAP supplier list, and sends anything uncertain to a human review screen. Approved invoices go to the SAP integrator as a versioned JSON/XML contract, and the integrator creates the A/P invoice drafts in SAP B1.

- LLM extraction of header and line items into a strict, validated schema (header-field accuracy 100% on a real-invoice evaluation set)
- Israeli-specific validation (tax-ID check digits, VAT by date, totals, allocation numbers, duplicates) and supplier matching that learns from reviews
- Hebrew, right-to-left review UI; auto-approval only for clean invoices from known suppliers
- Integrator API (pull + acknowledge); the system itself never writes to SAP

**Stack:** TypeScript · Next.js · Node · PostgreSQL · Claude API · Supabase Auth · Docker

→ [Full write-up, architecture and demo](./sap-invoice-intake/)

---

### 2. Maps Board: Shift Assignment Dashboard (Oriient)
**Status:** deployed internally, handed over to Product · **Role:** self-initiated, designed and built solo

Every day, the mapping operations team at an indoor-positioning SaaS company has to split that day's site-mapping sessions between supervisors whose shifts start at different times, then track each session until it's done. I built the internal web app the team uses to plan and track the day.

- Drag-and-drop board with one column per supervisor on shift. A map can't be given to a supervisor whose shift hasn't started by the map's start time
- One-click distribution that respects shift times, spreads new mappers evenly and balances load
- Live updates on every open board, with server-enforced roles: supervisors can only update their own maps
- Weekly shift schedules, daily CSV import, CSV/Excel export, analytics and per-mapper completion times

**Stack:** TypeScript · Next.js · React · Supabase (Postgres, Auth, Realtime) · Tailwind CSS · dnd-kit · Vitest · Vercel

→ [Full write-up, architecture and screenshots](./oriient-ops-dashboard/)

---

### 3. WhatsApp Invoice Delivery Bot for SAP Business One
**Status:** in production · **Role:** sole developer

A business running SAP B1 was exporting invoice PDFs manually and sending each one to customers over WhatsApp. Now a message like "invoice 1042 for customer X" to a bot pulls the right invoice from SAP and delivers it to the customer on WhatsApp.

- Natural-language request parsing
- Invoice lookup and PDF retrieval from SAP B1
- Delivery via the WhatsApp Business API, with confirmation back to the sender
- Runs on self-hosted n8n (Docker) with secrets kept out of the workflow

**Stack:** n8n · WhatsApp Business API · SAP B1 Service Layer · Docker

→ [Full write-up and sanitized workflow](./whatsapp-invoice-bot/)

---

### 4. Tsevet: AI Teammates for Small Businesses
**Status:** working and in use by me, no paying clients yet · **Role:** founder and sole developer

Small business owners in Israel do their own follow-ups, quotes, posts and reminders, usually in Hebrew or Arabic. Tsevet gives them a team of named AI workers, each with a face and a job, in a Hebrew-first, right-to-left web chat. Workers hand tasks to each other, run recurring jobs and connect to Gmail, Calendar and Sheets. Nothing goes out until the owner approves it on a card.

- Multi-agent team: any worker can hand a task to any teammate, and the work continues on the server with the app closed
- Approval enforced by the server: workers hold no sending credentials, and the owner approves the exact recipient and text
- One isolated service and volume per client, tested with a second real client
- A shared memory the owner can read and delete, plus recurring jobs and a monthly usage cap

**Stack:** TypeScript · Next.js · React · Supabase (Postgres, Auth) · Python · Docker · Railway · MCP · a self-hosted agent runtime · a hosted LLM

→ [Full write-up, architecture and screenshots](./tsevet-ai-teammates/)

---

## Contact

bashar.uni1@gmail.com · [linkedin.com/in/bashar-kassum1](https://linkedin.com/in/bashar-kassum1)

Source code for the invoice intake system and Tsevet is private (both are commercial products); happy to walk through either on a call.
