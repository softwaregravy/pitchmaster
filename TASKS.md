# PitchMaster V1 Task List

## **Phase 1: Project Setup & Basic Deployment**

### **Section 1: Initialize Project**
- [ ] Initialize local git repository
- [ ] Create a new Rails project (`rails new pitchmaster --database=postgresql`)
- [ ] Set up a GitHub repository and push initial commit
- [ ] Configure `.gitignore` to exclude unnecessary files
- [ ] Add essential gems (RSpec, Faker, FactoryBot, VCR, Amazing Print, Omniauth, Pundit, GoodJob)
- [ ] Configure RSpec as the test framework
- [ ] Create initial database migration
- [ ] Set up `.env` for managing environment variables

**Deliverable:** Rails project with initial setup committed to GitHub

### **Section 2: Deployment & CI/CD Setup**
- [ ] Create a Heroku app
- [ ] Set up PostgreSQL on Heroku
- [ ] Configure automatic deployments from GitHub to Heroku staging
- [ ] Add GitHub Actions for automated test runs on PRs
- [ ] Set up Rails production environment variables
- [ ] Deploy minimal Rails app to Heroku staging
- [ ] Ensure logs are accessible in Heroku dashboard

**Deliverable:** Rails app successfully deployed to Heroku with CI/CD pipeline running

### **Section 3: Feasibility**
- [ ] Write prompt template to generate search terms
- [ ] Implement Rakefile to call OpenAI API to generate search terms using static input
- [ ] Design getting sentiment score using OpenAI API
- [ ] Implement Rakefile to generate sentiment scores via OpenAI using static input
- [ ] curl command to Perigon's API `/articles`
- [ ] Implement Rakefile to call Perigon's API with static input
- [ ] Implement Rakefile which contains the body of an email

**Deliverable:** Basic feasibility tests for AI and API integrations

## **Phase 2: Core Models & Database Setup**

### **Section 4: User & Authentication**
- [ ] Create a `User` model with Devise authentication
- [ ] Allow User signup and login/logout
- [ ] Implement authentication using Omniauth for Google login
- [ ] Write happy path tests for authentication
- [ ] Implement logout functionality

**Deliverable:** Admin authentication working with Devise and Omniauth

### **Section 5: Client & Brand Guidelines Models**
- [ ] Create `Client` model with name, industry, contact details
- [ ] Create `BrandGuideline` model with voice, messaging, audience fields
- [ ] Associate `BrandGuideline` with `Client`
- [ ] Implement simple UI to create and edit Clients and Brand Guidelines
- [ ] Seed some test data for development
- [ ] Add validation for required fields
- [ ] Write happy path model tests
- [ ] Implement basic error handling for form submissions

**Deliverable:** CRUD for Clients and Brand Guidelines with UI

## **Phase 3: Initiatives & Article Processing**

### **Section 6: Initiatives Model & UI**
- [ ] Create `Initiative` model (title, description, goals, scope, messaging, launch dates, associated client_id)
- [ ] Create `InitiativeSearchTerm` model for initiative-specific queries
- [ ] Implement UI for creating and editing initiatives
- [ ] Auto-generate search terms when an initiative is created/edited
- [ ] Feed client and brand guidelines into OpenAI API to generate search terms
- [ ] Implement logic to refine generated search terms based on initiative details
- [ ] Write model validations for required fields
- [ ] Implement UI to display initiatives per client
- [ ] Write happy path tests for initiative creation

**Deliverable:** CRUD for Initiatives with auto-generated search terms using OpenAI API

### **Section 7: Nightly Article Fetching**
- [ ] Implement Perigon API integration (`GET /v1/articles` with relevant filters)
- [ ] Store fetched articles in an `Article` model, associated with initiatives
- [ ] Deduplicate articles before storing
- [ ] Create a background job using GoodJob to fetch articles nightly
- [ ] Add logging for API failures
- [ ] Write tests for API response parsing
- [ ] Implement basic UI for viewing fetched articles per initiative
- [ ] Ensure only relevant articles are stored based on search terms
- [ ] Display API quota usage in logs

**Deliverable:** Nightly background job successfully fetching articles per initiative

## **Phase 4: Relevancy & Pitch Drafts**

### **Section 8: Relevancy & Sentiment Analysis**
- [ ] Create our own sentiment scores using OpenAI API
- [ ] Implement logic to compare Perigon’s relevancy score with our sentiment adjustments
- [ ] Store the adjusted relevancy scores in the database
- [ ] Ensure articles can be filtered by relevancy score in the UI
- [ ] Write happy path tests for sentiment adjustments
- [ ] Create a background job to update relevancy scores daily

**Deliverable:** Relevancy and sentiment scoring pipeline functional

### **Section 9: Pitch Prompt Generation**
- [ ] Create `PitchArtifact` model to store past pitch data per User
- [ ] Implement user file upload for past pitches
- [ ] Generate initial pitch drafts based on uploaded data and guidelines using OpenAI API
- [ ] Break pitch generation into multiple steps, ensuring brand guidelines are respected
- [ ] Provide UI for users to view and refine pitch prompt
- [ ] Implement history tracking for pitch prompts
- [ ] Write happy path tests for pitch generation

**Deliverable:** Basic pitch prompt generation working using OpenAI API

## **Phase 5: Full End-to-End Workflow**

### **Section 10: Morning Article List & Export**
- [ ] Display a daily list of relevant articles per initiative
- [ ] Generate short summaries for each article, with links to full article and assets
- [ ] Show our relevancy score, Perigon's score, and our adjusted score.
- [ ] Use the user's pitch prompt to generate a Pitch Draft for the article
- [ ] Make a link to this draft available on each row, with the body of the draft encoded in the URL

**Deliverable:** Morning article list UI per initiative

### **Section 11: Durability of External Calls**
- [ ] Implement job wrapping for all OpenAI API calls to allow retries and exponential backoff on rate limits
- [ ] Implement job wrapping for Perigon API calls using the same retry strategy
- [ ] Define job failure handling; after X retries, move to a dead letter queue
- [ ] Utilize GoodJob’s built-in failure handling mechanisms where possible
- [ ] Monitor and log API failure patterns for better debugging

**Deliverable:** Reliable API call execution with automated retry handling

### **Section 12: E2E Testing & Final Staging Deployment**
- [ ] Write happy path tests for all core features
- [ ] Run full test suite in GitHub Actions before each deployment
- [ ] Deploy to staging and confirm E2E flows are functional
- [ ] Implement smoke tests for key workflows
- [ ] Add performance monitoring on staging
- [ ] Ensure logs capture key application events
- [ ] Conduct final UI review and refinements
- [ ] Validate user authentication flows
- [ ] Document test results and areas for improvement

**Deliverable:** E2E tests passing, deployment to staging confirmed functional

