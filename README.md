1. git remote add (remote repo)
2. git fetch
3. git pull origin main (remote branch)

# MongoDB Cloud

# Table of Contents
## Setup
1. [MongoDB Realm](#mongodb-realm)
2. [Application Setup](#application-setup)
3. [Realm SDK](#realm-sdk)
4. [Data Operations](#data-operations)
5. [Email and Password Auth](#email-and-password-auth)
6. [More Data Operations](#more-data-operations)
7. [Functions and Triggers](#functions-and-triggers)
8. [Schemas and Rules/Roles](#schemas-and-rulesroles)
9. [Application Setup](#application-setup)
    - [Install Tailwinds CSS](#install-tailwinds-css)
10. [Install Realm SDK](#install-realm-sdk)
    - [Anonymous authentication](#anonymous-authentication)
11. [Data Operations](#data-operations)
    - [Create Database and collection](#create-database-and-collection)

## MongoDB Realm
Services that MongoDB Realm offer's
<details>
<summary>MongoDB database</summary>

**DBaaS**: Database as a Service (DBaaS) is a cloud computing service that allows users to access and use a cloud database system without purchasing and setting up their own hardware, installing their own database software, or managing the database themselves.

</details>

<details>
<summary>Authentication</summary>
</details>

<details>
<summary>Sync</summary>
</details>

<details>
<summary>GraphQL</summary>

**GraphQL**: GraphQL is a query language, architecture style, and set of tools for creating and manipulating APIs.

</details>

<details>
<summary>Hosting</summary>

**Hosting**: Hosting is a service that provides storage and computing resources for websites and related services.

</details>

<details>
<summary>Push Notifications</summary>

**Push notifications**: are messages that are sent to a user's device without a specific request from the client.

</details>

<details>
<summary>SDK Options</summary>

**SDK**: SDK stands for software development kit, which is a set of tools that developers use to create applications for specific platforms.

</details>

### Creating a Realm application

## Application Setup
### Install Tailwinds CSS
[Tailwind CSS](https://cdnjs.com/libraries/tailwindcss)
```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/tailwindcss/4.0.0-alpha.9/lib.min.js">
```
### Install Realm SDK
[Realm SDK](https://www.mongodb.com/docs/realm/web/quickstart/)
```html
<script src="https://unpkg.com/realm-web/dist/bundle.iife.js"></script>
```
### Anonymous authentication
1. Select **Authentication** under **DATA ACCESS**
2. Under **Providers** select **Allow users to log in anonymously**
3. Turn on **Provider Enabled** and click **'Save Draft'**
4. Click through prompts in popup window, and then click **Review Draft & Deploy**
5. Click **Deploy**

## Data Operations
### Create Database and collection
1. Go to **Rules**
2. Click **Add Collection**
3. Name the collection
6. Add **Role** amd set permission to **readAndWriteAll**
7. Click **Review Draft & Deploy**

## Email and Password Auth

## More Data Operations

## Functions and Triggers

## Schemas and Rules/Roles

