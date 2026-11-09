# ClearVue Business Intelligence System

A group project focused on designing and presenting a modern NoSQL-based Business Intelligence (BI) solution for ClearVue Ltd. The project explores how a document database can support sales analysis, financial-period reporting, and future supplier analytics in a way that is more flexible than a traditional relational model.

> **Project:** CMPG321 — Data Dominators, Group 30  
> **Repository:** Enterprise NoSQL Business Intelligence (BI) System  
> **Status:** Academic project and prototype demonstration

## Overview

ClearVue Ltd. needs a reporting solution that can support daily, weekly, monthly, quarterly, and annual sales analysis while aligning with its custom financial calendar. The company’s financial periods do not follow the normal calendar structure, which makes consistent and accurate reporting more complex in a traditional relational setup.

This project investigates a document-oriented NoSQL design using MongoDB as the core database and Google Looker Studio for dashboard reporting. The aim is to show how data can be structured to support hierarchical, semi-structured, and growing business information while improving reporting speed and flexibility.

## Business problem

ClearVue currently faces challenges in producing timely and accurate business intelligence from sales data. Management needs reliable insight across multiple timeframes, including performance by customer, region, product, and representative. The reporting requirements are also shaped by ClearVue’s non-standard financial year, which runs from the last Saturday of one month to the last Friday of the next month.

At the same time, the organisation expects to move toward supplier-focused analytics in the future. That means the solution must be designed with flexibility in mind, rather than relying on rigid database structures that would require major redesign as new data sources emerge.

## Project goals

The project was designed to:

- Support sales reporting by day, week, financial month, quarter, and year.
- Align every report to ClearVue’s unique financial-period structure.
- Analyse performance by customer, region, product category, product range, and representative.
- Build a data model that can support future supplier analytics without reworking the entire system.
- Handle nested and semi-structured data naturally.
- Produce dashboards and visual summaries that are useful to business users.
- Demonstrate the benefits of a NoSQL document model over a traditional relational model for this use case.

## Proposed architecture

The design uses MongoDB as the main database for storing customer, sales, product, purchase, payment, and supplier-related data. Reporting is delivered through Google Looker Studio dashboards, which provide an accessible way for users to view KPI summaries and drill into key business questions.

```text
Source data files
        │
        ▼
  Data preparation / ETL
        │
        ▼
      MongoDB
        │
        ▼
  Google Looker Studio
        │
        ▼
    Business dashboards
```

The project materials describe a system where MongoDB stores structured and nested business data in a way that matches the way the organisation analyses it. Examples include embedded sales line items, customer account parameters, and product descriptors stored close to the main business entity they describe.

## Data model

The conceptual NoSQL design groups related information into collections so that common reporting paths are efficient and easier to query.

| Collection | Purpose |
| --- | --- |
| `customers` | Stores customer profile information, category and region details, representative references, account parameters, and current age-analysis summaries. |
| `sales` | Stores sales document headers with embedded sales lines, including product and transaction details for reporting. |
| `products` | Stores product master data, category details, brand and range information, and style-related attributes. |
| `suppliers` | Stores supplier master information to support future supplier analytics. |
| `purchases` | Stores purchase headers and embedded purchase lines for spend and cost analysis. |
| `payments` | Stores payment headers and related payment details for cash-flow and payment tracking. |

This approach supports embedded data where it is frequently accessed together, which reduces the need for complex joins and helps reporting run more naturally for business users. It also preserves flexibility because new data attributes can be added without requiring a rigid table redesign.

## Reporting and analytical needs

The project identifies several core business reports and performance questions in the project documentation:

- **Daily sales performance:** Daily totals by customer type and sales activity.
- **Monthly product trends:** Top products and product categories by revenue.
- **Regional comparisons:** Sales and performance across regions and branches.
- **Supplier analysis readiness:** Purchase and spend reporting by supplier for future supplier-focused decision making.
- **Age analysis:** Customer balances grouped into overdue periods to support collection and credit control.
- **Representative performance:** Weekly and monthly comparison of sales representatives.
- **Financial-period reporting:** Monthly, quarterly, and annual views based on ClearVue’s custom financial calendar.

The reporting design is built around data that is easy to aggregate and visualise, while also preserving the detail needed for deeper business investigation.

## Why NoSQL for this project

The NoSQL model is suitable because the business data has several characteristics that are difficult to handle efficiently with a rigid relational structure:

- hierarchical data (for example, product and customer groupings)
- semi-structured information in different entities
- nested transaction details
- evolving requirements as new analytics areas are introduced
- a need for faster, more flexible reporting and dashboard access

The project therefore uses a document-oriented database to better match the real-world structure of the data and the way management wants to query it.

## Repository contents

- [`Video Demonstration/`](./Video%20Demonstration/) — Video presentation for the project deliverable.
- [`README.md`](./README.md) — Overview of the project and its design direction.

This repository acts mainly as a project archive and presentation space for the coursework deliverables. It documents the thinking, architecture, and reporting direction rather than a full production-ready application.

## Presentation

The recorded presentation for this project is available here:

[Watch the Deliverable 2B video](./Video%20Demonstration/CMPG321%20Group%2030%20Deliverable%202B%20(Compressed).mp4)

## Deliverables

The project covers the required academic deliverables:

1. **Deliverable 1 — Requirements Analysis and Conceptual Design**  
   Business requirements, source-system analysis, preliminary success criteria, and a conceptual NoSQL design.

2. **Deliverable 2A — Physical Build and Implementation**  
   Prototype architecture, implementation approach, design trade-offs, and system documentation.

3. **Deliverable 2B — Presentation**  
   Recorded presentation of the proposed BI solution and how it aligns with ClearVue’s needs.

## Design considerations

The document model supports efficient access to data that is often read together, such as sales transactions and their detailed line items. This helps reduce unnecessary joins and makes the analytics layer easier to build around business questions. However, the project also recognises that NoSQL trade-offs exist, including denormalised data and the need for strong ETL validation.

The project’s success criteria focus on:

- accurate financial-period reporting
- correct generation of core reports
- sensible query performance for interactive analysis
- flexibility for future data changes
- stakeholder approval of the dashboards and insights

## AI use

AI tools were used during the project to help structure initial drafts, generate ideas for requirements, and support conceptual schema design. The project documentation notes that all outputs were reviewed and adapted against the original business context and supplied data to keep the work accurate and relevant.

---

*This project is part of the CMPG321 coursework and uses the fictional ClearVue Ltd. scenario provided in the project brief.*
