# Entity Relationship Diagram - Mermaid Code

## Mermaid ER Diagram

```mermaid
erDiagram
    USER {
        string id PK "CUID"
        string email "Unique"
        string name
        datetime createdAt
        datetime updatedAt
    }
    
    RESUME {
        string id PK "CUID"
        string userId FK "References USER"
        string title "Nullable"
        string description "Nullable"
        string photoUrl "Nullable"
        string colorHex "Default: #000000"
        string borderStyle "Default: squircle"
        string summary "Nullable"
        string firstName "Nullable"
        string lastName "Nullable"
        string jobTitle "Nullable"
        string city "Nullable"
        string country "Nullable"
        string phone "Nullable"
        string email "Nullable"
        string[] skills "Array"
        datetime createdAt
        datetime updatedAt
    }
    
    WORK_EXPERIENCE {
        string id PK "CUID"
        string resumeId FK "References RESUME"
        string position "Nullable"
        string company "Nullable"
        datetime startDate "Nullable"
        datetime endDate "Nullable"
        string description "Nullable"
        datetime createdAt
        datetime updatedAt
    }
    
    EDUCATION {
        string id PK "CUID"
        string resumeId FK "References RESUME"
        string degree "Nullable"
        string school "Nullable"
        datetime startDate "Nullable"
        datetime endDate "Nullable"
        datetime createdAt
        datetime updatedAt
    }
    
    USER_SUBSCRIPTION {
        string id PK "CUID"
        string userId FK "References USER, Unique"
        string stripeCustomerId "Unique"
        string stripeSubscriptionId "Unique"
        string stripePriceId
        datetime stripeCurrentPeriodEnd
        boolean stripeCancelAtPeriodEnd "Default: false"
        datetime createdAt
        datetime updatedAt
    }
    
    %% Relationships
    USER ||--o{ RESUME : "creates"
    USER ||--|| USER_SUBSCRIPTION : "has"
    RESUME ||--o{ WORK_EXPERIENCE : "includes"
    RESUME ||--o{ EDUCATION : "includes"
```

## Alternative Mermaid ERD (Simplified)

```mermaid
erDiagram
    USER {
        string id PK
        string email
        string name
    }
    
    RESUME {
        string id PK
        string userId FK
        string title
        string summary
        string firstName
        string lastName
        string jobTitle
        string email
        string phone
        string[] skills
    }
    
    WORK_EXPERIENCE {
        string id PK
        string resumeId FK
        string position
        string company
        datetime startDate
        datetime endDate
        string description
    }
    
    EDUCATION {
        string id PK
        string resumeId FK
        string degree
        string school
        datetime startDate
        datetime endDate
    }
    
    USER_SUBSCRIPTION {
        string id PK
        string userId FK
        string stripeCustomerId
        string stripeSubscriptionId
        datetime stripeCurrentPeriodEnd
    }
    
    USER ||--o{ RESUME : "1:N"
    USER ||--|| USER_SUBSCRIPTION : "1:1"
    RESUME ||--o{ WORK_EXPERIENCE : "1:N CASCADE"
    RESUME ||--o{ EDUCATION : "1:N CASCADE"
```

## Class Diagram Alternative

```mermaid
classDiagram
    class User {
        +String id
        +String email
        +String name
        +DateTime createdAt
        +DateTime updatedAt
    }
    
    class Resume {
        +String id
        +String userId
        +String title
        +String description
        +String photoUrl
        +String colorHex
        +String borderStyle
        +String summary
        +String firstName
        +String lastName
        +String jobTitle
        +String city
        +String country
        +String phone
        +String email
        +String[] skills
        +DateTime createdAt
        +DateTime updatedAt
    }
    
    class WorkExperience {
        +String id
        +String resumeId
        +String position
        +String company
        +DateTime startDate
        +DateTime endDate
        +String description
        +DateTime createdAt
        +DateTime updatedAt
    }
    
    class Education {
        +String id
        +String resumeId
        +String degree
        +String school
        +DateTime startDate
        +DateTime endDate
        +DateTime createdAt
        +DateTime updatedAt
    }
    
    class UserSubscription {
        +String id
        +String userId
        +String stripeCustomerId
        +String stripeSubscriptionId
        +String stripePriceId
        +DateTime stripeCurrentPeriodEnd
        +Boolean stripeCancelAtPeriodEnd
        +DateTime createdAt
        +DateTime updatedAt
    }
    
    User ||--o{ Resume : creates
    User ||--|| UserSubscription : subscribes
    Resume ||--o{ WorkExperience : includes
    Resume ||--o{ Education : includes
```

## Usage Instructions

### For GitHub/GitLab/Documentation:
1. Copy any of the mermaid code blocks above
2. Paste into your markdown files
3. The diagram will render automatically

### For Mermaid Live Editor:
1. Visit https://mermaid.live
2. Paste the code to see live preview
3. Export as PNG/SVG if needed

### Recommended Version:
The **first ERD version** is recommended as it:
- ✅ Shows all field details and constraints
- ✅ Includes data types and default values
- ✅ Shows nullable fields clearly
- ✅ Displays all relationship cardinalities
- ✅ Most comprehensive and professional

### Key Features Highlighted:
- **Primary Keys (PK)**: All entities use CUID strings
- **Foreign Keys (FK)**: Clear references between entities
- **Unique Constraints**: Shown on UserSubscription fields
- **Cascade Deletes**: WorkExperience and Education delete with Resume
- **Default Values**: colorHex, borderStyle, stripeCancelAtPeriodEnd
- **Nullable Fields**: Marked with "Nullable" annotation