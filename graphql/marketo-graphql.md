# Marketo (Adobe) GraphQL Schema

## Overview

Marketo Engage is Adobe's marketing automation platform offering programmatic access to leads, programs, campaigns, assets, lists, and bulk import/export via a REST API. This conceptual GraphQL schema represents the Marketo Engage REST API surface as a typed GraphQL layer, covering the core domains: lead database, campaigns, assets, programs, custom objects, and integrations.

**Provider:** Marketo (Adobe)
**Base REST API:** https://developers.marketo.com/rest-api/
**Developer Portal:** https://developers.marketo.com/
**Documentation:** https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/rest-api

## Schema Source

This schema was derived from the Marketo Engage REST API documentation and the community-supported client libraries available at https://github.com/Marketo/Community-Supported-Client-Libraries. It is a conceptual GraphQL representation of the REST API surface, not an officially published GraphQL endpoint.

## Domain Coverage

### Lead Database
The lead database is the central store for all person/lead records. Types include `Lead`, `LeadField`, `LeadActivity`, `LeadPartition`, `LeadDatabase`, and `WorkspaceLead`. The lead object supports hundreds of standard and custom fields, partitioned across workspaces.

### Companies and Opportunities
B2B objects linking leads to account-level data. Types include `Company`, `CompanyField`, `Opportunity`, `OpportunityRole`, and `NamedAccount`. These objects sync with CRM systems such as Salesforce and Microsoft Dynamics.

### Lists and Segmentation
Smart and static list management for targeting and segmentation. Types include `List`, `StaticList`, `DynamicList`, `SmartList`, `Filter`, and `AccountList`.

### Campaigns
Campaign execution and scheduling. Types include `Campaign`, `SmartCampaign`, `BatchCampaign`, `Trigger`, `Flow`, and `Schedule`. Smart campaigns contain trigger/filter logic and flow steps.

### Programs and Channels
Program hierarchy and membership tracking. Types include `Program`, `ProgramChannel`, `ProgramMember`, and `ABTest`. Programs organize campaigns and assets under a common reporting structure.

### Assets
Marketing asset management. Types include `Asset`, `LandingPage`, `LandingPageTemplate`, `Form`, `FormField`, `Email`, `EmailTemplate`, `Snippet`, `Folder`, `FolderType`, `Tag`, and `TagType`.

### Custom Objects
Extensible data objects linked to leads or companies. Types include `CustomObject`, `CustomObjectField`, and `CustomObjectList`.

### Activities
All interaction tracking. Types include `ActivityType`, `ActivityAttribute`, `MarketingActivity`, and `SalesActivity`.

### Webhooks and API Access
Integration and automation support. Types include `Webhook`, `APIKey`, and `TokenRecord`.

### CRM Integrations
Native CRM sync support. Types include `SalesforceSync`, `MSCRMSync`, `GoToWebinar`, `ZoomWebinar`, and `SocialMedia`.

### Workspaces and Partitions
Multi-workspace support for enterprise deployments. Types include `WorkspacePartition` and `WorkspaceLead`.

## Types Summary

| Type | Domain |
|---|---|
| Lead | Lead Database |
| LeadField | Lead Database |
| LeadActivity | Lead Database |
| LeadPartition | Lead Database |
| LeadDatabase | Lead Database |
| WorkspaceLead | Lead Database |
| Company | Companies |
| CompanyField | Companies |
| Opportunity | Opportunities |
| OpportunityRole | Opportunities |
| NamedAccount | Accounts |
| AccountList | Accounts |
| List | Lists |
| StaticList | Lists |
| DynamicList | Lists |
| SmartList | Lists |
| Filter | Lists |
| Campaign | Campaigns |
| SmartCampaign | Campaigns |
| BatchCampaign | Campaigns |
| Trigger | Campaigns |
| Flow | Campaigns |
| Schedule | Campaigns |
| Program | Programs |
| ProgramChannel | Programs |
| ProgramMember | Programs |
| ABTest | Programs |
| Asset | Assets |
| LandingPage | Assets |
| LandingPageTemplate | Assets |
| Form | Assets |
| FormField | Assets |
| Email | Assets |
| EmailTemplate | Assets |
| Snippet | Assets |
| Folder | Assets |
| FolderType | Assets |
| Tag | Assets |
| TagType | Assets |
| ActivityType | Activities |
| ActivityAttribute | Activities |
| MarketingActivity | Activities |
| SalesActivity | Activities |
| CustomObject | Custom Objects |
| CustomObjectField | Custom Objects |
| CustomObjectList | Custom Objects |
| Webhook | Integrations |
| APIKey | Integrations |
| TokenRecord | Integrations |
| SalesforceSync | Integrations |
| MSCRMSync | Integrations |
| GoToWebinar | Integrations |
| ZoomWebinar | Integrations |
| SocialMedia | Integrations |
| WorkspacePartition | Workspaces |

## File

- `marketo-schema.graphql` — Full GraphQL SDL with 65+ named types covering all domains above.
