# create-svelte

Everything you need to build a Svelte project, powered by [`create-svelte`](https://github.com/sveltejs/kit/tree/main/packages/create-svelte).

## Creating a project

If you're seeing this, you've probably already done this step. Congrats!

```bash
# create a new project in the current directory
npm create svelte@latest

# create a new project in my-app
npm create svelte@latest my-app
```

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://kit.svelte.dev/docs/adapters) for your target environment.

The purpose of the site is to support collaboration and information sharing within a Marine Corps unit. Although additional features will be developed over time, the first major feature is to track appropriate duty orders generation, routing, and approval. Additional features are expected, but will be developed on a future date.

We'll start with reviewing some of the high-level functions within this feature, scoping out the necessary pages and objects in our database. To keep things simple, we will start with basic functionality and add in user authentication and account management later.

Some basic functions include:
* View an index of events in a list. This list should include the ability to filter and sort based on a unit, individual, and routing status.
* Create new events. This should include the ability to include one or many individuals and the ability to include one or many events for those individuals.
* Review and recommend/not recommend and approve/deny events. This should include the ability to review event details and process events individually or in bulk. Each action here should be logged and timestamped.

More advanced functions include:
* Account creation. This should tie OAuth via Supabase support and include states for new accounts and verified accounts. Account verification can be completed via an email to any .mil account (binding the OAuth account to that email) or via approval from an administrator or appropriate unit leader. Accounts should be bound to an individual in the unit hierarchy.
* Authentication/login. This should include OAuth via Supabase support, allowing Gmail accounts to tie to individuals.
* Authorization/permissions. Every individual should have access to events they are on. Every individual should have access to create or withdraw events they are on.
  * Unit leaders should have access to view and endorse (recommend/not recommend) events for subordinates. This can include pulling events from one or more levels below in the hierarchy, bypassing subordinate leaders.
  * Administrator access to manipulate unit hierarchy, move individuals between units, approve/revoke permissions, and create/remove individuals.
* Supporting offline submission of events. This should include certain business rules for the aggregation of events performed by an individual, production of a appropriate exportable reports, and tracking offline submission status (generated, submitted, and certified).

Nice to have functions include:
* Upload events in bulk via spreadsheet (.csv).
* Download reports in spreadsheet (.csv).
* Upload/update individuals and unit assignments via spreadsheet (.csv).
* PKI authentication via CAC certificates.

For the database, we can start with everything under the public schema. As the project complexity grows, we can look at different approaches to divide the tables between schemas.

We should have tables for:
* Users
* Marines
* Roles
* Reviews
* Events
* Units
* Submissions
* Any join tables necessary
