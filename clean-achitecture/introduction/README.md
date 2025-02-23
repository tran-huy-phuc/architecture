![Clean Architecture](https://github.com/tran-huy-phuc/architecture/blob/main/clean-achitecture/introduction/images/clean-architecture.png)

## 1. What is Clean Architecture?

Clean Architecture, proposed by Robert C. Martin (Uncle Bob), is a software design pattern that organizes code into separate, independent layers. It focuses on **separation of concerns**, making the codebase **maintainable, scalable, and testable**.

## 2. The Layers of Clean Architecture

Clean Architecture follows a **layered, circular dependency rule: inner layers should not depend on outer layers**.

## 📌 Core Layers (From Inner to Outer)

1️⃣ **Entities (Enterprise Business Rules)**

• Represents core business logic and domain models.

• Independent of frameworks and databases.

• Example: User, Order, Product classes in an e-commerce app.

---

2️⃣ **Use Cases (Application Business Rules)**

• Contains application-specific logic.

• Implements business rules using entities.

• Calls repositories to retrieve or update data.

• Example: ProcessPaymentUseCase, AuthenticateUserUseCase.

---

3️⃣ **Interface Adapters (Presentation & Data Layer)**

• Adapts data between domain and external sources (UI, APIs, Databases).

• Repositories act as an interface between use cases and data sources.

• Example:

    + State Management (BloC, Provider, Riverpod, etc.)
    + Repositories (Data Fetching Layer)
    + DTOs (Data Transfer Objects) for APIs

---

4️⃣ **Frameworks & Drivers (Infrastructure Layer)**

• External systems like APIs, Databases, UI frameworks, Cloud Services.

• Should be replaceable without affecting business logic.

• Example:

    + Firebase, REST APIs, GraphQL
    + Flutter Widgets, HTTP clients, SQLite databases

## 3. Pros and Cons of Clean Architecture

✅ Pros (Why Use It?)

    ✔ Separation of Concerns: Makes the code modular and easier to maintain.

    ✔ Testability: Business logic can be tested independently of UI and external services.

    ✔ Scalability & Flexibility: Easy to replace UI frameworks, databases, or APIs without affecting core business logic.

    ✔ Better Collaboration: Teams can work independently on different layers.

❌ Cons (Challenges & Criticism)

    ✔ Over-Engineering: For small projects, it introduces unnecessary complexity.

    ✔ Too Many Files: Simple tasks require multiple files (UseCase, Repository, DataSource, DTO, etc.).

    ✔ Harder Onboarding: New developers may struggle to understand all the abstractions.

    ✔ More Boilerplate Code: Requires extra code for layers and dependency injection.

## 4. When Should You Use Clean Architecture?

✅ Recommended for:

	✔ Large & complex applications (e.g., enterprise apps, e-commerce platforms).
	✔ Long-term projects that require maintainability.
	✔ Apps with multiple data sources and business logic rules.

❌ Not necessary for:

	✔ Small apps with simple logic.
	✔ Quick MVPs where speed is more important than structure.