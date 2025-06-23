

````
# 🍕 Pizza Restaurant API

A RESTful Flask API to manage restaurants, pizzas, and their pricing using SQLAlchemy and Flask-Migrate. No frontend, just pure backend sauce. Tested using Postman.

---


## 🚀 Setup Instructions

### 1. Clone the repository

```bash
git clone https://github.com/r0dn3y7/pizza-api-challenge.git
cd pizza-api-challenge
````

### 2. Install dependencies & activate environment

```bash
pipenv install flask flask_sqlalchemy flask_migrate
pipenv shell
```

### 3. Set up the database

```bash
export FLASK_APP=server/app.py
flask db init
flask db migrate -m "Initial migration"
flask db upgrade
```

### 4. Seed the database

```bash
python -m server.seed
```

---

## 🧱 Project Structure (MVC)

```
.
├── server/
│   ├── app.py                  
│   ├── config.py               
│   ├── seed.py                 
│   ├── models/
│       ├── __init__.py
│       ├── restaurant.py
│       ├── pizza.py
│       └── restaurant_pizza.py
│   
├── migrations/
├── challenge-1-pizzas.postman_collection.json
└── README.md
```

---

## 🛠 Models

### 🍽️ Restaurant

* `id`: Integer (PK)
* `name`: String (required)
* `address`: String (required)
* Relationship: has many `RestaurantPizzas`

### 🍕 Pizza

* `id`: Integer (PK)
* `name`: String (required)
* `ingredients`: String (required)
* Relationship: has many `RestaurantPizzas`

### 💵 RestaurantPizza (Join Table)

* `id`: Integer (PK)
* `price`: Integer (must be between 1 and 30)
* `pizza_id`: Foreign Key to Pizza
* `restaurant_id`: Foreign Key to Restaurant
* Relationship: belongs to Pizza and Restaurant

---

## 🔌 Routes

### `GET /restaurants`

Returns a list of all restaurants.

### `GET /restaurants/<id>`

Returns a restaurant and its pizzas.

* If not found:

```json
{ "error": "Restaurant not found" }
```

### `DELETE /restaurants/<id>`

Deletes a restaurant and its associated restaurant\_pizzas.

* Success: `204 No Content`
* If not found:

```json
{ "error": "Restaurant not found" }
```

---

### `GET /pizzas`

Returns a list of all pizzas.

---

### `POST /restaurant_pizzas`

**Request Body:**

```json
{
  "price": 5,
  "pizza_id": 1,
  "restaurant_id": 3
}
```

**Success Response:**

```json
{
  "id": 4,
  "price": 5,
  "pizza_id": 1,
  "restaurant_id": 3,
  "pizza": {
    "id": 1,
    "name": "Emma",
    "ingredients": "Dough, Tomato Sauce, Cheese"
  },
  "restaurant": {
    "id": 3,
    "name": "Kiki's Pizza",
    "address": "address3"
  }
}
```

**Error (Invalid Price):**

```json
{
  "errors": ["Price must be between 1 and 30"]
}
```

---

## ✅ Validation Rules

* `RestaurantPizza.price` must be between **1 and 30**
* All fields are required
* Cascade delete ensures restaurant-related records are cleaned up

---

## 🧪 Postman Testing

1. Open Postman
2. Click **Import**
3. Select `challenge-1-pizzas.postman_collection.json`
4. Test each route

---

## 📦 Dependencies

* Flask
* Flask-SQLAlchemy
* Flask-Migrate
* Pipenv

---

## 👨‍🍳 Author

Built by [Rodney Amani]

---

````

---

### ✅ Final Step:

 commit it:

```bash
git add README.md
git commit -m "Add complete README with setup and API documentation"
git push
````

