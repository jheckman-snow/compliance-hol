# Step 2: External Data Integration via Snowflake Data Sharing

[← Previous: Step 1](step-01.md) | [Back to Index](index.md) | [Next: Step 3 →](step-03.md)

Now that we have our foundation data loaded (structured and semi-structured), we'll demonstrate how Global Risk Company accesses external regulatory intelligence through Snowflake Data Sharing. This represents the third data type in our progressive strategy: unstructured external data from regulatory bodies and compliance frameworks.

## Understanding Data Sharing for Compliance Intelligence

Snowflake Data Sharing enables Global Risk Company to access real-time regulatory updates, legal interpretations, and compliance frameworks from external providers without data movement. This external intelligence is then cross-referenced with internal compliance data using AI.

**Key Benefits for Regulatory Compliance:**
- Real-time access to regulatory updates
- No data duplication or ETL processes
- Secure access to sensitive regulatory information
- Integration with existing compliance workflows

## Accessing a Private Data Share

In this step, we'll simulate accessing external regulatory data through a private data share. In a real-world scenario, this could be regulatory documents from government agencies, legal interpretations from law firms, or compliance frameworks from industry bodies.

### Step 2a: List Available Data Shares

First, let's see what data shares are available to your account:

```sql
-- List all available data shares (both inbound and outbound)
SHOW SHARES;
```

### Step 2b: View Share Details

To examine the contents of a specific share before consuming it:

```sql
-- This shows the databases and schemas available in the share
DESC SHARE COMPLIANCE_DOCUMENTS_SHARE;
```

### Step 2c: Create Database from Share

Once you've identified the share you want to consume, create a database from it:

```sql
-- Create a database from a private data share
-- Replace with actual share provider account and share name
CREATE DATABASE EXTERNAL_REGULATORY_DATA 
FROM SHARE SFSENORTHAMERICA.JHECKMAN_AWS1.COMPLIANCE_DOCUMENTS_SHARE;

-- Grant access to the shared database
GRANT IMPORTED PRIVILEGES ON DATABASE EXTERNAL_REGULATORY_DATA TO ROLE SYSADMIN;
GRANT IMPORTED PRIVILEGES ON DATABASE EXTERNAL_REGULATORY_DATA TO ROLE PUBLIC;
```

### Step 2d: Explore Shared Data

Now explore the structure and content of the shared data:

```sql
-- List schemas in the shared database
SHOW SCHEMAS IN DATABASE EXTERNAL_REGULATORY_DATA;

-- List tables in a specific schema
SHOW TABLES IN DATABASE EXTERNAL_REGULATORY_DATA.PUBLIC;

-- Examine table structure
DESC TABLE EXTERNAL_REGULATORY_DATA.PUBLIC.COMPLIANCE_DOCUMENTS;

-- Sample the data to understand its structure
SELECT * FROM EXTERNAL_REGULATORY_DATA.PUBLIC.COMPLIANCE_DOCUMENTS LIMIT 5;
```

### Step 2e: AI-Powered Analysis of Shared Regulatory Data

Here is a query that demonstrate Snowflake's AI SQL capabilities for intelligent regulatory analysis using the stable Snowflake Cortex functions:

```sql
-- Query 1: AI-Powered Regulatory Classification and Analysis
-- Use SNOWFLAKE.CORTEX functions to analyze and categorize compliance documents
SELECT 
    cd.DOCUMENT_TITLE,
    -- Extract regulation type from document title
    CASE 
        WHEN cd.DOCUMENT_TITLE ILIKE '%GDPR%' THEN 'GDPR'
        WHEN cd.DOCUMENT_TITLE ILIKE '%HIPAA%' THEN 'HIPAA'
        WHEN cd.DOCUMENT_TITLE ILIKE '%PCI%' THEN 'PCI DSS'
        WHEN cd.DOCUMENT_TITLE ILIKE '%CCPA%' THEN 'CCPA'
        WHEN cd.DOCUMENT_TITLE ILIKE '%SOX%' THEN 'SOX'
        WHEN cd.DOCUMENT_TITLE ILIKE '%ISO%' THEN 'ISO 27001'
        WHEN cd.DOCUMENT_TITLE ILIKE '%NIST%' THEN 'NIST'
        ELSE 'Other'
    END as REGULATION_TYPE,
    -- Summarize the regulatory text
    SNOWFLAKE.CORTEX.SUMMARIZE(cd.TEXT) as AI_SUMMARY,
    -- Analyze sentiment of regulatory language
    SNOWFLAKE.CORTEX.SENTIMENT(cd.TEXT) as REGULATORY_SENTIMENT,
    -- Classify compliance complexity
    SNOWFLAKE.CORTEX.CLASSIFY_TEXT(
        cd.TEXT, 
        ['High Complexity', 'Medium Complexity', 'Low Complexity']
    ) as COMPLIANCE_COMPLEXITY,
    -- Extract key compliance actions
    SNOWFLAKE.CORTEX.EXTRACT_ANSWER(
        cd.TEXT, 
        'What is the primary compliance action required?'
    ) as PRIMARY_ACTION
FROM EXTERNAL_REGULATORY_DATA.PUBLIC.COMPLIANCE_DOCUMENTS cd
WHERE cd.TEXT IS NOT NULL
ORDER BY REGULATION_TYPE, cd.DOCUMENT_TITLE;

```

These AI-powered queries demonstrate how Global Risk Company can leverage Snowflake's Cortex functions to:
- Extract specific compliance obligations and required actions from regulatory documents
- Automatically summarize complex regulatory text for quick understanding  
- Classify documents by regulation type and compliance complexity
- Analyze regulatory sentiment to understand the tone and impact of regulations
- Extract key timeframes and deadlines for compliance planning
- Cross-reference external regulatory requirements with internal client data for personalized compliance analysis
- Generate detailed risk assessments for non-compliance scenarios using large language models
- Identify penalties and enforcement actions mentioned in regulations

**Key AI Functions Available:**
- `SNOWFLAKE.CORTEX.EXTRACT_ANSWER()` - Extract specific information from unstructured text
- `SNOWFLAKE.CORTEX.SUMMARIZE()` - Create concise summaries of complex documents
- `SNOWFLAKE.CORTEX.SENTIMENT()` - Analyze emotional tone and regulatory stance
- `SNOWFLAKE.CORTEX.CLASSIFY_TEXT()` - Categorize documents by complexity or type
- `SNOWFLAKE.CORTEX.COMPLETE()` - Generate comprehensive responses using Large Language Models

> **Note:** These queries use the generally available Snowflake Cortex functions in the SNOWFLAKE.CORTEX schema as documented in the [official Snowflake documentation](https://docs.snowflake.com/en/user-guide/snowflake-cortex/aisql). While newer AI_ prefixed functions exist as preview features, the SNOWFLAKE.CORTEX functions are stable and available in all Snowflake accounts with Cortex enabled.

This external data integration step demonstrates how Global Risk Company's AI-powered compliance platform leverages Snowflake's Data Sharing capabilities to access real-time regulatory intelligence, setting the foundation for the AI cross-referencing capabilities we'll build in the following steps.

---

**Next Step:** [Step 3: Snowflake Intelligence Setup](step-03.md)

[← Previous: Step 1](step-01.md) | [Back to Index](index.md) | [Next: Step 3 →](step-03.md)
