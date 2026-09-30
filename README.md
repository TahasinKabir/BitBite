[Uploading README.md…]()
# BitBite 🍽️

**A data-driven health and nutritional tracking application designed for personalized dietary management and weight tracking.**

BitBite is a smart nutrition platform that combines food logging, meal planning, wearable data, and AI-style insights to help users hit their weight and lifestyle goals. It ships with expert booking (nutritionists & yoga coaches), a research hub, daily challenges, and a rewards system — plus a separate admin panel for managing platform activity.

---

## ✨ Features

### For Users
- 🔐 **Authentication** — Signup, login, and social sign-in placeholders (Google/Facebook)
- 🧭 **Guided onboarding** — Captures goal, body type, activity level, diet preferences, health conditions, budget, and wearable device
- 📊 **Dashboard** — Daily overview of calories, water, weight, and activity
- 🍽️ **Food logging** — Log meals with emoji, calories, and meal type
- 📅 **Meal plans** — Day-by-day plans with macros (carbs / protein / fat) and estimated cost in ৳
- 💧 **Water tracker** — Simple daily cups counter
- ⚖️ **Weight logs** — Track progress toward a target weight
- 😴 **Sleep tracker** — Hours, quality, bedtime and wake time
- ⌚ **Wearable logs** — Steps, calories burned, heart rate, SpO₂, HRV, sleep hours
- 🛒 **Shopping list** — Auto-organized by category with prices
- 🧮 **Tools** — BMI calculator, calorie calculator, sleep and water trackers
- 🥗 **Hire a nutritionist** — 10 seeded specialists across weight-loss, PCOS, diabetes, clinical, budget, and family nutrition
- 🧘 **Hire a yoga coach** — 10 seeded coaches across beginner, power, stress-relief, back-pain, and advanced yoga
- 📚 **Research Hub** — Curated articles on nutrition, hydration, sleep, fiber, and healthy habits, with read history and save-for-later
- 🏆 **Achievements & rewards** — Unlockable badges plus a rewards catalog (T-shirt, bracelet, wristband, coupons) claimable once the target goal is reached
- 🎯 **Daily challenges** — 7 rotating micro-goals (hydration, meal logs, walking, sleep review, etc.) with points
- 🔔 **Notifications** — In-app reminders and AI-style insights

### For Admins
- Separate admin login (`admin@bitbite.com` / `admin12345` by default)
- Platform stats: total users, bookings, article reads, saved articles, reward claims, challenge completions
- Recent activity feed across bookings and reward claims

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|------------|
| Frontend | HTML5, CSS3, Vanilla JavaScript |
| Charts | [Chart.js 4.4.1](https://www.chartjs.org/) via CDN |
| Fonts | Google Fonts (Playfair Display, Outfit) |
| Backend | PHP (PDO) |
| Database | MySQL / MariaDB (utf8mb4) |
| Server | Apache (XAMPP) |
| Auth | PHP sessions + `password_hash` (bcrypt) |

---

## 📂 Project Structure

```
Bitbyte/
├── Software Engineering (BITBITE )/    # Course/project deliverables
├── ERD Diagram                          # Entity-Relationship diagram
├── BitBite_Final_Project_Report_With_Team.pdf
├── BitBite_Short_Test_Case_Report.pdf
├── index.html                           # Single-page frontend (all screens & modals)
├── style.css                            # Global styling
├── backend.php                          # PHP API — all actions dispatched via ?action=
├── test_connection.php                  # DB connectivity smoke test
└── bitbite_full_latest_database_setup.txt  # Full SQL setup script
```

---

## 🚀 Getting Started

### Prerequisites
- [XAMPP](https://www.apachefriends.org/) (or any Apache + PHP 7.4+ + MySQL/MariaDB stack)
- A modern browser

### Installation

1. **Clone the repo** into your XAMPP `htdocs` folder:
   ```bash
   git clone https://github.com/TahasinKabir/Bitbyte.git
   cd Bitbyte
   ```

2. **Start Apache and MySQL** from the XAMPP control panel.

3. **Set up the database**:
   - Open [phpMyAdmin](http://localhost/phpmyadmin)
   - Go to the **SQL** tab
   - Paste the entire contents of `bitbite_full_latest_database_setup.txt` and click **Go**
   - This creates the `bitbite_db` database with all tables and demo data

4. **Verify the connection** (optional):
   Visit `http://localhost/Bitbyte/test_connection.php`

5. **Launch the app**:
   Open `http://localhost/Bitbyte/index.html` in your browser.

### Demo Credentials

| Role | Email | Password |
|------|-------|----------|
| User | `araf@example.com` | `12345678` |
| Admin | `admin@bitbite.com` | `admin12345` |

---

## 🗄️ Database Overview

The `bitbite_db` schema is organized around a central `users` table with cascading foreign keys:

**Core tables**
- `users`, `profiles`, `user_settings`

**Tracking**
- `food_logs`, `weight_logs`, `water_logs`, `sleep_logs`, `wearable_logs`

**Planning & shopping**
- `meal_plans`, `shopping_list`

**Engagement**
- `notifications`, `achievements`, `daily_challenges`, `user_challenge_completions`

**Providers & bookings**
- `nutritionists`, `yoga_coaches`
- `nutritionist_hires`, `yoga_coach_hires` (with payment method, status, transaction ID)

**Content**
- `research_hub_articles`, `research_article_reads`, `saved_articles`

**Rewards**
- `reward_catalog`, `user_rewards` (with delivery address, phone, t-shirt size)

**Admin**
- `admins`

See `ERD Diagram` in the repo for the visual schema.

---

## 🔌 API Endpoints

All requests hit `backend.php?action=<name>` with a JSON body (POST):

### Auth
- `signup` — Create a user + default profile
- `login` — Session-based user login
- `logout` — Destroy session
- `me` — Return current user's full data payload
- `admin_login` / `admin_logout` — Admin session

### Profile & Tracking
- `save_profile` — Update onboarding/profile fields
- `add_food`, `delete_food`
- `add_weight` — Also updates current weight + auto-awards goal reward
- `set_water`
- `mark_notification`, `mark_all_notifications`

### Providers
- `hire_nutritionist`, `hire_yoga` — Book a session with payment info
- `cancel_hire` — Cancel by `kind` (nutritionist/yoga) and id

### Content & Engagement
- `read_article` — Log a read + increment count
- `toggle_save_article` — Save/unsave from favorites
- `complete_challenge` — Mark a daily challenge complete for today
- `claim_reward` — Requires target goal achieved + delivery details

### Admin
- `admin_stats` — Aggregate platform metrics + recent activity feed

---

## 🔒 Security Notes

- Passwords hashed with `password_hash(PASSWORD_DEFAULT)` (bcrypt)
- All queries use PDO prepared statements
- Session-gated endpoints via `requireLogin()` / `requireAdmin()`
- ⚠️ **For local/academic use only** — default DB credentials (`root` / no password) and hardcoded admin defaults should be changed before any production deployment. Add HTTPS, CSRF protection, and rate limiting for real-world use.

---

## 📸 Deliverables

The repo includes the project's academic deliverables:
- **BitBite_Final_Project_Report_With_Team.pdf** — Full project report
- **BitBite_Short_Test_Case_Report.pdf** — Test case documentation
- **ERD Diagram** — Database schema visualization
- **Software Engineering (BITBITE )/** — Additional coursework artifacts

---

## 👤 Author

**Tahasin Kabir** — [@TahasinKabir](https://github.com/TahasinKabir)

Built as a Software Engineering project.

---

## 📝 License

No license specified. Please contact the author before reusing this code.
