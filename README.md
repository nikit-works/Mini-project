# 🥗 Healthy Diet Website Recommendation

> **Full-Stack Personalized Nutrition, Diet Recommendation & 7-Day Meal Planning Platform**  
> Built with **PHP 8.2+**, **MySQL 8.0+**, **PDO**, **Bootstrap 5.3**, **Chart.js**, and **Vanilla CSS Design System**.

---

## 🌟 Project Overview

**HealthyDiet** is a production-quality full-stack web application designed to help users discover personalized healthy diets, scientific calorie targets, and tailored meal plans based on their unique biological metrics and dietary preferences.

The application calculates Body Mass Index (BMI), Basal Metabolic Rate (BMR), and Total Daily Energy Expenditure (TDEE) using the clinical **Mifflin-St Jeor equation**, and filters an extensive repository of healthy recipes using an intelligent multi-factor recommendation engine.

---

## ✨ Key Features

### 🌐 Public & User Experience
* **Hero Landing Page**: Live BMI & Calorie calculator preview, featured chef-developed dishes, dietary categories, benefits, and client testimonials.
* **Evidence-Based Health Assessment**: Questionnaire capturing Age, Biological Gender, Height (cm), Weight (kg), Physical Activity frequency, Primary Goals, Dietary boundaries (Vegetarian, Vegan, Non-Veg, Eggetarian, Pescatarian), and strict Food Allergens (Peanuts, Dairy, Gluten, Shellfish, Tree Nuts, Soy).
* **Scientific Recommendation Engine**: Rule-based scoring algorithm balancing macronutrient density, caloric proximity, and goal alignment, with **zero tolerance for allergen conflicts** and **dynamic explanation badges** (`✓ Matches Vegetarian`, `✓ High Protein`, `✓ 100% Peanuts-Free`).
* **7-Day Interactive Meal Planner**: Monday to Sunday visual calendar supporting Breakfast, Lunch, Dinner, and Snack slots with live daily calorie meters and a **1-Click Auto-Planner** that auto-populates a balanced week.
* **Weight & BMI Progress Tracker**: Interactive Chart.js timeline showing weigh-in trends over time with history table and metrics.
* **Favorites & Food Catalog**: Instant AJAX bookmarking, live search debouncing, category pills, calorie sliders, and macro filters.
* **Detailed Recipe Pages**: Ingredients checklists, step-by-step cooking instructions, macro progress meters, and allergen warnings.
* **Medical Disclaimer**: Visible, transparent nutritional disclaimer across all user pages.

### 🛡️ Admin Control Suite (`/admin/`)
* **Executive Dashboard**: Real-time KPI cards (Total Users, Meals, Categories, Favorites, Inquiries), User Demographics chart, and Fitness Goals distribution graph.
* **User Management CRUD**: View health profiles, edit roles, toggle account status (Active, Inactive, Banned), reset passwords, and delete users.
* **Healthy Meals CRUD**: Full recipe creation with image uploading, category assignment, macro breakdowns, ingredients, instructions, tags, and featured dish toggling.
* **Meal Categories Management**: Create, edit, and delete recipe categories with FontAwesome icons.
* **Diet Plans Oversight**: Monitor active user weekly meal plans and caloric totals.
* **Inquiries Inbox**: Manage contact submissions with Read/Replied status workflows and quick email responses.
* **Analytics & CSV Reports**: Export meals and user demographic datasets to CSV.
* **System Settings**: Application title, support email, calorie buffer percentages, and maintenance mode controls.

---

## 🔒 Security & Architecture

* **Zero SQL Injection**: 100% PDO prepared statements with parameter binding and emulation disabled.
* **Cross-Site Scripting (XSS) Prevention**: All dynamic output escaped using `htmlspecialchars(..., ENT_QUOTES, 'UTF-8')`.
* **CSRF Protection**: Unique cryptographic tokens generated per session and validated on all POST operations.
* **Session Security**: Cookie `HttpOnly`, `SameSite=Lax`, and `session_regenerate_id(true)` upon authentication to defeat session fixation.
* **Password Hashing**: Industry-standard `password_hash($pass, PASSWORD_BCRYPT)` and `password_verify()`.
* **Role-Based Access Control (RBAC)**: Strict server-side verification guards preventing non-admin access to `/admin/`.

