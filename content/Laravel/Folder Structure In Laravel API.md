
```c
laravel-api/
├── artisan                              // CLI entry point for Artisan commands
├── composer.json                        // PHP dependencies and autoloading config
├── composer.lock                        // Locked Composer package versions
├── package.json                         // Node.js dependencies (optional for API docs)
├── phpunit.xml                          // PHPUnit testing configuration
├── README.md                            // API documentation and setup guide
├── .env                                 // Environment variables (DO NOT commit)
├── .env.example                         // Template for environment configuration
├── .gitignore                           // Files/folders to ignore in Git
├── .editorconfig                        // Ensures consistent coding styles across editors
│
├── app/
│   ├── Console/
│   │   ├── Kernel.php                   // Registers scheduled commands and Artisan console
│   │   └── Commands/GenerateApiDocs.php // // Custom command to generate OpenAPI/Swagger docs
│   │
│   ├── Exceptions/
│   │   ├── Handler.php                  // Global exception handling → JSON error responses
│   │   └── ApiException.php             // // Custom exception for API error standardization
│   │
│   ├── Http/
│   │   ├── Kernel.php                   // HTTP middleware pipeline (API groups: throttle, auth)
│   │   ├── Controllers/
│   │   │   ├── Controller.php           // Base API controller with JSON response helpers
│   │   │   ├── AuthController.php       // // Handles login/register/token refresh endpoints
│   │   │   ├── UserController.php       // // RESTful API controller for user resource CRUD
│   │   │   └── ApiResourceController.php// // Generic controller pattern for API resources
│   │   ├── Middleware/
│   │   │   ├── Authenticate.php         // // Validates API token via Sanctum/Passport
│   │   │   ├── EnsureApiKeyIsValid.php  // // Custom middleware for API key validation
│   │   │   ├── JsonResponse.php         // // Ensures all responses return proper JSON format
│   │   │   └── RateLimitByTier.php      // // Custom rate limiting based on user subscription
│   │   ├── Requests/
│   │   │   ├── StoreUserRequest.php     // // Validation rules for POST /api/users
│   │   │   ├── UpdateUserRequest.php    // // Validation rules for PUT/PATCH /api/users/{id}
│   │   │   └── LoginRequest.php         // // Validation for authentication endpoint
│   │   ├── Resources/
│   │   │   ├── UserResource.php         // // Transforms User model → JSON API response
│   │   │   ├── PostResource.php         // // Transforms Post model with relationships
│   │   │   └── Collection/UserCollection.php // // Paginated collection transformer
│   │   └── Traits/
│   │       └── RespondsWithJson.php     // // Reusable trait for standardized API responses
│   │
│   ├── Models/
│   │   ├── User.php                     // // Eloquent model with hidden fields for API
│   │   ├── Post.php                     // // Eloquent model with API-visible attributes
│   │   └── Traits/HasApiTokens.php      // // Trait for managing Sanctum/Passport tokens
│   │
│   ├── Providers/
│   │   ├── AppServiceProvider.php       // // Registers API-specific bindings/macros
│   │   ├── RouteServiceProvider.php     // // Configures API route model binding
│   │   └── SanctumServiceProvider.php   // // Laravel Sanctum API auth provider (if used)
│   │
│   ├── Policies/
│   │   └── PostPolicy.php               // // Authorization logic for API resource actions
│   │
│   ├── Events/
│   │   └── UserCreated.php              // // Event fired after API user registration
│   │
│   ├── Listeners/
│   │   └── SendWelcomeEmail.php         // // Sends email when UserCreated event fires
│   │
│   ├── Jobs/
│   │   ├── ProcessImageUpload.php       // // Queueable job for async image processing
│   │   └── SendNotificationJob.php      // // Queueable job for push/email notifications
│   │
│   ├── Mail/
│   │   └── ApiWelcomeMail.php           // // Mailable for new API user onboarding
│   │
│   ├── Notifications/
│   │   └── PasswordResetNotification.php// // Notification class for API password reset
│   │
│   ├── Rules/
│   │   ├── ValidJson.php                // // Custom rule to validate JSON string input
│   │   └── PhoneNumber.php              // // Custom rule for international phone validation
│   │
│   ├── Interfaces/
│   │   └── ApiResponseInterface.php     // // Contract for standardized API response format
│   │
│   ├── Services/
│   │   ├── AuthService.php              // // Business logic for authentication flows
│   │   ├── UserService.php              // // Business logic for user management
│   │   └── ApiService.php               // // Base service with common API helper methods
│   │
│   └── Repositories/
│       ├── BaseRepository.php           // // Generic repository pattern base class
│       └── UserRepository.php           // // Data access layer for User model queries
│
├── bootstrap/
│   ├── app.php                          // // Creates Laravel app instance and loads providers
│   ├── providers.php                    // // Registers service providers for bootstrapping
│   └── cache/.gitkeep                   // // Placeholder for framework cache files
│
├── config/
│   ├── app.php                          // // App name, env, debug, providers, aliases
│   ├── auth.php                         // // API guards: sanctum/passport configuration
│   ├── cache.php                        // // Cache drivers (redis preferred for API scale)
│   ├── database.php                     // // Database connections and read/write config
│   ├── filesystems.php                  // // Disk configs for file upload endpoints
│   ├── logging.php                      // // Log channels (monitor API errors/debug)
│   ├── mail.php                         // // Mail config for transactional API emails
│   ├── queue.php                        // // Queue config for async API job processing
│   ├── services.php                     // // Third-party API keys (Stripe, SendGrid, etc.)
│   ├── session.php                      // // Session config (usually 'array' for stateless API)
│   ├── cors.php                         // // CORS config for frontend/mobile client access
│   ├── hashing.php                      // // Bcrypt/Argon2id config for password hashing
│   ├── sanctum.php                      // // Sanctum token auth settings (expiration, etc.)
│   ├── l5-swagger.php                   // // OpenAPI/Swagger documentation config (if used)
│   └── api.php                          // // Custom API config: versioning, rate limits, etc.
│
├── database/
│   ├── migrations/
│   │   ├── 2024_01_01_000000_create_users_table.php  // // Creates 'users' table for API auth
│   │   ├── 2024_01_01_000001_create_personal_access_tokens_table.php // // Sanctum tokens table
│   │   └── 2024_01_01_000002_create_posts_table.php  // // Example resource table for API
│   ├── seeders/
│   │   ├── DatabaseSeeder.php           // // Master seeder for API test data
│   │   └── UserSeeder.php               // // Seeds admin/test users for API development
│   └── factories/
│       ├── UserFactory.php              // // Fake user data generation for API testing
│       └── PostFactory.php              // // Fake post data for API endpoint testing
│
├── public/
│   ├── index.php                        // // Front controller; bootstraps Laravel for HTTP API
│   ├── .htaccess                        // // Apache rewrites for clean API URLs
│   ├── robots.txt                       // // Block crawlers from API endpoints
│   └── storage → ../storage/app/public  // // Symlink for publicly accessible file uploads
│
├── resources/
│   ├── lang/
│   │   ├── en/messages.php              // // English API response messages
│   │   ├── en/validation.php            // // English API validation error messages
│   │   └── es/messages.php              // // Spanish translations for multi-lang API
│   └── views/vendor/notifications/
│       └── email.blade.php              // // Blade template for transactional API emails
│
├── routes/
│   ├── api.php                          // // API routes with 'api' middleware group (stateless)
│   ├── console.php                      // // Registers custom Artisan commands for API tasks
│   └── channels.php                     // // Broadcast channel auth for API WebSocket events
│
├── storage/
│   ├── app/
│   │   ├── public/uploads/              // // Publicly accessible user file uploads via API
│   │   ├── private/exports/             // // Private generated files (CSV/PDF exports)
│   │   └── .gitkeep                     // // Placeholder to keep folder in Git
│   ├── framework/
│   │   ├── cache/                       // // Cached API responses/routes for performance
│   │   ├── sessions/                    // // Session storage (minimal use in stateless API)
│   │   └── views/                       // // Compiled email/notification Blade templates
│   ├── logs/
│   │   └── laravel.log                  // // API request logs, errors, debug info
│   └── .gitkeep                         // // Ensures storage directory is tracked in Git
│
├── tests/
│   ├── TestCase.php                     // // Base test class with API testing helpers
│   ├── Feature/
│   │   ├── AuthTest.php                 // // Tests login/register/token refresh endpoints
│   │   ├── UserApiTest.php              // // Tests CRUD operations on /api/users endpoint
│   │   └── RateLimitTest.php            // // Tests API throttling and rate limit headers
│   └── Unit/
│       ├── UserServiceTest.php          // // Tests business logic in isolation
│       └── UserResourceTest.php         // // Tests JSON transformation output structure
│
└── vendor/                              // // Composer dependencies (AUTO-GENERATED - DO NOT EDIT)
    ├── autoload.php                     // // Composer autoloader for PSR-4 class loading
    ├── laravel/sanctum/                 // // Laravel Sanctum API token authentication
    ├── laravel/framework/               // // Core Laravel framework source code
    └── ...                              // // All installed PHP packages
```


