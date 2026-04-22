### 1. Service / Action Classes
**What**: Plain PHP classes that hold business logic outside of controllers or models.  
**Why**: Keeps controllers thin, logic reusable, and easy to test.  
**Example**:
```php
// app/Actions/PlaceOrderAction.php
class PlaceOrderAction
{
    public function __invoke(CreateOrderDTO $data): Order
    {
        DB::transaction(function () use ($data) {
            $order = Order::create($data->toArray());
            $order->items()->createMany($data->items);
            PaymentProcessor::charge($data->paymentToken, $order->total);
        });
        return $order;
    }
}
```
**Controller**: `return (new PlaceOrderAction)($request->toDTO());`  
**Tip**: Think of controllers as *traffic cops* and actions/services as the *workers* doing the actual job.

---

### 2. DTO / Value Object
**DTO (Data Transfer Object)**: A simple, typed container to move data between layers. No business logic.  
**Value Object**: Represents a meaningful domain value (e.g., `Money`, `Email`). Usually immutable and validates itself.

**Example (DTO)**:
```php
readonly class CreateOrderDTO
{
    public function __construct(
        public string $customerId,
        public array $items,
        public string $paymentToken
    ) {}
    
    public function toArray(): array
    {
        return ['customer_id' => $this->customerId, ...];
    }
}
```
**Why**: Stops you from passing raw `request->all()` arrays around. Makes contracts explicit and IDE-friendly.  
**Tip**: In Laravel 10/11, `readonly` classes or `spatie/laravel-data` make this trivial.

---

### 3. Policies / Auth
**What**: Classes that define *who* can do *what* on a resource.  
**Why**: Centralizes authorization, keeps controllers clean.  
**Example**:
```php
// app/Policies/PostPolicy.php
class PostPolicy
{
    public function update(User $user, Post $post): bool
    {
        return $user->id === $post->user_id;
    }
}
```
**Usage**: `$user->can('update', $post)` or `@can('update', $post)` in Blade.  
**Tip**: Laravel auto-discovers policies if named `XxxPolicy` and registered via `Gate` or `AuthServiceProvider`.

---

### 4. Form Request
**What**: A specialized `Request` class that handles validation + authorization.  
**Why**: Removes validation from controllers, auto-redirects with errors, reusable across routes.  
**Example**:
```php
class StorePostRequest extends FormRequest
{
    public function authorize(): bool { return auth()->check(); }
    public function rules(): array { return ['title' => 'required|string|max:255']; }
}
```
**Controller**: `public function store(StorePostRequest $request)` → Laravel auto-validates before hitting the method.

---

### 5. `scopeInStock`
**What**: A **local query scope** on an Eloquent model.  
**Why**: Reuse common query fragments without repeating `where()` clauses.  
**Example**:
```php
class Product extends Model
{
    public function scopeInStock($query)
    {
        return $query->where('quantity', '>', 0);
    }
}
```
**Usage**: `Product::inStock()->get();`  
**Tip**: The `scope` prefix is mandatory in the definition, but you call it without `scope`.

---

### 6. Triple A Test (Arrange-Act-Assert)
**What**: A testing pattern to structure tests clearly.  
**Why**: Makes tests readable, debuggable, and consistent.  
**Laravel Example**:
```php
test('creates order for authenticated user', function () {
    // Arrange
    $user = User::factory()->create();
    $dto = new CreateOrderDTO($user->id, [[...]], 'tok_visa');

    // Act
    $order = (new PlaceOrderAction)($dto);

    // Assert
    expect($order)->toBeInstanceOf(Order::class)
        ->and($order->customer_id)->toBe($user->id)
        ->and(PaymentProcessor::fake()->charged())->toBeTrue();
});
```
**Tip**: Works with PHPUnit or Pest. Keep each phase separate; never mix setup with assertions.

---

### 7. Repository Pattern
**What**: A layer between your app and the database that abstracts data access.  
**Why**: Decouples business logic from Eloquent, easier to swap data sources or mock in tests.  
**Example**:
```php
interface ProductRepository { public function inStock(): Collection; }
class EloquentProductRepository implements ProductRepository {
    public function inStock(): Collection { return Product::inStock()->get(); }
}
```
**⚠️ Laravel Reality**: Eloquent *already* acts like a repository. The community often considers this pattern overkill unless you genuinely need to abstract the data layer (e.g., switching from MySQL to an API). Start with Eloquent + scopes + services. Add repositories only when you feel the pain.

---

### 8. Code Smells
**What**: Signs that code is hard to maintain (not bugs, but red flags).  
**Common Laravel Smells**:
- 🚩 **Fat Controller**: 100+ lines mixing validation, DB calls, emails, payments
- 🚩 **God Model**: `User` handles auth, billing, notifications, reporting
- 🚩 **Array Soup**: Passing `request->all()` or `['status' => 'active']` everywhere
- 🚩 **Duplicated Validation**: Same rules in 3 controllers
- 🚩 **Hardcoded Logic**: `if ($request->user()->role == 'admin')` scattered everywhere

**Fixes**: Form Requests, Policies, Action Classes, DTOs, Scopes, Service containers.

---

### 🔗 How They Fit Together (Real Flow)
```
HTTP Request 
   → FormRequest (validate + authorize)
   → Controller (thin, routes to action)
   → Action/Service (business logic, uses DTO)
   → Model/Scope (data access)
   → Policy (resource-level auth checks)
   → Test (AAA structure)
```
You don’t need to use all of these tomorrow. Pick **one** (e.g., Form Requests), master it, then layer the next.

---
