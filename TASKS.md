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

## **Phase 2: Core Models & Database Setup**

### **Section 3: User & Authentication**
- [ ] Create a `User` model with Devise authentication
- [ ] Allow User signup and login/logout
- [ ] Implement authentication using Omniauth for Google login
- [ ] Write happy path tests for authentication
- [ ] Implement logout functionality

**Deliverable:** Admin authentication working with Devise and Omniauth

### **Section 4: Client & Brand Guidelines Models**
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

### **Section 5: Initiatives Model & UI**
- [ ] Create `Initiative` model (title, description, goals, scope, messaging, launch dates, associated client_id)
- [ ] Create `InitiativeSearchTerm` model for initiative-specific queries
- [ ] Implement UI for creating and editing initiatives
- [ ] Auto-generate search terms when an initiative is created/edited
- [ ] Write model validations for required fields
- [ ] Implement UI to display initiatives per client
- [ ] Write happy path tests for initiative creation

**Deliverable:** CRUD for Initiatives with auto-generated search terms

### **Section 6: Nightly Article Fetching**
- [ ] Implement Perigon API integration (`GET /v1/articles` with relevant filters)
- [ ] Store fetched articles in an `Article` model, per client per day
- [ ] Deduplicate articles before storing
- [ ] Create a background job using GoodJob to fetch articles nightly
- [ ] Add logging for API failures
- [ ] Write tests for API response parsing
- [ ] Implement basic UI for viewing fetched articles
- [ ] Ensure only relevant articles are stored based on search terms
- [ ] Display API quota usage in logs

**Deliverable:** Nightly background job successfully fetching articles

## **Phase 4: Relevancy & Pitch Drafts**

### **Section 7: Relevancy & Sentiment Analysis**
- [ ] Implement logic to compare Perigon’s relevancy score with our sentiment adjustments
- [ ] Store the adjusted relevancy scores in the database
- [ ] Ensure articles can be filtered by relevancy score in the UI
- [ ] Implement UI sorting by relevancy score
- [ ] Write happy path tests for sentiment adjustments
- [ ] Create a background job to update relevancy scores daily

**Deliverable:** Relevancy and sentiment scoring pipeline functional

### **Section 8: Pitch Prompt Generation**
- [ ] Create `PitchArtifact` model to store past pitch data per User
- [ ] Implement user file upload for past pitches
- [ ] Generate initial pitch drafts based on uploaded data and guidelines
- [ ] Provide UI for users to view and refine pitch prompt
- [ ] Implement history tracking for pitch prompts
- [ ] Write happy path tests for pitch generation

**Deliverable:** Basic pitch prompt generation working

## **Phase 5: Full End-to-End Workflow**

### **Section 9: Morning Article List & Export**
- [ ] Display a daily list of relevant articles per client
- [ ] Generate short summaries for each article, with links to full article and assets
- [ ] Show our relevancy score, Perigon's score, and our adjusted score. 
- [ ] Use the user's pitch prompt to generate a Pitch Draft for the article
- [ ] Make a link to this draft available on each row, with the body of the draft encoded in the URL

**Deliverable:** Morning article list UI 

### **Section 10: E2E Testing & Final Staging Deployment**
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

