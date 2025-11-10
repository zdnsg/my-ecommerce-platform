Software Requirements Specification

Project Name: SchoolDash - Campus Supermarket Instant Delivery Platform
Version: 2.0
Author: SchoolDash Group 8
Date: 2025-11-11

Table of Contents

Introduction
1.1  Purpose
1.2  Project Background
1.3  Reference Materials

Overall Description
2.1  Objectives
2.1.1 Development Intention
2.1.2 Application Goals and Scope
2.1.3 Product Prospects

Specific Requirements
3.1  Core Entities (Class Diagram Description)
3.2  Functions
3.2.1 User & Authentication Module
3.2.2 Product & Inventory Module
3.2.3 Cart & Order Module
3.2.4 Delivery & Rider Module
3.2.5 Admin Backend Module
3.3  Other Properties (Non-functional Requirements)
3.3.1 API Interface Definition
3.3.2 Performance & Concurrency Requirements
3.3.3 Security & Permission Requirements

Interface Prototype (Key Page Description)
4.1  Home Page (User End)
4.2  Product List/Detail Page (User End)
4.3  Cart Page (User End)
4.4  Order Confirmation Page (User End)
4.5  Order Detail (Status Tracking) Page (User End)
4.6  Admin - Order Kanban (Admin End)
4.7  Rider - Order Taking Page (Rider End)

Function Description and Acceptance Verification Standards
5.1  Detailed Function Description
5.1.1 User Module
5.1.2 Product Module
5.1.3 Cart Module
5.1.4 Order Module
5.1.5 Admin Backend Module
5.1.6 Delivery (Rider) Module
5.2  Input/Output Format
5.3  Interface Acceptance Criteria
5.4  Functional Acceptance Criteria

1. Introduction

1.1 Purpose

This project, "SchoolDash - Campus Supermarket Instant Delivery Platform," aims to provide an efficient and convenient instant delivery solution for supermarket goods to students and faculty within the campus, solving the "last 500 meters" shopping problem.

This Software Requirements Specification (SRS) aims to clearly and completely define the project's functional and non-functional requirements, including system features, user interactions, business processes, and constraints, serving as the foundational blueprint for the entire project lifecycle.

This document will serve as the basis for ensuring all stakeholders (project team, developers, testers, instructors) have a consistent understanding of the project's scope, functions, and objectives. It establishes clear benchmarks to guide development, validate functionality, and for final acceptance.

1.2 Project Background

With the fast-paced nature of campus life, the demand from students and faculty for instant and convenient services is growing. Traditional campus supermarket shopping is time-consuming and offers a poor experience during inclement weather or busy periods. "SchoolDash" aims to solve these pain points by connecting campus supermarkets, students, and riders through a platform, offering an "order online, 30-minute delivery" instant retail service.

This project is proposed and developed by SchoolDash Group 8, aiming to optimize the e-commerce experience within the campus through technology, provide new order growth for supermarkets, offer convenience to students, and create income opportunities for campus riders (part-time).

1.3 Reference Materials

SchoolDash Group 8 (1).docx - (Project Team Introduction, Tech Stack, Timetable)

SchoolDash - Product Requirements Document (V1.5) - (Early PRD Draft)

Vue.js Official Documentation

Spring Boot Official Documentation / Django Official Documentation

2. Overall Description

2.1 Objectives

The primary objective of "SchoolDash" is to enable effective, real-time instant delivery of campus supermarket goods, ultimately enhancing convenience and improving supermarket operational efficiency. The platform is designed to capture and process orders via the user end (Mini Program/App), dispatch orders through the admin backend, and fulfill them via the rider end (Mini Program/App).

The system processes inventory and order data in real-time and presents it through intuitive interfaces to users (viewing products), administrators (processing orders), and riders (accepting deliveries), making it accessible and actionable.