---

## 🗄️ Database Architecture

The application uses **MySQL 8.0+** with 11 relational tables:
1. `users` — Authentication credentials, roles, statuses, and avatars.
2. `user_profiles` — Biometric metrics, calculated BMI, TDEE calorie target, macros, dietary framework, and allergens.
3. `meal_categories` — Recipe category taxonomy and icons.
4. `meals` — 25+ seed recipes with exact calories, protein, carbs, fat, fiber, ingredients, instructions, allergens, and tags.
5. `favorites` — User-to-meal bookmark relationships.
6. `meal_plans` — User weekly meal plan containers.
7. `meal_plan_items` — Day-of-week and meal slot scheduled recipes.
8. `progress_logs` — Date-stamped body weight and BMI tracking logs.
9. `contact_messages` — Inquiries and feedback records.
10. `admin_logs` — Administrative action audit logs with IP tracking.
11. `system_settings` — Platform configuration key-value storage.

---

## 🚀 Quick Setup & Installation

### Option 1: Running with PHP Built-In Server (Recommended for local dev)

1. **Clone or navigate to the project directory**:
   ```bash
   cd "d:\my project php"
   ```

2. **Configure Environment (`.env`)**:
   Ensure `.env` exists with your MySQL database credentials:
   ```ini
   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_NAME=healthy_diet_db
   DB_USER=root
   DB_PASS=root
   ```

3. **Initialize Database and Seed Data**:
   Run the 1-click database setup migration script:
   ```bash
   php database/setup.php
   ```
   *(Creates all 11 tables and inserts 25+ healthy recipes, meal categories, and sample accounts).*

4. **Start PHP Local Development Server**:
   ```bash
   php -S localhost:8000
   ```

