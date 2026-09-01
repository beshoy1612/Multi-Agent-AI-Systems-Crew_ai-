# AI Procurement Agent

AI Procurement Agent is a multi-agent system that automates product research and procurement analysis.

Given a product, target country, and list of e-commerce websites, the system:

* Generates optimized search queries
* Searches for relevant products across multiple sources
* Extracts product details and prices
* Selects and analyzes the best product options
* Generates a professional HTML procurement report

The project is built using CrewAI and follows a sequential multi-agent workflow.

## Workflow

```text
User Requirements
       |
       v
Search Query Agent
       |
       v
Web Search Agent
       |
       v
Product Scraping Agent
       |
       v
Procurement Report Agent
       |
       v
HTML Procurement Report
```

## Agents

### 1. Search Query Strategist

Generates diverse and targeted search queries based on:

* Product name
* Target country
* Product specifications
* Brands and models
* Price ranges and product variations

The output is structured as JSON using Pydantic.

### 2. Search Engine Agent

Uses Tavily to search for relevant product pages.

The agent:

* Processes multiple search queries
* Finds purchasable products
* Filters irrelevant and suspicious links
* Ignores low-confidence search results
* Collects product URLs for the next stage

### 3. Web Scraping Agent

Uses ScrapeGraphAI to extract structured product information from e-commerce pages.

Extracted data includes:

* Product title
* Product image
* Current price
* Original price
* Discount percentage
* Important specifications
* Product recommendation rank
* Recommendation notes

### 4. Procurement Report Agent

Analyzes the extracted product data and generates a professional HTML procurement report containing:

1. Executive Summary
2. Introduction
3. Methodology
4. Findings
5. Analysis
6. Recommendations
7. Conclusion
8. Appendices

The report uses Bootstrap for a clean and readable interface.

## Tech Stack

* Python
* CrewAI
* Google Gemini
* Tavily
* ScrapeGraphAI
* Pydantic
* AgentOps
* Bootstrap

## Project Structure

```text
AI-Procurement-Agent/
│
├── ai-agent-output/
│   ├── step1.json
│   ├── step2.json
│   ├── step3.json
│   └── step_4_procurement_report.html
│
├── main.py
├── requirements.txt
├── .env
└── README.md
```

## Installation

Clone the repository:

```bash
git clone <repository-url>
cd AI-Procurement-Agent
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate it.

**Windows:**

```bash
.venv\Scripts\activate
```

**Linux/macOS:**

```bash
source .venv/bin/activate
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

## Environment Variables

Create a `.env` file in the root directory:

```env
GEMINI_API_KEY=your_gemini_api_key
TAVILY_API_KEY=your_tavily_api_key
ScrapGraphAI_API_KEY=your_scrapegraphai_api_key
AGENTOPS_API_KEY=your_agentops_api_key
```

## Configuration

The workflow accepts the following inputs:

```python
{
    "product_name": "laptop for gaming",
    "website_list": [
        "www.amazon.eg",
        "www.jumia.com.eg",
        "www.noon.com/egypt-en",
        "www.sigma-computer.com/en",
        "https://2b.com.eg/"
    ],
    "country_name": "Egypt",
    "no_keyword": 10,
    "score_th": 0.8,
    "top_recommendations_no": 5
}
```

| Parameter                | Description                                      |
| ------------------------ | ------------------------------------------------ |
| `product_name`           | The product to search for                        |
| `website_list`           | E-commerce websites to search                    |
| `country_name`           | Target country                                   |
| `no_keyword`             | Number of generated search queries               |
| `score_th`               | Minimum search confidence score                  |
| `top_recommendations_no` | Number of products selected for the final report |

## Running the Project

Run the application:

```bash
python main.py
```

The system will process the workflow sequentially and save the results in:

```text
ai-agent-output/
```

The generated files are:

```text
step1.json                      # Generated search queries
step2.json                      # Search results
step3.json                      # Extracted product data
step_4_procurement_report.html  # Final procurement report
```

## Agent Monitoring

AgentOps is used to monitor and trace the multi-agent workflow.

## Future Improvements

* Product deduplication
* Cross-website product matching
* Price normalization and currency conversion
* Better validation for scraped data
* Support for more e-commerce websites and countries
* Price history tracking
* Interactive user interface
* Human approval before final recommendations

## Limitations

The system relies on third-party APIs and external e-commerce websites. Search results, product availability, prices, and extracted information may change depending on API responses and website structure.
