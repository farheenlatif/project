# Project Title

This project provides an interactive interface using FastAPI for data ingestion, processing, and visualization, backed by Memgraph and MongoDB. It enables users to ingest data files, view transaction details, and interact with data through a chat-based querying system with a real-time graph visualization feature.

## Table of Contents
- [Project Setup](#project-setup)
- [Environment Configuration](#environment-configuration)
- [Running the Application](#running-the-application)
- [Data Ingestion](#data-ingestion)
- [Transaction Viewing](#transaction-viewing)
- [Chat-based Querying and Visualization](#chat-based-querying-and-visualization)
- [Project Structure](#project-structure)

## Project Setup

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd <repository-name>
2. **Set up the necessary environment variables**

   Ensure you have the following keys configured in your environment for seamless access and functionality:

   - `OPENAI_API_KEY`
   - `MEMGRAPH_CREDENTIALS`
   - `AWS_ACCESS_KEY` and `AWS_SECRET_KEY` (for S3 access)
   - `MONGODB_URI` (for MongoDB connection)

3. **Connect Memgraph**: Ensure Memgraph is running and accessible. This is required before running the FastAPI application.

## Environment Configuration
To connect to necessary services like OpenAI, Memgraph, MongoDB, and AWS, ensure that all credentials are set up correctly. This can be done via .env files or setting environment variables directly.

## Running the Application
After setting up the environment variables and confirming the Memgraph connection, you can run the application using:
```bash
uvicorn App.app:app --port 8080
```

The FastAPI interface will be available at http://localhost:8080.

## Data Ingestion

To ingest data into MongoDB and Memgraph:
Use the /savedatatodb endpoint in FastAPI.
Send a POST request with the following JSON structure:
```bash{
  "wt_user_id": "11223",
  "case_id": "000010",
  "name": "okxtestfile",
  "originalName": "string",
  "threatTagging": "string",
  "publicCorruptionTag": "string",
  "description": "string",
  "case_creation_date": "string",
  "size": "string",
  "file_urls": [
    {
      "url": "path/to/Copy_of_300230333390045184_OKX.xlsx",
      "name": "string",
      "originalName": "okx_test",
      "coinexchange_id": "2"
    },
    {
      "url": "path/to/Copy_of_300230333390045184_OKX.xlsx",
      "name": "string",
      "originalName": "abc_test",
      "coinexchange_id": "1"
    }
  ]
}
```
## Transaction Viewing
To retrieve transaction details for a specific case, use the /gettransaction endpoint:

Send a `GET` request to `/gettransaction`.
Provide the case_id as a parameter to view detailed transaction data for that case.

## Chat-based Querying and Visualization
The project includes a chat-based querying system for flexible interactions with the database. Users can enter a query along with the `case_id` to fetch specific results.

Upon successful querying, a graph visualization will be generated. This visualization can be accessed through the graph.html file in the repository, offering a comprehensive, interactive view of the data.

## Project Structure

- **App**: Contains the FastAPI application code.
- **Endpoints**:
  - `savedatatodb`: Endpoint to ingest data.
  - `gettransaction`: Endpoint to fetch transactions based on `case_id`.
- **Templates**:
  - `graph.html`: A visual representation of the query results and data relationships.
