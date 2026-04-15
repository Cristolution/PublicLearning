



Sure—here’s a clean, consistent Laravel‑style **naming‑convention guide** you can use for your own backend projects (controllers, helpers, seeders, tasks, branches, variables, functions, files, etc.). I’ll keep it opinionated but close to what the Laravel community generally follows.stackoverflow+4

---

## 1. Classes and files

**Controllers**

- Class: `SingularNounController`
    
    - `UserController`, `PostController`, `OrderController`
        
- File: `UserController.php`, `PostController.php`
    
- Route resource name: plural snake_case
    
    - `users`, `posts`, `orders`
        

**Models**

- Class: `SingularStudlyCase`
    
    - `User`, `Post`, `OrderItem`
        
- Migration / table: `snake_case` and plural
    
    - `users`, `posts`, `order_items`
        

**Seeders**

- Class: `SingularNounSeeder` or `NounTableSeeder`
    
    - `UserSeeder`, `PostSeeder`, `UsersTableSeeder`
        
- File: `UserSeeder.php`, `PostSeeder.php`
    
    - All in `database/seeders/`.laravel+1
        

**Tasks / Jobs**

- Class: `StudlyCase` (verb‑focused)
    
    - `ProcessPayment`, `SendWelcomeEmail`, `SyncInventory`
        
- File: `ProcessPayment.php`, `SendWelcomeEmail.php`
    
    - In `app/Jobs/`.[laravolt](https://laravolt.dev/v6/naming-conventions)
        

**Helpers / Helpers files**

- Helper functions: `snake_case`
    
    - `format_date()`, `is_active()`, `full_name()`
        
- Helper file: `helpers.php` or `HelperNameHelpers.php`
    
    - Often in `app/Helpers/` and loaded via `composer.json` `files` section.laravel-news+1
        

---

## 2. Functions and variables

**Methods inside controllers / services**

- `camelCase`, verb‑first
    
    - `index()`, `store()`, `updateUser()`, `sendNotification()`
        
- Private methods: still `camelCase`
    
    - `validateRequest()`, `prepareData()`
        

**Variables**

- `camelCase` or `snake_case` depending on your style; Laravel itself uses `camelCase` in PHP.[laravolt](https://laravolt.dev/v6/naming-conventions)
    
    - `$user`, `$orderItems`, `$isActive`
        
- Avoid abbreviations unless obvious
    
    - Prefer `$user` over `$u`, `$orderItems` over `$oItems`
        

---

## 3. Database and migrations

- **Table names**: plural, `snake_case`
    
    - `users`, `posts`, `order_items`
        
- **Column names**: `snake_case`
    
    - `first_name`, `last_name`, `created_at`, `is_active`
        
- **Foreign keys**: singular model + `_id`
    
    - `user_id`, `post_id`
        
- **Pivot tables**: `table_a_table_b` (alphabetical or by role)
    
    - `role_user`, `permission_user`
        

Laravel’s default naming plays nicely with Eloquent (e.g., `App\Models\Post` → table `posts`).stackoverflow+2

---

## 4. Branch naming (Git)

Use a **type‑prefix + hyphenated** pattern, e.g.pullpanda+1

|Type|Example branch name|
|---|---|
|feature|`feature/user-authentication`|
|bugfix|`bugfix/login-validation`|
|hotfix|`hotfix/500-error-on-profile`|
|refactor|`refactor/posts-controller`|
|chore|`chore/add-code-sniffer-config`|
|docs|`docs/update-api-readme`|

Variations (depending on team): CamelCase (`FeatureUserAuth`) or dots (`feature.user-auth`) are also used, but the slash style above is very common in Laravel‑adjacent teams.dev+1

---

## 5. Folder / directory structure naming

- Everything `snake_case` or `StudlyCase` matching your namespace.reddit+1
    
    - `app/Http/Controllers/`
        
    - `app/Models/`
        
    - `app/Jobs/`
        
    - `app/Listeners/`
        
    - `app/Helpers/`
        
    - `database/seeders/`
        
    - `app/Support/` (for traits, interfaces, base services)
        
- Custom domains / modules (DDD‑style):
    
    - `app/Modules/Billing/Http/Controllers/`
        
    - `app/Modules/Billing/Models/Invoice.php`
        

---

## 6. Example quick table of naming patterns

|Concept|Class name (PHP)|File name|DB / route name|
|---|---|---|---|

|Concept|Class name (PHP)|File name|DB / route name|
|---|---|---|---|
|Resource model|`User`|`User.php`|`users`|
|Controller|`UserController`|`UserController.php`|`users`|
|Seeder|`UserSeeder`|`UserSeeder.php`|N/A|
|Job / task|`ProcessPayment`|`ProcessPayment.php`|N/A|
|Helper function|N/A|in `helpers.php`|N/A|
|Git branch|N/A|`feature/new-login`|N/A|

---

If you tell me which structure you’re using (standard Laravel, DDD, modules, etc.), I can give you a **ready‑to‑copy markdown table** you can paste into your own “Laravel Backend Naming Guide” doc and tweak per project.