5. **Open in your web browser**:
   Navigate to: [http://localhost:8000](http://localhost:8000)

---

### Option 2: Running with XAMPP (Apache + MySQL)

1. **Copy the project folder** into your XAMPP `htdocs` directory:
   ```text
   C:\xampp\htdocs\healthy-diet
   ```

2. **Start Apache and MySQL** from the XAMPP Control Panel.

3. **Import Database**:
   - Open [http://localhost/phpmyadmin](http://localhost/phpmyadmin)
   - Create a new database named `healthy_diet_db`
   - Import `database/database.sql`
   - *OR* simply visit [http://localhost/healthy-diet/database/setup.php](http://localhost/healthy-diet/database/setup.php) in your browser.

4. **Verify Database Credentials**:
   Open `.env` in `C:\xampp\htdocs\healthy-diet\.env` and adjust `DB_USER=root` and `DB_PASS=""` if XAMPP root has no password.

5. **Access Application**:
   Open [http://localhost/healthy-diet/](http://localhost/healthy-diet/)

---

## 🔑 Demo Login Accounts

| Role | Email | Password | Profile Summary |
|---|---|---|---|
| **Administrator** | `admin@healthydiet.com` | `Admin@123` | Full admin control, CRUD suite, reports & settings |
| **User (Sample 1)** | `emily@healthydiet.com` | `User@123` | 28yo Female, Vegetarian, Weight Loss goal, Peanuts-free |
| **User (Sample 2)** | `marcus@healthydiet.com` | `User@123` | 26yo Male, Non-Vegetarian, Muscle Gain goal, Shellfish-free |

*New users can also register freely on the `/register.php` page.*

---

## 📁 Project Structure

```text
healthy-diet/
├── .env                       # Active Environment Configuration
├── .env.example               # Template Configuration
├── README.md                  # Complete System Documentation
│
├── index.php                  # Landing Page with Hero, CTA, Preview, Testimonials
├── about.php                  # Nutritional Science & Algorithm Explanation
├── contact.php                # Inquiries Form (Saves to MySQL)
├── login.php                  # User & Admin Authentication
├── register.php               # User Registration & Profile Initialization
├── logout.php                 # Secure Session Destruction
│
├── dashboard.php              # User Dashboard (BMI, Calories, Today's Plan, Recs)
├── health-assessment.php      # Health Questionnaire & Live Calibration
├── recommendations.php        # Personalized Recommendation Engine & Filters
├── meals.php                  # Searchable Food Catalog & Pagination
├── meal-details.php           # Deep Recipe Details, Ingredients & Macros
├── meal-plan.php              # 7-Day Interactive Meal Planner & Auto-Generator
├── favorites.php              # Saved Favorite Meals
├── progress.php               # Weight & BMI Progress Tracker (Chart.js)
├── profile.php                # Account Settings & Password Update
│
├── 404.php                    # Not Found Error Page
├── 403.php                    # Forbidden Error Page
├── 500.php                    # Internal Server Error Page
│
├── admin/
│   ├── index.php              # Executive KPI Dashboard & Demographics Charts
│   ├── users.php              # User Management CRUD & Health Assessment Inspector
│   ├── meals.php              # Recipe CRUD with Image Upload & Macro Editor
│   ├── categories.php         # Meal Categories CRUD
│   ├── diet-plans.php         # User Diet Plans Oversight
│   ├── messages.php           # Inquiries Inbox & Status Workflow
│   ├── reports.php            # Platform Analytics & CSV Export
│   └── settings.php           # Global Platform Configuration
│
├── api/
│   ├── favorites.php          # AJAX Favorite Toggle
│   ├── meal-plan.php          # AJAX Add/Remove/Auto-Generate Meal Plan
│   ├── progress.php           # AJAX Progress Timeline Data
│   ├── recommendations.php    # AJAX Filtered Recommendations
│   └── search-meals.php       # AJAX Live Search
│
├── config/
│   ├── env.php                # Lightweight Zero-Dependency .env Parser
│   ├── config.php             # Core Bootstrapping, Headers & Flash Messages
│   └── database.php           # PDO Database Connection Singleton
│
├── includes/
│   ├── auth.php               # Auth Guard, Session & CSRF Protection
│   ├── admin-auth.php         # Admin Access Guard & Audit Logger
│   ├── functions.php          # BMI, BMR/TDEE & Scoring Algorithm Engine
│   ├── header.php             # Public Header Layout & Assets
│   ├── navbar.php             # Responsive Navigation Bar
│   ├── footer.php             # Footer & Medical Disclaimer
│   ├── admin-header.php       # Admin Header Layout
│   ├── admin-sidebar.php      # Admin Sidebar Navigation
│   └── admin-footer.php       # Admin Footer Layout
│
├── assets/
│   ├── css/
│   │   ├── style.css          # Modern Design System, Glassmorphism, UI Tokens
│   │   └── admin.css          # Admin Suite Stylesheet
│   ├── js/
│   │   ├── main.js            # Toast Alerts, AJAX Favorites, Search Debounce
│   │   ├── calculators.js     # Live Scientific BMI & Calorie Calculators
│   │   └── admin.js           # Admin Dashboard Interactivity
│   └── images/                # Brand Logo, Avatars, and Recipe Imagery
│
├── uploads/                   # Upload Storage for Recipes & Avatars
│   ├── meals/
│   └── avatars/
│
└── database/
    ├── database.sql           # Complete Schema (11 Tables) + 25+ Seed Recipes
    ├── setup.php              # 1-Click Database Setup & Migration Runner
    └── generate_assets.php    # Visual Asset Generator
```

---

## 🧪 Testing & Verification

1. **PHP Syntax Linter**:
   All files verified with `php -l`.
2. **Database Integrity**:
   Foreign key cascading, indexes, and unique constraints tested and verified.
3. **Responsive Design**:
   Validated across mobile (375px), tablet (768px), and desktop (1440px) viewport widths.
4. **Recommendation Scoring**:
   Verified strict exclusion of peanut/dairy allergens for sensitive profiles and accurate calorie matching.

---

## 📜 License

This project is open-source and available under the **MIT License**.
