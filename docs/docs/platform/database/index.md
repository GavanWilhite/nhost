---
title: 'Database'
sidebar_position: 1
---

Every Nhost app comes with a Postgres database. Postgres is the world's most advanced open-source relational database and the most popular SQL database among developers. The database is hosted with Amazon RDS.

Tables are managed in the Hasura Console.

---

## Creating tables

1. In Hasura Console, go to the **Data** tab, select the **public** schema in the left menu and click **Create Table**
2. Enter a table name
3. Add table columns
4. Add a primary key (usually the ID column)
5. (Optional) Add foreign keys
6. (Optional) Add unique keys
7. Click **Add Table**

When a table is created, the table is created in Postgres and added to your GraphQL API.

#### Schemas

You should use the `public` schema when developing your app. `auth` and `storage` are reserved for system functionality like user and file management. You are allowed to modify permissions for tables in the `auth` and `storage` schemas, however.

---

## Modifying table schema

1. In Hasura Console, go to the **Data** tab and click on the table you want to edit in the left menu
2. Click **Modify**
3. Modify or add table columns

#### Track foreign-key relations

1. Click on Data in the top menu.
2. A list of untracked foreign-key relations is presented.
3. Click Track All (recommended) or click Track for each relationship you want to track.

---

## Deleting tables

1. In Hasura Console, go to the **Data** tab and select the table you want to delete in the left menu
2. Click **Modify**
3. Scroll to the bottom of the page and click **Delete table** to open the confirmation dialog
