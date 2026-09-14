# AI Agents using Spring AI & Thymeleaf

🔗 **Live Demo**: https://springboot-llm-project-complete.onrender.com
*(Free hosting — may take 30–50 seconds to wake up if it's been inactive.)*

A fully functional, interactive AI Agent system built using **Spring Boot 4.1**, **Spring AI 2.0.0**, and **Thymeleaf**.
This project showcases how to build AI Agents capable of dynamic function calling (tool execution) to resolve user travel queries (flights, hotels, weather) and e-commerce customer support tasks (order status, canceling orders, inventory checks).

The chat model runs on **Groq's free API** (OpenAI-compatible), so the entire project can be run and deployed at **zero cost**.

---

## 🌟 Features

- **Multi-domain AI Agent**:
  - **Travel Assistant**: Search flights, hotels, and retrieve weather forecasts.
  - **Customer Support Agent**: Cancel orders, check order status, view inventory, and check item availability.
- **Function Calling / Agentic Tools**: Uses Spring AI's `@Tool` annotations to register Java methods as executable agent tools, dynamically parsed by the chat model.
- **Conversational Memory**: Maintains context across multiple turns using Spring AI's chat memory.
- **Modern UI**: Styled with Tailwind CSS, featuring light/dark mode, real-time Markdown parsing for AI responses, chat-history cleaning, and instant suggestion templates.
- **Free & Deployable**: Runs entirely on Groq's free-tier API and can be deployed for free using Docker on platforms like Render.

---

## 📂 Project Structure

```text
├── README.md
├── .gitignore
├── docs/
│   ├── prompt.md
│   └── understand.excalidraw
└── ai-agents-using-spring-ai/
    └── ai-agent-backend/
        ├── Dockerfile
        ├── pom.xml
        ├── mvnw / mvnw.cmd
        └── src/
            ├── main/
            │   ├── java/.../backend/
            │   │   ├── AiAgentBackendApplication.java
            │   │   ├── config/
            │   │   ├── controller/
            │   │   ├── model/
            │   │   ├── service/
            │   │   └── tools/
            │   └── resources/
            │       ├── templates/chat.html
            │       └── application.yml
```

---

## 🛠️ Tech Stack

- **Backend**: Spring Boot, Spring Web, Spring AI, Lombok
- **AI Provider**: [Groq](https://console.groq.com) (free, OpenAI-compatible API)
- **Frontend**: Thymeleaf, Tailwind CSS, Marked.js (Markdown renderer)
- **Language**: Java 21+
- **Containerization**: Docker
- **Hosting**: Render (free tier)

---

## ⚙️ Configuration & Setup

### 1. Prerequisites
- **Java 21** or higher
- **Maven** (or use the included Maven Wrapper `./mvnw`)
- A **free Groq API key** — get one at [console.groq.com](https://console.groq.com) → API Keys

### 2. Environment Variables
Set the following before running the app:

```bash
# Windows (Command Prompt)
set OPENAI_API_KEY=gsk_your_groq_key_here
set CHAT_MODEL=qwen/qwen3.8-27b

# Windows (PowerShell)
$env:OPENAI_API_KEY="gsk_your_groq_key_here"
$env:CHAT_MODEL="qwen/qwen3.8-27b"

# Mac/Linux
export OPENAI_API_KEY="gsk_your_groq_key_here"
export CHAT_MODEL="qwen/qwen3.8-27b"
```

> **Note:** The variable is named `OPENAI_API_KEY` for compatibility with Spring AI's OpenAI starter, but the value should be your **Groq** key.

### 3. application.yml

```yaml
server:
  port: ${PORT:8081}

spring:
  application:
    name: ai-agent-backend

  ai:
    openai:
      api-key: ${OPENAI_API_KEY:default-key}
      base-url: https://api.groq.com/openai/v1
      chat:
        model: ${CHAT_MODEL:qwen/qwen3.8-27b}
```

---

## 🚀 Running Locally

Navigate to the `ai-agent-backend` directory and start the server:

```bash
cd ai-agents-using-spring-ai/ai-agent-backend
./mvnw spring-boot:run      # Mac/Linux
mvnw.cmd spring-boot:run    # Windows
```

Once started, open your browser and navigate to:
👉 **http://localhost:8081/**

---

## 🐳 Running with Docker

A `Dockerfile` is included in `ai-agent-backend/`:

```bash
cd ai-agents-using-spring-ai/ai-agent-backend
docker build -t ai-agent-backend .
docker run -p 8081:8081 \
  -e OPENAI_API_KEY=gsk_your_groq_key_here \
  -e CHAT_MODEL=qwen/qwen3.8-27b \
  ai-agent-backend
```

---

## ☁️ Deploying on Render (Free)

1. Push this repository to your own GitHub account.
2. Go to [render.com](https://render.com) → **New Web Service** → connect your repo.
3. Set:
   - **Language**: Docker
   - **Root Directory**: `ai-agents-using-spring-ai/ai-agent-backend`
   - **Instance Type**: Free
4. Add environment variables:
   - `OPENAI_API_KEY` → your Groq key
   - `CHAT_MODEL` → `qwen/qwen3.8-27b`
5. Click **Deploy Web Service** and wait for the build to finish.

> **Note:** Render's free tier spins down after 15 minutes of inactivity and takes ~30–50 seconds to wake up on the next request.

---

## 🤖 Registered Agent Tools

| Tool Class | Method Name | Description |
| :--- | :--- | :--- |
| `FlightTools` | `searchFlight` | Searches flights by source, destination, and date. |
| `HotelTools` | `searchHotel` | Finds hotels matching a city and max budget per night. |
| `WeatherTools` | `getForecast` | Retrieves weather conditions (temp, status) for a city. |
| `OrderTools` | `getOrderStatus` | Finds order dispatch status by its numeric ID (e.g. `1042`). |
| `OrderTools` | `cancelOrder` | Cancels an active order using the order ID. |
| `OrderTools` | `getOrderCount` | Fetches the total count of mock orders. |
| `InventoryTools` | `checkStock` | Checks item availability by product name. |
| `InventoryTools` | `getAllProductsInStock` | Returns all available products in stock. |

---

## 💡 Example Prompt for Testing

> *"Plan a trip from Delhi to Goa on 2026-08-21. My total budget for flight + one night hotel is ₹7000. What should I book, and what's the weather going to be like?"*

The agent will:
1. Search flights from Delhi to Goa on the given date.
2. Check for hotels in Goa.
3. Fetch the weather forecast for Goa.
4. Calculate options that fit within the budget and return a tailored plan.

---

## ⚠️ Notes on Free-Tier Model Availability

Groq periodically updates and deprecates models on its free tier. If you get a `404: model does not exist` error, check your account's currently available models at [console.groq.com/playground](https://console.groq.com/playground) and update the `CHAT_MODEL` environment variable accordingly.

---

## 📄 License

This project is provided for educational purposes. Check the original repository for any applicable license terms before redistributing.
