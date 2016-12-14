---
layout: single
title: Python e-commerce frameworks
tags: [python, django, e-commerce, framework]
---
There are a lot of e-commerce frameworks in PHP and one pretty cool in Ruby on Rails([https://github.com/spree/spree][1]), but now I will tell this field in python.

# Key features I’m caring about:

## Functional requirements
* Multilingual (dashboard or admin panel in Chinese)
 * Product Types (different product may have different fields)
* Search (build-in one will save your time)
* Customer Accounts (store customer related things)
* Dynamic Categories (the requirements change all the time, so make this part more generic)
* Price sorting/filtering (products always need sorting and filtering)
* Payment Methods (should be an independent one as we will integrate a niche payment provider)
* Wishlist (store products and shops)

## Developing requirements
* Documented (the important one as e-commerce website is much complex)
* Development Status (Stable to use)
* Django Version (we need the newer version will have longer support)
* Github stars (we all believe this)
* Easy to use
* API support
* Recent Commits (showing repo dead or not?)

# Let’s see some candidates

## Django SHOP
- Document: [http://django-shop.readthedocs.io/en/latest/][2]
- Github: [https://github.com/awesto/django-shop][3]
- Multilingual: False
- Development Status: Unknown
- Version: 0.9.3
- Easy: Yes
- Django Version: 1.9+
- API: Yes

## **Django Oscar**
- Document: [http://django-oscar.readthedocs.io/en/latest/index.html][4]
- Github: [https://github.com/django-oscar/django-oscar][5]
- Development Status: Production/Stable
- Version: 1.3.0
- Django Version: 1.8.8+
- Easy: No
- API: Yes

## Shuup
- Document: [http://shuup.readthedocs.io/en/latest/index.html][6]
- Github: [https://github.com/shuup/shuup][7]
- Multilingual: False
- Development Status: Stable
- Version: 0.6.0
- Easy: No
- Django Version: 1.8+
- API: Yes

## Cartridge
- Document: [http://cartridge.jupo.org/][8]
- Github: [https://github.com/stephenmcd/cartridge][9]
- All based on Mezzanine
- Version: 0.12.0
- API: No
- If you use Mezzanine before, this will be the better choose

## Finally, I choose `django-oscar`, as 
- I need Chinese support, it has 95% finished in Chinese. 
- It has more stars;
- It is django style design, complex but has more documents;
- It is much more flexible with dynamic design, so I can customize it  to meet my requirements.

# Refs
https://www.djangopackages.com/grids/g/ecommerce/

[1]:	https://github.com/spree/spree
[2]:	http://django-shop.readthedocs.io/en/latest/
[3]:	https://github.com/awesto/django-shop
[4]:	http://django-oscar.readthedocs.io/en/latest/index.html
[5]:	https://github.com/django-oscar/django-oscar
[6]:	http://shuup.readthedocs.io/en/latest/index.html
[7]:	https://github.com/shuup/shuup
[8]:	http://cartridge.jupo.org/
[9]:	https://github.com/stephenmcd/cartridge