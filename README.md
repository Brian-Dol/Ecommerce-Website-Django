<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:7c2d12,100:f97316&height=170&section=header&text=Django%20Ecommerce%20Store&fontColor=ffffff&fontSize=44&fontAlignY=38&desc=Product%20catalogue%20with%20variants%20and%20email-verified%20accounts&descAlignY=60&descSize=16" alt="Django Ecommerce Store" />

![Python](https://img.shields.io/badge/Python-3-3776ab?style=flat-square&logo=python&logoColor=white)
![Django](https://img.shields.io/badge/Django-3.2-092e20?style=flat-square&logo=django&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003b57?style=flat-square&logo=sqlite&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap-4-7952b3?style=flat-square&logo=bootstrap&logoColor=white)
![jQuery](https://img.shields.io/badge/jQuery-0769ad?style=flat-square&logo=jquery&logoColor=white)

</div>

A Django storefront foundation: a catalogue of products grouped by category, a product detail page, and user accounts with an email verification flow. It is a compact base to build cart and checkout features on.

## ✨ Features

- 🛍️ **Home page** listing all products
- 📦 **Product detail pages** at `/product/<slug>/` with auto-generated slugs
- 🗂️ **Categories** with images, plus **colour and size variants** that carry their own price
- 🖼️ Multiple images per product
- 🔐 **Registration and login** using the email address as the username; login is blocked until the email is verified
- ✉️ Email-token activation view (`/accounts/activate/<token>/`) backed by a `Profile` model created through a `post_save` signal
- 🛠️ Django admin for managing catalogue data

## 🏗️ Architecture

| App | Responsibility |
| --- | --- |
| `home` | Index view listing products |
| `products` | `Category`, `ColorVariant`, `SizeVariant`, `Product`, `ProductImage` models and product page |
| `accounts` | `Profile` (email token, verified flag, image), login, register, activate |
| `base` | Abstract `BaseModel` (UUID primary key, timestamps) and the activation email helper |
| `ecomm` | Project settings and URL routing |

## 🧰 Tech stack

| Layer | Technology |
| --- | --- |
| Backend | Django 3.2, Pillow (image fields) |
| Database | SQLite (default Django settings) |
| Frontend | Django templates, Bootstrap, jQuery, Font Awesome |

## 🚀 Getting started

```bash
git clone https://github.com/Brian-Dol/Ecommerce-Website-Django.git
cd Ecommerce-Website-Django
python -m venv venv && source venv/bin/activate   # Windows: venv\Scripts\activate
pip install django pillow
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

Add categories and products at http://127.0.0.1:8000/admin/, then browse the store at http://127.0.0.1:8000/.

## 🗺️ Notes

- There is no `requirements.txt`; the install line above lists the packages the code imports.
- The activation email helper currently returns early (`base/emails.py`), so no email is sent and the SMTP credentials in settings are blank. Remove the early `return` and add credentials to enable it; until then, verify users via the admin (`Profile.is_email_verified`).
- Cart, checkout and payments are not implemented.
- `SECRET_KEY` is hard-coded and `DEBUG = True`; use environment variables for any real deployment.
- A development `db.sqlite3` and some `__pycache__` files are committed to the repository.

## 👤 Author

**Brian Dol**, Senior Full Stack Engineer · [Portfolio](https://portfolio.dol-brian23.workers.dev/) · [LinkedIn](https://linkedin.com/in/brian-dol-31a06115a/)
