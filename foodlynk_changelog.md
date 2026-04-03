<div align="center">

```
███████╗ ██████╗  ██████╗ ██████╗ ██╗  ██╗   ██╗███╗   ██╗██╗  ██╗
██╔════╝██╔═══██╗██╔═══██╗██╔══██╗██║  ╚██╗ ██╔╝████╗  ██║██║ ██╔╝
█████╗  ██║   ██║██║   ██║██║  ██║██║   ╚████╔╝ ██╔██╗ ██║█████╔╝ 
██╔══╝  ██║   ██║██║   ██║██║  ██║██║    ╚██╔╝  ██║╚██╗██║██╔═██╗ 
██║     ╚██████╔╝╚██████╔╝██████╔╝███████╗██║   ██║ ╚████║██║  ██╗
╚═╝      ╚═════╝  ╚═════╝ ╚═════╝ ╚══════╝╚═╝   ╚═╝  ╚═══╝╚═╝  ╚═╝
```

### *A food ordering platform for restaurants and clients — built to learn PHP.*

<br>

[![PHP](https://img.shields.io/badge/PHP-777BB4?style=flat-square&logo=php&logoColor=white)](https://www.php.net/)
[![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![Apache](https://img.shields.io/badge/Apache-D22128?style=flat-square&logo=apache&logoColor=white)](https://httpd.apache.org/)
![Type](https://img.shields.io/badge/project-personal-orange?style=flat-square)
![Status](https://img.shields.io/badge/status-learning-yellow?style=flat-square)

<br>

> *"You don't learn PHP by reading about it. You learn it by breaking things and figuring out why."*

</div>


## 🚀 Version History

| Version | Title | Highlights |
|:---:|:---|:---|
| `v1.0` | **Foundation** | Core structure: `index.php`, login, sign-in, and brand maker pages with their CSS files. No PHP logic yet. |
| `v1.1` | **First Database Work** | Created the database. Wired up `client_signing.php` and `brand_creation.php` to insert data, and both login pages to fetch and validate credentials. First SQL queries inside PHP. |
| `v1.2` | **Refactoring & New Pages** | Updated PHP code and file naming. Added `master_admin_dashboard.php`, `brand_waiting.php`, and `brand_status.php` for the brand approval flow. |
| `v1.3` | **Brand Dashboard** | Added `brand_dashboard.php` to insert meals. Made brand names unique with a duplicate check. Fixed redirects in `brand_login.php` and `index.php`. Included `DATABASE.md`. |
| `v1.4` | **Logout & Unlimited Quantity** | Added a logout button and the unlimited quantity option in `brand_dashboard.php`. Updated `index.php` to fetch only approved brands and render them as cards. |
| `v1.5` | **Menu & Ordering** | Added `menu.php` and `menu.css` to display meals and let clients purchase while writing order data to the database. First real end-to-end user flow. |
| `v1.6` | **Back to It** | Not much changed — was busy, but kept the project alive. |
| `v1.7` | **Major Design Overhaul** | New color scheme, animations, renamed HTML elements, deleted old files, merged files to improve aesthetics. |
| `v1.8` | **Dashboard Power-Up & Client Account** | Added delete and disable options for meals in `brand_dashboard.php`, redesigned the popup form. Upgraded `menu.php` with sorting, filtering, searching, and a cart. Added `client_account.php` and `client_edit_profile.php` with their CSS. Small database adjustments. |
| `v1.9` | **Full Checkout Flow** | Made the activate button functional with confirmation popups. Grouped order history in `client_account.php`. Improved `add_to_cart` scroll memory. Added `checkout.php`, `confirm.php`, and `success.php` with their CSS. |

---

## ⚠️ Things I Know Need Improvement

Since this is a learning project, there are things I'm aware of but haven't refactored yet:

| Issue | What I did | What I should do |
|:---|:---|:---|
| SQL Injection | `mysqli_real_escape_string()` | Use prepared statements with `mysqli_prepare()` |
| Server-side validation | Relied on HTML `required` attributes | Validate types and lengths in PHP too |
| Flat order table | One row per meal line in `orders` | Separate `orders` + `order_items` tables |
| Session authorization | Only store email in session | Add proper authorization checks on protected pages |
| Database credentials | Hardcoded in every file | Move to a config file or `.env` |

---

