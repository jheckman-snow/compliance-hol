# Step 4: Create Cortex Search Service

[← Previous: Step 3](step-03.md) | [Back to Index](index.md) | [Next: Step 5 →](step-05.md)

Now we'll create a Cortex Search service using the shared regulatory database to enable natural language searching of compliance document content. This will complement our semantic model by providing unstructured text search capabilities.

## Create Cortex Search Service

Navigate to **AI & ML** → **Cortex Search** to create a search service for our compliance documents.

<img src="images/image052.png" alt="alt text" width="45%">

### Configure Search Service

**Basic Configuration:**
- **Database:** `SNOWFLAKE_INTELLIGENCE`
- **Schema:** `CONFIG` (create if it doesn't exist)
- **Name:** `Compliance_Document_Search`

<img src="images/image054.png" alt="alt text" width="45%">

### Select Source Table

**Table Configuration:**
- **Database:** `EXTERNAL_REGULATORY_DATA`
- **Schema:** `PUBLIC`
- **Table:** `COMPLIANCE_DOCUMENTS`

<img src="images/image055.png" alt="alt text" width="45%">

### Configure Search Column

**Search Column:**
- Select `TEXT` as the column to search (this contains the regulatory content)

<img src="images/image056.png" alt="alt text" width="45%">

### Select Attributes

**Return Attributes:**
- Select `DOCUMENT_TITLE` and `URL` as additional attributes to return with search results

<img src="images/image057.png" alt="alt text" width="45%">

### Finalize Configuration

1. **Leave all columns selected** on the column selection page
2. **Set refresh lag** to 1 day (appropriate for static regulatory documents)
3. **Create the search service**

<img src="images/image060.png" alt="alt text" width="45%">

## Monitor Search Service Status

Wait for the search service to show **ACTIVE** status. This may take a few minutes to index the document content.

> **Troubleshooting:** If the service hangs in 'Initialize', run: 
> ```sql
> DESC CORTEX SEARCH SERVICE COMPLIANCE_DOCUMENT_SEARCH;
> ```
> Check the `indexing_error` column for permission issues on the external database, schema, table, or warehouse.

## Test the Search Service

Once active, you can test the search service directly with SQL:

```sql
-- Test basic search functionality
SELECT 
    document_title,
    url,
    search_preview
FROM TABLE(
    SNOWFLAKE_INTELLIGENCE.CONFIG.COMPLIANCE_DOCUMENT_SEARCH(
        'GDPR data protection requirements'
    )
) 
LIMIT 5;

-- Search for specific compliance topics
SELECT 
    document_title,
    url,
    search_preview
FROM TABLE(
    SNOWFLAKE_INTELLIGENCE.CONFIG.COMPLIANCE_DOCUMENT_SEARCH(
        'penalties enforcement actions PCI DSS'
    )
) 
LIMIT 5;

-- Search for technical security requirements
SELECT 
    document_title,
    url,
    search_preview
FROM TABLE(
    SNOWFLAKE_INTELLIGENCE.CONFIG.COMPLIANCE_DOCUMENT_SEARCH(
        'firewall network security controls'
    )
) 
LIMIT 5;
```

## Verify Search Results

Confirm that the search service returns relevant results:

1. **Content Relevance**: Results should match the search terms semantically
2. **Source Attribution**: Document titles and URLs should be included
3. **Preview Quality**: Search previews should show relevant text snippets
4. **Performance**: Queries should execute quickly (sub-second response times)

## Search Service Capabilities

Your Cortex Search service now provides:

**Natural Language Search:**
- Semantic understanding of compliance terminology
- Contextual matching beyond exact keyword searches
- Ability to find related concepts and synonyms

**Structured Results:**
- Document titles for easy identification
- Source URLs for verification and deep-dive reading
- Text previews showing relevant content excerpts

**Integration Ready:**
- Prepared for agent integration in the next step
- Optimized for regulatory document corpus
- Configured for compliance-specific search patterns

The search service is now ready to be integrated with our compliance agent to provide comprehensive document search capabilities alongside structured data analysis.

---

**Next Step:** [Step 5: Create Comprehensive Compliance Agent](step-05.md)

[← Previous: Step 3](step-03.md) | [Back to Index](index.md) | [Next: Step 5 →](step-05.md)