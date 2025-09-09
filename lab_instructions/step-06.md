# Step 6: Test Complete Compliance Intelligence

[← Previous: Step 5](step-05.md) | [Back to Index](index.md) | [Next: Step 7 →](step-07.md)

Now we'll comprehensively test our Global Risk Compliance Agent across all data sources: structured internal data, semi-structured security incidents, and external regulatory documents.

## Access Snowflake Intelligence

Navigate to **Snowflake Intelligence** from the main Snowflake interface. You should see your **Global Risk Compliance Agent** in the dropdown.

<img src="images/image047.png" alt="alt text" width="45%">

## Test Internal Compliance Data Queries

Start with queries that focus on your internal compliance monitoring data:

### Query 1: Client Analysis
```
Show me the top 5 client organizations by number of scheduled audits.
```

This tests the relationship between CLIENT_ORGANIZATIONS and AUDIT_EVENTS tables.

### Query 2: Regional Compliance
```
Count the total client organizations by region that have GDPR audits scheduled.
```

This tests complex filtering and grouping across related tables.

### Query 3: Risk Assessment
```
Which clients have multiple compliance assessments scheduled?
```

This tests the synonym functionality (assessment = audit) and relationship queries.

### Query 4: Security Incident Analysis
```
Which clients have critical security incidents?
```

This tests the SECURITY_INCIDENTS_VIEW and its relationship to CLIENT_ORGANIZATIONS.

### Query 5: Cross-Source Risk Analysis
```
Show me clients with both high-risk security incidents and upcoming audits.
```

This tests relationships across all three data sources (clients, audits, security incidents).

## Test Document Search Capabilities

Test the agent's document search functionality:

### Query 4: Document Discovery
```
What GDPR documents are available in our regulatory database?
```

### Query 5: Regulatory Analysis  
```
What are the key requirements for GDPR Article 17 Right to Erasure?
```

**Expected Result:** Document search (not SQL generation) with source citations.

### Query 6: Compliance Framework Analysis
```
What penalties are mentioned for PCI DSS non-compliance?
```

### Query 7: Framework Comparison
```
What are the differences between HIPAA and GDPR privacy requirements?
```

## Test Advanced Cross-Source Intelligence

These queries test the agent's ability to combine all data sources:

### Query 8: Client-Specific Regulatory Guidance
```
What GDPR requirements apply to our healthcare clients in Europe?
```

**Expected Result:** Combination of client industry/region data with relevant GDPR document content.

### Query 9: Comprehensive Risk Assessment
```
Which clients have security incidents that could impact their upcoming compliance audits?
```

### Query 10: Industry Risk Assessment  
```
Which financial services clients have critical security incidents that could impact PCI DSS compliance?
```

**Expected Result:** Cross-reference of security incident data with client industries and regulatory requirements.

## Evaluate Agent Performance

For each query, assess:

### Structured Data Queries (Queries 1-3, 5, 8-10)
- **SQL Generation**: Verify appropriate joins between CLIENT_ORGANIZATIONS, AUDIT_EVENTS, and SECURITY_INCIDENTS_VIEW
- **Relationship Utilization**: Confirm the agent uses defined table relationships between all three data sources
- **Synonym Recognition**: Check if 'assessment' synonym works for 'audit' and 'event'/'breach' work for incidents
- **View Integration**: Ensure the SECURITY_INCIDENTS_VIEW provides structured access to risk categories and incident details

### Document Search Queries (Queries 4, 6-7)
- **No SQL Generation**: Document searches should use Cortex Search, not SQL
- **Source Citations**: Results should include document titles and URLs
- **Content Accuracy**: Verify returned content matches actual document text

### Combined Intelligence Queries (Queries 8-10)
- **Multi-Source Integration**: Queries should seamlessly combine structured and unstructured data
- **Contextual Relevance**: Results should be appropriate for the specific client/industry context
- **AI-Enhanced Insights**: Look for intelligent cross-referencing and recommendations

## Mark Successful Queries

For queries that provide accurate, useful results:
1. **Click 👍** to mark them as successful
2. **Review generated SQL** (for structured data queries) to understand the agent's reasoning
3. **Note response patterns** that work well for future reference

## Troubleshooting

**If document search isn't working:**
- Verify the Cortex Search service is ACTIVE in step 4
- Check that the search service is properly attached to the agent in step 5
- Confirm permissions on the EXTERNAL_REGULATORY_DATA database

**If cross-source queries fail:**
- Ensure both the semantic model and search service are attached to the agent
- Verify table relationships are properly defined in the semantic model
- Check that synonyms are configured correctly

Your Global Risk Compliance Agent now demonstrates comprehensive AI-driven compliance intelligence!

---

**Next Step:** [Step 7: Review and Lab Completion](step-07.md)

[← Previous: Step 5](step-05.md) | [Back to Index](index.md) | [Next: Step 7 →](step-07.md)
