# Step 5: Create Comprehensive Compliance Agent

[← Previous: Step 4](step-04.md) | [Back to Index](../README.md) | [Next: Step 6 →](step-06.md)

Now we'll create a comprehensive Global Risk Company compliance agent that incorporates both our semantic model and the Cortex Search service to provide intelligent analysis across all our data sources.

## Create the Agent

Navigate to the **Agents** section in Snowflake and click **Create Agent**.

### Basic Agent Configuration

**Agent Details:**
- **Name:** `Global_Risk_Compliance_Agent`
- **Display Name:** `Global Risk Compliance Agent`
- **Description:** `Comprehensive compliance intelligence agent with access to internal audit data, client organizations, security incidents, and external regulatory documents via semantic modeling and document search`

Click **Create** to create the basic agent structure.

## Configure Agent Tools

Click on your newly created agent to edit it, then go to the **Tools** section to add both the semantic model and search service.

### Add Internal Compliance Semantic Model

1. **Add Semantic View**
2. **Configuration:**
   - **Database:** `SI_COMPLIANCE_HOL`
   - **Schema:** `PUBLIC`
   - **Semantic View:** `INTERNAL_COMPLIANCE_MONITORING`
   - **Warehouse:** `COMPUTE_WH` (or your default warehouse)
   - **Query Timeout:** `600`
   - **Description:** `Internal compliance monitoring data including client organizations, audit events, and security incidents with relationship modeling for complex queries across structured and semi-structured data`

### Add Cortex Search Service

1. **Add Cortex Search Service**
2. **Configuration:**
   - **Database:** `SNOWFLAKE_INTELLIGENCE`
   - **Schema:** `CONFIG`
   - **Search Service:** `COMPLIANCE_DOCUMENT_SEARCH`
   - **Display Name:** `Compliance Documents`
   - **URL Column:** `URL`
   - **Description:** `Search regulatory documents and compliance frameworks for specific requirements, obligations, and guidance from external data sources`

### Save Agent Configuration

Click **Save** to preserve your agent configuration with both the semantic model and search service.

## Agent Capabilities

Your Global Risk Compliance Agent now has comprehensive capabilities:

**Structured Data Analysis (via Semantic Model):**
- Client organization details and industry classifications
- Audit schedules, types, and compliance status
- Security incident reports with risk assessments and categorization
- Cross-referenced relationships between clients, audits, and security incidents

**Unstructured Data Search (via Cortex Search):**
- Full-text search of regulatory document content
- GDPR, HIPAA, PCI DSS, and other compliance framework documents
- Natural language queries against document text
- Citation tracking with source URLs

**AI-Powered Analysis:**
- Natural language querying across all data sources
- Cross-referencing internal compliance with external regulations
- Relationship-aware queries spanning multiple tables and data formats
- Intelligent synonym recognition for compliance terminology

## Verify Agent Setup

1. **Refresh** the Agents page to ensure your agent appears
2. **Confirm** both the semantic model and search service are attached
3. **Check** that all configurations are saved properly
4. **Verify** the agent shows both tools in the configuration panel

## Agent Architecture Overview

Your agent now provides:

```
Global Risk Compliance Agent
├── Semantic Model (Structured Data)
│   ├── CLIENT_ORGANIZATIONS
│   ├── AUDIT_EVENTS  
│   └── SECURITY_INCIDENTS_VIEW
└── Cortex Search (Unstructured Data)
    └── COMPLIANCE_DOCUMENTS (External Regulatory Text)
```

This architecture enables:
- **Multi-source intelligence** across structured and unstructured data
- **Cross-format analysis** combining relational queries with document search
- **Comprehensive compliance insights** from both internal operations and external regulations

The agent is now ready for comprehensive testing with both structured queries and document search capabilities!

---

**Next Step:** [Step 6: Test Agent with Multi-Source Queries](step-06.md)

[← Previous: Step 4](step-04.md) | [Back to Index](../README.md) | [Next: Step 6 →](step-06.md)
