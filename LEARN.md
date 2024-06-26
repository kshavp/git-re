### Set Up your Database :

- Go to your [Supabase Dashboard](https://supabase.io/dashboard).
- Select your project / Create a new one.
- Navigate to the "Project Settings" in the sidebar of your newly created project.
- Now go to "API" under `CONFIGURATION` section.
- Copy the `URL` and `ANON-PUBLIC` from this tab and paste in your .env.local file respectively.

### For authentication, we have used Github OAuth using Supabase. To set this up:

- Go to [Github](https://github.com/) website.
- Click on your profile icon, located on top-right of the webpage.
- Click on "Settings" and go to `Developers settings` by scrolling down the page.
- Click on `OAuth Apps` and create a new application.
- From here you'll get two secret credentials - "Client ID" and "Secret".
- Now navigate to Supabase, and go inside "Authentication" tab from the sidebar.
- Under "Providers", find GitHub and fill in the "Client ID" and "Secret" fields with the details from your GitHub OAuth App.
- If you haven't created a GitHub OAuth App yet, you can follow [this guide](https://docs.github.com/en/developers/apps/building-oauth-apps/creating-an-oauth-app).
- Save your changes.
- Now you can do the authentication using github.

### For the recent users storage, we need to create a table in Supabase:

- Go to your [Supabase Dashboard](https://supabase.io/dashboard).
- Select your project.
- Navigate to the "SQL Editor" tab in the sidebar.
  <img width="208" alt="Screenshot 2024-05-12 at 5 26 14 PM" src="https://github.com/ashutosh-rath02/git-re/assets/65452005/ad9e27bc-38bb-47c3-8854-4ab3b5375e1c">
- Run the following SQL query:

```sql
create table
  public.recent_users (
    id bigint generated by default as identity,
    created_at timestamp with time zone not null default now(),
    name text not null,
    avatar_url text not null,
    bio text null,
    username text not null,
    constraint recent_users_pkey primary key (id),
    constraint recent_users_username_key unique (username)
  ) tablespace pg_default;
```

- This will create a table named `recent_users` in your Supabase project.
- Open that table from `Table Editor` and disable the RLS Policy.
  <img width="1366" alt="Screenshot 2024-05-12 at 5 32 04 PM" src="https://github.com/ashutosh-rath02/git-re/assets/65452005/e6a9b10d-6b17-40f1-b441-e7c89f364832">
  <img width="1337" alt="Screenshot 2024-05-12 at 5 32 30 PM" src="https://github.com/ashutosh-rath02/git-re/assets/65452005/68f7bc0b-79ba-424f-96bd-649756a7c228">
