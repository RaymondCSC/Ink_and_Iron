# Ink & Iron

> _Note:_ This document is intended to be relatively short. Be concise and precise. Assume the reader has no prior knowledge of your application and is non-technical. 

## Partner Intro
* Partner Name(s): Rafiq Omair, Caroline Therence
* Contact(s): rafiq.omair@mail.utoronto.ca, c.tejowinoto@mail.utoronto.ca, Titles, Primary/Secondary contact roles> !!!!!!!!
* Description: <Brief description of the partner organization in 2–4 lines. What they do, who they serve, and why they matter.>

## Description about the project
Ink & Iron is an application designed to connect incarcerated individuals with reading materials by streamlining the book request and donation process.  
We aim to solve the problem of accessibility to books in correctional facilities, where requests are often lost in bureaucracy or denied due to unclear facility rules.  

## Key Features
* **Home Page**  
  Mission statement, CTAs for “Request Books” & “Donate,” 3-step “How it works” cards, impact counters, and partner logos.  

* **Request Books**  
  Request form (recipient name, inmate ID, facility autocomplete, genres/titles, consent).  
  Live rule checks from facility directory.  
  Success screen with public request ID and privacy notice.  

* **Track Request**  
  Track status using public request ID + last name.  
  Timeline states: Received → Matched → Shipped → Delivered/Refused.  
  If shipped, shows carrier and tracking. If refused, displays reason and next steps.  

* **Facility Directory**  
  Search and filters (province, paperback-only, last verified).  
  Facility cards with address, rules, contact, last verified date.  
  Facility detail pages for full rules.  

* **Donate**  
  Books: wishlist + pledge form.  
  Funds: Stripe checkout with thank-you page.  

* **FAQ & Contact**  
  FAQs organized by topics with anchor links.  
  Contact form with response-time notes and alternative email.  

* **Volunteer Portal (Private)**  
  Volunteer login with queue of incoming requests.  
  Claim/unclaim, view details, update statuses.  
  Match from inventory or add to purchase list.  

* **Admin Portal (Private)**  
  Dashboard with KPIs, request and facility management, CRUD inventory, donations, user roles, audit logs.  

## Instructions
* **Accessing the application:** Register through our website 
* **Requesting Books:** Navigate to *Request Books* → fill out form → receive Request ID → use *Track Request* to check progress.  
* **Donating Books/Funds:** Navigate to *Donate* → choose Books or Funds → follow pledge or Stripe checkout.  
* **Tracking Requests:** Go to *Track Request* → enter Request ID + last name → view status.  
* **Facility Directory:** Navigate to *Facilities* → search/filter → click card for detail.  
* **Volunteer Use:** Log in → access queue → claim/unclaim requests → update request status.  
* **Admin Use:** Log in → dashboard → manage requests, facilities, inventory, donations, and users.  

## Development requirements
* **Requirements:** <OS requirements, dependencies (Node, Python, etc.), package managers, libraries>  
* **Setup:**  
  1. Clone repository: `git clone https://github.com/RaymondCSC/Ink_and_Iron.git`  
  2. Install dependencies: `To be done in future one coding started`  
  3. Configure environment: `To be done in future one coding started`  
  4. Run application: `To be done in future one coding started`  
* **Notes:** <Any special setup steps like database, API keys, Stripe test keys, etc. To be done in future one coding started>  

## Deployment and Github Workflow
* We use feature branches (`feature/<name>`), which are merged into `dev` after peer review.  
* Pull requests are submitted from `feature/<name>` → `dev`, reviewed by at least one teammate.  
* Once tested, `dev` merges into `main` for production deployment.  
* Deployment is handled via (Some one fill this) with automated pipelines.  !!!!!!!!!!!!!!!!!!!
* Workflow justification: This prevents conflicts, ensures code review, and keeps production stable while allowing parallel development.  

## Coding Standards and Guidelines
* We follow consistent naming conventions, clear comments, and linting standards to maintain readability and long-term maintainability.  
* Code reviews ensure style and functionality consistency across the team.  

## Licenses
* License type: <MIT / Apache 2.0 / GPL / etc.>  We don't know yet?????? !!!!!!!!!!!!!
* This allows <freedom of modification, commercial use, etc. depending on license>.  
* We chose this license to ensure accessibility and flexibility for both developers and end-users.  
