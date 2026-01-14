# 📚 Bilingual Group Progress Report

<p align="center">
  <img src="https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white" alt="Next.js"/>
  <img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI"/>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript"/>
  <img src="https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white" alt="LangChain"/>
  <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL"/>
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker"/>
</p>

<p align="center">
  <strong>An AI-powered system for automating bilingual (English & Mandarin) progress reports for preschools</strong>
</p>

<p align="center">
  EtonHouse International School × Singapore Institute of Technology AAI ITP Project
</p>

---

## 🎯 Overview

Teachers capture rich learning evidence through photos, videos, and observations, but transforming this into meaningful reports for parents is manual and time-consuming. **Bilingual Group Progress Report** is an AI-assisted workflow that automatically compiles class-level newsletters every two weeks, freeing teachers' time while delivering consistent, bilingual updates to families.

### The Challenge

- 📸 Teachers capture extensive learning evidence but reporting remains manual
- 👨‍👩‍👧 Families want concise, bilingual snapshots aligned to learning domains
- ⏰ Report generation is time-consuming and inconsistent across classes

### Our Solution

An intelligent automation platform that transforms rough teacher notes and media into professionally formatted, bilingual progress reports with human-in-the-loop quality control.

---

## ✨ Key Features

### 🤖 Intelligent Automation

| Feature | Description | Technology |
|---------|-------------|------------|
| **Bilingual Generation** | Instantly transforms rough teacher notes into English & Mandarin captions while preserving educational content | LLM / LangChain |
| **Smart Media Tagging** | Auto-categorizes uploaded media by activity type (e.g., "Numeracy", "Outdoor Play") to save sorting time | Computer Vision |

### 👩‍🏫 Teacher Workflow

| Feature | Description | Technology |
|---------|-------------|------------|
| **Visual Editor** | Dashboard to review AI drafts, swap images, and edit text before publishing | Next.js / React |
| **One-Click Publishing** | Generates high-fidelity, branded PDFs ready for parents, matching school design guidelines | Playwright PDF Engine |

### 🔒 Enterprise Safety

