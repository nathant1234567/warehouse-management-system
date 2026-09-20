# Warehouse Inventory & Order Management System

[![Java](https://img.shields.io/badge/Java-17+-orange.svg)](https://www.oracle.com/java/)
[![Database](https://img.shields.io/badge/Database-SQLite-003B57.svg)](https://www.sqlite.org/)
[![Testing](https://img.shields.io/badge/Testing-JUnit-green.svg)](https://junit.org/)

A robust, database-backed warehouse and inventory management system implemented in Java. The application tracks complex warehouse operations—including stock batches, part locations, customer orders, purchase orders, deliveries, and fulfillment workflows—persisting state across relational SQLite databases and automatically generating visual HTML reports.

---

## Key Features

- **Relational Data Persistence (SQLite)**:
  - Connects to embedded SQLite relational databases (`warehousedata.sqlite`, `originaldata-2025.sqlite`) via [`DatabaseHandler`](src/DatabaseHandler.java).
  - Enforces schema integrity, entity relationships, and transactional updates across operational records.
- **Full Inventory & Order Lifecycle Management**:
  - **Parts & Batches**: Tracks part specifications, inventory quantities, shelf locations, and batch arrivals.
  - **Customer Orders**: Manages multi-item orders, tracks fulfillment statuses, and handles customer profiles.
  - **Purchase Orders & Deliveries**: Tracks incoming supplier shipments, restock schedules, and delivery logs.
- **Automated HTML Reporting & Dashboards**:
  - Automatically compiles and renders styled HTML summary reports in the `html/` directory to visualize real-time warehouse metrics, stock levels, and order statuses.
- **Automated Unit Testing**:
  - Includes a JUnit test suite (`WarehouseTest.java`) ensuring consistency across data queries, calculations, and entity models.

---

## Architecture & Project Structure

The project employs an object-oriented domain model with centralized collection managers (`AllEntities`) and dedicated database handlers:

```
├── html/                          # Auto-generated HTML dashboards & visual reports
├── lib/                           # External dependencies (SQLite JDBC driver, JUnit)
├── originaldata-2025.sqlite       # Baseline seed database
├── warehousedata.sqlite           # Active operational SQLite database
├── src/
│   ├── Main.java                  # Main application entry point
│   ├── DatabaseHandler.java       # SQLite JDBC connection and query executor
│   ├── Warehouse.java             # Core warehouse operations coordinator
│   │
│   ├── # Domain Models
│   ├── Part.java, Batch.java      # Inventory & batch tracking models
│   ├── Customer.java              # Customer identity model
│   ├── Order.java, OrderItem.java # Customer order and line item models
│   ├── PurchaseOrder.java         # Inbound stock orders
│   ├── Delivery.java              # Fulfillment and dispatch logs
│   ├── Location.java, Date.java   # Value objects for warehouse coordinates & dates
│   │
│   ├── # Entity Collections / Managers
│   ├── AllEntities.java           # Base entity management abstraction
│   ├── AllParts.java, AllBatches.java
│   ├── AllCustomers.java, AllCustomerOrders.java
│   ├── AllPurchaseOrders.java, AllDeliveries.java
│   └── webview/                   # Webview & HTML report generation components
└── test/
    └── WarehouseTest.java         # Automated JUnit tests
```

---

## Getting Started

### Prerequisites
- **Java Development Kit (JDK)**: Version 11 or higher (Java 17 recommended)
- **IDE**: IntelliJ IDEA, Eclipse, or terminal with `javac`

### Installation & Execution

1. **Clone the repository**:
   ```bash
   git clone https://github.com/nathant1234567/warehouse-system-uni.git
   cd warehouse-system-uni
   ```

2. **Open in IntelliJ IDEA**:
   - Open IntelliJ IDEA and select **Open**.
   - Navigate to the cloned `warehouse-system-uni` folder.
   - Ensure the SQLite JDBC driver and JUnit `.jar` files in `lib/` are recognized (**File > Project Structure > Libraries**).

3. **Run via CLI**:
   ```bash
   # Compile
   javac -cp "lib/*:src" -d out src/*.java

   # Execute
   java -cp "out:lib/*" Main
   ```

4. **View Generated Reports**:
   Open any `.html` file inside the `html/` directory in your browser to inspect the visual inventory and order dashboard.

---

## Testing

Run the automated test suite in IntelliJ by right-clicking `test/WarehouseTest.java` and selecting **Run 'WarehouseTest'**, or via CLI:

```bash
java -cp "out:lib/*" org.junit.runner.JUnitCore WarehouseTest
```
