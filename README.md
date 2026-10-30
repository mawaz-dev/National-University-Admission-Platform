# 🎓 NUCAP – National University Admission Platform

**Built for the NUCAP Agentic AI Hackathon by Innovista**

A web platform that helps Pakistani students track university admission deadlines, calculate their merit, and find the universities that fit their academic profile. Admission data is collected automatically from university websites, so students don't have to check each site by hand.

![Next.js](https://img.shields.io/badge/Next.js-15-black?logo=next.js)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white)
![Tailwind](https://img.shields.io/badge/Tailwind-4-06B6D4?logo=tailwindcss&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-6-2D3748?logo=prisma)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Neon-336791?logo=postgresql&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green.svg)

---

## 💡 The Problem

Every year, many talented Intermediate (12th grade) students miss admission opportunities in Pakistan because:

- Information is scattered across many university websites with different layouts
- Deadlines, test dates, and merit criteria change often
- Students can't easily tell their chances or compare merit across universities

## ✅ The Solution

NUCAP centralizes admission information in one place, keeps it fresh with automated scraping, and gives each student a personalised view of their options.

## ✨ Features

### For Students
- 👤 **Academic Profile** – Store Matric and Intermediate marks, test scores, and preferences
- 🧮 **Merit Calculator** – University-specific merit formulas (NUST, FAST, COMSATS, Punjab University)
- 🎯 **University Matching** – Match score and admission chance (High / Good / Medium / Low) per university
- ⏰ **Deadline Dashboard** – Upcoming admission dates in one view
- 🏫 **University Explorer** – Browse universities and their departments
- 📅 **NUST Test Series Dates** – Registration and test dates exposed through a public API

### For Administrators
- 🔑 **Admin Panel** – Protected login for managing platform data
- 🏛️ **University & Department Management** – Add universities and their departments
- 📊 **Merit Lists** – Create and update merit lists per department
- 🗓️ **Admission Timeline** – Add deadlines and important dates

### Automation
- 🤖 **Scheduled Scraping** – A daily Vercel Cron job runs scrapers for NUST, FAST, and COMSATS
- 🧾 **Scraping Logs** – Every scrape run is logged for monitoring
- 🔄 **n8n Workflows** – Example n8n workflow definitions (`nust-scraper.json`, `gemini.json`, `deepseek.json`) for LLM-assisted data extraction

## 🧰 Tech Stack

| Layer | Technology |
|---|---|
| Framework | Next.js 15 (App Router), React 19 |
| Language | TypeScript |
| Styling / UI | Tailwind CSS 4, shadcn/ui, Radix UI, Lucide icons |
| Forms | React Hook Form + Zod |
| Auth | Clerk (students), cookie-based session (admin) |
| Database | PostgreSQL (Neon) with Prisma ORM |
| Scraping | Jina AI Reader + Cheerio |
| Hosting / Cron | Vercel |
| Testing | Jest, Testing Library, Playwright |

## 🗄️ Data Model

`User` · `StudentProfile` · `University` · `Department` · `MeritList` · `AdmissionTimeline` · `UniversityUpdate` · `StudentMatch` · `ScrapingLog` · `NustTestSeries`

See [`prisma/schema.prisma`](prisma/schema.prisma).

## 📁 Project Structure

```
├── prisma/                 # Schema, migrations, seed data
├── src/
│   ├── app/                # Pages and API routes
│   │   ├── dashboard/  matches/  profile/  universities/
│   │   ├── admin/          # Admin panel
│   │   └── api/            # student, admin, universities, cron, nust-dates
│   ├── components/ui/      # shadcn/ui components
│   ├── lib/                # Prisma client, merit calculator, admin auth
│   ├── services/scraper/   # Scraping manager + NUST / FAST / COMSATS scrapers
│   └── middleware.ts       # Clerk + admin route protection
├── scripts/                # Dev, DB, and scraper test scripts
├── __tests__/              # Jest unit, integration, security tests
├── tests/                  # Playwright E2E tests
└── vercel.json             # Daily cron schedule
```

## ⚙️ Getting Started

### Prerequisites

- Node.js 18+ (22 recommended)
- A PostgreSQL database (local, [Neon](https://neon.tech), Supabase, or Vercel Postgres)
- A [Clerk](https://clerk.com) application
- A [Jina AI](https://jina.ai) API key (for scraping)

### Installation

```bash
git clone https://github.com/saadkhantareen/pak-institutioner.git
cd pak-institutioner
npm install
```

### Environment Variables

Create a `.env.local` file in the project root:

```env
# Database
DATABASE_URL="postgresql://user:password@host:5432/nucap?schema=public"

# Clerk
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
CLERK_SECRET_KEY=your_clerk_secret_key

# Admin panel
ADMIN_USERNAME=your_admin_username
ADMIN_PASSWORD=your_strong_password
ADMIN_SESSION_TOKEN=a_long_random_string

# Scraping & cron
JINA_API_KEY=your_jina_api_key
CRON_SECRET=a_long_random_string

# App
NEXT_PUBLIC_BASE_URL=http://localhost:3000
```

### Database Setup

```bash
npm run db:generate   # Generate Prisma client
npm run db:migrate    # Run migrations
npm run db:seed       # Seed universities
```

### Run

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000). The admin panel is at `/admin`.

### Useful Commands

```bash
npm run build          # Production build
npm run db:studio      # Prisma Studio
npm test               # Jest tests
npm run e2e            # Playwright E2E tests
npx tsx scripts/test-scraper.ts NUST   # Try a scraper
```

See [QUICKSTART.md](QUICKSTART.md) for a step-by-step local setup.

## 🚢 Deployment

1. Push the repo to GitHub and import it in [Vercel](https://vercel.com)
2. Add the environment variables above
3. Run `npx prisma migrate deploy` against your production database
4. Set your production domain and redirect URLs in the Clerk dashboard

The daily scrape is configured in `vercel.json` and calls `/api/cron/scrape-universities`, which requires `Authorization: Bearer <CRON_SECRET>`.

## 🗺️ Roadmap

- [ ] More universities (the Punjab University scraper, then others)
- [ ] Email / SMS deadline reminders
- [ ] Historical merit trends and charts
- [ ] Urdu language support
- [ ] AI chat assistant for admission questions

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## 📄 License

This project is licensed under the MIT License.

## 👨‍💻 Author

**Saad Khan Tareen** – [@saadkhantareen](https://github.com/saadkhantareen)
