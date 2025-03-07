# Winncom Lead Agent

## Project Overview

The Winncom Lead Agent is an automated email processing system designed to monitor a Gmail inbox, classify incoming emails as leads or information requests, generate appropriate responses, and forward them to human agents for review before sending.

## Documentation Structure

This project's documentation is organized into the following files:

1. **README.md** (this file): Project overview, requirements, and implementation plan
2. **[SYSTEM_ARCHITECTURE.md](SYSTEM_ARCHITECTURE.md)**: Detailed system architecture and component design
3. **[API_CONTRACTS.md](API_CONTRACTS.md)**: API endpoint specifications and data formats

## MVP Focus

For the initial Minimum Viable Product (MVP), we will focus on:
1. **Gmail Integration**: Setting up secure access to read emails from designated Gmail accounts
2. **Lead Identification**: Developing a system to accurately classify incoming emails as leads or information requests
3. **Basic Information Extraction**: Identifying key details from emails such as contact information and product interests

Later phases will incorporate response generation, knowledge base integration, and a more sophisticated review interface.

## Key Features

- **Gmail Integration**: Seamlessly connects with Gmail to monitor and process incoming emails
- **Email Classification**: Automatically categorizes emails as sales leads or information requests
- **Information Extraction**: Identifies and extracts key details from incoming emails
- **Response Generation**: Creates tailored responses based on email content and available knowledge base
- **Human Review Interface**: Provides an easy-to-use interface for reviewing and approving generated responses
- **Web-Based Access**: Accessible via browser tab or potentially as a browser extension

## System Requirements

### Functional Requirements

1. **Email Monitoring**
   - Connect to Gmail accounts via OAuth 2.0
   - Monitor inbox for new emails on a configurable schedule (initially every 30 minutes)
   - Process various email formats (plain text, HTML, with attachments)
   - Flag emails that require special attention (e.g., from VIP customers)

2. **Email Classification**
   - Analyze email content to determine if it's a lead or information request
   - Identify lead type (new customer vs. existing customer)
   - Recognize product-specific inquiries related to computer products
   - Extract key information (contact details, specific interests, questions)
   - Handle edge cases and ambiguous emails with a "needs review" category

3. **Information Lookup**
   - Access Winncom product database for accurate product information
   - Identify relevant product details needed for response
   - Support for expanding knowledge base over time
   - Cache frequently accessed information for performance

4. **Response Generation**
   - Create personalized, contextually appropriate responses
   - Include relevant product/service information
   - Maintain consistent brand voice and messaging
   - Support templates for common response types

5. **Human Review Process**
   - Present generated responses to human agents for review
   - Allow for editing before sending
   - Provide feedback mechanism to improve future responses
   - Track response status (pending review, approved, sent)

6. **User Interface**
   - Web-based dashboard accessible via browser
   - Intuitive interface for reviewing and managing emails
   - Notification system for new emails requiring review
   - Mobile-responsive design for on-the-go review

### Non-Functional Requirements

1. **Performance**
   - Process emails within 5 minutes of scheduled check
   - Handle up to 20 emails per day (with capacity to scale)
   - Response generation completed within 30 seconds

2. **Security**
   - Secure OAuth 2.0 integration with Gmail
   - Encrypted storage of email content and responses
   - Role-based access control for human reviewers
   - Compliance with data protection regulations
   - Secure API communications with Winncom product database

3. **Reliability**
   - System uptime of 99.9%
   - Error handling and recovery mechanisms
   - Backup and restore capabilities
   - Logging of all system activities for troubleshooting

4. **Scalability**
   - Support for multiple Gmail accounts/inboxes
   - Ability to handle increasing email volume
   - Modular architecture to allow for future enhancements

## Technology Stack (Proposed)

- **Backend**: Python with FastAPI for email processing, classification, and response generation
- **Gmail Integration**: Gmail API with OAuth 2.0 authentication
- **Classification**: 
  - MVP: Rule-based system with keyword matching and basic NLP
  - Future: Machine learning models for improved accuracy
- **Frontend**: React for the web interface with Material UI components
- **Database**: 
  - PostgreSQL for structured data
  - Redis for caching frequently accessed information
- **Deployment**: Docker containers, cloud hosting (AWS/GCP)
- **CI/CD**: GitHub Actions for continuous integration and deployment

For a detailed view of how these components interact, see the [System Architecture](SYSTEM_ARCHITECTURE.md) document.

## Detailed MVP Specifications

### Gmail API Integration
- Use OAuth 2.0 for secure authentication
- Request read-only access to emails initially
- Implement webhook or polling mechanism to detect new emails
- Store email metadata and content securely
- Handle rate limiting and API quotas appropriately

