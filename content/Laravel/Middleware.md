# Middleware in Laravel

Middleware provides a way to filter HTTP requests entering your application.

---

## 1. Creating Middleware

```bash
php artisan make:middleware CheckAge
```

```php
// app/Http/Middleware/CheckAge.php
public function handle($request, Closure $next)
{
    if ($request->age < 18) {
        return redirect('/home');
    }
    return $next($request);
}
```

---

## 2. Registering Middleware

### Global Middleware (Kernel.php)
```php
// app/Http/Kernel.php
protected $middleware = [
    \Illuminate\Foundation\Http\Middleware\CheckForMaintenanceMode::class,
    \App\Http\Middleware\TrustProxies::class,
];
```

### Route Middleware
```php
// Register in Kernel.php
protected $routeMiddleware = [
    'auth' => \Illuminate\Auth\Middleware\Authenticate::class,
    'admin' => \App\Http\Middleware\AdminMiddleware::class,
    'age' => \App\Http\Middleware\CheckAge::class,
];
```

---

## 3. Using Middleware

### In Routes
```php
// Single middleware
Route::get('/profile', 'UserController@show')->middleware('auth');

// Multiple middleware
Route::get('/admin', 'AdminController@index')->middleware(['auth', 'admin']);

// Except / only
Route::group(['middleware' => ['auth']], function () {
    Route::get('/dashboard', function () {});
});
```

### In Controller
```php
public function __construct()
{
    $this->middleware('auth')->except('index');
    $this->middleware('admin')->only('destroy');
}
```

---

## 4. Middleware Parameters

```php
// Define parameter
public function handle($request, Closure $next, $role)
{
    if (!$request->user()->hasRole($role)) {
        abort(403);
    }
    return $next($request);
}

// Usage
Route::put('/post/{id}', 'PostController@update')->middleware('role:admin');
```

---

## 5. Middleware Groups

```php
// In Kernel.php
protected $middlewareGroups = [
    'web' => [
        \Illuminate\Cookie\Middleware\EncryptCookies::class,
        \Illuminate\Session\Middleware\StartSession::class,
        // ...
    ],
    'api' => [
        'throttle:60,1',
        'auth:api',
    ],
];

// Usage
Route::group(['middleware' => ['web']], function () {
    // Routes
});
```