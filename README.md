# ClearVue Business Intelligence System

A group project exploring how ClearVue Ltd. could replace slow, manual sales reporting with a flexible NoSQL-based business intelligence (BI) solution. The design focuses on ClearVue’s custom financial calendar, sales performance reporting, and a data foundation that can grow to support supplier analytics.

> **Project:** CMPG321 — Data Dominators, Group 30  
> **Repository:** Enterprise NoSQL Business Intelligence (BI) System  
> **Status:** Academic project and prototype demonstration

## Why this project exists

ClearVue Ltd. needs timely, dependable answers to questions about sales: how performance changes over time, which products and regions are doing well, and where managers should focus next. Its financial periods do not follow ordinary calendar months, which makes consistent reporting more difficult. The company also expects to place greater emphasis on supplier analytics in the future.

This project investigates a document-oriented NoSQL approach to those needs. MongoDB is proposed for storing operational and reference data, with transaction details represented in nested documents where they are naturally read together. Data processing and streaming technologies, together with a BI dashboard, form the broader proposed solution.

## Project goals

The solution is intended to:

- Report on sales by day, week, financial month, quarter, and year.
- Apply ClearVue’s financial calendar consistently: a financial month runs from the last Saturday of the preceding month through the last Friday of the current month.
- Support analysis by customer, region, representative, product, product category, and range.
- Make it possible to extend the model for supplier-focused reporting without redesigning every existing collection.
- Accommodate hierarchical and semi-structured information, including product attributes and customer account parameters.
- Provide clear visual summaries and allow users to move from high-level trends toward transaction details.
- Explore the use of streaming data, such as payment transactions, for more timely insights.

## Proposed solution at a glance

The design uses MongoDB as the document database. Data from the supplied spreadsheet files is cleaned and transformed before loading; a streaming pipeline such as Apache Kafka is proposed for incoming transactions; and a BI tool presents reports and dashboards to business users.

```text
Source spreadsheets / transaction events
                 │
         ETL and validation
       (Kafka for streaming events)
                 │
              MongoDB
                 │
        BI dashboards and reports
```

This diagram describes the intended architecture, not a guarantee that every component is configured for one-click deployment in this repository. The project materials mention different dashboard options at different stages: Power BI appears in the requirements, while Google Looker Studio appears in the implementation report. The choice of visualization tool should therefore be confirmed against the prototype being demonstrated.

## Data model

The conceptual MongoDB design groups data around the way it is used. It favors embedding information that is commonly read together, while keeping large or independently queried histories in their own collections where appropriate.

| Collection | Purpose |
| --- | --- |
| `customers` | Customer profile, category and region descriptions, representative details, account parameters, and a current age-analysis summary. Recent sales may be stored as a limited subset or referenced. |
| `sales` | Sales header information with its line items embedded, including product identifiers and transaction-time product details useful for reporting. |
| `products` | Product master data with category, brand, range, and style details. |
| `suppliers` | Supplier profile and payment or credit information, ready for future supplier analysis. |
| `purchases` | Purchase transactions with their line items embedded. |
| `payments` | Payment header information and associated payment lines. |

Embedding header and line-item data keeps a transaction together for common reads. Selected descriptive fields can be copied into transaction documents so historical reports remain useful even if a product’s current description changes. This is a deliberate read-performance and reporting trade-off; it also means that data updates and consistency rules need to be considered carefully.

## Reporting needs

The project documentation identifies these core analytical use cases:

- **Daily sales:** Sales totals by financial day and customer type, to help spot day-to-day changes.
- **Product trends:** Top products by revenue within product categories and ranges over a financial month.
- **Regional performance:** Compare sales across branches, stores, or regions to inform resource allocation and planning.
- **Supplier spend:** Purchases and associated costs by supplier, supporting future vendor comparisons.
- **Age analysis:** Outstanding customer balances grouped into overdue periods, supporting cash-flow monitoring and credit control.
- **Management summaries:** Weekly representative performance, quarterly regional analysis, and annual overviews.

ClearVue’s financial calendar is a central design requirement rather than a presentation detail. ETL logic and report queries must use the same period definitions so that totals reconcile across daily, monthly, quarterly, and annual views.

## Technology direction

- **Database:** MongoDB, a document-oriented NoSQL database.
- **Streaming:** Apache Kafka is proposed for transaction or payment events.
- **Data preparation:** ETL processes to validate, transform, and load source data.
- **Visualization:** A BI dashboarding tool, with Power BI and Google Looker Studio both referenced in the project materials.

These technologies are the documented design direction. Check the demonstration and accompanying project materials for which components are actually implemented and how they are connected.

## Repository contents

- [`Video Demonstration/`](./Video%20Demonstration/) — Group 30’s Deliverable 2B presentation video.
- [`README.md`](./README.md) — Project overview and guide to the documented design.

The repository currently provides the project overview and presentation. It does not currently document a runnable application, ETL scripts, Kafka configuration, or database seed data. If implementation files are added, this section should be updated with their locations and verified setup instructions.

## Viewing the presentation

The recorded presentation is available here:

[Watch or download the Deliverable 2B video](./Video%20Demonstration/CMPG321%20Group%2030%20Deliverable%202B%20(Compressed).mp4)

## Team

**Data Dominators — Group 30**

- B. Gudla (45997519) — Group Leader
- Z. Nxesi (45183538)
- S. N. Mazibuko (46105948)
- M. Khoza (37600915)
- M. Mashimbye (43314392)

## Project deliverables

The project was prepared for CMPG321 in response to ClearVue Ltd.’s RFP 02/2025:

1. **Deliverable 1 — Requirements Analysis and Conceptual Design:** Business and analytical requirements, source-data analysis, preliminary success criteria, and a conceptual MongoDB model.
2. **Deliverable 2A — Physical Build and Implementation:** The proposed system architecture, implementation approach, design trade-offs, critical success factors, and system documentation.
3. **Deliverable 2B — Presentation:** A recorded demonstration of the proposed solution and its alignment with ClearVue’s requirements.

## Design considerations

The document model is intended to reduce lookups for common reporting paths and to represent hierarchical data naturally. That does not make NoSQL universally better than a relational database: embedding can duplicate descriptive values, large or unbounded arrays need care, and analytical consistency depends on sound ETL and data-quality checks. Financial-period logic, validation of source data, and appropriate indexes are essential to producing trustworthy reports. The project’s success criteria include accurate financial reporting, correct core reports, responsive common queries, flexibility for new supplier data, and stakeholder acceptance.

## AI use

AI tools were used during the coursework for brainstorming and initial drafting of requirements, success criteria, and conceptual schema ideas. The group’s documentation states that generated material was reviewed and adapted against the supplied data and project context. AI assistance was used as a drafting aid; it does not replace validation of the model, implementation, or reported results.

---

*Course project for CMPG321. ClearVue Ltd. is the fictional business context supplied in the project brief.*
