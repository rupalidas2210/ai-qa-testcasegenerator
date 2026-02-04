# Spectrum Brand Manager

## High Level Component Diagram

As part of the Spectrum Brand Manager initiative, two new components will be introduced:

- **Brand Manager Web** – Frontend UI where users interact with brand features.
- **Brand Manager App (BFF)** – Backend-for-Frontend that orchestrates data from backend APIs.

Built on existing OMS OrderHub codebase for faster delivery.

## Login Workflow

- Uses Spectrum login system
- Access controlled via Feature IDs and Roles
- Authorization via Omni Auth Library
- Roles managed using Access Manager and Configuration Manager


## Brand Manager Screen Components – Phase 1

### Brand Level Stats
- Uses existing OrderHub aggregate API

### Store Level Stats
- Combines Stores API and NOS Bulk Order API
- Pagination considered future enhancement

### Orders Screen
- Fetch orders via OrderHub
- Pagination depends on NOS API support

### Order Details Screen
- Uses OrderHub Order Details API
- Integrates with SHREWS for refunds and SRs

### Order and Customer Search
- Order ID → Order Hub
- Customer ID → Fetch orders by customer

### Cancellations via Expedite
- Bulk cancel API provided by OMS

## Database and Storage

- CosmosDB used for expedite reports
- CSV generated dynamically by FE






