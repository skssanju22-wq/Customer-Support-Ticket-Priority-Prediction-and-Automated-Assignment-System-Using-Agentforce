# Customer Support Ticket Priority Prediction and Automated Assignment System Using Agentforce

Salesforce project based on the uploaded project specification. The solution analyzes the latest support ticket for an Account, determines priority from the ticket description, creates a high-priority Task, and returns assignment/priority information for Agentforce.

## Project flow

Account Name
→ Find Account
→ Find latest Support Ticket
→ Analyze Description
→ High / Medium / Low
→ High: Create Urgent Task
→ Assign support level
→ Return result to Agentforce

## Priority rules

| Priority | Description keywords |
|---|---|
| High | `urgent`, `not working`, `failure` |
| Medium | `issue`, `slow`, `delay` |
| Low | none of the above |

These rules follow the supplied project document.

## Repository structure

```text
force-app/main/default/
├── classes/
│   ├── SupportTicketPriorityService.cls
│   ├── SupportTicketPriorityService.cls-meta.xml
│   ├── SupportTicketPriorityServiceTest.cls
│   └── SupportTicketPriorityServiceTest.cls-meta.xml
├── objects/
│   └── Support_Ticket_Intelligence__c/
│       ├── Support_Ticket_Intelligence__c.object-meta.xml
│       └── fields/
│           ├── Ticket_Number__c.field-meta.xml
│           ├── Customer__c.field-meta.xml
│           ├── Contact__c.field-meta.xml
│           ├── Issue_Type__c.field-meta.xml
│           ├── Description__c.field-meta.xml
│           ├── Priority_Level__c.field-meta.xml
│           ├── Status__c.field-meta.xml
│           ├── Created_Date__c.field-meta.xml
│           ├── Assigned_To__c.field-meta.xml
│           ├── SLA_Breach_Risk__c.field-meta.xml
│           └── Resolution_Time__c.field-meta.xml
└── flows/
    └── README-Agentforce-Flow.md
```

## Deploy

1. Install Salesforce CLI.
2. Authenticate to a Salesforce Developer Org / Sandbox.
3. Create a Salesforce DX project or copy this repository into one.
4. Deploy:

```bash
sf project deploy start --source-dir force-app/main/default
```

5. Run tests:

```bash
sf apex run test --tests SupportTicketPriorityServiceTest --result-format human --wait 10
```

## Apex usage

The main invocable action is:

```text
SupportTicketPriorityService.analyzeTicket
```

Input:
- `accountName`

Outputs:
- `accountId`
- `ticketId`
- `priorityLevel`
- `assignedTo`
- `actionMessage`

## Important implementation note

The uploaded specification describes an Auto-Launched Flow and an Agentforce subagent/action. Salesforce orgs can differ in which Agentforce metadata types are deployable through source format. Therefore, the repository includes the deployable Apex/object metadata plus a configuration guide for creating the Flow and Agentforce topic/action in Setup.

## Source

This implementation is based on the uploaded project document, which defines the custom object, fields, priority keywords, Flow logic, and Agentforce configuration. 
