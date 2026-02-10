1. README (GitHub README content)
 Project Title

Generative AI for Demystifying Legal Documents

👥 Team

Team Name: CodeChef (VITC)
Team Lead: Shrinikhaythan

 Overview

Legal documents such as rental agreements are often lengthy, complex, and filled with difficult legal jargon that most users overlook or misunderstand. This project introduces an end-to-end Generative AI platform that simplifies legal agreements and transforms them into clear, actionable insights.

The system acts as a personal AI legal assistant that reads legal documents, extracts critical information, highlights risky clauses, and answers user queries in simple language.

 What This Project Does

Simplifies complex legal agreements into plain language

Flags risky or dangerous clauses

Extracts key structured data (rent, dates, deposit, parties)

Provides a personalized chatbot per user

Sends reminders and alerts for important deadlines

Stores documents securely in tenant-isolated storage

Architecture Overview

User uploads legal document (PDF)

Google Cloud Document AI extracts text and structure

Vertex AI (Gemini) processes and simplifies legal content

Important clauses and risks are identified

Data stored in Firestore with vector embeddings

Personalized chatbot enables Q&A and insights

Alerts and reminders generated for users

 Tech Stack

Google Cloud Document AI – Document extraction

Vertex AI (Gemini) – LLM + RAG processing

Firestore – Structured data + embeddings storage

Google Cloud Storage – Document upload & storage

RAG Architecture – Context-aware legal chatbot

 Future Enhancements

Multi-language legal document support

Legal professional analytics tools

Email & SMS reminder system

Secure authentication system

Blockchain-based document verification
