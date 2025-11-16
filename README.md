```markdown
# CarbonCompass – AI-Powered Sustainable Location Recommender
AI-driven geospatial intelligence platform built on Cloudflare Workers, Workers AI, D1, and a React + Mapbox frontend.

CarbonCompass helps businesses identify the most sustainable buildings for their next location by analyzing environmental metrics, walkability, emissions, transit access, and more. The platform provides an interactive map, a chat-powered recommendation engine, and a full reasoning pipeline—all running on Cloudflare’s serverless stack.

---

## Key Features

### 1. Interactive Map (React + Mapbox GL)
- Displays all business-ready buildings using GeoJSON data.
- Markers color-coded by computed Green Score.
- Hover popups show building attributes (energy rating, vacancy, area).
- Highlighted visualization for recommended locations returned by the AI.

### 2. Workers AI Recommendation Engine
- Uses Cloudflare Workers AI (Llama 3.3) to:
  - Understand user intent (e.g., café, retail, co-working).
  - Rank buildings based on environmental and business criteria.
  - Produce explanation text describing the rationale behind each choice.
- Supports embeddings for similarity clustering (optional).

### 3. Cloudflare Worker Backend
- Handles all coordination between the frontend and Workers AI.
- Processes GeoJSON building data.
- Computes or updates Green Scores dynamically.
- Accepts user chat messages and produces structured recommendations.
- Exposes a clean API consumed by the frontend.

### 4. Chat Interface with Memory
- React chat widget allows natural conversation with the AI.
- The Worker stores session memory and user context in Cloudflare D1.
- Follow-ups like “why did you pick option 3?” use stored context.
- Fully satisfies Cloudflare's “memory/state” requirement.

### 5. Detailed Insights Modal
- Clicking any recommended building opens a modal with:
  - Green Score breakdown
  - Explanation from Workers AI
  - Transit access
  - Nearby parks, solar potential, or POIs
  - Additional sustainability metrics

---

## Architecture Overview

React + Mapbox Frontend
|
|  /chat or /recommend API
v
Cloudflare Worker

* processes building data
* calls Workers AI (Llama 3.3)
* computes Green Scores
* updates recommendation set
* writes/reads D1 memory
  |
  v
  Cloudflare D1 (chat memory + user context)

Additional Details:
- Cloudflare R2 for storing large GeoJSON building datasets.
- Durable Objects for per-user chat state (if scaling).

---

## Tech Stack

Frontend
- React (Next.js or Vite)
- TailwindCSS
- Mapbox GL JS

Backend
- Cloudflare Workers (Typescript)
- Cloudflare Workers AI (Llama 3.3)
- Cloudflare D1

Data
- GeoJSON building dataset (vacancy, area, energy rating, emissions)
- Precomputed and dynamic Green Score metrics

---

## API Endpoints

### `POST /api/chat`
Handles all chatbot messages.

Input:
```json
{
  "session_id": "abc123",
  "message": "I want a retail space"
}

Response:

```json
{
  "recommendations": [
    {
      "id": 12,
      "score": 91,
      "reason": "High walkability and low emissions zone"
    }
  ],
  "session_id": "abc123"
}

## Example Conversation Flow

User:
“I’m looking for a place to open a café.”

Workers AI:
“Based on energy efficiency, high pedestrian traffic, and nearby parks, here are 5 optimal locations.”

Frontend:
Highlights those buildings on the map and provides modal insights.

---
