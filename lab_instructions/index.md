# Snowflake Intelligence HOL

## Overview

Global Risk Company's AI-powered regulatory compliance platform processes three distinct types of data to enable intelligent cross-referencing between structured internal compliance data and unstructured external regulatory information.

**Structured Data**: Traditional relational data stored in CSV format with defined schemas
- `client_organizations.csv` - Client companies using the Global Risk Company platform with their regulatory focus areas
- `audit_events.csv` - Scheduled and completed compliance audits across clients

**Semi-Structured Data**: JSON formatted security incident reports that provide context about security events
- `security_incidents.json` - Security incident records with nested objects containing asset information, mitigation steps, and risk assessments

**External Data**: Regulatory intelligence accessed via Snowflake Data Sharing
- Real-time regulatory updates and compliance frameworks
- AI-powered analysis and cross-referencing capabilities

## Lab Steps

This hands-on lab is divided into 7 streamlined steps that progressively build Global Risk Company's comprehensive compliance intelligence platform:

### Data Foundation
1. [**Step 1: Getting Data Into Snowflake**](step-01.md) - Load structured and semi-structured compliance data with view creation
2. [**Step 2: External Data Integration via Snowflake Data Sharing**](step-02.md) - Access external regulatory intelligence with AI analysis

### AI Intelligence Setup
3. [**Step 3: Snowflake Intelligence Setup & Semantic Models**](step-03.md) - Configure platform and create semantic model
4. [**Step 4: Create Cortex Search Service**](step-04.md) - Build document search for regulatory content
5. [**Step 5: Create Comprehensive Compliance Agent**](step-05.md) - Build unified agent with semantic model and search capabilities

### Testing and Completion
6. [**Step 6: Test Complete Compliance Intelligence**](step-06.md) - Comprehensive testing across all data sources
7. [**Step 7: Review and Lab Completion**](step-07.md) - Lab summary, validation, and cleanup

## Learning Objectives

By completing this lab, you will learn how to:
- Load and process multiple data formats in Snowflake (structured, semi-structured, external)
- Leverage Snowflake Data Sharing for external intelligence integration
- Use Cortex AISQL functions for AI-powered regulatory analysis
- Build comprehensive Snowflake Intelligence agents with dual semantic models
- Create and configure semantic models for intelligent data querying
- Implement document search using Cortex Search for unstructured content
- Cross-reference internal compliance data with external regulatory intelligence
- Test and validate cross-source AI intelligence capabilities

## Key Technologies Demonstrated

- **Snowflake Data Sharing**: Secure external data integration
- **Cortex AISQL Functions**: AI-powered text analysis and extraction
- **Snowflake Intelligence**: Natural language querying platform
- **Semantic Models**: Intelligent data relationship modeling
- **Cortex Search**: Unstructured document search and analysis
- **Multi-Format Data Integration**: CSV, JSON, and shared data sources

## Prerequisites

- Access to a Snowflake account with SYSADMIN role
- Basic familiarity with SQL
- Understanding of compliance and regulatory concepts

## Estimated Time

Complete lab: 1-1.5 hours (streamlined 7-step version with simplified testing)

---

**Ready to get started?** Begin with [Step 1: Getting Data Into Snowflake](step-01.md)