|#|File/Component|When It Runs|What It Does|
|---|---|---|---|
|1|`public/index.php`|**First**|Web server routes request here. Bootstraps Laravel, loads `bootstrap/app.php`.|
|2|`bootstrap/app.php`|**Second**|Creates `$app` instance, registers service providers, sets exception handler.|
|3|`app/Http/Kernel.php`|**Third**|Defines middleware stack, maps route groups (`api`), builds the execution pipeline.|
|4|Global Middleware|**Before Route**|Runs automatically on every request: `TrimStrings`, `TrustProxies`, `PreventRequestsDuringMaintenance`.|
|5|`routes/api.php`|**After Global MW**|Matches URI → controller/method. Resolves route parameters & model binding (`{id}` → `User::findOrFail()`).|
|6|Route Middleware|**Before Controller**|Executes attached middleware: `throttle:60,1`, `auth:sanctum`, custom `EnsureApiKeyIsValid`.|
|7|Form Request|**Auto-resolved by DI**|Laravel instantiates `StoreXxxRequest`. Runs `authorize()` → if `true`, runs `rules()`. **Fails → returns 422 JSON immediately.**|
|8|Controller|**After Validation**|Receives validated request. **Never contains business logic**. Calls Service layer.|
|9|Service|**Inside Controller**|Handles business rules, transactions, external API calls, complex calculations.|
|10|Repository / Model|**Inside Service**|Executes DB queries via Eloquent. Returns collection/model instances.|
|11|API Resource|**Before Response**|`XxxResource::collection($data)` or `new XxxResource($model)`. Calls `toArray()` to shape JSON.|
|12|Response|**Final Output**|Laravel serializes Resource → JSON, sets headers (`application/json`), sends to client.|
|13|Post-Response|**After Response Sent**|`TerminateMiddleware` runs, dispatched `Events` fire, `Queued Jobs` pushed, logs written.|