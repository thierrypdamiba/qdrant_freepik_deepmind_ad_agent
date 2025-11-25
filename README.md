# 🎨 Ad Generation Agent

An AI-powered advertisement creation system that combines vector search, multimodal AI, and generative image models to create compelling marketing content.

## 🌟 Features

- **Smart Product Search**: Uses Qdrant vector database with CLIP embeddings to find relevant products
- **AI Image Generation**: Leverages Freepik API to generate stunning ad visuals with product references
- **Intelligent Copywriting**: Uses Google Gemini to create compelling ad copy
- **Complete Workflow**: End-to-end pipeline from query to finished advertisement
- **Web Interface**: Interactive frontend showcasing the agent workflow

## 🏗️ Architecture

```
Query → Qdrant Search → Image Generation (Freepik) → Copy Generation (Gemini) → Complete Ad
```

### Key Components

1. **Agent (`agent.py`)**: Core logic for creating ads
2. **API Server (`api.py`)**: FastAPI server for the web interface
3. **Frontend (`frontend/`)**: Next.js web interface
4. **Scripts (`scripts/`)**: Utilities for data ingestion and verification

## 🚀 Quick Start

### Prerequisites

- Python 3.10+
- Node.js 18+ (for frontend)
- API keys for:
  - Qdrant Cloud
  - Freepik API
  - Google Gemini

### Installation

1. **Clone and setup environment**:
```bash
git clone <your-repo>
cd monday
```

2. **Install Python dependencies**:
```bash
pip install -r requirements.txt
```

3. **Create `.env` file**:
```bash
# Qdrant Configuration
QDRANT_URL=https://your-cluster.qdrant.io
QDRANT_API_KEY=your_qdrant_api_key
QDRANT_COLLECTION=shopping-queries-images

# AI Model APIs
GEMINI_API_KEY=your_gemini_api_key
FREEPIK_API_KEY=your_freepik_api_key

# Optional: Model Configuration
FREEPIK_MODEL=flux-1-1-pro
TEXT_EMBEDDING_MODEL=Qdrant/clip-ViT-B-32-text
```

4. **Install frontend dependencies**:
```bash
cd frontend
npm install
cd ..
```

## 💡 Usage

### Run the Agent (Web Interface)

The easiest way to run the agent is using the start script:

```bash
./start_agent.sh
```

This will start both the backend API (port 8001) and the frontend (port 3001).
Open http://localhost:3001 in your browser.

### Run Manually

1. **Start the API**:
```bash
python api.py
# Server runs on http://localhost:8001
```

2. **Start the frontend** (in another terminal):
```bash
cd frontend
npm run dev
# Frontend runs on http://localhost:3001
```

### Run CLI Agent

You can also run the agent directly from the command line:

```bash
# Basic usage
python agent.py "beach vacation essentials"

# With options
python agent.py "weekend mountain adventure" --num-products 3
```

## 📁 Project Structure

```
monday/
├── agent.py                    # Main ad generation agent logic
├── api.py                      # FastAPI server
├── start_agent.sh              # Startup script
├── requirements.txt            # Python dependencies
├── .env                        # Environment variables
│
├── frontend/                   # Next.js web interface
│   ├── app/                    # Next.js app directory
│   └── components/             # React components
│
├── scripts/                    # Utility scripts
│   ├── verify_setup.py         # Verification script
│   ├── check_collection.py     # Check Qdrant collection
│   ├── ingest_data.py          # Data ingestion script
│   └── test_pipeline.py        # Pipeline test script
│
└── README.md                   # This file
```

## 🔧 Utilities

- **Verify Setup**: `python scripts/verify_setup.py`
- **Test Pipeline**: `python scripts/test_pipeline.py`
- **Check Collection**: `python scripts/check_collection.py`

## 🔑 Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `QDRANT_URL` | Qdrant cluster URL | `https://xyz.qdrant.io` |
| `QDRANT_API_KEY` | Qdrant API key | `your_api_key` |
| `QDRANT_COLLECTION` | Collection name | `shopping-queries-images` |
| `GEMINI_API_KEY` | Google Gemini API key | `AIza...` |
| `FREEPIK_API_KEY` | Freepik API key | `fp_...` |

## 📝 License

MIT License
