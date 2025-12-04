# Airbnb Data Pipeline

## Website Description
**Target:** [Airbnb](https://www.airbnb.com/) (Almaty listings).
**Type:** Dynamic website (React-based) requiring JavaScript rendering.
**Content:** The project scrapes rental listings, handling infinite scrolling and pagination using Playwright to extract titles, prices, and links.

## How to Run Scraping (Manual)
1. **Install dependencies:**
   ```bash
   pip install pandas playwright apache-airflow
   playwright install
   
2. Run the scraper:
   
Bash


   python src/scraper.py
   
   *This creates data/raw_data.csv.*

## How to Run Airflow
1. Start Airflow:
   Run in terminal:
   
Bash


   export AIRFLOW_HOME=$(pwd)
   airflow standalone
   
   *(For Windows PowerShell: `$env:AIRFLOW_HOME = Get-Location`)*

2. Access Interface:
   - Open http://localhost:8080.
   - Login with admin and the password shown in the terminal.

3. Run Pipeline:
   - Find `airbnb_project_dag`.
   - Toggle the switch to Unpause (Blue).
   - Click the Play ▶️ button -> Trigger DAG.

## Expected Output
After the pipeline finishes, the data/ folder will contain:
1. `raw_data.csv`: Raw data (>100 records).
2. `cleaned_data.csv`: Processed data without duplicates.
3. `output.db`: SQLite database with the final table.

Database Schema (`listings` table):
- id: INTEGER (Primary Key)
- title: TEXT
- price_original: TEXT (e.g., "$ 150")
- price_cleaned: INTEGER (e.g., 150)
- link: TEXT
`