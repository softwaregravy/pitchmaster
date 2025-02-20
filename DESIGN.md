
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
  - Schedule a nightly background job to crawl designated periodicals and retrieve new articles.  
  - For each article, parse the content and generate a lightweight embedding using a candidate model (e.g., OpenAI’s `text-embedding-ada-002` or a Sentence Transformer).  
  - Store both the raw article data and its embedding in a vector database (e.g., FAISS, Pinecone, or Milvus).  
  - Semantic Matching: Articles are matched based on conceptual relevance rather than just keyword searching. The embedding and vector search database already performs concept-based matching.
- **Error Logging:**  
  - Capture parsing and network errors in a centralized log.  
  - Update periodical status and trigger automated retries upon repeated failures.  
- **Deliverables:**  
  - A robust scheduled job system that performs crawling, embedding generation, storage, and error reporting.

### 6. Relevancy & Sentiment Pipeline  
- **Daily Query Processing:**  
  - For each brand/initiative, convert its guidelines into a query embedding. (Highly cacheable)  
  - Perform an approximate nearest neighbor search in the vector database to retrieve the top 10–50 candidate articles based on baseline relevance.  
- **Post-Processing: Sentiment Analysis & Brand-Specific Rules:**  
  - **Entity-Level Sentiment:**  
    - Apply Named Entity Recognition (NER) to detect brand mentions in each retrieved article.  
    - Use an aspect-based sentiment analysis model (e.g., fine-tuned BERT variants or VADER for lighter use cases) to evaluate sentiment in context.  
  - **Custom Brand Rules:**  
    - Integrate brand-specific guidelines (e.g., “mentions with competitor X are critical” or “references to a vacuum cleaner indicate irrelevance”) to adjust the sentiment score.  
  - **Final Scoring:**  
    - Combine the baseline relevance score from the embedding search with the sentiment adjustments to produce a refined ranking per brand/initiative.  
- **Deliverables:**  
  - A prototype scoring engine with API endpoints and benchmark reports comparing baseline versus sentiment-enhanced relevancy.


### 7. Morning Article List & Pitch Drafts

- **Article Listing:**
  - Retrieve and display articles sorted by the refined scores combining relevance and sentiment.
  - Provide options for viewing both top-tier articles and a broader “below the line” set for extended coverage.
- **Content Generation:**
  - Automatically generate a concise (<50 word) summary for each article, highlighting its relevance to the brand/initiative.
- **Pitch Draft Generation:**
  - **Training-Based Drafts:** Users can upload 10-100 past pitch emails to train the system to generate drafts in their style and voice.
  - **Contextual Drafting:** The generated draft references guidelines and previous pitches to maintain consistency.
  - **Journalist Email Inclusion:** If available, the draft will include the journalist’s email.
  - **User Upload Interface:** Users can upload past emails via the dashboard for training.
  - Offer a “Pitch Journalist” link that pre-fills an email draft with references to the brand guidelines and pitch samples using URL parameters.
  - Note: V1 does not send emails directly; users will need to copy or export the draft.
- **Export Options:**
  - Include CSV export functionality for integration with external tools like Google Sheets or Airtable.
- **Deliverables:**
  - An automated daily article list generation job, integrated with a refined scoring mechanism, email draft generation service, and CSV export tool within the dashboard.

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
