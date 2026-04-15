# API Routes in Laravel

RESTful API routing with Laravel.

---

## 1. Basic API Routes

```php
// routes/api.php

Route::get('/users', 'UserController@index');
Route::post('/users', 'UserController@store');
Route::get('/users/{userId}', 'show');
Route::put('/users/{userId}', 'update');
Route::delete('/users/{userId}', 'destroy');
```

---

## 2. Resource Routes

```php
// API Resource (no create/edit views)
Route::apiResource('posts', 'PostController');

// Multiple resources
Route::apiResources([
    'posts' => 'PostController',
    'comments' => 'CommentController',
]);
```

---

## 3. API Controller

```bash
php artisan make:controller API/PostController --api
```

```php
class PostController extends Controller
{
    public function index()
    {
        return Post::all();
    }

    public function store(Request $request)
    {
        $post = Post::create($request->validated());
        return response()->json($post, 201);
    }

    public function show(Post $post)
    {
        return $post;
    }

    public function update(Request $request, Post $post)
    {
        $post->update($request->validated());
        return response()->json($post);
    }

    public function destroy(Post $post)
    {
        $post->delete();
        return response()->json(null, 204);
    }
}
```

---

## 4. Route Parameters & Validation

```php
Route::get('/posts/{post}/comments', 'PostController@comments');

Route::post('/posts', function (Request $request) {
    $request->validate([
        'title' => 'required|max:255',
        'body' => 'required',
        'author_id' => 'exists:users,id',
    ]);
});
```

important note: we can make the validation here or in the controller, but it is better to have a separate file to the validation(and authorization )as:
```php
php artisan make:request StorePostRequest
```

and the output will be as 
```php
<?php
namespace App\Http\Requests;

use Illuminate\Foundation\Http\FormRequest;
use App\Rules\ValidSlug;  // Your custom rule

class StorePostRequest extends FormRequest
{
    public function authorize(): bool  // Permission check
    {
        return auth()->check();  // Logged in only
    }

    public function rules(): array  // Validation
    {
        return [
            'title' => 'required|min:3|max:255',
            'slug' => ['required', new ValidSlug],  // Custom rule
            'content' => 'required|min:10',
        ];
    }

    public function messages(): array  // Custom error msgs
    {
        return [
            'title.required' => 'Post title is mandatory!',
        ];
    }
}
```

so in the controller
```php
public function store(StorePostRequest $request) { Post::create($request->validated() + [ 'slug' => generate_slug($request->title) // Your helper ]); return redirect()->route('posts.index'); }
```

---

## 5. API Authentication

### Using Laravel Sanctum

```php
// routes/api.php
Route::middleware('auth:sanctum')->group(function () {
    Route::get('/user', function (Request $request) {
        return $request->user();
    });
    
    Route::post('/logout', 'AuthController@logout');
});

// Login route
Route::post('/login', 'AuthController@login');
```

---

## 6. API Response Helpers

```php
// JSON responses
return response()->json(['data' => $posts], 200);
return response()->json(['message' => 'Created'], 201);
return response()->json(['error' => 'Not found'], 404);

// Resource collections
return PostResource::collection($posts);

// With Meta
return response()->json([
    'data' => $posts,
    'meta' => ['total' => 100]
]);
```

---

## 7. Rate Limiting

```php
// In RouteServiceProvider
protected function mapApiRoutes()
{
    Route::prefix('api')
        ->middleware('api')
        ->group(base_path('routes/api.php'));
}

// Using throttle
Route::middleware('throttle:60,1')->group(function () {
    // routes
});
```

---

## 8. API Versioning

```php
// routes/api.php
Route::prefix('v1')->group(function () {
    Route::get('/posts', 'V1\PostController@index');
});

Route::prefix('v2')->group(function () {
    Route::get('/posts', 'V2\PostController@index');
});
```