"SchoolDash" aims to let students (users) get supermarket goods instantly, allow supermarket administrators to process online orders efficiently, and give riders clear delivery tasks. This visibility helps improve efficiency for all parties, achieve refined operations, and ultimately enhance the quality of campus life.

2.1.1 Development Intention

"SchoolDash" is intended to be a highly user-friendly instant delivery solution, capable of integrating with existing campus supermarket operations (inventory management) with minimal friction. The system's design core is flexibility and ease of use, making it simple to promote within the campus environment.

The system facilitates dynamic product inventory management, allowing supermarket administrators to easily list, delist, modify products, and update stock. The order process (placing, paying, accepting, packing, delivering) is designed to be clear, allowing users to track order status in real-time. Rider dispatching (auto-dispatch/manual-assign) ensures timely delivery. Furthermore, role-based user management (User, Admin, Rider) ensures data isolation and security.

By emphasizing process automation, real-time synchronization, and user-centric design, "SchoolDash" serves as a powerful tool for managing instant retail in any campus environment.

2.1.2 Application Goals and Scope

Real-time Product Browsing and Purchasing: "SchoolDash" provides a real-time shelf of campus supermarket goods. Users can browse, search, add to cart, and pay online. The system continuously collects and analyzes inventory data to ensure front-end availability.

Order Fulfillment and Delivery: The platform provides a full-loop process from order generation, merchant acceptance, supermarket packing, rider pickup, to final delivery. Users can track order status in real-time (Pending Acceptance, Packing, Delivering, Delivered).

Features: "SchoolDash" provides advanced features including real-time inventory synchronization, low-stock warnings (admin end), real-time order status pushes, and rider order-taking and status updates.

Application Areas (Scope):

Users (Students/Faculty): Place orders from dormitories, libraries, offices, etc., and receive snacks, drinks, and daily necessities within 30 minutes.

Supermarket Admins (B-end): Receive and process online orders in the backend, pick and pack goods, and manage online inventory.

Riders (P-end): Receive delivery tasks, follow instructions to pick up goods from the supermarket, and deliver to the designated dormitory building.

Platform (Management): Strictly limited to a specific campus area.

2.1.3 Product Prospects

"SchoolDash" consists of front-end and back-end components that work together to provide a cohesive instant delivery solution.

Front-end Components: This includes web-based (or Mini Program) user interfaces that allow users to interact with the platform (browse, order, pay, track). It provides an admin backend interface for administrators (manage products, orders) and a rider interface for riders (accept orders). The interface design is simple and easy to use, enabling users to complete operations quickly and clearly.

Back-end Component: The backend handles the core business logic of "SchoolDash." It is responsible for managing users, products, inventory, processing order state transitions (state machine), handling payment callbacks, and dispatching rider tasks. The backend manages the core database and implements locking mechanisms for orders and inventory. The backend architecture (Spring Boot / Django) ensures system reliability, scalability, and security, allowing the system to function effectively as order volume increases. The platform uses a modular design, allowing components (like Order, Product, User) to be upgraded or extended independently.

3. Specific Requirements

3.1 Core Entities (Class Diagram Description)

This section describes the core business entities of the "SchoolDash" platform, covering main modules like User, Product, Order, and Rider. Each entity collaborates to build an efficient and flexible instant delivery system.

3.1.1 User Entity

Represents the C-end user (Student/Faculty). Core attributes: UserID, Phone, Password (encrypted), Nickname, Avatar. Users can log in, log out, manage their delivery addresses, and view orders.

3.1.2 Address Entity

Belongs to a User. Core attributes: AddressID, UserID, Campus, Building, RoomNumber, ContactName, ContactPhone, IsDefault.

3.1.3 Product Entity

Represents a product in the supermarket. Core attributes: ProductID, ProductName, CategoryID, Price, MainImage, Description, Stock. Products are managed by admins in the backend (CRUD, list/delist).

3.1.4 Stock Entity

