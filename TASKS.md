# PitchMaster V1 Task Estimates

## Phase 1: Project Setup & Basic Deployment

### Section 1: Initialize Project
| TODO | Description | Estimate |
|------|-------------|----------|
| [ ] | <ul><li>Initialize local git repository</li> <li>Create a new Rails project (`rails new pitchmaster --database=postgresql`)</li> <li>Set up a GitHub repository and push initial commit</li> <li>Configure `.gitignore` to exclude unnecessary files</li> </ul> | 2 hours |
| [ ] | Add and configure essential gems (RSpec, Faker, FactoryBot, VCR, Amazing Print, Pundit, GoodJob) | 4 hours |
| [ ] | Set up `.env` for managing environment variables | 2 hours |
| **TOTAL** | | **1 day, 0 hours** |

### Section 2: Deployment & CI/CD Setup
| TODO | Description | Estimate |
|------|-------------|----------|
| [ ] | <ul><li>Create a Heroku app</li><li>Set up PostgreSQL on Heroku</li><li>Set up auto deploys from Github</li></ul> | 2 hours |
| [ ] | Set up auto-migration on Heroku | 2 hours |
| [ ] | Add GitHub Actions for automated test runs on PRs | 2 hours |
| [ ] | Set up Rails staging & production environment variables | 2 hours |
| [ ] | <ul><li>Deploy minimal Rails app to Heroku staging & production </li><li>Ensure logs are accessible in Heroku dashboard</li></ul> | 2 hours |
| **TOTAL** | | **1 day, 2 hours** |

### Section 3: Feasibility
| TODO | Description | Estimate |
|------|-------------|----------|
| [ ] | Write prompt template to generate search terms | 4 hours |
| [ ] | Implement Rakefile to call OpenAI API to generate search terms using static input | 4 hours |
| [ ] | Design getting sentiment score using OpenAI API | 4 hours |
| [ ] | Implement Rakefile to generate sentiment scores via OpenAI using static input | 4 hours |
| [ ] | get access to Perigon's API | 2 hours |
| [ ] | curl command to Perigon's API `/articles`, using search terms from previous steps | 2 hours |
| [ ] | Implement Rakefile to call Perigon's API with static input | 4 hours |
| [ ] | Implement Rakefile which contains the body of an email in a link | 4 hours |
| **TOTAL** | | **3 days, 4 hours** |

## Phase 2: Core Models & Database Setup

### Section 4: User & Authentication
| TODO | Description | Estimate |
|------|-------------|----------|
| [ ] | Create a `User` model with Devise authentication | 4 hours |
| [ ] | Allow User signup and login/logout | 4 hours |
| **TOTAL** | | **1 day, 0 hours** |

### Section 5: Client & Brand Guidelines Models
| TODO | Description | Estimate |
|------|-------------|----------|
| [ ] | Create `Client` model with name, industry, contact details | 2 hours |
| [ ] | Create `BrandGuideline` model with voice, messaging, audience fields | 2 hours |
| [ ] | Associate `BrandGuideline` with `Client` | 2 hours |
| [ ] | Implement simple UI to create and edit Clients and Brand Guidelines | 8 hours |
| [ ] | Seed some test data for development | 2 hours |
| [ ] | Add validation for required fields | 2 hours |
| [ ] | Write happy path model tests | 4 hours |
| [ ] | Implement basic error handling for form submissions | 4 hours |
| **TOTAL** | | **3 days, 2 hours** |

## Phase 3: Initiatives & Article Processing

### Section 6: Initiatives Model & UI
| TODO | Description | Estimate |
|------|-------------|----------|
| [ ] | Create `Initiative` model (title, description, goals, scope, messaging, launch dates, associated client_id) | 4 hours |
| [ ] | Create `InitiativeSearchTerm` model for initiative-specific queries | 2 hours |
| [ ] | Implement UI for creating and editing initiatives | 8 hours |
| [ ] | Auto-generate search terms when an initiative is created/edited | 8 hours |
| [ ] | Feed client and brand guidelines into OpenAI API to generate search terms | 8 hours |
| [ ] | Implement logic to refine generated search terms based on initiative details | 8 hours |
| [ ] | Write model validations for required fields | 2 hours |
| [ ] | Implement UI to display initiatives per client | 4 hours |
| [ ] | Write happy path tests for initiative creation | 4 hours |
| **TOTAL** | | **6 days, 0 hours** |

