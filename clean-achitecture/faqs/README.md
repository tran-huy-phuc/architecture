**- Is Clean Architecture only for large projects?**
> No! Clean Architecture benefits both small and large projects, but its **true power** is seen in complex applications that grow over time.

---

**Is Clean Architecture the same as MVVM, MVP, or MVC?**
> No! Those are UI-layer patterns, while Clean Architecture covers the entire application structure, including business logic and data management.

---

**What are the drawbacks of Clean Architecture?**
> • More code at the start → Due to multiple layers.

> • Steep learning curve → Especially for beginners.

> • May seem over-engineered → For small projects.

---

**What are the differences between "Enterprise Business Rules" (Entities) and "Application Business Rules" (Use Cases)?**
| Feature | **Enterprise Business Rules (Entities)** | **Application Business Rules (Use Cases)** |
|---------|------------------------------------|--------------------------------------|
| **Definition** | Core business rules that define domain models and concepts, independent of any specific application. | Application-specific logic that orchestrates how entities are used in workflows. |
| **Scope** | Broad, reusable across multiple applications. | Specific to a particular application’s workflows. |
| **Dependencies** | No external dependencies (e.g., APIs, databases, frameworks). | Can depend on **Entities**, but not on external frameworks or infrastructure. |
| **Change Frequency** | Changes **rarely**, as they represent fundamental business rules. | Changes **more frequently**, as they depend on specific application needs. |
| **Example 1: E-commerce App** | `Product` entity with `id`, `name`, `price`, `description`. | `CheckoutUseCase` that calculates total price, applies discounts, and processes payment. |
| **Example 2: Finance App** | `Transaction` entity with `amount`, `currency`, `date`, `type`. | `GenerateMonthlyReportUseCase` that aggregates transactions for reporting. |

---

**"Entities should be pure", does that mean we won't have any business logic inside entities?**

The idea that Entities should be pure doesn't mean they have zero business logic—it means they should have only **essential business rules related to themselves** and remain independent of external layers (like data sources or UI).

✅ What Kind of Logic Belongs in Entities?

Entities can contain domain-specific logic that defines their behavior. This logic should:

✔ Ensure data integrity (e.g., validation rules).

✔ Encapsulate essential business rules that don't depend on external services.

✔ Prevent invalid states by enforcing constraints.

✅ Good Example (Entity with Business Logic)

```dart
class Order {
  final List<OrderItem> items;
  final DateTime createdAt;

  Order(this.items, this.createdAt) {
    if (items.isEmpty) {
      throw ArgumentError('Order must have at least one item');
    }
  }

  double get totalPrice => items.fold(0, (sum, item) => sum + item.price);
}
```

📌 Why is this good?

✔ The Order entity enforces a rule that it must have at least one item.

✔ It calculates total price, which is an intrinsic behavior of an order.

✔ No dependencies on external services (like APIs or databases).

❌ Bad Example (Entity with External Dependencies)

```dart
class Order {
  final List<OrderItem> items;

  Order(this.items);

  Future<void> saveToDatabase(Database db) async {
    await db.insertOrder(this);
  }
}
```

🔴 Why is this bad?

✔ The entity now depends on a Database, breaking separation of concerns.

✔ If the database changes, the entity must change, making it harder to test and maintain.