Represents the real-time inventory of a product. Core attributes: ProductID, AvailableStock. This is core data for high-concurrency reads and writes.

3.1.5 CartItem Entity

Represents an item in the user's shopping cart. Core attributes: UserID, ProductID, Quantity.

3.1.6 Order Entity

Represents a user's purchase order. Core attributes: OrderID, OrderNumber, UserID, TotalAmount, DeliveryFee, PaidAmount, Status, ShippingAddress (snapshot), CreateTime, PaymentTime.

3.1.7 OrderItem Entity

Represents a specific product within an order (snapshot). Core attributes: OrderID, ProductID, ProductName, Price, Quantity.

3.1.8 Admin Entity

Represents a supermarket or platform administrator. Core attributes: AdminID, Username, Password (encrypted), Role (e.g., Manager, Packer). Responsible for logging into the admin backend.

3.1.9 Rider Entity

Represents a delivery person. Core attributes: RiderID, Name, Phone, Status (Online/Offline/Delivering). Riders log in, accept orders, and update delivery status via the rider end.

3.2 Functions

3.2.1 User & Authentication Module (User & Auth)

Description: Provides basic authentication functions for users to access the platform and make purchases.

Requirements:

Users must be able to log in and register via Phone+VerificationCode / Password.

Provide a "Forgot Password" function.

Users can manage (CRUD, set default) their on-campus delivery addresses.

Addresses must be structured (Campus, Building, RoomNumber).

3.2.2 Product & Inventory Module (Product & Inventory)

Description: Clearly displays in-stock products to users and allows administrators to manage them.

Requirements:

The user end must provide clear product categories, lists, and search functions.

Product lists must reflect real-time (or near-real-time) stock status ("Sold Out" or "Only N left").

Products with zero stock cannot be added to the cart.

Admins must be able to perform CRUD operations and list/delist products in the backend.

Admins must be able to modify stock in real-time (stock-in / inventory check).

3.2.3 Cart & Order Module (Cart & Order)

Description: Handles the complete user flow from selection, checkout, payment, to viewing orders.

Requirements:

Users can perform CRUD operations on the cart (add, remove, update, clear).

The cart footer should in real-time calculate the total price of selected items.

Checkout must re-verify inventory and check against the "minimum order value."

Submitting an order must lock the stock.

After an order is created, the user must pay within 10 minutes, or the order is automatically canceled, and stock is released.

Users can view all orders in their personal center and filter by status.

Order statuses (Pending Payment, Pending Acceptance, Packing, Delivering, Delivered) must be clearly displayed on the user end.

3.2.4 Delivery & Rider Module (Rider & Dispatch)

Description: Manages riders and the delivery process to ensure orders are fulfilled timely.

Requirements:

Riders must log in to the rider end with a dedicated account and can switch between "On Duty" (Online) and "Off Duty" (Offline).

Only "Online" riders can receive new order pushes (dispatch) or "grab" orders from the order pool.

After accepting an order, the rider must follow the process and click "Picked Up" and "Delivered."

When the rider clicks "Picked Up," the user's order status changes to "Delivering."

When the rider clicks "Delivered," the order process is complete.

3.2.5 Admin Backend Module (Admin Backend)

Description: Allows supermarket administrators to process orders, manage products, and riders.

Requirements:

Provide Role-Based Access Control (Admin, Packer, etc.).

Admins can view all orders in the backend and filter by status (especially "Pending Acceptance").

Admins must be able to perform "Accept Order" (status changes to "Packing") and "Call Rider / Assign" (status changes to "Pending Pickup / Delivering").

Admins should be able to see rider statuses (Online/Offline/Delivering) for manual dispatch.

(See 3.2.2) Product and inventory management functions.

3.3 Other Properties (Non-functional Requirements)

3.3.1 API Interface Definition

Description: Standardizes communication between the front-ends (User, Admin, Rider) and the back-end.

Requirements:

