
# Webscraping & Article Extraction  
- Commercial vs. In-House:  
  - Decision: Use Perigon API instead of building an in-house crawler.  
  - API Calls Needed:  
    - `GET /v1/articles` with parameters:
      - `language=en`
      - `country=us`
      - `sortBy=relevancy`
      - `q=<search_terms>` (initiative-specific terms)  
  - Logging & Monitoring:  
    - Log API failures and track usage limits.  
    - Implement alerts if API calls fail repeatedly.  
- Deliverables:
  - Rake task POC of all perigon api calls needed 

# Client Setup & Brand Guidelines  
- Data Models:  
  - Client Model: Contains basic info (name, industry, contact details).  
  - BrandGuideline Model: Stores brand voice, messaging, target audience, etc.  
- Search Term Generation:  
  - When brand guidelines or initiative details change, regenerate default search terms.  
  - Users can manually add search terms, but cannot remove default ones -- they get regenerated. In future update, we can support persistent negative overrides.
  - Data Model:  
    - `initiative_search_terms`: Initiative ID, default system-generated terms, user-added terms.  
- Form Interface:  
  - Use chatbot-driven forms to prompt users with questions.  
  - Fallback to traditional forms for direct editing.  
- Integration:  
  - Ensure that uploaded materials (PDFs, images, text) auto-populate guideline fields.  
  - Question: How should we prioritize auto-filled content versus manual edits?
    - Suggested approach. Keep all assets saved, use content from assets in the context of the chat to update the fields. 
- Deliverables:  
  - Detailed ERD for Client and Brand models.  
  - UI to view and modify search terms - Client/Brand level  

# Initiatives  
- Data Model:  
  - Initiative Model:  
    - Fields: title, description, goals, scope, messaging, launch dates, associated client_id.  
  - Initiative Search Terms Model: Stores query terms for nightly pulls.  
- User Interaction:  
  - Chatbot-assisted creation and update forms similar to guidelines.  
  - Pod-Leaders/Pod-Members should have UI cues based on permissions.  
- Deliverables:  
  - Complete scaffold for initiatives with role-based validations.  
  - Documentation on form flows and expected user inputs.
  - Search term auto-generation logic.  
  - UI for modifying search terms.  

# Nightly Article Pull  
- Process:  
  - Schedule a nightly background job to call the Perigon API
  - Deduplicate results before storing.  
- API Calls Needed:  
  - `GET /v1/articles` with initiative-specific terms.  
- Data Model Updates:  
  - `articles`: Stores full article data, timestamps, source info, and Perigon’s relevancy score.  
- Deliverables:  
  - Background job to fetch, deduplicate, and store articles.  
  - Monitoring tools for tracking API usage.  

# Relevancy & Sentiment Pipeline  
- Daily Query Processing:  
  - Retrieve stored articles for processing.  
  - Compare our sentiment scoring against Perigon’s relevancy ranking.  
- Post-Processing: Sentiment Analysis & Brand-Specific Rules:  
  - Custom Brand Rules:  
    - Integrate brand-specific guidelines (e.g., “mentions with competitor X are critical” or “references to a vacuum cleaner indicate irrelevance”) to adjust the sentiment score.  
  - Final Scoring:  
    - Combine the baseline relevance score from the embedding search with the sentiment adjustments to produce a refined ranking per brand/initiative.  
- Deliverables:  
  - A prototype scoring engine with API endpoints and benchmark reports comparing baseline versus sentiment-enhanced relevancy.
  - Store full article content for troubleshooting.  
  - Build a pipeline for custom sentiment scoring.  

# Pitch Draft Training
- Process:
  - User uploads 10-100 past pitch emails to be used for training
  - User can give direct prompt guidance
- Data Models:
  - Pitch Artifact
  - Trained Prompt
- Fine Tuning vs. Prompting:
  - V1 will feature a generated prompt
  - if needed, we will consider fine-tuning and custom assistants
- Deliverables:
  - User can upload training docs
  - System generates voice prompt

# Morning Article List & Pitch Drafts
- Article Listing:
  - Retrieve and display articles sorted by the refined scores combining relevance and sentiment.
  - Provide options for viewing both top-tier articles and a broader “below the line” set for extended coverage.
- Content Generation:
  - Automatically generate a concise (<50 word) summary for each article, highlighting its relevance to the brand/initiative.
- Pitch Draft Generation:
  - Contextual Drafting: The generated draft references guidelines and previous pitches to maintain consistency.
  - Journalist Email Inclusion: If available, the draft will include the journalist’s email.
  - User Upload Interface: Users can upload past emails via the dashboard for training.
  - Offer a “Pitch Journalist” link that pre-fills an email draft with references to the brand guidelines and pitch samples using URL parameters.
  - Note: V1 does not send emails directly; users will need to copy or export the draft.
- Export Options:
  - Include CSV export functionality for integration with external tools like Google Sheets or Airtable.
- Deliverables:
  - An automated daily article list generation job, integrated with a refined scoring mechanism, email draft generation service, and CSV export tool within the dashboard.

### User Management & Permissions  
- Roles & Models:  
  - User Model: Standard Devise integration for email/password authentication.  
  - Role-based model using CanCanCan/Pundit to manage permissions.  
  - Roles include Super-User, Admin, Pod-Leader, and Pod-Member.  
- UI & Access:  
  - Create an admin interface for adding users, assigning roles, and modifying permissions.  
  - Ensure pod-based restrictions:  
    - Pod-Members see only their assigned clients and initiatives.  
    - Pod-Leaders see all within their pod; Admins see firm-wide.  
- Deliverables:  
  - Complete user management interface with role assignment.  
  - Documentation on permission rules and testing for role-based access.

# Activity Log  
- Logging Actions:  
  - Record key events:  
    - Client and guideline creation/updates.  
    - Initiative creation/updates.  
    - Article review actions and pitch draft generation.  
  - Use a polymorphic ActivityLog model that can track various actions.  
- Visibility & Access:  
  - Pod-Members: view logs for their assigned clients/initiatives.  
  - Pod-Leaders/Admins: view logs across all accessible domains.  
- Deliverables:  
  - ActivityLog model with clear associations and metadata.  
  - Front-end log viewer with filters by user, client, initiative, and action type.
- Question: What retention policy should be applied to logs for performance and privacy reasons?

# Next Steps & Open Questions  
- Immediate Decisions:  
  - Finalize webscraping strategy: buy vs. build?  
  - Determine the optimal approach for relevancy scoring (direct model vs. embedding + vector search).  
- Research & Prototyping:  
  - Test several extraction libraries for quality and performance.  
  - Benchmark scoring methods for cost and scalability.  
- Clarifications Needed:  
  - Expected volume and frequency of crawled articles?  
  - How often should periodical metadata be updated?  
  - Are there additional email integrations beyond Gmail to support?  
  - What are the non-functional requirements (e.g., uptime, error tolerance) for the nightly job?  
- Deliverables:  
  - A decision matrix for webscraping options.  
  - Prototype demos for both relevancy scoring approaches and email draft generation.
