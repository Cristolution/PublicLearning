# Eloquent Relationships in Laravel

Eloquent ORM provides powerful relationship handling between database tables.

---

## 1. One-to-One

```php
// User model
public function profile()
{
    return $this->hasOne(Profile::class);
}

// Profile model
public function user()
{
    return $this->belongsTo(User::class);
}

// Usage
$user = User::find(1);
$user->profile->bio;
```

---

## 2. One-to-Many

```php
// Post model
public function comments()
{
    return $this->hasMany(Comment::class);
}

// Comment model
public function post()
{
    return $this->belongsTo(Post::class);
}

// Usage
$post = Post::find(1);
$post->comments()->where('approved', true)->get();
```

---

## 3. Many-to-Many

```php
// User model
public function roles()
{
    return $this->belongsToMany(Role::class);
}

// Usage
$user->roles()->attach($roleId);
$user->roles()->detach($roleId);
$user->roles()->sync([1, 2, 3]);
```

---

## 4. HasMany Through

```php
// Country -> Posts -> Comments
public function comments()
{
    return $this->hasManyThrough(Comment::class, Post::class);
}
```

---

## 5. Polymorphic

```php
// Image model
public function imageable()
{
    return $this->morphTo();
}

// User, Post, Product can have images
public function images()
{
    return $this->morphMany(Image::class, 'imageable');
}

// Usage
$user->images()->create(['url' => 'photo.jpg']);
$post->images()->create(['url' => 'cover.jpg']);
```

---

## 6. Querying Relationships

```php
// Eager loading (avoid N+1 problem)
$users = User::with('profile')->get();

// Lazy eager loading
$users = User::all();
$users->load('profile');

// Check if relationship exists
$user->profile->exists;

// Relationship count
$post->comments_count;
```