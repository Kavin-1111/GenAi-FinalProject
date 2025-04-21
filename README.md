Company Information Extractor

This app allows users to input a company name and automatically extracts detailed company information from the web using a combination of:
Domain Discovery
- Uses Google Search to find the **official website** of a company.

Web Scraping & Text Extraction
- Crawls the main page and internal links using `requests` with a fallback to `Selenium` for JavaScript-heavy pages.
- Extracts and cleans the visible text content using **BeautifulSoup**.

Text Chunking & Embedding
- Splits raw website content into chunks (~500 words).
- Encodes each chunk into dense vector embeddings using SentenceTransformers (`all-MiniLM-L6-v2`).

Supabase Vector Store
- Stores embeddings and text chunks in a **Supabase** table.
- Enables **semantic retrieval** of the most relevant content using cosine similarity.

Gemini (Google Generative AI)
- Sends the top relevant text chunks to **Gemini 1.5 Flash**.
- Asks it to extract structured fields like:
  - Description, Industry, Software Classification
  - Customers, Investors, Employee Headcount
  - Address Info (City, Region, ZIP, Country)
  - Finance, Email, Phone, and more

SerpAPI Fallback
- For missing fields, uses **SerpAPI** to intelligently search the web and retrieve any remaining information.

 Input
- Company name (e.g., jman group,lenovo)

 Output
- JSON-style dictionary with key-value pairs:
  
{
  "Company Description": "Zurich Insurance is a leading...",
  "Industry": "Insurance",
  "Email": "contact@zurich.com",
  ...
}
- Streamlit for UI
- SentenceTransformers for semantic embeddings
- Google Gemini for language understanding and information extraction
- Supabase for vector storage and retrieval
- BeautifulSoup, Selenium, requests for scraping
- SerpAPI for fallback field completion

Third Party Applications Used
-Serp Api
-Crunch base
-Clearbit Company API
-Finnhub

Challenges
-No financial data available explcitly for many companies
-LLM api rate Limits
-No third parties are free of cost
-No sites avaliable for few websites
-Selenium debugging isses as is heavy weight

