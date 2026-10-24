# SDCHACK_KALIDERES

# FlowUp
Work in a **Flow, Up**-scale the performance!

# Description
FlowUp is an orbyte ecosystem AI-based that ensure accuracy and provide automation to work in a flow and up-scale SME's performance

#  Team Information
| Field | Details |
|-------|---------|
| Team Name | KALIDERES |
| Team Domain | Domain 2 | 
| SDG Track | SDG 8 and SDG 9 |
| Team Leader | Carlos Lee |
| University | Asia Pacific University |
| Number Of Member | 4 |

| Team Name | Github Account |
|-----------|----------------|
| Abraham Darell Jeremiah | @B04-Favela |
| Aska Aidan | @Vioclast
| Carlos Lee | @lee-carlos |
| Jones Ruben Tobias | @jones-ruben-tobias |

# Links 
| Resource | Link |
|----------|------|
| Github Repository | https://github.com/lee-carlos/SDCHACK_KALIDERES_1/ | 
| Live Demo | https://flowup-mvp.replit.app |
| Slide Deck |  | 
| Demo Video |  |

# Overview
Problem Micro and small grocery retailers in Malaysia run daily operations across WhatsApp, spreadsheets, paper notes and memory. Sales and stock are recorded in different places, owners often learn an item is out of stock only when a customer asks for it, and financial figures are hard to verify. Late reorders, expired goods and unchecked records quietly cost margin, and small teams cannot afford complex systems or formal training.

As a solution, FlowUp is here! as an integrated, easy-to-use platform that connects sales, inventory and finances for micro and small grocery retailers in Malaysia. By replacing scattered WhatsApp messages, spreadsheets and paper notes with a single connected flow, it gives owners real-time stock visibility, timely reorder and expiry alerts, and verifiable financial records, helping them protect margin without complex systems or formal training.

# Key Features 
- **Automation Stock Reminder**
  FlowUp checks stock conditions and flags items that need checking or restocking before they run out, so owners no longer find out when a customer asks.

- **One Connected Store System**
  Cashier sales update stock automatically, while products, suppliers, finance and budget live in one place with dashboards and charts for sales, stock and spending.

- **Role-based control with human approval**
  Owner, cashier, supply, finance and analyst each see only what they need. The system flags data that needs review, a person verifies or corrects it, and every action is kept in an audit log.


# How we use Replit
- **Development:**
  FlowUp was built in Replit. We first wrote a structured specification (roles, data flow, formulas and reference test numbers), then used Replit Agent to generate the app and refined it in the Replit workspace.
  
- **Hosting:**
  FlowUp is published through Replit Deployments. The deployment is currently private, so access must be arranged for authorised reviewers before the demonstration.
Live application: https://flowup-retail-orbyte-mvp.replit.app

- **Database:**
  Synthetic store data is stored in the Replit-hosted database. (PostgreSQL database) 

# Challenges
- **Scope**
  Our first design covered the whole store (cashier, warehouse, finance, owner). The brief asks for one clear use case, so we narrowed the MVP to one journey: goods received → compared with the purchase order → refund claim approved → stock and supplier score updated → reorder and discount recommendations. Other modules moved to the roadmap.
  
- **Inconsistency Number**
  Dashboards must agree with each other. We defined every formula once (stock reminder, EOQ, holding cost, supplier score) and checked the results against a reference dataset and a reconciliation check (opening stock + goods in − cost of goods sold = closing stock).
  
- **Keeping AI honest** 
  We did not want a model inventing numbers. All numbers come from rules; AI only writes short explanations and supplier message drafts, with a template fallback if it is unavailable.

# What We Learned
What we learned

- A detailed specification before prompting Replit Agent gave far better results than short prompts.

- Human approval plus an audit log makes automation easier for SME owners to trust.

- Rules should decide the numbers; AI should only explain them.

# Future Improvement

- [ ] QR Scanning for incoming stock
- [ ] Expand to another role
- [ ] AI demand forecasting and unusual-transaction detection
- [ ] Features for the supplier
