1. git remote add (remote repo)
2. git fetch
3. git pull origin main (remote branch)

# MongoDB Cloud

# Table of Contents

## Setup

1. [MongoDB Realm](#mongodb-realm)
2. [Application Setup](#application-setup)
3. [Realm SDK](#install-realm-sdk)
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
12. [Implement Anonymous User Authentication](#implement-anonymous-user-authentication)
13. [Implement adding likes and likes count](#implement-adding-likes-and-likes-count)
14. [Email and Password Auth](#email-and-password-auth)
15. [Implementing email user login](#implementing-email-user-login)
16. [Adding custom user data](#adding-custom-user-data)
17. [Adding comments](#adding-comments)

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
<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/tailwindcss/4.0.0-alpha.9/lib.min.js"
/>
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
4. Add **Role** amd set permission to **readAndWriteAll**
5. Click **Review Draft & Deploy**

## Implement Anonymous User Authentication

```javascript
const REALM_APP = new Realm.App({
  id: "mongocloudapp-psyui",
});

const AUTHENTICATE_USER_ANONYMOUSLY = async () => {
  const ANOVYNOUS_USER = await REALM_APP.logIn(Realm.Credentials.anonymous());
  console.log(ANOVYNOUS_USER);
};

if (!REALM_APP.currentUser.isLoggedIn) {
  AUTHENTICATE_USER_ANONYMOUSLY();
}

console.log(REALM_APP?.currentUser);

const SITE_LIST = [{}];

const SITE_LIST_CONTAINER_DIV = document.getElementById("html-document-id");

SITE_LIST.forEach((siteData) => {
  const SITE_ITEM_FRAGMENT = `
        HTML
        `;

  SITE_LIST_CONTAINER_DIV.insertAdjacentHTML("beforeend", SITE_ITEM_FRAGMENT);
});
```

## Implement adding likes and likes count

```javascript
 async function onVoteButtonClicked(siteID, imageName){
     const INSERT_VOTE = await REALM_APP.currentUser.mongoClient("mongodb-atlas")
      .db("vinividevici")
      .collection("likes")
      .insertOne({
        site_id: siteID.toString(),
        voter_id: REALM_APP.currentUser.id,
        image_name: imageName
      });
      console.log(INSERT_VOTE);

      const BUTTON_TO_UPDATE = document.getElementById(`vote-count-${siteID}`)
      const VOTE_COUNT = await REALM_APP.currentUser.mongoClient("mongodb-atlas")
      .db("vinividevici")
      .collection("likes")
      .count({
        site_id: siteID.toString()
      });

      BUTTON_TO_UPDATE.innerText = VOTE_COUNT;
    }
<button
    onclick="onVoteButtonClicked(${siteData.sight_id}, '${siteData.name}')"
    id="vote-button-${siteData.sight_id}"
    type="button"
    class="vote-button relative inline-flex items-center px-4 py-2 rounded-l-md border border-gray-300 bg-white text-sm font-medium text-gray-700 hover:bg-gray-50 focus:z-10 focus:outline-none focus:ring-1 focus:ring-indigo-500 focus:border-indigo-500"
>
```

## Email and Password Auth

1. Go to App Services
2. Click **Authentication**
3. Click **Email/Passwords**
4. Enable Provider
5. Under **User Confirmation** select **Automatically confirm users**
6. Under Password Reset, select **Send a password reset email**
7. Click **Save Draft**

## Implementing email user login

```javascript
<button
    onclick="onLoginButtonClicked()"
    id="login-button"
    type="button"
    class="group relative w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
>
<script type="text/javascript">
      const EMAIL_FIELD = document.getElementById("email-address");
      const PASSWORD_FIELD = document.getElementById("password");
      const LOGIN_BUTTON = document.getElementById("login-button");

      const REALM_APP = new Realm.App({
        id: "mongocloudapp-psyui",
      });

      async function onLoginButtonClicked() {
        try {
          const EMAIL_PASSWORD_CREDENTIALS = await Realm.Credentials.emailPassword(
            EMAIL_FIELD.value.toLowerCase().trim(),
            PASSWORD_FIELD.value
          );
          const EMAIL_PASSWORD_USER = await REALM_APP.logIn(EMAIL_PASSWORD_CREDENTIALS);
          window.location.href = "index.html"
        } catch(e) {
          console.log(e)
        }
      }
```

## Adding custom user data

1. Go to **App Users**
2. Click **User Settings**
3. Enable **"Custom User Data"**

## Adding comments
```javascript
function storage() {
  const url_params = new URLSearchParams(window.location.search);
  const site_id_param = url_params.get("site-id");
  const site_location_param = url_params.get("location");

  console.log(site_id_param + "\n" + site_location_param);

  const site_list = [{}];

  const site_data = site_list.find(
    (site) => site_id_param === site.sight_id.toString()
  );

  const site_image = document.getElementById("site-image");
  const site_name = document.getElementById("site-name");
  const site_location = document.getElementById("site-location");

  site_image.src = site_data.image_url;
  site_image.alt = site_data.name;
  site_name.innerText = site_data.name;
  site_location.innerText = site_data.location;
  async function onCommentButtonClicked() {
    const comment_box = document.getElementById("comment");
    try {
      const insert_comment = await realm_app.currentUser
        .mongoClient("mongodb-atlas")
        .db("vinividevici")
        .collection("comments")
        .insertOne({
          site_id: site_id_param,
          comment: comment_box.value,
          commenter: realm_app?.currentUser?.id,
        });
      console.log(insert_comment);

      const comments_from_db = await realm_app.currentUser
        .mongoClient("mongodb-atlas")
        .db("vinividevici")
        .collection("comments")
        .find({
          site_id: site_id_param,
        });
      console.log(comments_from_db);

      const comments_container = document.getElementById(
        "comment-list-container"
      );
      comments_container.innerHTML = "";
      comments_from_db.forEach((comment) => {
        const single_comment = `
                            <li>
                              <div class="flex space-x-3">
                                <div>
                                  <div class="mt-1 text-sm text-gray-700">
                                    <p class="comment-text">${comment.comment}</p>
                                  </div>
                                  <div class="mt-2 text-sm space-x-2">
                                    <button
                                      type="button"
                                      class="text-gray-900 font-medium"
                                    >
                                      Delete
                                    </button>
                                    <button
                                      type="button"
                                      class="text-gray-900 font-medium"
                                    >
                                      Update
                                    </button>
                                  </div>
                                </div>
                              </div>
                            </li>
                            `;
        comments_container.insertAdjacentHTML("beforeend", single_comment);
      });
      comment_box.value = "";
    } catch (e) {
      console.log(e + "What the heck?");
    }
}
```

## More Data Operations

## Functions and Triggers

## Schemas and Rules/Roles

### 90&\*O@0Fqi02UVrQ
