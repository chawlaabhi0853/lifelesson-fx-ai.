# Life Lesson FX OpenAI Webhook

Alert-only TradingView webhook receiver for five markets. No broker connectivity or order execution.

## Deploy
Python 3.11+, build `pip install -r requirements.txt`, start `uvicorn server:app --host 0.0.0.0 --port $PORT`.

Configure private host environment variables `WEBHOOK_SECRET`, `REPORTS_SECRET`, `OPENAI_API_KEY`, `OPENAI_MODEL` (optional), and `DB_PATH` (persistent storage recommended). Never commit actual secrets.

Endpoints: `GET /health`, `POST /webhook/{WEBHOOK_SECRET}`, `GET /reports/{REPORTS_SECRET}`. Webhook requires JSON `system=LifeLessonFX`, allowed `symbol`, `event=BUY_CANDIDATE|SELL_CANDIDATE`, `time_ms`, `reference_entry`, `reference_sl`, `reference_tp`.

The receiver returns WATCH or NO TRADE only. AI is explanatory, not trade approval. Production needs durable job queue, storage, webhook delivery tests and exact Pine alert payload compatibility verification before connecting existing alerts.