See the [API Contracts](API_CONTRACTS.md#gmail-integration-api) for detailed endpoint specifications.

### Lead Classification System
- Implement rule-based classification with the following categories:
  - New customer lead
  - Existing customer inquiry
  - Information request
  - Not relevant/spam
  - Needs human review
- Classification rules will consider:
  - Email sender domain and address
  - Subject line keywords
  - Email body content analysis
  - Presence of specific product mentions
  - Question patterns and request language

See the [Classification API](API_CONTRACTS.md#classification-api) for related endpoints.

### Information Extraction
- Extract and structure the following data points:
  - Contact information (name, email, phone if available)
  - Company information
  - Product interests
  - Specific questions asked
  - Urgency indicators
  - Preferred contact method if specified

See the [Information Extraction API](API_CONTRACTS.md#information-extraction-api) for related endpoints.

### Data Storage
- Secure database for storing:
  - Email metadata
  - Classification results
  - Extracted information
  - Processing status
  - Audit logs

For database schema details, refer to the [Data Storage Layer](SYSTEM_ARCHITECTURE.md#4-data-storage-layer) section.

## Project Phases

### Phase 1: Foundation (MVP)
- Set up project structure and development environment
- Implement Gmail API integration
- Create basic email processing pipeline
- Develop simple classification rules
- Build minimal dashboard for monitoring

### Phase 2: Core Functionality
- Build response generation system
- Develop human review interface
- Implement feedback mechanism
- Create comprehensive dashboard

### Phase 3: Enhancement
- Improve classification accuracy
- Expand knowledge base integration
- Add analytics and reporting
- Optimize performance

### Phase 4: Deployment & Scaling
- Comprehensive testing
- Production deployment
- User training
- Monitoring and maintenance plan

## Open Questions (With Current Answers)

- **What is the expected volume of emails to process daily?**  
  Less than 10 per day initially, but needs further clarification.

- **Are there specific types of leads or information requests to prioritize?**  
  Yes, most leads will be from new or existing customers looking to improve their business with new computer products.

- **What existing systems (CRM, knowledge base) need to be integrated?**  
  We will need to integrate with the Winncom product database. This is a significant unknown that requires further investigation.

- **What is the desired response time for different types of emails?**  
  We eventually want to respond to all emails within 24 hours.

- **What metrics will be used to measure success?**  
  We will measure the quality of email classification and response generation. Manual review will be used initially.

## Next Steps

1. **Finalize Technical Architecture**
   - Confirm technology stack choices
   - Create system architecture diagram
   - Define API contracts between components
   - ✅ See [SYSTEM_ARCHITECTURE.md](SYSTEM_ARCHITECTURE.md) and [API_CONTRACTS.md](API_CONTRACTS.md)

2. **Set Up Development Environment**
   - Initialize repository with basic project structure
   - Configure development tools and linting
   - Set up CI/CD pipeline

3. **Implement Gmail API Integration**
   - Create authentication flow
   - Develop email fetching mechanism
   - Build secure storage for email data
   - Follow the [Gmail Integration API](API_CONTRACTS.md#gmail-integration-api) specifications

4. **Develop Classification Prototype**
   - Implement rule-based classification system
   - Create test suite with sample emails
   - Measure and iterate on classification accuracy
   - Implement the [Classification API](API_CONTRACTS.md#classification-api)

5. **Design Basic UI**
   - Create wireframes for dashboard
   - Implement minimal viable interface
   - Test usability with stakeholders

## Glossary

**Lead**: A potential sales opportunity identified from an email, typically from a new or existing customer expressing interest in Winncom's computer products or services.

**Information Request**: An email inquiry seeking specific information about products, services, or company details, but not necessarily indicating immediate purchase intent.

**Classification**: The process of categorizing incoming emails as leads, information requests, or other categories based on content analysis.

**Information Extraction**: The process of identifying and extracting structured data (like contact information, product interests, etc.) from unstructured email text.

**OAuth 2.0**: An authorization framework that enables third-party applications to obtain limited access to a user's account on an HTTP service, used for Gmail API integration.

**Human Review**: The process where a human agent reviews automatically classified emails and generated responses before they are sent to ensure accuracy and appropriateness.

**Rule-based Classification**: A classification approach that uses predefined rules and patterns to categorize emails, as opposed to machine learning-based approaches.

**API (Application Programming Interface)**: A set of defined rules that allow different applications to communicate with each other, used throughout the system for component interactions.

**JWT (JSON Web Token)**: A compact, URL-safe means of representing claims to be transferred between two parties, used for authentication in the system.

**Webhook**: A method for an application to provide other applications with real-time information, potentially used for detecting new emails in Gmail.

**NLP (Natural Language Processing)**: A field of artificial intelligence that helps computers understand, interpret, and manipulate human language, used in email classification and information extraction.