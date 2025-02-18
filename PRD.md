# Overview
This PRD covers the V1 feature set for our PR Management System. It focuses on immediate-value capabilities and defers less critical enhancements to a future section.

## Main Capabilities

### Client Setup & Brand Guidelines
- **Client/Brand Profile Creation**  
  Users start by creating a client/brand profile.
- **Guidelines Form/Chatbot**  
  A standard form or chatbot prompts for brand voice, messaging, and audience.
- **Material Upload**  
  Uploaded files (text, PDFs, images) can auto-fill sections of the brand guidelines.
- **Direct Editing**  
  Users can manually adjust the guidelines after the initial setup.

### Initiatives
- **Multiple Initiatives**  
  Each client can have one or more initiatives (e.g., product launches).
- **Stored Details**  
  Key goals, scope, and messaging for each initiative are captured.
- **Creation & Updating**  
  Pod-members and pod-leaders can create, view, and modify initiative records.

### Nightly Article Pull
- **Automated Retrieval**  
  The system gathers relevant articles overnight for each client and initiative.
- **Relevancy Scoring**  
  Articles receive a score based on their content and keywords.
- **Publicly Traded Clients**  
  Finance or earnings-focused mentions default to a lower relevancy score.

### Article List
- **Morning Compilation**  
  Pods see a daily list of articles grouped by client and initiative.
- **Article Details**  
  Each entry shows publication name, a 50-word summary, author, relevancy score, and an optional image.
- **Draft Pitch Link**  
  Clicking an entry lets users view full details or start a pitch draft.

### Pitch Integration
- **Draft Generation**  
  A “Pitch Journalist” link creates a pre-filled email draft referencing guidelines and pitch samples.
- **No Direct Sending**  
  V1 does not handle sending emails; drafts must be copied or exported.
- **Future Email Workflow**  
  Future versions may include a fully integrated email-sending system.

## User Roles
- **Super-User**  
  Full oversight of the entire system.
- **Admin**  
  Manages firm-wide settings and user permissions.
- **Billing-Manager**  
  Oversees subscription and payment details for a PR firm.
- **Pod-Leader**  
  Can see and manage all clients and initiatives within a pod.
- **Pod-Member**  
  Limited to assigned clients and initiatives within the same pod.

## Security & Authentication
- **Email/Password**  
  Uses built-in authentication from the chosen framework (e.g., Django or Devise).
- **No SSO**  
  External authentication methods are deferred for future releases.

## Activity Log
- **Key Actions**  
  Logs creation or updates of initiatives, article reviews, pitch drafts, and guideline edits.
- **Visibility**  
  - Pod-members see logs for their assigned clients.
  - Pod-leaders and admins see logs for all clients under their domain.

## Future Features
- **Real-Time Monitoring**  
  Move from nightly pulls to near real-time alerts.
- **Email Analytics**  
  Track open rates, click-throughs, and response metrics.
- **Integrations**  
  Connect with Slack, Monday, or external databases.
- **Custom Reporting**  
  Generate flexible report templates for clients.
- **Feedback-Driven Relevancy**  
  Users rate or comment on article relevance to refine scoring.

## Timeline & Next Steps
- **Primary Feature Delivery**  
  Implement client setup, brand guidelines, initiatives, nightly article pulls, article listing, and pitch drafting.
- **Validation**  
  Roll out internally to confirm product-market fit.
- **Further Enhancements**  
  Use feedback to prioritize new features and potential pivots.
