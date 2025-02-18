
### 1. Webscraping & Article Extraction  
- **Commercial vs. In-House:**  
  - **Commercial Options:**  
    - Evaluate newsapi, cision, and meltwater for data quality, pricing, and coverage.  
    - **Question:** What is our monthly article volume estimate, and do these services scale economically?  
  - **In-House Approach:**  
    - Use Ruby libraries like [ruby-readability](https://github.com/cantino/ruby-readability).  
    - Alternatives:  
      - Python: [trafilatura](https://github.com/adbar/trafilatura)  
      - Node: [Mozilla Readability](https://github.com/mozilla/readability)  
    - **Requirements:**  
      - Develop a crawler to fetch and process pages for each periodical.  
      - Handle various formats and rate-limiting.  
    - **Question:** Do we have the bandwidth to build and maintain a robust crawler and extraction pipeline?  
- **Logging & Monitoring:**  
  - Implement detailed logs for errors and parsing failures.  
  - Alert system for repeated failures on a given periodical.  
- **Deliverables:**
  - Get demos of the commercial products
  - Reach out to OS maintainers for any advice
  - A decision on which approach to try first
  - POC for whichever approach we want
  - Revisit Decision based on learnings

### 2. Client Setup & Brand Guidelines  
- **Data Models:**  
  - **Client Model:** Contains basic info (name, industry, contact details).  
  - **BrandGuideline Model:** Stores brand voice, messaging, target audience, etc.  
- **Form Interface:**  
  - Use chatbot-driven forms to prompt users with questions.  
  - Fallback to traditional forms for direct editing.  
- **Integration:**  
  - Ensure that uploaded materials (PDFs, images, text) auto-populate guideline fields.  
  - **Question:** How should we prioritize auto-filled content versus manual edits?
    - Suggested approach. Keep all assets saved, use content from assets in the context of the chat to update the fields. 
- **Deliverables:**  
  - Detailed ERD for Client and Brand models.  

### 3. Initiatives  
- **Data Model:**  
  - **Initiative Model:**  
    - Fields: title, description, goals, scope, messaging, launch dates, associated client_id.  
  - Relate initiatives to clients using associations in Rails.
- **User Interaction:**  
  - Chatbot-assisted creation and update forms similar to guidelines.  
  - Pod-Leaders/Pod-Members should have UI cues based on permissions.  
- **Deliverables:**  
  - Complete scaffold for initiatives with role-based validations.  
  - Documentation on form flows and expected user inputs.
- **Question:** Are there additional initiative attributes (e.g., KPIs) we should capture now?

### 4. Periodicals Onboarding & Tracking (if homegrown)
- **Data Model:**  
  - **Periodical Model:**  
    - Fields: name, base URL, crawl frequency, status (active, retry, failed), last crawl date, error log.  
- **Onboarding Process:**  
  - UI for manual entry or batch CSV import.  
  - Ability to mark a periodical as “essential” or “optional” for crawl priority.  
  - **Question:** Should we allow periodic reviews or updates for periodical metadata?  
- **Error Handling:**  
  - Implement a retry mechanism with a maximum number of attempts.  
  - Automatically change status to “failed” after threshold reached and notify an admin.  
- **Deliverables:**  
  - Admin dashboard for managing periodicals, error logs, and retry statuses.

### 5. Nightly Article Pull  
- **Process:**  
  - Schedule a nightly background job for crawling each periodical.  
  - Each job retrieves articles, parses content, and stores raw data.  
- **Error Logging:**  
  - Capture parsing and network errors in a centralized log.  
  - Update corresponding periodical status if failures occur repeatedly.  
- **Data Linking:**  
  - Associate articles with relevant clients/initiatives based on keywords.  
- **Deliverables:**  
  - A robust scheduled job system with detailed error reporting and logging.

### 6. Relevancy Scoring  
- **Scoring Mechanism:**  
  - Use a small, cost-effective ML model to score articles for relevancy and sentiment on a per-client/per-initiative basis.  
  - **Options:**  
    - Direct prompt evaluation with a lightweight transformer.  
    - Generate embeddings (e.g., with OpenAI embeddings, or a distilled model) and perform a vector DB search (consider Pinecone or similar).  
  - **Question:** Is there a hybrid approach to first filter and then fine-tune with a more expensive model?  
- **Integration:**  
  - Form client/initiative prompt using key inputs and then evaluate each article.  
  - Store the score with each article record.  
- **Deliverables:**  
  - Prototype scoring engine and API endpoints for score retrieval.  
  - Benchmark report comparing direct prompt vs. embedding-based search.

### 7. Morning Article List & Pitch Drafts  
- **Article Listing:**  
  - Retrieve articles sorted by relevancy score with a cutoff for “top” articles.  
  - Option to view “below the line” articles (lower score) for extended coverage.  
  - **Content Generation:**  
    - Generate a short (<50 word) summary focused on brand/initiative relevance using a lightweight summarization tool.  
- **Pitch Drafts:**  
  - Automatically generate pre-filled email drafts referencing the brand guidelines and pitch samples.  
  - Use URL parameters for Gmail (e.g., `to`, `su`, `body`) to allow quick redirection.  
    - **Question:** Are Gmail URL parameters consistent across all devices and email clients?  
- **Export Options:**  
  - Provide CSV export functionality compatible with Google Sheets/Airtable.  
- **Deliverables:**  
  - Automated daily article list generation job.  
  - Email draft generation service with direct URL linking.  
  - CSV export tool integrated into the dashboard.

### 8. User Management & Permissions  
- **Roles & Models:**  
  - **User Model:** Standard Devise integration for email/password authentication.  
  - Role-based model using CanCanCan/Pundit to manage permissions.  
  - Roles include Super-User, Admin, Pod-Leader, and Pod-Member.  
- **UI & Access:**  
  - Create an admin interface for adding users, assigning roles, and modifying permissions.  
  - Ensure pod-based restrictions:  
    - Pod-Members see only their assigned clients and initiatives.  
    - Pod-Leaders see all within their pod; Admins see firm-wide.  
- **Deliverables:**  
  - Complete user management interface with role assignment.  
  - Documentation on permission rules and testing for role-based access.

### 9. Activity Log  
- **Logging Actions:**  
  - Record key events:  
    - Client and guideline creation/updates.  
    - Initiative creation/updates.  
    - Article review actions and pitch draft generation.  
  - Use a polymorphic ActivityLog model that can track various actions.  
- **Visibility & Access:**  
  - Pod-Members: view logs for their assigned clients/initiatives.  
  - Pod-Leaders/Admins: view logs across all accessible domains.  
- **Deliverables:**  
  - ActivityLog model with clear associations and metadata.  
  - Front-end log viewer with filters by user, client, initiative, and action type.
- **Question:** What retention policy should be applied to logs for performance and privacy reasons?


### 10. Next Steps & Open Questions  
- **Immediate Decisions:**  
  - Finalize webscraping strategy: buy vs. build?  
  - Determine the optimal approach for relevancy scoring (direct model vs. embedding + vector search).  
- **Research & Prototyping:**  
  - Test several extraction libraries for quality and performance.  
  - Benchmark scoring methods for cost and scalability.  
- **Clarifications Needed:**  
  - Expected volume and frequency of crawled articles?  
  - How often should periodical metadata be updated?  
  - Are there additional email integrations beyond Gmail to support?  
  - What are the non-functional requirements (e.g., uptime, error tolerance) for the nightly job?  
- **Deliverables:**  
  - A decision matrix for webscraping options.  
  - Prototype demos for both relevancy scoring approaches and email draft generation.
