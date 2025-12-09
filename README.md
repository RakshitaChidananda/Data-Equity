📄 Data-Equity: Automated Contract Extraction Using Snowflake Document AI

This repository contains the complete implementation of an automated contract-processing pipeline built using Snowflake Document AI, Snowpark Python, and Snowflake Tasks. The goal of this project is to extract structured contract information—such as contractor name, signing date, RFP number, amounts, and task details—from large PDF documents efficiently and accurately. The system automatically detects large files, splits PDFs into chunks, processes them using Document AI, and stores the final extracted results in a unified Snowflake table.

🎯 Project Objectives

Automate the ingestion and processing of contract PDF files.
Handle large PDFs by splitting them into manageable chunks.
Use Snowflake Document AI to extract key contract fields.
Consolidate extraction outputs into a clean, final table.
Enable continuous automated processing using Snowflake Tasks.
Improve accuracy and reliability of contract metadata extraction.

📚 Data Sources

The project processes contract PDF files stored in Snowflake stages:
AUTOMATION_TESTING_SOURCE → Raw contract PDFs uploaded by the client.
AUTOMATION_TESTING_PROCESSED → Preprocessed or split PDFs used for Document AI.
Document AI model: DAEN_DATA_EQUITY (custom-trained model).

🧠 Key Methodologies & Technologies

PyPDF Library
Reads PDF files, counts pages, and performs splitting for large files.

Snowflake Document AI
Extracts structured information such as contractor, signing date, RFP number, amounts, and more.

Snowflake Tasks
Schedules the automation to run every minute.

Table Reconstruction Logic
Combines chunk-level predictions into final contract-level results.

⚙️ Setup Instructions

1. Open Snowflake Worksheets

Run the setup scripts located in:

Environment Setup Code

Recreate Tasks with new procedure

2. Upload Contract PDFs

Upload documents

3. Run the Processing Procedure Manually
CALL PROCESS_CONTRACTS_PYTHON();

4. Start Automated Processing
ALTER TASK AUTO_CONTRACT_TASK RESUME;

5. View Final Results

SELECT * FROM AUTOMATION_TESTING_FINAL;

🚀 How the Automation Works

The Snowpark Python procedure scans the source stage.

It skips documents already processed.

Large PDFs (>120 pages) are split into smaller chunks.

Each chunk is uploaded to the processed stage.

Snowflake Document AI extracts structured fields.

Extraction outputs are merged and cleaned.

Final results are stored in AUTOMATION_TESTING_FINAL.

A Snowflake Task runs this automatically every minute.

📌Future Enhancements

Improve extraction of low-accuracy fields (e.g., TASK, MAXIMUM_AMOUNT).

Add dashboards for monitoring accuracy and processing times.

Integrate with external storage such as S3 for document archiving.
