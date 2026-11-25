# PHP OOP User Management

A small **object-oriented PHP** user system that demonstrates core OOP features: abstract classes, interfaces, traits, namespaces, PSR-4-style autoloading and dependency injection.

![PHP](https://img.shields.io/badge/PHP-OOP-777BB4?logo=php&logoColor=white)

## Design

```
App\Core\AbstractUser      (abstract)  name, email, bcrypt-hashed password
App\Core\AuthInterface     (interface) login(), logout()
App\Core\LoggerTrait       (trait)     logActivity()
        │
        ├── App\Models\Admin        extends AbstractUser, implements AuthInterface, uses LoggerTrait
        └── App\Models\RegularUser  extends AbstractUser, implements AuthInterface

App\Services\AuthService   authenticate(AuthInterface $user, ...)  works with any user type
autoload.php               spl_autoload_register: maps namespaces to folders
```

| Concept | Where |
|---------|-------|
| Abstract class | `APP/Core/AbstractUser.php` |
| Interface | `APP/Core/AuthInterface.php` |
| Trait | `APP/Core/LoggerTrait.php` (used only by `Admin`) |
| Polymorphism / dependency injection | `APP/Services/AuthService.php` accepts any `AuthInterface` |
| Secure passwords | `password_hash()` and `password_verify()` |
| Autoloading | `autoload.php` |

## Run

```bash
php -S localhost:8000
```

Then open http://localhost:8000. `index.php` creates an `Admin` and a `RegularUser`, logs both in through `AuthService`, then logs the admin out, printing each result and the admin's activity log.
