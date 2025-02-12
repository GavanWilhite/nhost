---
title: 'Schema'
sidebar_position: 4
---

Hasura Auth stores all its data in a dedicated `auth` PostgreSQL schema. When Hasura Auth starts, it checks if the `auth` schema exists, then automatically syncs the following tables and their corresponding Hasura metadata:

```mermaid
erDiagram
migrations {
    integer id PK
    varchar name
    varchar hash
    timestamp executed_at "CURRENT_TIMESTAMP"
}

users ||--o{ user_roles : roles
user_roles }o--|| roles: role
users }o--|| roles: role
users ||--o{ refresh_tokens: refreshTokens
users ||--o{ user_providers: provider
providers ||--o{ user_providers: user

provider_requests {
    uuid id PK "gen_random_uuid()"
    test redirect_url
}


refresh_tokens {
    uuid refresh_token PK
    uuid user_id FK
    timestamptz created_at "now()"
    timestamptz expires_at
}

providers {
    text id PK
}
user_providers {
    uuid id PK "gen_random_uuid()"
    timestamptz created_at "now()"
    timestamptz updated_at "now()"
    uuid user_id FK
    text access_token
    text refresh_token
    text provider_id FK
    text provider_user_id
}
user_roles {
    uuid id PK "gen_random_uuid()"
    timestamptz created_at "now()"
    uuid user_id FK
    text role FK
}
users {
    uuid id PK "gen_random_uuid()"
    timestamptz created_at "now()"
    timestamptz updated_at "now()"
    timestamptz last_seen "nullable"
    boolean disabled "false"
    text display_name "''"
    text avatar_url "''"
    varchar locale
    email email "nullable"
    text phone_number "nullable"
    text password_hash "nullable"
    boolean email_verified "false"
    boolean phone_number_verified "false"
    email new_email "nullable"
    text otp_method_last_used "nullable"
    text otp_hash "nullable"
    timestamptz opt_hash_expires_at "now()"
    text default_role FK "user"
    boolean is_anonymous "false"
    text totp_secret "nullable"
    text active_mfa_type "nullable"
    text ticket "nullable"
    timestamptz ticket_expires_at "now()"
    jsonb metadata "nullable"
}

roles {
    text roles PK
}
```