Standardized Interfaces: All API interactions must follow RESTful style, using JSON format for data exchange.

Interface Documentation: Must provide clear API documentation (e.g., Swagger/OpenAPI).

Versioning: APIs should support versioning to accommodate future updates.

3.3.2 Performance & Concurrency Requirements

Description: The system needs to handle the high-concurrency nature of instant retail, especially for inventory and orders.

Requirements:

Page Load: Core pages (Home, Product List) load time should be within 2 seconds.

Inventory Consistency (Core): Must technically guarantee strong inventory consistency to prevent overselling. Use database pessimistic locking, optimistic locking, or Redis distributed locks when locking stock (submitting order) and decrementing stock (payment).

Order State Machine: The transition of order states must be idempotent and reliable.

Real-time: After a user places an order, the delay for it appearing in the admin's "Pending Acceptance" list should be within 5 seconds.

3.3.3 Security & Permission Requirements

Description: Ensures system data security and user permission isolation.

Requirements:

Authentication: All backend APIs (except login/register/product browsing) must be authenticated via Token.

Data Transmission: All data transmission must use HTTPS.

Password Storage: User and rider passwords must be stored with salt and hash.

Permission Isolation (Access Control): Permissions must be strictly validated. User A can only view their own orders; Rider B can only view orders they accepted; Admin C can access the backend.

4. Interface Prototype (Key Page Description)

"SchoolDash" includes three main front-end applications (User End, Admin End, Rider End). Interfaces should be intuitive, easy to use, and responsive.

4.1 Home Page (User End)

Description: The main entry point for the user end, providing product categories and recommendations.

Interface Components:

Top: On-campus delivery address (e.g., XX Campus - XX Dorm), "XX-Minute Delivery" promise.

Middle: Search bar, product category grid (Snacks, Drinks, Daily...), promo Banner, popular product feed.

Bottom: Tab Bar (Home, Categories, Cart, Me).

4.2 Product List/Detail Page (User End)

Description: Displays product information and allows adding to cart.

Interface Components:

List Page: Left side for sub-categories, right side for product card grid.

Product Card: Includes image, name, price, "+" (quick add) button.

(Optional) Detail Page: A modal or new page showing more images and details.

4.3 Cart Page (User End)

Description: The page where users edit selected products before checkout.

Interface Components:

Top: Product list (with checkbox, quantity stepper, delete button).

Bottom (Fixed): "Select All" checkbox, Total Amount (real-time calculation), "Checkout (N)" button.

Status: If minimum order value is not met, the button is grayed out with a tip "N more to go."

4.4 Order Confirmation Page (User End)

Description: The final step for the user to submit an order.

Interface Components:

Top: Delivery address card (switchable).

Middle: Product list (summary), delivery fee, coupons, remarks box.

Bottom (Fixed): Total payable amount, "Submit Order" button.

4.5 Order Detail (Status Tracking) Page (User End)

Description: Allows users to track order status after payment.

Interface Components:

Top: Order Status Diagram (Pending Acceptance -> Packing -> Delivering -> Delivered).

Middle: Delivery info (Rider info, contact), product list.

Bottom: Action buttons (e.g., Cancel Order, Order Again, Review).

4.6 Admin - Order Kanban (Admin End)

Description: The core interface for supermarket admins to process orders.

Interface Components:

Layout: Multi-column Kanban board (Trello style).

Columns: "Pending Acceptance" (new orders flash here with sound), "Packing," "Pending Pickup," "Delivering."

Card: One card per order, showing building, room number, and order summary.

Actions: Click "Accept" or "Call Rider" buttons on the card, or drag the card to the next column.

4.7 Rider - Order Taking Page (Rider End)

Description: The interface for riders to receive and process tasks.

Interface Components:

Status Switch: "On Duty / Off Duty" toggle at the top.

Order List: New order modal (dispatch) or order pool list (grab).

