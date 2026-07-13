# O.R.A.C.L.E

> **An AI-powered SMS stock intelligence agent that monitors your watchlist, detects significant market movements, analyzes the news behind them, and delivers concise, actionable insights directly to your phone. Stay informed without constantly watching the market, and manage your portfolio using simple natural-language SMS commands.**

O.R.A.C.L.E (Optimized Reasoning and Analytics for Capital & Live Events) continuously monitors the stocks you care about, identifies meaningful price movements, investigates the events driving those changes, and notifies you with AI-generated summaries via SMS. Whether you're away from your screen or on the move, Oracle keeps you connected to the market through intelligent, real-time updates.

![O.R.A.C.L.E](docs/example.png)
---

## Features

- Real-time monitoring of your personalized stock watchlist
- AI-powered analysis of significant price movements
- Automated market news research and summarization
- Instant SMS notifications powered by Twilio
- Natural-language SMS commands for managing your watchlist
- FastAPI backend for deployment and scalability
- Development and research modes for local testing

---

## How It Works

```text
        Your Watchlist
               │
               ▼
     Monitor Stock Prices
               │
               ▼
 Significant Price Movement?
        │               │
       No              Yes
        │               │
        ▼               ▼
 Continue         Analyze Market News
 Monitoring             │
                        ▼
             Generate AI Summary
                        │
                        ▼
              Deliver SMS Alert
                        │
                        ▼
         Receive User SMS Commands
                        │
                        ▼
             Update Watchlist
```

---

## Prerequisites

- Python 3.11+
- OpenAI API Key
- Twilio Account & Phone Number
- Dependencies listed in `requirements.txt`

---

## Environment Setup

Create a `.env` file in the project root.

```env
OPENAI_API_KEY=your-openai-api-key
TWILIO_PHONE_NUMBER=your_twilio_phone_number
TWILIO_ACCOUNT_SID=your_twilio_account_sid
TWILIO_AUTH_TOKEN=your_twilio_auth_token
TARGET_PHONE_NUMBER=your_phone_number
WEBHOOK_URL=your_public_webhook_url
```

> **Note:** `WEBHOOK_URL` should be the public HTTPS endpoint Twilio uses to send requests to your `/receive-message` route.

---

## Installation

```bash
git clone <repository-url>
cd oracle

pip install -r requirements.txt

cp .env.example .env
```

Update `.env` with your credentials before running the application.

---

## Running Oracle

### Start the FastAPI Server

```bash
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

Oracle will begin monitoring your watchlist, process incoming SMS messages, and automatically deliver alerts whenever significant market activity is detected.

---

## SMS Commands

Manage your watchlist using natural language.

| Action | Example |
|---------|---------|
| Add a stock | `Track AAPL` |
| Remove a stock | `Stop tracking TSLA` |
| View watchlist | `Show my watchlist` |
| Check stock price | `Price of NVDA` |

---

## Development Mode

Run Oracle locally.

```bash
python main.py -test
```

Run the research pipeline for a specific stock.

```bash
python main.py -test -research AAPL
```

---

## Docker

Build:

```bash
docker build -t oracle .
```

Run:

```bash
docker run -p 8000:8000 --env-file .env oracle
```

---

## Project Structure

```text
oracle/
├── main.py                # FastAPI app and entry point
├── lib/                   # Core logic (agents, SMS, stock checker, tools, tracker)
├── resources/             # Data files (alert history, tracker list)
├── requirements.txt       # Python dependencies
├── .env                   # Environment variables
└── README.md              # This file
```

---

## Alert Pipeline

Whenever a tracked stock experiences a significant price movement, Oracle automatically:

1. Detects the movement.
2. Collects the latest relevant market news.
3. Uses AI to determine the likely cause.
4. Generates a concise summary.
5. Delivers an SMS notification with the key insights.

---

## License

This project is licensed under the MIT License.
