# ResolveX 🚀
### Smart Customer Support Automation

![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=flat-square&logo=typescript&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![Flask](https://img.shields.io/badge/Flask-000000?style=flat-square&logo=flask&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=flat-square&logo=supabase&logoColor=white)
![n8n](https://img.shields.io/badge/n8n-FF6D5B?style=flat-square&logo=n8n&logoColor=white)

ResolveX is a full-stack automation engine designed to streamline customer support workflows. By leveraging AI and low-code automation, it transforms raw customer complaints into categorized, prioritized, and actionable tickets, reducing manual triage time and accelerating response cycles.

## 📖 Overview

ResolveX bridges the gap between customer submissions and resolution. Instead of manual sorting, the system automatically analyzes incoming requests to detect duplicates, assign priority levels, and generate AI-driven responses. It integrates a modern React frontend with a robust Flask backend and n8n workflows to handle complex automation logic.

## ✨ Features

- **🤖 AI-Powered Triage**: Automatic classification of issues, priority detection, and duplicate identification.
- **⚡ Automated Workflows**: Integration with n8n for complex routing and automated email simulations.
- **📧 Smart Responses**: Generates context-aware responses for moderate-priority issues to maintain high customer satisfaction.
- **📊 Ticket Management**: A clean dashboard for submitting and tracking customer complaints.
- **🔌 Extensible Architecture**: Designed to easily integrate with external ticketing systems like Jira or Zendesk.

## 🛠 Tech Stack

### Frontend
- **Framework**: React (Vite)
- **Language**: TypeScript
- **Styling**: Tailwind CSS
- **Routing**: React Router
- **Icons**: Lucide React
- **Notifications**: React Hot Toast

### Backend & Infrastructure
- **API**: Python Flask
- **Database/Auth**: Supabase / Firebase
- **Automation**: n8n
- **Emailing**: EmailJS

## 🚀 Getting Started

### Prerequisites

- **Node.js** (v18+)
- **Python** (v3.9+)
- **npm** or **yarn**
- **Supabase Account** (for database and authentication)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/dharunkumar-sh/resolve-x.git
   cd resolve-x
   ```

2. **Frontend Setup**
   ```bash
   # Install dependencies
   npm install

   # Start development server
   npm run dev
   ```

3. **Backend Setup**
   ```bash
   # Navigate to backend directory (if applicable)
   cd backend
   
   # Create virtual environment
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   
   # Install requirements
   pip install -r requirements.txt
   
   # Start the Flask server
   python app.py
   ```

4. **Environment Configuration**
   Create a `.env` file in the root directory and add your credentials:
   ```env
   VITE_SUPABASE_URL=your_supabase_url
   VITE_SUPABASE_ANON_KEY=your_supabase_key
   VITE_EMAILJS_SERVICE_ID=your_service_id
   VITE_EMAILJS_TEMPLATE_ID=your_template_id
   VITE_EMAILJS_PUBLIC_KEY=your_public_key
   ```

## ⚙️ Usage

1. **Submission**: The user submits a complaint via the React frontend.
2. **Processing**: The Flask backend receives the request and triggers the AI analysis pipeline.
3. **Automation**: n8n workflows classify the ticket and check for duplicates.
4. **Resolution**:
   - **High Priority**: Flagged for immediate human intervention.
   - **Moderate Priority**: Automated AI response sent via EmailJS.
   - **Low Priority**: Queued for standard processing.

## 🤝 Contributing

Contributions are welcome! Please follow these steps:
1. Fork the Project.
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`).
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`).
4. Push to the Branch (`git push origin feature/AmazingFeature`).
5. Open a Pull Request.

## 📄 License

This project is currently unlicensed. Please contact the maintainer for usage permissions.