Order Detail: After accepting, clearly shows "Pick up" (supermarket address) and "Deliver" (Dorm-Room), and product list.

Action Buttons (Prominent): "I have Picked Up", "I have Delivered".

5. Function Description and Acceptance Verification Standards

5.1 Detailed Function Description

5.1.1 User Module

Description: Manages user identity and basic information.

Functions:

Login/Register: Via phone + code/password.

Address Management: CRUD for on-campus addresses, set default.

Personal Center: View order history, modify profile.

Acceptance: See 5.3 and 5.4

5.1.2 Product Module

Description: Manages and displays products.

Functions:

User End: Browse categories, search by keyword, view details.

Admin End: CRUD for products, list/delist, modify stock.

Acceptance: See 5.3 and 5.4

5.1.3 Cart Module

Description: A temporary storage area for user-selected products.

Functions:

Add/Remove/Update products.

Real-time total price calculation.

Verify stock and minimum order value at checkout.

Acceptance: See 5.3 and 5.4

5.1.4 Order Module

Description: Handles the entire transaction flow from placing, paying, to completion.

Functions:

Create Order (lock stock), Payment (10-min countdown).

Order auto-cancel on timeout (release stock).

User views order list and status details.

User can perform actions like "Cancel" (pending payment) or "Review" (delivered).

Acceptance: See 5.3 and 5.4

5.1.5 Admin Backend Module

Description: The operational platform for the supermarket side.

Functions:

Order Processing: View new orders, accept orders, dispatch.

Product Management: (See 5.1.2).

Rider Management: View rider status, manually assign orders.

Acceptance: See 5.3 and 5.4

5.1.6 Delivery (Rider) Module

Description: The fulfillment tool for the rider side.

Functions:

Status Switch: On Duty / Off Duty.

Order Reception: Grab / Dispatched.

Status Update: Click "Picked Up," "Delivered."

Acceptance: See 5.3 and 5.4

5.2 Input/Output Format

Input:

All requests from C/P/B ends to the backend use application/json format.

Use POST for login, etc., and GET for queries.

Output:

All data returned from the backend to the three ends is in application/json format.

Follows a unified response structure: { "code": 0, "message": "success", "data": { ... } } or { "code": 5001, "message": "Insufficient stock", "data": null }.

5.3 Interface Acceptance Criteria

Home Page: Product categories and lists must display correctly, add-to-cart buttons must be clickable.

Cart: When quantity is changed, the total amount at the bottom must update in real-time (no delay).

Order Confirmation (Checkout): Must correctly display the default address, and the total amount (including delivery fee) must be calculated correctly.

Admin Order Kanban: New orders ("Pending Acceptance") must appear on the kanban within 5 seconds, with a visual/audio cue.

Rider End: "On Duty/Off Duty" switch must function correctly. "Picked Up" / "Delivered" buttons must be clickable and trigger API requests.

5.4 Functional Acceptance Criteria

Inventory (Core):

When product stock is 1, User A adds 1 to cart. User B fails to add, receiving "Insufficient stock."

User A submits the order (stock locked to 0). User B views the product list, it shows "Sold Out."

User A does not pay within 10 minutes, the order is canceled, and stock is released back to 1.

User C can now purchase the product.

Order Status (Core):

User pays successfully. Order status becomes Pending Acceptance. Admin kanban shows a new order.

Admin clicks "Accept Order." Order status becomes Packing.

Rider clicks "Picked Up." Order status becomes Delivering.

Rider clicks "Delivered." Order status becomes Delivered.

(At each step, the user's order detail page status should refresh in near-real-time.)*

Minimum Order Value:

Set minimum order value to 20. When user's cart total is 15, the "Checkout" button is grayed out and shows "5 more to go."

Permissions:

When not logged in, users can browse products, but clicking "Add to Cart" or "Me" must redirect to the login page.

Using Student A's Token, attempting to query Student B's order details must fail (API should return 403 or 404).