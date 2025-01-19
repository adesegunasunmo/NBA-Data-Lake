# Building a Serverless NBA Data Lake with AWS

This repository provides the setup_nba_data_lake.py script, a one-stop solution to automate building your NBA data lake on AWS.  The script streamlines the integration of essential services:
- **Amazon S3:** Securely stores your NBA data, ready for analysis.
- **AWS Glue:** Creates a data catalog for efficient data discovery.
- **Amazon Athena:** Enables you to query your NBA data directly with SQL-like syntax.
  
With this setup, you'll have the infrastructure in place to store and analyze NBA data for insightful discoveries.

---

## Getting Started

### Prerequisites

*   **NBA API Key**: Obtain your free API key from [SportsData.io](https://sportsdata.io).
*   **AWS Account**: Ensure you have an active AWS account and are familiar with AWS services.
*   **Basic Python Knowledge**: You'll use Python to run the setup script.

---
## Architectural Overview
<img width="632" alt="Screenshot 2025-01-19 215457" src="https://github.com/user-attachments/assets/77a3fdad-04ef-469c-a029-90e8b6d893d8" />
- **CloudShell →** Execute the ```setup_nba_data_lake.py``` script.
- **NBA API →** Fetch player data and send it to the CloudShell environment.
- **CloudShell →** Store fetched data in **Amazon S3**.
- **AWS Glue →** Create a data catalog of the NBA data stored in S3.
- **Amazon Athena →** Query the data stored in S3 using SQL.

---
## Setup Instructions

### Step 1: Access AWS CloudShell

1.  Go to [aws.amazon.com](https://aws.amazon.com/) and sign in to your account.
2.  In the top-right corner, next to the search bar, click the **CloudShell icon** (a square with `>_` inside) to open the AWS CloudShell environment.

---

### Step 2: Create the `setup_nba_data_lake.py` Script

1.  In the CloudShell terminal, type the following command to create a new file:

    ```bash
    nano setup_nba_data_lake.py
    ```

2.  **In another window,** go to the project repository on GitHub and copy the contents of the `setup_nba_data_lake.py` file.

3.  **Go back to the CloudShell terminal** and paste the copied code into the file.

4.  Locate the line under "# SportsData.io configurations" that contains `"api_key"`. Replace the placeholder with your API key:

    ```python
    api_key = "your_sportsdata_api_key"
    ```

5.  Save and exit the file:

    *   Press `Ctrl + X` to exit.
    *   Press `Y` to confirm saving.
    *   Press `Enter` to confirm the file name.

---

### Step 3: Create the `.env` File

1.  In the CloudShell terminal, type the following command:

    ```
    nano .env
    ```

2.  Paste the following lines into the file, replacing `your_sportsdata_api_key` with your actual API key:

    ```bash
    SPORTS_DATA_API_KEY=your_sportsdata_api_key
    NBA_ENDPOINT=[https://api.sportsdata.io/v3/nba/scores/json/Players](https://api.sportsdata.io/v3/nba/scores/json/Players)
    ```

3.  Save and exit the file:

    *   Press `Ctrl + X` to exit.
    *   Press `Y` to confirm saving.
    *   Press `Enter` to confirm the file name.

---

### Step 4: Run the Script

Run the setup script by typing the following command in the CloudShell terminal:

```bash
python3 setup_nba_data_lake.py
```

If everything is configured correctly, you should see the following messages:

- Resources were successfully created.
- Sample data was uploaded successfully.
- Data Lake Setup Completed.

**Step 5: Verify the Setup**

### Check S3 Resources

1. In the AWS Management Console, search for S3 in the search bar and navigate to the service.
2. Look for the **Sports-analytics-data-lake** bucket.
3. Click on the bucket name and verify the following structure:
- `raw-data` folder containing the `nba_player_data.json` file.
4. Open the `nba_player_data.json` file to view its contents (a JSON string of various NBA player data).

### Query the Data with Amazon Athena

1. In the AWS Management Console, search for Athena and navigate to the service.
2. Paste the following sample query into the Athena query editor:

```
SELECT FirstName, LastName, Position, Team
FROM nba_players
WHERE Position = 'PG';
```

Click **Run**. You should see query results under the "Query Results" section.

---

### What I Learned

1. **Securing AWS Services:** Implementing least privilege IAM policies to ensure security.
2. **Automation with Python:** Using scripts to automate the creation and setup of AWS services.
3. **API Integration:** Fetching data from external APIs and integrating it into AWS workflows.
4. **Querying Data:** Using Amazon Athena to analyze data stored in an S3 data lake.

---

### Future Enhancements
1. Automate data ingestion workflows using AWS Lambda.
2. Implement a data transformation layer with AWS Glue ETL.
3. Add advanced analytics and visualizations using AWS QuickSight.

---

### Contribute
If you’d like to contribute to this project, feel free to fork the repository, make changes, and submit a pull request. Feedback is always welcome!

