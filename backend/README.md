# 🏠 Rental Agreement AI Assistant

An intelligent AI-powered platform that helps tenants understand their rental agreements, identify potential issues, and manage their rental obligations through natural language interaction.

## 🌟 Overview

This project was built as part of a GenAI hackathon to address the common problem of tenants not fully understanding complex rental agreements. The AI assistant analyzes uploaded rental documents, extracts key information, identifies potential red flags, and provides an interactive chatbot interface for tenant questions.

## 🚀 Live Demo

**Deployed Application:** [https://rental-agreement-ai-865102500816.us-central1.run.app](https://rental-agreement-ai-865102500816.us-central1.run.app)

## 🎯 Key Features

### 📄 Document Processing
- **PDF Upload & Analysis** - Upload rental agreements in PDF format
- **Document AI Integration** - Automatic text extraction using Google Cloud Document AI
- **Intelligent Summarization** - AI-generated summaries highlighting key terms

### 🔍 Smart Analysis
- **Red Flag Detection** - Identifies potentially problematic clauses
- **Risk Assessment** - Highlights concerning terms and unusual conditions
- **Structured Data Extraction** - Automatically extracts key information like rent amount, due dates, landlord details

### 💬 Interactive AI Chatbot
- **Natural Language Queries** - Ask questions about your rental agreement in plain English
- **Intelligent Tool Selection** - AI automatically chooses the right tool based on your question type
- **Contextual Responses** - Answers are tailored to your specific rental document

### 📅 Smart Reminders
- **Automatic Rent Reminders** - Sets up payment notifications based on extracted due dates
- **Proactive Alerts** - Helps tenants stay on top of their rental obligations

## 🏗️ Technical Architecture

### Backend Stack
- **FastAPI** - Modern Python web framework for APIs
- **LangChain & LangGraph** - AI agent orchestration and tool management
- **Google Cloud Platform**
  - **Vertex AI (Gemini)** - Large language model for AI conversations
  - **Document AI** - PDF text extraction and processing
  - **Cloud Storage** - Document storage
  - **Firestore** - NoSQL database for document chunks and metadata
- **Python 3.12** - Core runtime environment

### Frontend Stack
- **Pure HTML/CSS/JavaScript** - Lightweight, responsive web interface
- **Modern UI Design** - Clean, professional interface optimized for document interaction

### AI Agent System
The core of the application is an intelligent agent system that uses different tools based on user intent:

#### 🛠️ Available Tools

1. **Structured Info Tool** (`get_structured_info`)
   - **Purpose:** Extract specific factual data
   - **Triggers:** Questions like "What is my rent amount?", "When is rent due?", "Who is my landlord?"
   - **Data:** Rent amount, due dates, addresses, names, lease duration, security deposits

2. **Firestore Search Tool** (`firestore_search`) 
   - **Purpose:** Analyze content for concerns and provide interpretations
   - **Triggers:** Questions like "What are the red flags?", "Are there any concerning clauses?", "What should I worry about?"
   - **Analysis:** Risk assessment, problematic terms, unusual conditions

3. **Rent Calculation Tool** (`get_days_until_rent`)
   - **Purpose:** Calculate time remaining until next payment
   - **Triggers:** "How many days until rent is due?", "When is my next payment?"
   - **Output:** Specific countdown and payment scheduling

4. **Reminder Tool** (`set_rent_reminder`)
   - **Purpose:** Create automated payment reminders
   - **Triggers:** "Remind me about rent", "Set up payment alerts"
   - **Function:** Proactive notification system

#### 🧠 Intelligent Tool Selection
The AI agent uses advanced semantic understanding to map user questions to the appropriate tools:
- **Intent Recognition** - Understands what the user is trying to accomplish
- **Semantic Mapping** - Maps similar concepts to the right tools
- **Fallback Logic** - Gracefully handles edge cases and errors

## 📂 Project Structure

```
backend/
├── agent/                          # AI Agent System
│   ├── agent_graph.py             # Main agent orchestration and LangGraph setup
│   ├── rag_tool.py                # Firestore search and analysis tool
│   ├── structured_info_tool.py    # Data extraction tool
│   ├── summarizer_tool.py         # Document summarization tool
│   ├── reminder_tool.py           # Rent reminder system
│   └── __init__.py               # Package initialization
├── frontend/                      # Web Interface
│   ├── index.html                # Main dashboard
│   ├── styles.css               # Responsive styling
│   ├── script.js                # Frontend JavaScript logic
│   └── README.md                # Frontend documentation
├── config.py                     # Configuration settings
├── integrated_server.py          # Main production server
├── main.py                       # Alternative server entry point
├── requirements.txt              # Python dependencies
├── Dockerfile                    # Container configuration
├── .dockerignore                 # Docker ignore rules
├── .env                          # Environment variables
└── silken-granite-472417-g7-3a424d2a6806.json  # Google Cloud credentials
```

## 🚀 Deployment

### Cloud Platform
- **Google Cloud Run** - Serverless container platform
- **Region:** us-central1
- **Configuration:** 2GB RAM, 1 CPU, auto-scaling enabled
- **URL:** [https://rental-agreement-ai-865102500816.us-central1.run.app](https://rental-agreement-ai-865102500816.us-central1.run.app)

### Container Setup
```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 8080
CMD ["python", "integrated_server.py"]
```

## 📋 API Endpoints

### Core Endpoints
- `GET /` - Web dashboard interface
- `GET /api/health` - Health check and system status
- `POST /api/upload-document/` - Upload and process rental agreements
- `POST /api/query-agent/` - Interactive AI chatbot queries

### Usage Examples

#### Document Upload
```bash
curl -X POST "https://rental-agreement-ai-865102500816.us-central1.run.app/api/upload-document/" \
     -H "X-User-ID: your-user-id" \
     -F "file=@rental_agreement.pdf"
```

#### AI Chat Query
```bash
curl -X POST "https://rental-agreement-ai-865102500816.us-central1.run.app/api/query-agent/" \
     -H "X-User-ID: your-user-id" \
     -d "query=What is my monthly rent amount?"
```

## 🔧 Local Development

### Prerequisites
- Python 3.12+
- Google Cloud SDK
- Valid Google Cloud Project with enabled APIs:
  - Vertex AI API
  - Document AI API
  - Cloud Storage API
  - Firestore API

### Setup Steps
1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd genai-hackathon/backend
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure Google Cloud credentials**
   - Place service account key in project root
   - Update config.py with your project settings

4. **Run locally**
   ```bash
   python integrated_server.py
   ```
   
5. **Access the application**
   - Web Interface: http://localhost:8080
   - API Documentation: http://localhost:8080/docs

## 🔍 How It Works

### 1. Document Upload Process
```
User uploads PDF → Document AI extracts text → AI generates summary → 
Extracts structured data → Stores in Firestore → Sets automatic reminders
```

### 2. AI Query Process  
```
User asks question → Agent analyzes intent → Selects appropriate tool → 
Retrieves relevant data → Generates natural language response
```

### 3. Intelligent Tool Routing
The AI agent intelligently routes queries based on semantic understanding:
- **Data queries** → Structured Info Tool
- **Analysis queries** → Firestore Search Tool  
- **Time queries** → Rent Calculation Tool
- **Reminder requests** → Reminder Tool

## 🛡️ Error Handling & Resilience

### Quota Management
- **429 Error Handling** - Graceful retry logic for Vertex AI rate limits
- **Fallback Responses** - User-friendly messages when AI services are unavailable
- **Circuit Breaker Pattern** - Prevents cascade failures

### Data Validation
- **Input Sanitization** - Validates all user inputs
- **File Type Checking** - Ensures only valid PDF files are processed  
- **Error Recovery** - Graceful handling of processing failures

## 📊 System Monitoring

### Health Checks
- **Service Status** - Real-time monitoring of all Google Cloud services
- **API Endpoints** - Automated health checking
- **Performance Metrics** - Response time and error rate tracking

### Logging
- **Comprehensive Logging** - Detailed logs for debugging and monitoring
- **Error Tracking** - Automatic error reporting and alerting
- **Usage Analytics** - User interaction and feature usage tracking

## 🎯 Use Cases

### For Tenants
- **First-time renters** understanding complex lease terms
- **Experienced renters** identifying unusual or problematic clauses
- **Anyone needing quick answers** about their rental agreement
- **Rent management** with automatic reminders

### For Property Managers
- **Tenant education** - Help tenants understand their agreements
- **Reduced support queries** - AI handles common questions
- **Improved tenant relationships** through transparency

## 🚧 Future Enhancements

### Planned Features
- **Multi-language support** for non-English rental agreements
- **Lease comparison tool** to compare multiple rental options
- **Legal resource integration** with tenant rights databases
- **Mobile app** for iOS and Android
- **Email/SMS notifications** for rent reminders
- **Landlord dashboard** for property managers

### Technical Improvements
- **Enhanced AI models** with fine-tuning on rental agreement data
- **Real-time collaboration** features for multiple tenants
- **Advanced analytics** and reporting capabilities
- **Integration APIs** for property management software

## 🏆 Hackathon Achievement

This project was developed during a GenAI hackathon with the following achievements:
- **Fully functional AI system** deployed to production
- **Real-world problem solving** addressing tenant pain points
- **Advanced AI integration** with multiple Google Cloud services
- **Professional deployment** on Google Cloud Run
- **Scalable architecture** ready for production use

## 📜 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- **Google Cloud Platform** for providing robust AI and cloud infrastructure
- **LangChain/LangGraph** for excellent AI agent orchestration tools
- **FastAPI** for the modern, high-performance web framework
- **The GenAI Hackathon** for inspiring this innovative solution

---

**Built with ❤️ during the GenAI Hackathon**

**Deployed at:** [https://rental-agreement-ai-865102500816.us-central1.run.app](https://rental-agreement-ai-865102500816.us-central1.run.app)
