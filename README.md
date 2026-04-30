# 🎬 Cineplex Ticket Booking System

A desktop-based cinema management application built with Python, Tkinter, and MySQL. Designed for cinema staff to manage movie listings, issue tickets, and track booking history through a simple GUI.

---

## Features

- **Staff Login** — Secure employee authentication against a MySQL database
- **Movie Dashboard** — Live view of available movies, prices, and remaining seats
- **Ticket Booking** — Issue tickets by customer name, movie ID, and seat count with automatic seat deduction
- **Sales History** — View all booking records in a sortable table via JOIN query
- **Logout** — Session management returning to the login screen

---

## Tech Stack

- **Python 3**
- **Tkinter** — GUI framework
- **MySQL** — Backend database
- **mysql-connector-python** — Database driver

---

## Database Setup

Run the following SQL to create the required database and tables:

```sql
CREATE DATABASE cineplex_db;
USE cineplex_db;

CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    password VARCHAR(50) NOT NULL,
    full_name VARCHAR(100) NOT NULL
);

CREATE TABLE movies (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    available_seats INT NOT NULL
);

CREATE TABLE bookings (
    id INT AUTO_INCREMENT PRIMARY KEY,
    customer_name VARCHAR(100) NOT NULL,
    movie_id INT NOT NULL,
    seats_booked INT NOT NULL,
    total_price DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (movie_id) REFERENCES movies(id)
);
```

Seed some sample data to get started:

```sql
INSERT INTO employees (username, password, full_name) VALUES ('admin', 'admin123', 'Admin User');

INSERT INTO movies (title, price, available_seats) VALUES
('Inception', 12.00, 100),
('Interstellar', 10.00, 80),
('The Dark Knight', 11.00, 60);
```

---

## Installation

**1. Clone the repository**
```bash
https://github.com/afif-hasan/cineplex_ticket_booking.git
```

**2. Install dependencies**
```bash
pip install mysql-connector-python
```

**3. Configure database credentials**

Open `main.py` and update the `get_db()` function with your MySQL credentials:
```python
return mysql.connector.connect(
    host="localhost",
    user="your_username",       # update this
    password="your_password",   # update this
    database="cineplex_db"
)
```

**4. Run the application**
```bash
python main.py
```

---

## Usage

1. Log in with a valid staff username and password
2. The dashboard loads all available movies with seat availability
3. Fill in the customer name, movie ID, and number of seats, then click **Issue Ticket**
4. Click **View All Bookings** to open the sales history window
5. Click **Logout** to return to the login screen

---

## Project Structure

```
cineplex-booking/
│
├── main.py        # All application logic and GUI
└── README.md
```

---

## Known Limitations

- Passwords are stored in plain text — not suitable for production use
- No seat selection (only seat count)
- Single-file architecture; larger scale would benefit from MVC separation

---

## Author

**Afif Hasan** — [github.com/afif-hasan](https://github.com/afif-hasan)
