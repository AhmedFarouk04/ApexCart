# ApexCart - README

## Overview

This is a full-featured **E-Commerce web application** built with **ASP.NET Core MVC (.NET 8)** using a clean, layered architecture (Clean Architecture / Onion Architecture principles).  

The project implements core e-commerce functionalities including product browsing, cart management (guest + authenticated), wishlist, ratings & reviews, secure checkout with **Stripe** payments, user authentication with email verification, and a complete **Admin Dashboard** for managing products, categories, orders, users, ratings, reviews, wishlists, and admin activity logs.

**Repository**: https://github.com/AhmedFarouk04/Ecommerce-aspnet-mvc

## Key Features

### Customer Features
- **Product Catalog** with advanced search, filtering (category, price range, rating, stock), sorting, and autocomplete suggestions.
- **Guest & Authenticated Cart** – Session-based for guests, database-backed for logged-in users with automatic merge on login.
- **Wishlist** – Add/remove products with real-time heart icon toggle.
- **Ratings & Reviews** – Users can rate (1-5 stars) and write reviews per product.
- **Secure Checkout** – Shipping address collection and Stripe payment integration.
- **Order History** – View orders, details, edit address (before payment), cancel unpaid orders.
- **User Profile** – Update username, email (with verification), profile picture, change password.
- **Email Verification** – OTP-based for registration and email changes.
- **Forgot/Reset Password** – Token-based reset flow.
- **Brute-force Protection** – IP-based login attempt limiting with temporary blocks.

### Admin Features
- **Dashboard** – Overview of total products, categories, users, stock value, latest products, and category stats.
- **Product Management** – Create, edit, delete products with image upload (watermark + thumbnail generation).
- **Category Management** – CRUD operations (cannot delete categories with products).
- **Order Management** – View all orders with filtering/sorting, change order status.
- **User Management** – List, search, promote/demote admins, suspend/restore, delete users.
- **Ratings & Reviews Management** – View and delete user ratings/reviews.
- **Wishlist Management** – View and remove wishlist items across users.
- **Admin Activity Logging** – All admin actions are logged with timestamp and details.

### Technical Highlights
- **Clean Architecture** – Separation into layers:
  - `ECommerce.Web` (MVC UI)
  - `ECommerce.Application` (Services, DTOs, Interfaces, AutoMapper profiles)
  - `ECommerce.Core` (Entities, Enums, Repository interfaces)
  - `ECommerce.Infrastructure` (EF Core DbContext, Repositories, Identity)
- **Repository + Unit of Work Pattern** – Full control over transactions and data access.
- **Dependency Injection** – All services/repositories registered in `Program.cs`.
- **AutoMapper** – Mapping between Entities ↔ DTOs ↔ ViewModels.
- **Image Processing** – Using **ImageSharp**: automatic watermark, thumbnail generation, quality compression.
- **AJAX Cart & Wishlist** – Real-time updates without page refresh (add/remove/update quantity).
- **Responsive & Modern UI** – Custom CSS with CSS variables, Bootstrap-inspired components, skeleton loaders.
- **Security** – Identity with roles (Admin/Customer), anti-forgery, login security service, email confirmation.
- **Stripe Integration** – Checkout Session + webhook handling for payment confirmation and stock deduction.

## Tech Stack

- **Backend**: ASP.NET Core 8 MVC
- **Database**: SQL Server (Entity Framework Core Code-First)
- **ORM**: Entity Framework Core
- **Identity**: ASP.NET Core Identity (custom ApplicationUser)
- **Payments**: Stripe (Checkout Session + Webhooks)
- **Image Processing**: SixLabors.ImageSharp
- **Caching**: MemoryCache (for login security & optional product caching)
- **Email**: SMTP (configurable in appsettings)
- **Frontend**: Razor Views, vanilla JS + jQuery (minimal), Bootstrap-like custom CSS
- **Validation**: Data Annotations + custom attributes (MaxFileSize, AllowedExtensions)

## Project Structure

```
ECommerceSolution/
├── ECommerce.Web/                  # MVC Project (Controllers, Views, wwwroot)
├── ECommerce.Application/          # Services, DTOs, Interfaces, AutoMapper
├── ECommerce.Core/                 # Entities, Enums, Repository Interfaces
├── ECommerce.Infrastructure/       # DbContext, Repositories, Identity
└── README.md
```

## Setup & Running Locally

### Prerequisites
- .NET 8 SDK
- SQL Server (LocalDB or full instance)
- Stripe account (for payment testing – use test keys)
- SMTP credentials for email (or use Ethereal/Mailtrap for testing)

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/AhmedFarouk04/ECommerceSolution.git
   cd ECommerceSolution
   ```

2. **Update connection string** in `appsettings.json` or `appsettings.Development.json`
   ```json
   "ConnectionStrings": {
     "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=ECommerceDb;Trusted_Connection=true;MultipleActiveResultSets=true"
   }
   ```

3. **Add migrations & update database**
   ```bash
   dotnet ef migrations add InitialCreate --project ECommerce.Web
   dotnet ef database update --project ECommerce.Web
   ```

4. **Configure Stripe keys** in `appsettings.json`
   ```json
   "Stripe": {
     "PublishableKey": "pk_test_...",
     "SecretKey": "sk_test_...",
     "WebhookSecret": "whsec_..."
   }
   ```

5. **Configure Email settings** (optional for development)
   ```json
   "EmailSettings": {
     "From": "your@email.com",
     "Password": "xxx",
     "Host": "smtp.gmail.com",
     "Port": "587"
   }
   ```

6. **Run the application**
   ```bash
   dotnet run --project ECommerce.Web
   ```

7. **Default accounts**
   - Register a new user → automatically becomes **Customer**
   - To create first Admin: after registration, manually add "Admin" role via database or use the admin panel once you promote a user.



## Contributing

Feel free to fork and submit pull requests. Major features should be discussed first via issues.

## License

MIT License – feel free to use and modify for personal or commercial projects.

---

**Built with ❤️ using ASP.NET Core 8**  
Happy coding! 🚀
