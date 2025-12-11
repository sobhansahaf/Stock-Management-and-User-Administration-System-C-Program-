# **Stock Management and User Administration System (C Program)**

This project is a stock management system written in C that handles users, stocks, and trading operations. It simulates a basic stock exchange environment with support for both **admin** and **member (user)** accounts. The system uses text files for persistent data storage and provides full CRUD (Create, Read, Update, Delete) functionality for users, stocks, and trades.

---

## **Features**

### **🔐 Login System**

* Users log in using a **username and password**.
* Two account types:

  * **Admin**
  * **Member (regular user)**

### **👨‍💼 Admin Capabilities**

Admins have full control over system data, including:

#### **User Management**

* Add new users (admin or member).
* Search users by:

  * Last name
  * National code
* Edit and view all users.
* View users associated with a specific stock.
* View stocks owned by a specific user.
* Delete or update user data.

#### **Stock Management**

* Add new stocks.
* Edit stock value and amount.
* View all stocks.
* Search stocks by code.

---

## **👤 Member (User) Capabilities**

Members can interact with the simulated stock market:

* View personal account information.
* Buy stocks.
* Sell stocks.
* View recently added stocks.
* Search stocks by code.
* View all stocks they currently own.
* See profit/loss per holding.

Stock purchases and sales automatically update:

* User balance
* Stock amount in global inventory
* Shop (transaction history) records

---

## **📁 Data Storage**

The system uses text files for persistent storage:

| File          | Description                                             |
| ------------- | ------------------------------------------------------- |
| **users.txt** | Stores all user accounts                                |
| **stock.txt** | Stores all available stocks                             |
| **shop.txt**  | Stores user purchase/sale records                       |
| **set.txt**   | Stores global ID counters for users, stocks, and trades |

Each file acts as a simple database table with structured rows.

---

## **📦 Data Structures**

### **User Structure**

```c
struct user {
    int id;
    long int ncode;
    int isadmin;
    long int money;
    int step;
    char fname[50];
    char lname[50];
    char username[50];
    char password[50];
};
```

### **Stock Structure**

```c
struct stock {
    int id;
    long int code;
    char name[50];
    float value;
    long int amount;
};
```

### **Shop Structure (Trading Records)**

```c
struct shop {
    int id;
    int userid;
    int stockid;
    long int amount;
    float value;
    float sellvalue;
    int isactive;
};
```

### **Set Structure (ID Manager)**

```c
struct set {
    int userid;
    int stockid;
    int shopid;
};
```

---

## **🔧 Main Functionalities in Code**

### **User Functions**

* Add, delete, update users
* Get user by:

  * ID
  * Username
  * National code
  * Family name
* Print individual or all users

### **Stock Functions**

* Add, delete, update stock
* Get stock by:

  * ID
  * Stock code
* Print individual or all stocks

### **Shop/Trade Functions**

* Add trade record (buy)
* Update trade record (sell)
* Get trade by ID
* Print:

  * Users who own a particular stock
  * Stocks owned by a particular user

---

## **🖥 Program Flow**

### 1. **Startup**

* User enters username and password.
* System identifies:

  * **Admin** → Admin menu
  * **Member** → Member menu

### 2. **Menus**

Each menu uses a step-based navigation system controlled by stored `user.step` and `goto` statements.

### 3. **Loops and Navigation**

* The system heavily uses `goto` to navigate between menus.
* All changes persist through updates to `.txt` files.

---

## **⚠ Notes and Considerations**

* The program uses `system("cls")` (Windows only).
* Data is stored as plain text — no encryption.
* The program relies on `goto`, which works but can reduce readability.
* File reading uses patterns that may risk reading past EOF; careful handling is required for production use.

---

