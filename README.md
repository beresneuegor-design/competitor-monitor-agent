# 🔍 Competitor Monitor Agent — n8n

> Scrapes competitor websites daily → detects changes → Groq AI analyzes what changed and why → sends intel report to Telegram.

![n8n](https://img.shields.io/badge/n8n-workflow-FF6B6B?style=flat-square)
![Groq](https://img.shields.io/badge/Groq-LLaMA%203.3%2070B-F55036?style=flat-square)
![Telegram](https://img.shields.io/badge/Telegram-Bot%20API-26A5E4?style=flat-square&logo=telegram)
![Google Sheets](https://img.shields.io/badge/Google%20Sheets-34A853?style=flat-square&logo=google-sheets)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

## ✨ What it does

Every day the agent:
1. **Scrapes** competitor websites (pricing, offers, homepage)
2. **Compares** with previous version stored in Sheets
3. **Detects** changes: new products, price updates, promotions
4. **Analyzes** with Groq AI: what changed, why it matters, what to do
5. **Sends** competitive intelligence report to Telegram

## 🏗️ Architecture

```
Schedule Trigger (7:00 AM daily)
        │
        ▼
┌──────────────┐
│ HTTP Request  │  scrapes competitor URLs
│ (for each)    │  extracts text content
└──────┬───────┘
       │
       ▼
┌──────────────┐
│  Code (JS)    │  compares with previous snapshot
│               │  detects what changed
└──────┬───────┘
       │
  ┌────┴────┐
  ▼         ▼
Changes   No changes
  │           │
  ▼           ▼
Groq AI    Skip
analyzes
  │
  ▼
┌──────────────┐
│ Google Sheets │  saves new snapshot
└──────┬───────┘
       │
       ▼
┌──────────────┐
│   Telegram    │  sends intel report
└──────────────┘
```

## 💡 Sample Report

```
🔍 Competitor Intel — 03.06.2025

⚡ CHANGES DETECTED: 2

1. competitor.pl — Pricing page
   Changed: Basic plan dropped from 299 PLN → 249 PLN
   Analysis: Likely responding to market pressure. Consider matching or emphasizing value-add.

2. rival-agency.pl — Homepage
   Changed: New hero text "AI automation in 48h"
   Analysis: Pushing faster delivery promise. Opportunity to compete on quality over speed.
```

## 🚀 Setup

1. Import `workflow.json` into n8n
2. Add competitor URLs to Google Sheets watchlist
3. Add credentials: Groq API, Google Sheets OAuth2, Telegram Bot
4. Set your Telegram chat ID
5. Activate — runs daily at 7:00 AM

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| Automation | n8n |
| Scraping | n8n HTTP Request node |
| AI Analysis | Groq — LLaMA 3.3 70B |
| Storage | Google Sheets (snapshots) |
| Alerts | Telegram Bot API |

---
*Built by [VinteliVision](https://vintelivision.com) — AI automation for Polish SMBs.*
