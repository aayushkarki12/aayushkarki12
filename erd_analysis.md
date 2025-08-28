# Entity Relationship Diagram Analysis

## Entities Identified

### 1. Resume
- **Primary Key**: id (String, CUID)
- **Foreign Key**: userId (String) - References external User entity (not in schema)
- **Attributes**: title, description, photoUrl, colorHex, borderStyle, summary, firstName, lastName, jobTitle, city, country, phone, email, skills (array), createdAt, updatedAt

### 2. WorkExperience  
- **Primary Key**: id (String, CUID)
- **Foreign Key**: resumeId (String) - References Resume.id
- **Attributes**: position, company, startDate, endDate, description, createdAt, updatedAt

### 3. Education
- **Primary Key**: id (String, CUID) 
- **Foreign Key**: resumeId (String) - References Resume.id
- **Attributes**: degree, school, startDate, endDate, createdAt, updatedAt

### 4. UserSubscription
- **Primary Key**: id (String, CUID)
- **Foreign Key**: userId (String) - References external User entity (not in schema)
- **Attributes**: stripeCustomerId, stripeSubscriptionId, stripePriceId, stripeCurrentPeriodEnd, stripeCancelAtPeriodEnd, createdAt, updatedAt

## Relationships

### 1. Resume ↔ WorkExperience
- **Type**: One-to-Many (1:N)
- **Description**: One Resume can have multiple WorkExperiences
- **Constraint**: CASCADE DELETE (when Resume is deleted, all related WorkExperiences are deleted)

### 2. Resume ↔ Education  
- **Type**: One-to-Many (1:N)
- **Description**: One Resume can have multiple Educations
- **Constraint**: CASCADE DELETE (when Resume is deleted, all related Educations are deleted)

### 3. User ↔ Resume (Implied)
- **Type**: One-to-Many (1:N) 
- **Description**: One User can have multiple Resumes
- **Note**: User entity not defined in schema, but referenced by userId

### 4. User ↔ UserSubscription (Implied)
- **Type**: One-to-One (1:1)
- **Description**: One User has one UserSubscription
- **Constraint**: UNIQUE constraint on userId
- **Note**: User entity not defined in schema, but referenced by userId

## Key Constraints

1. **Unique Constraints**:
   - UserSubscription.userId (UNIQUE)
   - UserSubscription.stripeCustomerId (UNIQUE)  
   - UserSubscription.stripeSubscriptionId (UNIQUE)

2. **Cascade Constraints**:
   - WorkExperience.resumeId → Resume.id (CASCADE DELETE)
   - Education.resumeId → Resume.id (CASCADE DELETE)

3. **Default Values**:
   - Resume.colorHex: "#000000"
   - Resume.borderStyle: "squircle"
   - UserSubscription.stripeCancelAtPeriodEnd: false
   - All createdAt: now()
   - All updatedAt: auto-update

## Data Types
- **IDs**: String (CUID format)
- **Dates**: DateTime
- **Text**: String (various lengths)
- **Boolean**: Boolean
- **Array**: String[] (skills in Resume)