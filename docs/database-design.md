# Database Design - AutoSync Portfolio

## Overview
Using Amazon DynamoDB (NoSQL) for scalability and performance.

## Tables

### 1. autosync-users
**Purpose:** Store user account information

**Keys:**
- Partition Key: `userId` (String)

**Attributes:**
| Attribute | Type | Description |
|-----------|------|-------------|
| userId | String | Unique user identifier (PK) |
| email | String | User's email address |
| username | String | Display name |
| fullName | String | User's full name |
| createdAt | String | ISO timestamp |
| profileComplete | Boolean | Setup completion status |

**Example:**
```json
{
  "userId": "user_abc123",
  "email": "alice@example.com",
  "username": "alice",
  "fullName": "Alice Johnson",
  "createdAt": "2024-12-30T10:00:00Z",
  "profileComplete": true
}
```

### 2. autosync-skills
**Purpose:** Store user skills and proficiency levels

**Keys:**
- Partition Key: `userId` (String)
- Sort Key: `skillId` (String)

**Attributes:**
| Attribute | Type | Description |
|-----------|------|-------------|
| userId | String | User identifier (PK) |
| skillId | String | Skill identifier (SK) |
| skillName | String | Name of the skill |
| proficiency | Number | 1-5 rating |
| category | String | Frontend/Backend/DevOps/etc |
| yearsOfExperience | Number | Years using skill |
| createdAt | String | ISO timestamp |
| updatedAt | String | ISO timestamp |

**Example:**
```json
{
  "userId": "user_abc123",
  "skillId": "skill_001",
  "skillName": "React",
  "proficiency": 4,
  "category": "Frontend",
  "yearsOfExperience": 2,
  "createdAt": "2024-12-30T10:00:00Z",
  "updatedAt": "2024-12-30T10:00:00Z"
}
```

## Query Patterns

### Get User by ID
```javascript
GetItem(userId: "user_abc123")
```

### Get All Skills for User
```javascript
Query(userId: "user_abc123")
// Returns all skills for this user
```

### Get Specific Skill
```javascript
GetItem(userId: "user_abc123", skillId: "skill_001")
```

## Design Decisions

**Why DynamoDB over RDS?**
- Serverless (no server management)
- Automatic scaling
- Single-digit millisecond latency
- Pay only for what we use
- Perfect for variable workloads

**Why Composite Key for Skills?**
- Each user has multiple skills
- Easy to query all skills for one user
- Efficient storage and retrieval
- Supports future features (filtering, sorting)

## Cost Estimation
- Free tier: 25GB storage, 25 WCU, 25 RCU
- On-demand pricing: ~$0.25 per million reads
- Expected MVP cost: $0-2/month
