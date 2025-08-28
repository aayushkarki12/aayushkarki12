# Level 0 Data Flow Diagram - AI Resume System

## System Overview
This Level 0 DFD represents the highest-level view of the AI Resume System, showing the main process and its interactions with external entities.

## Diagram

```
┌──────────────┐                                    ┌──────────────┐
│              │    1. Resume Input Data             │              │
│              │    (Personal details, work          │              │
│     USER     │    experience, education)           │      AI      │
│              │────────────────────────────────────▶│    RESUME    │
│              │                                     │    SYSTEM    │
│              │    2. Subscription/Payment Info     │              │
│              │────────────────────────────────────▶│   (Process   │
│              │                                     │     0.0)     │
│              │                                     │              │
│              │◀────────────────────────────────────│              │
│              │    5. AI-powered Resume             │              │
└──────────────┘                                    │              │
                                                     │              │
                                                     │              │
┌──────────────┐                                    │              │
│              │◀────────────────────────────────────│              │
│    STRIPE    │    3. Subscription Info/            │              │
│   (Payment   │       Payment Request               │              │
│   Gateway)   │                                     │              │
│              │────────────────────────────────────▶│              │
│              │    4. Confirmation/Payment Status   │              │
└──────────────┘                                    └──────────────┘
```

## Components Description

### External Entities
1. **USER** - The person using the system to create resumes
2. **STRIPE (Payment Gateway)** - Third-party payment processing service

### Process
1. **AI RESUME SYSTEM (Process 0.0)** - The main system that processes user input and generates AI-powered resumes

### Data Flows

| Flow # | From | To | Data Description |
|--------|------|----|--------------------|
| 1 | User | AI Resume System | Resume Input Data (personal details, work experience, education) |
| 2 | User | AI Resume System | Subscription/Payment Information |
| 3 | AI Resume System | Stripe | Subscription Info/Payment Request |
| 4 | Stripe | AI Resume System | Confirmation/Payment Status |
| 5 | AI Resume System | User | AI-powered Resume (Generated output) |

## Data Flow Details

### Input Flows (User → System)
- **Resume Input Data**: Contains personal information, work history, educational background, skills, and other resume-relevant information
- **Subscription/Payment Info**: Payment details, subscription preferences, billing information

### Payment Processing Flows (System ↔ Stripe)
- **Payment Request**: Subscription details, payment amount, user identification
- **Payment Confirmation**: Transaction status, subscription activation, payment receipt information

### Output Flow (System → User)
- **AI-powered Resume**: Professionally formatted resume generated using AI based on user input, customized according to user preferences and industry standards

## System Boundary
The AI Resume System boundary includes all resume generation logic, user interface, payment processing coordination, and data management. External entities (User and Stripe) are outside the system boundary.