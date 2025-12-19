# Ex.07 Restaurant Website
## Date:

## AIM:
To develop a static Restaurant website to display the food items and services provided by them.

## DESIGN STEPS:

### Step 1:
Requirement collection.

### Step 2:
Creating the layout using HTML and CSS.

### Step 3:
Updating the sample content.

### Step 4:
Choose the appropriate style and color scheme.

### Step 5:
Validate the layout in various browsers.

### Step 6:
Validate the HTML code.

### Step 7:
Publish the website in the given URL.

## PROGRAM:
```
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('core.urls')),
]
In core/urls.py (create it):
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home_view, name='home'),
    path('menu/', views.menu_view, name='menu'),
    path('administration/', views.admin_view, name='administration'),
    path('contact/', views.contact_view, name='contact'),
]

4. Views
In core/views.py:
from django.shortcuts import render

def home_view(request):
    return render(request, 'home.html')

def menu_view(request):
    # example food list
    foods = [
        {'name': 'Biryani', 'image': 'menu/biryani.jpg'},
        {'name': 'Pizza', 'image': 'menu/pizza.jpg'},
        {'name': 'Pasta', 'image': 'menu/pasta.jpg'},
        # add up to 12 ...
    ]
    return render(request, 'menu.html', {'foods': foods})

def admin_view(request):
    # team members list
    team = [
        {'name': 'Raj', 'role': 'Head Chef', 'image': 'team/raj.jpg'},
        {'name': 'Anjali', 'role': 'Manager', 'image': 'team/anjali.jpg'},
        # add 4 more ...
    ]
    return render(request, 'administration.html', {'team': team})

def contact_view(request):
    contact_info = {
        'address': '123 Spice Street, Chennai City',
        'phone': '+91-9876543210',
        'email': 'contact@spicedelight.com',
    }
    return render(request, 'contact.html', {'contact': contact_info})

5. Templates & Static files
Folder structure under core:
core/
  templates/
    home.html
    menu.html
    administration.html
    contact.html
    base.html
  static/
    css/
      style.css
    images/
      banner.jpg
      menu/
        biryani.jpg
        pizza.jpg
        ...
      team/
        raj.jpg
        anjali.jpg
        ...
You can use a base.html for common header/nav/footer, and extend it.
core/templates/base.html
{% load static %}
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>{% block title %}Spice Delight{% endblock %}</title>
<style>
body {
  font-family: Arial, sans-serif;
  background: #f5f5f5;
  margin: 0; padding: 0;
}

header {
  background-color: #c0392b;
  padding: 10px;
  color: white;
}

nav ul {
  list-style: none;
  text-align: center;
  padding: 0;
}

nav ul li {
  display: inline-block;
  margin: 0 15px;
}

nav ul li a {
  color: white;
  text-decoration: none;
  font-weight: bold;
}

.banner {
  width: 100%;
  height: 300px;
  object-fit: cover;
}

.intro {
  padding: 40px;
  text-align: center;
}

.menu-grid, .team-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
  padding: 20px;
}

.menu-grid .item img, .team-grid .member img {
  width: 100%;
  border-radius: 10px;
}

footer {
  background-color: #333;
  color: white;
  text-align: center;
  padding: 10px;
}

</style>

</head>
<body>
  <header>
    <img src="{% static 'images/banner.jpg' %}" alt="Banner" class="banner">
    <nav>
      <ul>
        <li><a href="{% url 'home' %}">Home</a></li>
        <li><a href="{% url 'menu' %}">Menu</a></li>
        <li><a href="{% url 'administration' %}">Administration</a></li>
        <li><a href="{% url 'contact' %}">Contact Us</a></li>
      </ul>
    </nav>
  </header>

  <main>
    {% block content %}{% endblock %}
  </main>

  <footer>
    <p>Designed by Your Name © 2025</p>
  </footer>
</body>
</html>
home.html
{% extends 'base.html' %}
{% block title %}Home — Spice Delight{% endblock %}
{% block content %}
<section class="intro">
  <h1>Welcome to Spice Delight</h1>
  <p>Serving traditional flavors with a modern twist. Join us for an unforgettable experience.</p>
</section>
{% endblock %}
menu.html
{% extends 'base.html' %}
{% block title %}Menu — Spice Delight{% endblock %}
{% block content %}
<section class="menu">
  <h2>Our Menu</h2>
  <div class="menu-grid">
    {% for food in foods %}
      <div class="item">
        <img src="{% static 'images/'|add:food.image %}" alt="{{ food.name }}">
        <p>{{ food.name }}</p>
      </div>
    {% endfor %}
  </div>
</section>
{% endblock %}
administration.html
{% extends 'base.html' %}
{% block title %}Administration — Spice Delight{% endblock %}
{% block content %}
<section class="team">
  <h2>Our Team</h2>
  <div class="team-grid">
    {% for member in team %}
      <div class="member">
        <img src="{% static 'images/'|add:member.image %}" alt="{{ member.name }}">
        <p>{{ member.name }} – {{ member.role }}</p>
      </div>
    {% endfor %}
  </div>
</section>
{% endblock %}
contact.html
{% extends 'base.html' %}
{% block title %}Contact Us — Spice Delight{% endblock %}
{% block content %}
<section class="contact">
  <h2>Contact Us</h2>
  <p>📍 Address: {{ contact.address }}</p>
  <p>📞 Phone: {{ contact.phone }}</p>
  <p>✉️ Email: {{ contact.email }}</p>
</section>
{% endblock %}

```

## OUTPUT:
<img width="1920" height="1080" alt="Screenshot 2025-12-19 205048" src="https://github.com/user-attachments/assets/87459b3e-4701-4bbd-b494-44793f33c4c5" />
<img width="1920" height="1080" alt="Screenshot 2025-12-19 205109" src="https://github.com/user-attachments/assets/d7ee7977-62f7-468f-bb44-5b3e94237290" />
<img width="1920" height="1080" alt="Screenshot 2025-12-19 205123" src="https://github.com/user-attachments/assets/67ff93df-c89f-4b3f-be6d-d0fddaa68bc5" />
<img width="1920" height="1080" alt="Screenshot 2025-12-19 205208" src="https://github.com/user-attachments/assets/bf42028c-85e0-4d67-9746-eae43069ea8a" />


## RESULT:
The program for designing software company website using HTML and CSS is completed successfully.
