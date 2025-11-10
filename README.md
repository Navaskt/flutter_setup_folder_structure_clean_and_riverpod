# Flutter Clean Architecture + Riverpod Boilerplate

Welcome! This project serves as a robust and scalable boilerplate for Flutter applications, built upon the principles of **Clean Architecture** and using **Riverpod** for state management.

The goal is to provide a clear and maintainable structure that separates concerns, making the codebase easy to test, maintain, and scale.

---

## 🚀 Getting Started

To get a local copy up and running, follow these simple steps.

### Prerequisites

-   [Flutter SDK](https://flutter.dev/docs/get-started/install) (latest stable version recommended)
-   An editor like [VS Code](https://code.visualstudio.com/) or [Android Studio](https://developer.android.com/studio)

### Installation

1.  **Clone the repo:**
    ```sh
    git clone https://github.com/your-username/your-repository-name.git
    ```
2.  **Navigate to the project directory:**
    ```sh
    cd your-repository-name
    ```
3.  **Install dependencies:**
    ```sh
    flutter pub get
    ```
4.  **Run the app:**
    ```sh
    flutter run
    ```

---

## 📂 Automated Folder Structure

This project includes a powerful shell script to automate the creation of the folder structure for new features. This ensures consistency and saves time.

### How to Use the Script

1.  **Make the script executable** (you only need to do this once):
    ```sh
    chmod +x create_clean_riverpod_structure.sh
    ```

2.  **Create a single feature:**
    The script will create all the necessary directories for a new feature under `lib/features/`.
    ```sh
    ./create_clean_riverpod_structure.sh your_feature_name
    ```
    *Example:*
    ```sh
    ./create_clean_riverpod_structure.sh login
    ```

3.  **Create multiple features at once:**
    You can generate structures for multiple features by separating their names with spaces.
    ```sh
    ./create_clean_riverpod_structure.sh login home profile
    ```

---

## 🏛️ Architecture Overview

This project follows the principles of **Clean Architecture**, which divides the app into three main layers: **Data**, **Domain**, and **Presentation**. The code is organized by feature, promoting modularity and separation of concerns.

```
lib
├── core/            # Shared code, services, and utilities
│   ├── config/      # App-wide configurations (e.g., themes)
│   ├── services/    # Core services (e.g., Dio client, logger)
│   ├── utils/       # Utility functions and constants
│   └── widgets/     # Shared widgets used across multiple features
│
├── features/        # Each feature is a self-contained module
│   └── your_feature_name/
│       ├── data/
│       │   ├── datasources/ # Handles data retrieval (API, local DB)
│       │   ├── models/      # Data Transfer Objects (DTOs), extends Domain Entities
│       │   └── repositories/ # Implements Domain Repositories
│       │
│       ├── domain/
│       │   ├── entities/    # Core business objects (plain Dart objects)
│       │   ├── repositories/ # Abstract contracts for data layers
│       │   └── usecases/    # Business logic, orchestrates data flow
│       │
│       └── presentation/
│           ├── providers/   # Riverpod providers for state management
│           ├── screens/     # UI screens/pages
│           └── widgets/     # Feature-specific widgets
│
├── routes/          # GoRouter or other navigation setup
└── main.dart        # App entry point
```

### Layers Explained

1.  **Domain Layer**
    -   **What it is:** The innermost layer. It contains the core business logic and rules of the application.
    -   **Key Rule:** It is completely independent of any other layer. It doesn't know anything about the UI or where the data comes from.
    -   `entities`: Plain Dart objects representing your core business models.
    -   `repositories`: Abstract classes that define the contract for what the data layer must do (e.g., `abstract class UserRepository { Future<User> getUser(String id); }`).
    -   `usecases`: These classes orchestrate the flow of data to and from the UI by calling the repositories.

2.  **Data Layer**
    -   **What it is:** This layer is responsible for fetching data—from a remote API, a local database, or any other source.
    -   **Key Rule:** It implements the repository contracts defined in the domain layer.
    -   `models`: Data Transfer Objects (DTOs) that are often generated from JSON. They can be converted to and from domain `entities`.
    -   `datasources`: The classes that actually make the network requests or database calls (e.g., using `http` or `Dio`).
    -   `repositories`: Concrete implementations of the abstract repositories from the domain layer.

3.  **Presentation Layer**
    -   **What it is:** The outermost layer, responsible for everything the user sees and interacts with.
    -   **Key Rule:** It depends on the domain layer to get data and execute business logic.
    -   `screens`: The pages of your application.
    -   `widgets`: UI components specific to a feature.
    -   `providers`: **Riverpod providers** that manage the state of the UI. They call usecases from the domain layer and expose the state to the UI.

---

## ✨ State Management with Riverpod

This boilerplate uses **Riverpod** for state management due to its compile-safe, simple, and powerful approach.

-   **Providers** are located in `lib/features/your_feature/presentation/providers/`.
-   Keep UI widgets "dumb"—their only job is to display state and forward user events to the providers.
-   Providers call usecases to trigger business logic and update their state, causing the UI to rebuild.

---

##🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](https://github.com/your-username/your-repository-name/issues).

---

## License

This project is licensed under the MIT License - see the `LICENSE` file for details.

---
_This README was generated by GitHub Copilot._