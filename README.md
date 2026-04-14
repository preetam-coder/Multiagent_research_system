
An intelligent multi-agent research system powered by AI that automates research gathering, analysis, and report generation. ResearchMind orchestrates multiple specialized AI agents to deliver comprehensive, well-structured research reports in minutes.

## 🌟 Features

- **🔍 Intelligent Search Agent** — Crawls the web using Tavily API to find recent, reliable information
- **📖 Smart Reader Agent** — Intelligently scrapes and extracts deep content from identified resources
- **✍️ Expert Writer Agent** — Generates well-structured, detailed research reports with proper formatting
- **🎯 Critic Agent** — Reviews and evaluates report quality with constructive feedback and scoring
- **🎨 Modern UI** — Sleek Streamlit interface with custom styling for seamless user experience
- **⚡ Fast Processing** — Completes research tasks in minutes instead of hours

## 🛠️ Tech Stack

### Core Technologies
- **LangChain** — Multi-agent orchestration and chain management
- **Mistral AI** — Powerful LLM for agent reasoning
- **LangGraph** — Workflow management for agent execution
- **Streamlit** — Modern web interface

### Tools & Libraries
- **Tavily API** — Real-time web search
- **BeautifulSoup4** — Web scraping and HTML parsing
- **Requests** — HTTP client for web requests
- **Pydantic** — Data validation and settings management
- **Rich** — Beautiful terminal output and logging

### Supporting Libraries
- **python-dotenv** — Environment variable management
- **aiohttp** — Async HTTP support
- **pandas** — Data handling
- **tiktoken** — Token counting for LLMs

### 2. Create a Virtual Environment (Optional but Recommended)
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Set Up Environment Variables
Create a `.env` file in the root directory:
```
MISTRAL_API_KEY=your_mistral_api_key_here
TAVILY_API_KEY=your_tavily_api_key_here
```

## 💻 Usage

### Run the Streamlit App
```bash
streamlit run app.py
```

The app will be available at `http://localhost:8501`

### Run the Pipeline Programmatically
```python
from pipeline import run_research_pipeline

topic = "Your research topic here"
results = run_research_pipeline(topic)

print(results['report'])
print(results['critique'])
```

## 📁 Project Structure

```
ResearchMind/
├── app.py              # Streamlit web interface
├── agents.py           # Agent definitions and LLM setup
├── pipeline.py         # Research pipeline orchestration
├── tools.py            # Specialized tools (web_search, scrape_url)
├── requirements.txt    # Project dependencies
├── .env               # Environment variables (create this)
├── .gitignore         # Git ignore rules
└── README.md          # This file
```

## 🔄 How It Works

### Research Pipeline Stages

1. **Search Stage** 🔍
   - Search Agent queries the web using Tavily API
   - Fetches top 5 most relevant results
   - Returns titles, URLs, and content snippets

2. **Scraping Stage** 📖
   - Reader Agent identifies the most relevant URL from search results
   - Deep scrapes the selected URL to extract detailed content
   - Cleans HTML and extracts pure text (max 3000 characters)

3. **Writing Stage** ✍️
   - Writer Agent combines search and scraped content
   - Generates a structured research report with:
     - Introduction
     - Key Findings (minimum 3 points)
     - Conclusion
     - Sources

4. **Critique Stage** 🎯
   - Critic Agent evaluates the report
   - Provides score out of 10
   - Lists strengths and areas for improvement
   - Gives a one-line verdict

## 🧠 System Architecture

```
User Input (Topic)
       ↓
┌─────────────────────────────┐
│   Search Agent               │  Tavily Web Search
│   (LangChain + Mistral)      │
└─────────────────────────────┘
       ↓ Search Results
┌─────────────────────────────┐
│   Reader Agent               │  URL Scraping
│   (LangChain + Mistral)      │  BeautifulSoup
└─────────────────────────────┘
       ↓ Scraped Content
┌─────────────────────────────┐
│   Writer Chain               │  Report Generation
│   (LangChain + Mistral)      │
└─────────────────────────────┘
       ↓ Draft Report
┌─────────────────────────────┐
│   Critic Chain               │  Quality Evaluation
│   (LangChain + Mistral)      │
└─────────────────────────────┘
       ↓
Final Report + Critique
```

## 📊 Example Output

**Input:** "Latest developments in Artificial Intelligence"

**Output:**
- Comprehensive research report with industry-latest findings
- Quality score and constructive feedback
- Properly formatted with sources and citations

## 🔐 Security & Best Practices

- 🔑 API keys stored in `.env` (never commit to repo)
- 🛡️ Environment variables loaded via `python-dotenv`
- ⚠️ Error handling for failed API calls
- 🔄 Retry logic with `tenacity` for robustness
- 📝 Input validation with `pydantic`

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/YourFeature`)
3. Commit your changes (`git commit -m 'Add YourFeature'`)
4. Push to the branch (`git push origin feature/YourFeature`)
5. Open a Pull Request

## 🐛 Known Limitations

- Scraping may fail on JavaScript-heavy websites
- API rate limits apply from Mistral and Tavily
- Report quality depends on topic clarity and available sources
- Scraping timeout: 8 seconds per URL

## 🚧 Future Enhancements

- [ ] Support for multiple LLM providers (OpenAI, Claude, etc.)
- [ ] Advanced caching to reduce API calls
- [ ] PDF export for generated reports
- [ ] Multi-language support
- [ ] Batch research processing
- [ ] Custom prompt templates
- [ ] Integration with academic databases
- [ ] Real-time streaming for long reports
