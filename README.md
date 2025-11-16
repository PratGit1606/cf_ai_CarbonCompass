# CarbonCompass – AI-Powered Sustainable Location Recommender

CarbonCompass is a lightweight AI-driven tool that helps users discover environmentally sustainable business locations. It combines a React + Mapbox interface with Cloudflare Workers, Workers AI (Llama 3.3), and D1 for chat memory.

Live Demo: https://cf-ai-carbon-compass.vercel.app/  
Backend Worker API: https://eco-spirit-worker.phegde9.workers.dev/

To try it: open the link → click **View Demo** → interact with the chatbot and explore recommended locations on the map.

---

## How It Works
- Users ask the chatbot for a type of business (e.g., café, retail, workspace).
- The Cloudflare Worker sends building data and the query to Workers AI.
- Workers AI selects recommended buildings based on sustainability and location metrics.
- The frontend highlights those buildings on the map and displays explanations.
- Chat context is stored in Cloudflare D1 to support follow-up questions.

---

## Example Demo
User:  
“Find me a good spot for a café.”

CarbonCompass Response:  
Highlights several buildings with strong walkability, transit access, and low emissions, plus an explanation for each recommended location. Clicking a highlighted marker opens additional sustainability insights and scoring details.

---
