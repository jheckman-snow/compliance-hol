# Step 3: Snowflake Intelligence Setup & Semantic Models

[← Previous: Step 2](step-02.md) | [Back to Index](index.md) | [Next: Step 4 →](step-04.md)

Now that we have our data foundation in place (structured, semi-structured, and external data), we'll set up Snowflake Intelligence and create semantic models for our compliance datasets.

## Snowflake Intelligence Setup

### Important Requirements:
  * Users for Snowflake Intelligence need to have a default role and a default warehouse
  * The database needs to be named `Snowflake_intelligence`
  * Users need permission to call Cortex functions and access underlying data

### Create Metadata Objects

Create a new worksheet and run this script to create the database and schema needed for Snowflake Intelligence:

```sql
use role sysadmin;
create database snowflake_intelligence;
create schema snowflake_intelligence.agents;

-- make sure anyone in the account can SEE agents
grant usage on schema snowflake_intelligence.agents to role public;

-- optional - you can grant other roles the ability to create agents
-- grant create agent on schema snowflake_intelligence.agents to role <some_role>;
```

## Create Semantic View

We'll create a semantic view to cover our structured data:

###Internal Compliance Data

Navigate to **AI & ML** → **Cortex Analyst** and create a new semantic view:

**Configuration:**
- **Database:** `SI_COMPLIANCE_HOL`
- **Schema:** `PUBLIC`
- **Name:** `internal_compliance_monitoring`
- **Description:** `Internal compliance data including client organizations, audit events, and security incidents`

**Select Tables:**
- `CLIENT_ORGANIZATIONS`
- `AUDIT_EVENTS`
- `SECURITY_INCIDENTS_VIEW` (the structured view we created from JSON data)

**Key Configuration Steps:**
1. **Move ID columns to dimensions:**
   - AUDIT_EVENTS: Move `AUDIT_ID` and `CLIENT_ID` to dimensions
   - CLIENT_ORGANIZATIONS: Move `CLIENT_ID` to dimensions
   - SECURITY_INCIDENTS_VIEW: Move `CLIENT_ID` to dimensions
   - Mark `CLIENT_ID` columns as unique identifiers in all tables
   - Mark `AUDIT_ID` and `INCIDENT_ID` as unique identifiers

2. **Add synonyms:**
   - AUDIT_NAME: Add 'assessment' and 'review' as synonyms
   - INCIDENT_TYPE: Add 'event' and 'breach' as synonyms
   - RISK_CATEGORY: Add 'priority' and 'severity' as synonyms

3. **Define relationships:**
   - **Relationship 1:** `AuditEvents_to_ClientOrganizations`
     - Left Table: `AUDIT_EVENTS`
     - Right Table: `CLIENT_ORGANIZATIONS`  
     - Join on: `CLIENT_ID`
   
   - **Relationship 2:** `SecurityIncidents_to_ClientOrganizations`
     - Left Table: `SECURITY_INCIDENTS_VIEW`
     - Right Table: `CLIENT_ORGANIZATIONS`
     - Join on: `CLIENT_ID`

### Test Your Semantic View

Test with sample queries:

**For Internal Compliance Model:**
```
What are the different client organizations in Europe?
How many audits are scheduled for GlobalBank Financial Services?
Count the total client organizations by region that have GDPR audits scheduled
Which clients have critical security incidents?
Show me the risk breakdown of security events by client industry
What is the average risk score for incidents in the financial services sector?
```

### Save and Verify

1. Save the semantic models
2. Add successful test queries as verified queries
3. Refresh the page to ensure all configurations are saved

---

**Next Step:** [Step 4: Create Comprehensive Compliance Agent](step-04.md)

[← Previous: Step 2](step-02.md) | [Back to Index](index.md) | [Next: Step 4 →](step-04.md)