### Section 7: Nightly Article Fetching
| TODO | Description | Estimate |
|------|-------------|----------|
| [ ] | Implement Perigon API integration (`GET /v1/articles` with relevant filters) | 8 hours |
| [ ] | Store fetched articles in an `Article` model, associated with initiatives | 4 hours |
| [ ] | Deduplicate articles before storing | 4 hours |
| [ ] | Create a background job using GoodJob to fetch articles nightly | 8 hours |
| [ ] | Add logging for API failures | 2 hours |
| [ ] | Write tests for API response parsing | 4 hours |
| [ ] | Implement basic UI for viewing fetched articles per initiative | 8 hours |
| [ ] | Ensure only relevant articles are stored based on search terms | 4 hours |
| [ ] | Display API quota usage in logs | 2 hours |
| **TOTAL** | | **5 days, 4 hours** |

## Phase 4: Relevancy & Pitch Drafts

### Section 8: Relevancy & Sentiment Analysis
| TODO | Description | Estimate |
|------|-------------|----------|
| [ ] | Create our own sentiment scores using OpenAI API | 8 hours |
| [ ] | Implement logic to compare Perigon's relevancy score with our sentiment adjustments | 8 hours |
| [ ] | Store the adjusted relevancy scores in the database | 2 hours |
| [ ] | Ensure articles can be filtered by relevancy score in the UI | 4 hours |
| [ ] | Write happy path tests for sentiment adjustments | 4 hours |
| [ ] | Create a background job to update relevancy scores daily | 4 hours |
| **TOTAL** | | **3 days, 6 hours** |

### Section 9: Pitch Prompt Generation
| TODO | Description | Estimate |
|------|-------------|----------|
| [ ] | Create `PitchArtifact` model to store past pitch data per User | 4 hours |
| [ ] | Implement user file upload for past pitches | 8 hours |
| [ ] | Generate initial pitch drafts based on uploaded data and guidelines using OpenAI API | 2 days |
| [ ] | Break pitch generation into multiple steps, ensuring brand guidelines are respected | 2 days |
| [ ] | Provide UI for users to view and refine pitch prompt | 8 hours |
| [ ] | Implement history tracking for pitch prompts | 4 hours |
| [ ] | Write happy path tests for pitch generation | 8 hours |
| **TOTAL** | | **6 days, 0 hours** |

## Phase 5: Full End-to-End Workflow

### Section 10: Morning Article List & Export
| TODO | Description | Estimate |
|------|-------------|----------|
| [ ] | Display a daily list of relevant articles per initiative | 8 hours |
| [ ] | Generate short summaries for each article, with links to full article and assets | 8 hours |
| [ ] | Show our relevancy score, Perigon's score, and our adjusted score. | 4 hours |
| [ ] | Use the user's pitch prompt to generate a Pitch Draft for the article | 8 hours |
| [ ] | Make a link to this draft available on each row, with the body of the draft encoded in the URL | 4 hours |
| **TOTAL** | | **4 days, 0 hours** |

### Section 11: Durability of External Calls
| TODO | Description | Estimate |
|------|-------------|----------|
| [ ] | Implement job wrapping for all OpenAI API calls to allow retries and exponential backoff on rate limits | 8 hours |
| [ ] | Implement job wrapping for Perigon API calls using the same retry strategy | 8 hours |
| [ ] | Define job failure handling; after X retries, move to a dead letter queue | 4 hours |
| [ ] | Utilize GoodJob's built-in failure handling mechanisms where possible | 4 hours |
| [ ] | Monitor and log API failure patterns for better debugging | 4 hours |
| **TOTAL** | | **3 days, 4 hours** |

### Section 12: E2E Testing & Final Staging Deployment
| TODO | Description | Estimate |
|------|-------------|----------|
| [ ] | Write happy path tests for all core features | 2 days |
| [ ] | Run full test suite in GitHub Actions before each deployment | 4 hours |
| [ ] | Deploy to staging and confirm E2E flows are functional | 8 hours |
| [ ] | Implement smoke tests for key workflows | 8 hours |
| [ ] | Add performance monitoring on staging | 4 hours |
| [ ] | Ensure logs capture key application events | 4 hours |
| [ ] | Conduct final UI review and refinements | 8 hours |
| [ ] | Validate user authentication flows | 4 hours |
| [ ] | Document test results and areas for improvement | 8 hours |
| **TOTAL** | | **6 days, 0 hours** |
