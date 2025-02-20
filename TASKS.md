# Web Application Development Task List

## Phase 1: Foundation & Infrastructure
### 1.1: Project Setup
- [ ] Initialize Rails application with Postgres configuration
- [ ] Set up Git repository and branch structure
- [ ] Configure Tailwind CSS and Stimulus frameworks
- [ ] Install and configure Good_job for background processing
- [ ] Create development, staging, and production environments
- [ ] Configure Heroku deployment pipeline
- [ ] Set up CI/CD workflows
- [ ] Implement API keys management for OpenAI/Anthropic

### 1.2: User Authentication & Management
- [ ] Implement Devise for user authentication
- [ ] Create User model with required attributes
- [ ] Implement role-based authorization (Super-User, Admin, Pod-Leader, Pod-Member)
- [ ] Set up CanCanCan/Pundit for permission management
- [ ] Design and implement user management interface
- [ ] Create role assignment functionality for administrators
- [ ] Set up user invitation workflow
- [ ] Implement password reset functionality
- [ ] Configure email notifications for account actions
- [ ] Add user profile management

### 1.3: Database Schema & Models
- [ ] Design and implement Client model
- [ ] Create BrandGuideline model with associations
- [ ] Implement Initiative model with client associations
- [ ] Design Activity Log with polymorphic associations
- [ ] Create Periodical model for tracking
- [ ] Implement Article model with vector storage capability
- [ ] Set up database indexes for optimized queries
- [ ] Configure database validations and constraints
- [ ] Implement soft delete functionality where appropriate
- [ ] Create database seeding scripts for development

## Phase 2: Core Features Development
### 2.1: Client & Brand Guidelines Management
- [ ] Implement client creation interface
- [ ] Create form interface for brand guidelines
- [ ] Build chatbot-driven form functionality (BIG)
- [ ] Implement file upload for brand assets (PDFs, images)
- [ ] Create auto-population logic from uploaded materials (BIG)
- [ ] Build traditional form fallback interface
- [ ] Implement version history for brand guidelines
- [ ] Create client dashboard view
- [ ] Build search and filter functionality for clients

### 2.2: Initiatives Management
- [ ] Build initiative creation interface
- [ ] Implement initiative update functionality
- [ ] Create chatbot-assisted initiative forms (BIG)
- [ ] Add initiative association with clients
- [ ] Implement role-based initiative visibility

## Phase 3: AI Integration & Article Processing
### 3.1: Web Scraping & Article Extraction
- [ ] Evaluate commercial APIs (newsapi, cision, meltwater)
- [ ] Test in-house extraction libraries (ruby-readability)
- [ ] Implement crawler for fetching pages (BIG)
- [ ] Build article extraction pipeline (BIG)
- [ ] Implement error handling and retry mechanism
- [ ] Build logging system for extraction errors
- [ ] Create alert system for repeated failures
- [ ] Develop admin dashboard for periodical management
- [ ] Implement periodical onboarding interface
- [ ] Build batch import functionality for periodicals

### 3.2: Vector Database & Embedding Generation
- [ ] Select and configure vector database solution
- [ ] Implement embedding generation using OpenAI/Anthropic
- [ ] Create storage mechanism for article embeddings
- [ ] Build background job for generating embeddings
- [ ] Implement approximate nearest neighbor search
- [ ] Build query embedding generation for brands/initiatives
- [ ] Create optimization for batch embedding operations

### 3.3: Relevancy & Sentiment Analysis
- [ ] Implement baseline relevance scoring using embeddings
- [ ] Build Named Entity Recognition (NER) integration
- [ ] Create aspect-based sentiment analysis pipeline
- [ ] Implement brand-specific rule processing
- [ ] Build combined scoring algorithm
- [ ] Create API endpoints for relevancy scoring
- [ ] Implement caching for frequently accessed scores
- [ ] Build benchmark testing framework
- [ ] Create visualization for score comparison

## Phase 4: Advanced Features & Integration
### 4.1: Training System for Reach-outs
- [ ] Create upload interface for training samples
- [ ] Implement training corpus management
- [ ] Build model training pipeline
- [ ] Create version tracking system
- [ ] Implement model evaluation metrics
- [ ] Build UI for training status and history
- [ ] Create user-level model customization
- [ ] Implement corpus transparency features
- [ ] Build training job scheduling

### 4.2: Article List & Pitch Draft Generation
- [ ] Build morning article list generation system
- [ ] Implement sorted article display by relevance
- [ ] Create article summary generation functionality
- [ ] Implement pitch draft generation button
- [ ] Build pitch template management system
- [ ] Create export functionality for article lists
- [ ] Implement CSV export for external tools
- [ ] Build email draft preview interface
- [ ] Create styling for generated drafts
- [ ] Implement brand guideline integration in drafts

