# Dynamic Office-Based Rule Configuration Framework

## Overview

This document describes a configuration-driven architecture for handling office-specific UI validations and business rules without requiring application redeployment.

---

## Problem Statement

Enterprise applications often contain business rules that vary by office, branch, customer, or region.

Examples:

* A field is mandatory for one office but optional for another.
* Certain fields are hidden based on office.
* Validation rules differ by office.
* UI behavior changes depending on operational requirements.

A common implementation is to introduce office-specific conditions in application code:

```java
if ("NYK".equals(officeId)) {
    shipperField.setRequired(true);
}
```

As the number of offices and rules grows, the code becomes difficult to maintain and every change requires:

* Code modification
* Testing
* Deployment
* Application restart

---

## Design Goals

* Support office-specific configurations
* Avoid code changes for rule updates
* Eliminate unnecessary deployments
* Improve runtime performance
* Provide a scalable and maintainable solution

---

## Proposed Solution

Store office-specific configurations in the database as JSON documents and load them into an in-memory cache.

Applications evaluate rules from cache instead of hardcoded conditions.

---

## Configuration Model

### Database Table

| Column      | Description                 |
| ----------- | --------------------------- |
| OFFICE_ID   | Office identifier           |
| SCREEN_NAME | Screen identifier           |
| CONFIG_JSON | Configuration document      |
| ACTIVE      | Active flag                 |
| UPDATED_AT  | Last modification timestamp |

---

### Example Configuration

```json
{
  "fields": {
    "shipper": {
      "required": true
    },
    "consignee": {
      "readOnly": true
    },
    "hazmat": {
      "visible": false
    }
  }
}
```

---

## Architecture

```text
Database (Source of Truth)
        ↓
Configuration Repository
        ↓
Configuration Cache
        ↓
Rule Service
        ↓
UI / Business Layer
```

---

## Startup Flow

1. Load all active configurations.
2. Parse JSON documents.
3. Populate in-memory cache.
4. Serve all rule evaluations from cache.

---

## Runtime Flow

```text
User Request
      ↓
Rule Service
      ↓
Cache Lookup
      ↓
Apply Rule
```

No database call is required during normal request processing.

---

## Cache Refresh Strategy

When a configuration changes:

1. Update configuration JSON in the database.
2. Invoke a cache refresh API.
3. Reload only the affected office configuration.

Example:

```http
POST /admin/config/reload?office=NYK
```

This ensures new configurations become available immediately without application restart.

---

## Performance Benefits

### Traditional Approach

```text
Request
  ↓
Business Logic
  ↓
Hardcoded Office Conditions
```

Challenges:

* Growing code complexity
* Frequent deployments
* Maintenance overhead

### Configuration-Driven Approach

```text
Request
  ↓
Rule Service
  ↓
In-Memory Cache Lookup
```

Benefits:

* O(1) lookup performance
* Reduced database load
* Faster response times
* Improved scalability

---

## Future Enhancements

Potential extensions include:

* Global → Region → Office inheritance
* Conditional rule evaluation
* Rule versioning
* Audit history
* Redis distributed caching
* Event-driven cache refresh

---

## Conclusion

A JSON-based office configuration framework provides a flexible and scalable mechanism for managing office-specific business behavior.

By externalizing configuration from application code and serving rule evaluations directly from cache, the solution improves maintainability, operational agility, and runtime performance while eliminating unnecessary deployments for business-driven changes.