| Feature | Description | Technology |
|---------|-------------|------------|
| **Seamless Integration** | Connects directly to existing storage (OneDrive/SharePoint) and syncs rosters from Kagami | REST API |
| **Privacy Architecture** | Strict Role-Based Access Control and automated scripts ensuring raw footage deletion post-generation | Auto-Delete / Audit Logs |

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                 Docker Compose / Swarm (Application Deployment)          │
│  ┌─────────────────────┐    ┌─────────────────────────────────────────┐ │
│  │  Frontend Container │    │         Backend API Container           │ │
│  │  (Next.js/TypeScript│    │           (FastAPI/Python)              │ │
│  │                     │    │  ┌─────────────┬─────────────────────┐  │ │
│  │  • Dashboard UI     │◄──►│  │ API         │ AI/ML Logic         │  │ │
│  │  • Editorial        │    │  │ Endpoints   │ (LangChain)         │  │ │
│  │    Controls         │    │  ├─────────────┼─────────────────────┤  │ │
│  │                     │    │  │ PDF         │ Kagami Sync         │  │ │
│  │                     │    │  │ Generator   │ Adapter             │  │ │
│  └─────────────────────┘    │  │ (Playwright)│                     │  │ │
│                             │  └─────────────┴─────────────────────┘  │ │
│                             └──────────┬───────────────┬──────────────┘ │
└────────────────────────────────────────┼───────────────┼────────────────┘
                                         │               │
                    ┌────────────────────┘               └────────────────┐
                    ▼                                                     ▼
           ┌───────────────┐                                    ┌─────────────────┐
           │   PostgreSQL  │                                    │  Cloud Storage  │
           │   Database    │                                    │  (EtonHouse     │
           │               │                                    │   S3/OneDrive)  │
           └───────────────┘                                    └─────────────────┘
                                                                         │
                    ┌────────────────────────────────────────────────────┤
                    ▼                                                    ▼
           ┌───────────────┐                                    ┌───────────────┐
           │ External AI   │                                    │  Kagami SMS   │
           │ Service       │                                    │  (Legacy)     │
           │ (OpenAI)      │                                    │               │
           └───────────────┘                                    └───────────────┘
```

---

## 🛠️ Tech Stack

### Frontend
- **Framework**: Next.js 14 with TypeScript
- **Styling**: Tailwind CSS
- **State Management**: React Context / Zustand

### Backend
- **API Framework**: FastAPI (Python)
- **AI/ML**: LangChain, OpenAI GPT-4
- **Computer Vision**: Custom CV models for activity classification
- **Task Queue**: Celery with Redis
- **PDF Generation**: Playwright

### Infrastructure
- **Database**: PostgreSQL
- **Containerization**: Docker Compose / Docker Swarm
- **Cloud Storage**: Integration with SharePoint/OneDrive/Google Drive
- **External Systems**: Kagami SMS (roster sync)

---

## 📁 Project Structure

```
bilingual-progress-report/
├── frontend/                   # Next.js application
│   ├── app/                    # App router pages
│   ├── components/             # React components
│   │   ├── dashboard/          # Dashboard UI components
│   │   ├── editor/             # Visual editor components
│   │   └── ui/                 # Shared UI components
│   ├── lib/                    # Utility functions
│   └── public/                 # Static assets
│
├── backend/                    # FastAPI application
│   ├── api/                    # API endpoints
│   │   ├── routes/             # Route handlers
│   │   └── deps.py             # Dependencies
│   ├── core/                   # Core configurations
│   ├── models/                 # Database models
│   ├── services/               # Business logic
│   │   ├── ai/                 # AI/ML services
│   │   │   ├── bilingual.py    # Bilingual generation
│   │   │   ├── tagging.py      # Smart media tagging
│   │   │   └── curriculum.py   # Curriculum mapping
│   │   ├── pdf/                # PDF generation
│   │   └── integrations/       # External integrations
│   │       ├── kagami.py       # Kagami sync adapter
│   │       └── storage.py      # Cloud storage connector
│   └── workers/                # Celery tasks
│
├── docker/                     # Docker configurations
│   ├── Dockerfile.frontend
│   ├── Dockerfile.backend
│   └── docker-compose.yml
│
├── scripts/                    # Utility scripts
│   ├── auto_delete.py          # Media auto-deletion
│   └── audit_log.py            # Audit logging
│
└── docs/                       # Documentation
    ├── API.md
    └── DEPLOYMENT.md
```

---

## 🚀 Getting Started

### Prerequisites

- Node.js 18+
- Python 3.10+
- Docker & Docker Compose
- PostgreSQL 15+

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/bilingual-progress-report.git
   cd bilingual-progress-report
   ```

2. **Set up environment variables**
   ```bash
   cp .env.example .env
   # Edit .env with your configuration
   ```

3. **Start with Docker Compose**
   ```bash
   docker-compose up -d
   ```

4. **Or run locally for development**
   
   Frontend:
   ```bash
   cd frontend
   npm install
   npm run dev
   ```
   
   Backend:
   ```bash
   cd backend
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   uvicorn main:app --reload
   ```

5. **Access the application**
   - Frontend: http://localhost:3000
   - API Documentation: http://localhost:8000/docs

---

## 🔐 Security & Privacy

Our system is designed with **privacy-first architecture**:

| Risk | Level | Mitigation Strategy |
|------|-------|---------------------|
| **Data Privacy & Leakage** | 🔴 High | Zero-retention policy for raw footage. Automated scripts delete media 24h after publication. Role-based access ensures class isolation. |
| **Kagami Integration Failure** | 🟡 Medium | Fallback design pattern with manual CSV drag-and-drop support. |
| **AI Hallucinations** | 🟡 Medium | Human-in-the-loop workflow. AI never auto-publishes; teachers must review and approve every generation. |

### Privacy Features
- 🔒 Strict Role-Based Access Control (RBAC)
- 🗑️ Automated media deletion post-publication
- 📝 Comprehensive audit logging
- 🚫 "No-Photo List" support for student exclusions
- 🔐 Integration with existing security infrastructure

---

## 📅 Project Timeline

| Phase | Duration | Activities |
|-------|----------|------------|
| **Discovery & Scoping** | Month 1 | On-site workflow observation, Kagami data structure mapping, storage permissions audit |
| **Core Development** | Months 2-5 | Next.js Dashboard, Python AI Engine, Kagami integration, secure "Drop Box" setup |
| **User Testing & Pilot** | Months 6-7 | Single centre deployment, real-scenario testing, AI prompt refinement |
| **Final Handover** | Month 8 | Security audit, documentation delivery, full system rollout |

---

## 👥 Team

| Role | Members | Responsibilities |
|------|---------|------------------|
| **Full Stack Engineer** | Zulfaqar Hafez, Royston Teo, Shawn Lim | Teacher Dashboard UI, Editorial Approval Workflow, PDF Generation Engine |
| **AI Engineer** | Max Tan, Daniel Chua | Bilingual Prompt Engineering, Auto-tagging Logic (CV), Curriculum Mapping |
| **Cloud Architecture** | Zulfaqar Hafez, Royston Teo | Docker Containerization, Async Task Queues (Celery), Secure "Drop Box" Setup |
| **Security Engineer** | Shawn Lim, Daniel Chua, Max Tan | Role-Based Access, Auto-Deletion Scripts, Audit Log Implementation |

---

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is developed as part of the SIT AAI ITP programme in collaboration with EtonHouse International School.

---

## 🙏 Acknowledgments

- **EtonHouse International School** - Industry partner and domain expertise
- **Singapore Institute of Technology** - Academic support and guidance
- **Team 23** - Development and implementation

---

<p align="center">
  <strong>Presented by Team 23</strong><br>
  EtonHouse × SIT AAI ITP Bilingual Group Progress Report (MVP)
</p>
