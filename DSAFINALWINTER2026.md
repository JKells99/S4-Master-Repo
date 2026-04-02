# Warehouse Inventory & Order Priority System

## Final Project Overview

You will build a Spring Boot API that manages a warehouse system while applying Data Structures and Algorithm knowledge.

## Requirements Summary

### MUST INCLUDE:
- Spring Boot API Structure (Controller, Service, Repository)
- SQL Database
- Binary Search Tree for Order Priority
- ONE manual sorting algorithm (no built-in sorting)
- Demo video
- Readme with answers to the questions

---

# Requirements

## 1. Database and Entities

You must implement the following entities with proper JPA annotations:

### Product
- id (Primary Key)
- name (String)
- price (double)
- stock (int)

### Customer
- id (Primary Key)
- name (String)
- email (String)

### Order
- id (Primary Key)
- orderDate (LocalDate)
- priorityLevel (int: 1–10)
- Many-to-One relationship with Customer

### OrderItem
- id (Primary Key)
- quantity (int)
- Many-to-One relationship with Product
- Many-to-One relationship with Order

### Relationship Requirements
- One Customer → Many Orders
- One Order → Many OrderItems
- One Product → Many OrderItems

---

## 2. API Requirements

You must create REST endpoints for:

### Product Endpoints
- GET /products (get all products)
- POST /products (create product)
- GET /products/sorted?by=price
- GET /products/sorted?by=stock

### Order Endpoints
- POST /orders (create order)
- GET /orders (get all orders)
- POST /orders/add-to-priority-tree

### BST Endpoints
- GET /orders/priority/inorder
- GET /orders/priority/highest
- GET /orders/priority/lowest

---

## 3. Binary Search Tree Requirements

You must:
- Implement your own BST
- Insert orders based on priorityLevel
- Left child = lower priority
- Right child = higher priority

### Required Methods
- insert(Order order)
- inorder traversal (must return sorted priorities)
- findHighest()
- findLowest()

### Expected Behavior
- In-order traversal returns sorted results
- Highest = rightmost node
- Lowest = leftmost node



---

## 4. Unit Testing 
- You must write 3 unit test to test your program
- Test cases are up to you! 

# BST Implementation (This code is broken and needs to be fixed)

```
class OrderNode {
    Order data;
    OrderNode left;
    OrderNode right;

    public OrderNode(Order data) {
        this.data = data;
    }
}
```
```

class OrderBST {

    OrderNode root;

    // TODO: Fix insertion logic
    public void insert(Order order) {
        root = insertRecursive(root, order);
    }

    private OrderNode insertRecursive(OrderNode current, Order order) {

        if (current == null) {
            return new OrderNode(order);
        }

        if (order.getPriorityLevel() < current.data.getPriorityLevel()) {
            current.right = insertRecursive(current.right, order);
        } else {
            current.left = insertRecursive(current.left, order);
        }

        return current;
    }

    // TODO: Implement inorder traversal
    public void inorder(OrderNode node) {
        if (node == null) return;

        System.out.println(node.data.getPriorityLevel());
    }

    // TODO: Fix highest priority logic
    public Order findHighest() {
        OrderNode current = root;

        while (current.left != null) {
            current = current.left;
        }

        return current.data;
    }
}
```

---

## 5. Sorting Requirements

You must implement ONE sorting algorithm manually.

### Allowed Algorithms
- Bubble Sort
- Selection Sort
- Insertion Sort

### Not Allowed
- Collections.sort()
- Stream.sorted()

### Sorting Features
- Sort products by price
- Sort products by stock

---

# Sorting (Broken Insertion Sort)
```

public List<Product> sortByPrice(List<Product> products) {

    for (int i = 0; i < products.size(); i++) {

        Product current = products.get(i);
        int j = i;

        while (j > 0 && products.get(j).getPrice() < current.getPrice()) {
            products.set(j, products.get(j - 1));
            j--;
        }

        products.set(j, current);
    }

    return products;
}
```
---

## 6. Service Layer Requirements

- Must contain business logic
- Must inject repository layer
- Must implement sorting logic
- Must handle invalid inputs

---

## 7. Controller Requirements

- Must expose REST endpoints
- Must not contain business logic
- Must inject service layer
- Must return proper responses based on situiation

---

# Controller (Incomplete)
```
@RestController
@RequestMapping("/products")
public class ProductController {

    @Autowired
    private ProductService productService;

    @GetMapping("/sorted")
    public List<Product> getSorted(@RequestParam String by) {

        // TODO: handle multiple sort types
        return productService.sortByPrice(productService.getAllProducts());
    }
}
```

---

# Service (Incomplete)
```
@Service
public class ProductService {

    public List<Product> getAllProducts() {
        return new ArrayList<>();
    }

    // TODO: Fix sorting logic
}
```

---

## 8. Your Tasks

You must fix and complete the following:

1. BST insertion logic
2. BST inorder traversal
3. BST highest and lowest methods
4. Sorting algorithm
5. Service logic for sorting
6. Database integration (JPA + Repository)
7. Entity relationships
8. Expose proper HTTP verbs in the controller based on situation
  

---

## 9. Application Therory Questions (Required)

Answer all questions clearly. Focus on understanding, not length.

### Binary Search Tree
- Why does an inorder traversal of a BST return sorted results? Explain in your own words.
- What happens to the tree if you insert values in order (1,2,3,4,5)? How does this affect performance?
- Where would you place duplicate priority values in your tree? Explain your choice.

### Sorting Algorithm
- Explain how your sorting algorithm works step-by-step using a small example.
- What is the time complexity of your algorithm?
- When would your sorting algorithm perform well?
- Why is your sorting algorithm ideal or not ideal for very large datasets?

### System Design
- Why might you choose to sort data in your application instead of the database?
- What is one advantage of using a BST in this system?
- What is one limitation of your current design?

  

## 10. Submission Requirements

- All source code in a GitHub repository
- A demo video showing:
  - API being used in Postman. (Cover the API features) 
    - BST traversal results
    - Sorting results
    - Creating of Product and Customer
- A markdown file answering all questions and also outlining where and when you used AI to help with your development work. 

 
