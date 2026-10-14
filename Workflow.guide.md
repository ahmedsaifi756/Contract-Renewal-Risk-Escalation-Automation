
# Workflow Guide

## 1. Receive Contract Input

The workflow begins at a webhook, which acts as the entry point for incoming contract information.

## 2. Validate Contract Input

The workflow checks the incoming request before processing. Invalid input should be handled explicitly rather than passed through the entire workflow.

## 3. AI Contract Term Extraction

The AI model extracts structured fields from the supplied contract information.

Expected fields may include:
- Contract ID
- Vendor name
- Renewal date
- Notice period in days
- Auto-renewal status
- Annual contract value

The exact output depends on the configured prompt and input format.

## 4. Validate and Normalize Contract Terms

The workflow checks extracted values before using them downstream. Dates, numeric fields, and boolean values should be represented consistently.

## 5. Calculate Renewal Metrics

The workflow calculates the notice deadline and days remaining until that deadline.

These calculations depend on valid dates and the selected date-handling rules.

## 6. Determine Renewal Risk

The workflow evaluates the calculated metrics against configured business rules and assigns a risk status.

The example urgent-review status is `URGENT_REVIEW`.

## 7. Store the Result in PostgreSQL

The processed contract information is saved to the configured database table.

The actual database columns, uniqueness constraints, and conflict-handling behavior are defined by the implementation.

## 8. Send a Conditional Slack Alert

The workflow checks whether the contract meets the configured alert condition. Urgent contracts trigger a Slack notification.

Non-urgent contracts should follow the non-alert path.

## Operational Note

Review failed executions, missing fields, invalid dates, duplicate submissions, and database or Slack errors before using the workflow with real business data.
