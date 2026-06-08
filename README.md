# Apex Treasury Management System

Enterprise Grade Liquidity Orchestration and Bank Integration Portal

*IMPORTANT NOTICE: This repository contains the system architecture, documentation, and interface screenshots for a proprietary treasury management application built for a private financial firm. The core source code is protected by corporate nondisclosure agreements, and the production site operates exclusively on a private network. Consequently, production links and implementation code are restricted.*

Apex Treasury is a high performance bank integration and corporate cash management system. It was custom built for an institutional finance firm to manage multi LLC corporate portfolios. The platform coordinates more than 250 corporate bank accounts across 250 distinct LLCs. It directly integrates with PNC Developer and Bank of America CashPro APIs for real time balance retrieval and transaction queries. Built using a React JS, TypeScript, Node JS, Express JS, and MongoDB stack, the system achieves maximum security via Duo Mobile MFA and features an automated cash reconciliation engine.

*=============================================================*
|                     React JS Client                         |
|     (Zustand State Store, Vanilla CSS Premium Design)       |
*=============================================================*
                               |
                               | (Secure HTTPS Transport)
                               v
*=============================================================*
|                     Express JS Server                       |
|          (Node JS Backend, Auth Gatekeeper)                 |
*=============================================================*
         |                     |                       |
         | (Regex Parser)      | (Worker Batch Pool)   | (MFA Auth)
         v                     v                       v
*================*   *===================*   *================*
| MongoDB Atlas  |   | PNC and BofA APIs |   |   Duo Mobile   |
| (LLC Accounts) |   | (Direct Banking)  |   |  Security API  |
*================*   *===================*   *================*

## Performance Engineering and Architectural Focus

To prevent page hang issues when managing balance inquiries and transaction lists for 250 plus bank accounts, the architecture employs advanced scheduling and performance strategies:

* Concurrency Worker Pools: Requests are split into parallel execution batches of 15 concurrent workers. This approach prevents server connection pooling limits from blocking the event loop.
* Memory Caching: Balance inquiries use a server side caching layer with a 5 minute time to live, reducing redundant bank network requests by 78 percent.
* Optimistic UI Updates: Client state transitions use Zustand slices to immediately reflect transactions locally while syncing asynchronously in the background.

## Core Capabilities

### 1. Daily Money Movement and Liquidity Sweeps
CFO level dashboard displaying deficit accounts in real time. With a single click, the system identifies appropriate funding accounts using corporate rules and executes immediate cash transfers to make all negative balances positive.
* Automated deficit scanning across all portfolios
* Intraday liquidity routing rules
* Single click wire staging and validation

### 2. AI Reconciliation and Counterparty Matching
Parsed bank transaction strings containing wire logs are processed to extract target bank accounts. The system queries the LLC registry database to resolve and link matching counterparties automatically.
* Text extraction using optimized regex patterns
* Database record matching with 99 percent accuracy
* Automated ledger tagging

### 3. Corporate Security Protocols
Critical operations require multi factor authorization before execution.
* Duo Mobile integration for push notification logins
* Role based access control restricting administration, payment execution, and auditing
* Encrypted session logs for audit compliance

### 4. Excel to QBO Web Converter
Accounts team can upload standard CSV or Excel bank ledger sheets. The converter transforms the records into QuickBooks Online Web Connect format for seamless synchronization.
* Parser for multiple column layouts
* Auto conversion to QBO schema
* Safe file compilation in browser memory

## Key Performance and Impact Metrics

* Zero UI hangs observed during simultaneous 250 plus account inquiries
* Bank connection resolution time under 2 seconds via worker parallelization
* Deficit sweeps executed and cleared in under 450 milliseconds
* 100 percent real time visibility for CFO and executive officers

## Testing Strategy

* Unit Testing: Validates Zustand store transitions, reconciliation regex parsers, and sweep calculation logic.
* Integration Testing: Tests Express controller routes and mocks bank API communication.
* Security Testing: Validates role access privileges and simulates Duo authentication states.

## User Interface and Feature Documentation

### Core Authentication Portal
Secure entrance interface featuring Duo MFA authorization before dashboard access.
![Login Screen](docs/screenshots/login.png)
![Duo Mobile Security Check](docs/screenshots/loginDUOAuth.png)

### Administrator Portal
Administration dashboard to configure LLC corporate entities and set permissions.
![Admin Dashboard](docs/screenshots/adminDashboard.png)

### Treasury Homepage and Portfolio Hub
Overview of global treasury accounts, liquidity metrics, and portfolio status.
![Homepage UI](docs/screenshots/homepage.png)

### Balance Inquiries and Transaction Logs
Highly responsive transaction grids loading 250 plus accounts instantly.
![Account Balance Grid 1](docs/screenshots/balanceInquiry_1.png)
![Account Balance Grid 2](docs/screenshots/balanceInquiry_2.png)
![Transaction Log Grid 1](docs/screenshots/transactions_1.png)
![Transaction Log Grid 2](docs/screenshots/transactions_2.png)
![Transaction Log Grid 3](docs/screenshots/transactions_3.png)
![Transaction Log Grid 4](docs/screenshots/transactions_4.png)

### Daily Money Movement Sweeps
Interface for CFO users to execute single click liquidity balances correction.
![Daily Cash Sweeping](docs/screenshots/dailyMoneyMovement.png)
![Account Transfer Execution](docs/screenshots/accountTransferPNC.png)

### Wires and Domestic Transfer
Payment execution page to configure and authorize domestic wire transactions.
![Wire Setup Page](docs/screenshots/usDomesticWire.png)

### Document Converter and Bookkeeping Tools
Excel transaction upload converting data directly to QBO files.
![QBO Conversion Tool](docs/screenshots/excelToQBO.png)

### Check Image and Payment Auditing
Payment tracking sheets and check image retrieval options.
![Check Services Screen](docs/screenshots/checkServices.png)
![Payment Tracking Grid](docs/screenshots/paymentTrackingSheet.png)
