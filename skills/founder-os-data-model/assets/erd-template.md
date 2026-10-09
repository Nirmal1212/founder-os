# ERD — <Product Name> data model

> Entities are 1:1 with the founder-os-context glossary. Render with Mermaid.

```mermaid
erDiagram
  ACCOUNT ||--o{ WORKSPACE : owns
  WORKSPACE ||--o{ MEMBERSHIP : has
  USER ||--o{ MEMBERSHIP : "belongs via"
  WORKSPACE ||--o{ PROJECT : contains

  ACCOUNT {
    uuid id PK
    string name
    enum plan
    timestamptz created_at
  }
  WORKSPACE {
    uuid id PK
    uuid account_id FK
    string name
    timestamptz created_at
  }
  MEMBERSHIP {
    uuid user_id PK_FK
    uuid workspace_id PK_FK
    enum role
    timestamptz joined_at
  }
  USER {
    uuid id PK
    citext email "unique, PII"
    timestamptz created_at
  }
  PROJECT {
    uuid id PK
    uuid workspace_id FK
    string title
    timestamptz created_at
  }
```

**Cardinality legend:** `||--o{` = one-to-many (mandatory parent, optional children) · `}o--o{` = many-to-many (resolve with a join entity).

**Notes**
- M:N between USER and WORKSPACE resolved via MEMBERSHIP (carries `role`).
- Flag PII attributes; note on-delete behavior on each FK.
