# CRM Document Ingest

This workflow handles Nexus CRM document upload handoff events.

It is intentionally narrow: normalize document metadata, connect it to CRM entities when provided, create enrichment artifacts, and record failures without inventing business context.
