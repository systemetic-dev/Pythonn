### Pythonn
### In this i practice how to write clean code
       Basics clear
     • if-else 
     • loops
     • functions and recursion 
     • Lists
     • Tuples
     • Classes, Objects(instance), inheritance , abstraction , polymorphism,
     • virtual environment
     • pip
# now moving to advanced 

Key concepts of HTTP for backend engineers:

1. HTTP Introduction and Core Principles (0:00 - 5:48)
Statelessness: HTTP has no memory of past interactions. Each request is self-contained and must carry all necessary information (headers, auth tokens) for the server to process it. Benefits include simplicity and scalability (requests can be distributed across multiple servers).
Client-Server Model: The client (browser/app) initiates communication, and the server processes the request and sends a response (HTML, JSON, etc.).

2. Evolution of HTTP (5:49 - 7:30)
HTTP/1.0: Opened a new TCP connection for every request/response, which was inefficient.
HTTP/1.1: Introduced persistent connections (keep-alive), allowing multiple requests over one TCP connection. Added chunked transfer and caching mechanisms.
HTTP/2.0: Introduced multiplexing (multiple requests over one connection), binary framing, header compression, and server push.
HTTP/3.0: Built on the QUIC protocol (over UDP instead of TCP) for faster connection establishment and better handling of packet loss.

3. HTTP Messages Structure (7:31 - 9:08)
Request: Contains Method, URL, Version, Headers, and optional Body.
Response: Contains Version, Status Code, Headers, and optional Body.
A blank line separates headers from the body.

4. HTTP Headers (9:09 - 16:22)
Headers are key-value pairs representing metadata.
Request Headers: `User-Agent` (client type), `Authorization` (credentials), `Accept` (preferred content types).
Response Headers: `Content-Type` (data format), `Set-Cookie` (session management).
Security Headers: `Content-Security-Policy` (prevents XSS), `X-Frame-Options` (prevents clickjacking), `X-Content-Type-Options` (prevents MIME sniffing).
Headers offer extensibility and act as remote control instructions for the server.

5. HTTP Methods and Idempotency (16:23 - 20:06)
Methods define the intent of the action.
Idempotent Methods: Multiple identical requests have the same effect as a single request (`GET`, `PUT`, `DELETE`, `HEAD`, `OPTIONS`).
Non-Idempotent Methods: Multiple requests may result in different states (`POST` creates new resources each time).

6. OPTIONS Method and CORS (20:07 - 38:50)
CORS (Cross-Origin Resource Sharing): A browser security mechanism protecting cross-origin requests.
Pre-flight Request (`OPTIONS`): The browser sends a pre-flight `OPTIONS` request to check if the server allows the actual request (e.g., a `PUT` request with custom headers) from the specific origin.
CORS Headers: `Access-Control-Allow-Origin`, `Access-Control-Allow-Methods`, `Access-Control-Allow-Headers`.
Max-Age: Caches pre-flight results to improve performance.

7. Response Status Codes (38:51 - 55:19)
2xx (Success): `200 OK`, `201 Created`, `204 No Content` (e.g., successful pre-flight).
4xx (Client Errors): `400 Bad Request`, `401 Unauthorized`, `403 Forbidden` (no permission), `404 Not Found`, `409 Conflict` (resource already exists).
5xx (Server Errors): `500 Internal Server Error`, `502 Bad Gateway`, `503 Service Unavailable`, `504 Gateway Timeout` (upstream server failed to respond).

8. HTTP Caching (55:20 - 1:02:28)
Stores responses to reduce server load and latency.
Cache-Control: Defines how long a resource is cached (`max-age`).
ETag: A hash identifier for a version of a resource. The client sends this back in subsequent requests (`If-None-Match`) to check if the resource has changed.

9. Content Negotiation and Compression (1:02:29 - 1:08:50)
Negotiation: Client specifies preferences via headers (`Accept` for type, `Accept-Language`, `Accept-Encoding`).
Compression: Servers compress data (e.g., `gzip`) if supported by the client to reduce payload size.

10. Persistent Connections and Large Data (1:08:51 - 1:15:17)
Keep-Alive: Explicit header to maintain connections.
Multipart Data: Used for uploading large files (binary data) in parts.
Chunked Transfer: Server sends large responses in chunks rather than all at once (often used with `Transfer-Encoding: chunked`).

11. SSL, TLS, and HTTPS (1:15:18 - End)
SSL/TLS: Protocols for encrypting data in transit to prevent interception.
HTTPS: HTTP running over a TLS connection.

The concept of routing in backend development, focusing on how requests find their destination on a server. Routing maps a specific URL path and HTTP method to a particular handler or instruction set that processes the request.

### Core Concepts of Routing
Intent vs. Location: While HTTP methods express the "what" (action/intent) of a request (e.g., GET, POST), routing expresses the "where" (location/resource) (0:09-0:46).
Mapping: Routing is the process of mapping a combination of an HTTP method and a URL path to specific server-side logic (1:55).

### Types of Routing
1.  Static Routes (4:35): Routes with fixed, constant paths that do not change based on user input. They always return the same type of data.
Example: `GET /api/books` fetches a list of books (2:17).
Example: `POST /api/books` creates a new book (3:19).
2.  Dynamic Routes (5:24): Routes that contain variable parameters, allowing the server to extract information directly from the URL to perform actions on specific resources.
Path Parameters (8:45): Variables embedded directly in the path, usually denoted by a colon (e.g., `:id`).
Example: `GET /api/users/123` uses `123` as the user ID to fetch specific user details (5:30).
3.  Query Parameters (9:09): Key-value pairs appended to the end of a URL after a question mark (`?`) to provide additional information, filter results, or send metadata, commonly used in GET requests to avoid using a body.
Example: `GET /api/search?query=some+value` passes `some value` to the search function (9:13).
Use Case: Pagination (`/api/books?page=2&limit=20`) to fetch specific chunks of data (12:44).
4.  Nested Routes (15:09): A practice used to represent hierarchical relationships between resources semantically.
Example: `GET /api/users/123/posts/456` fetches a specific post (`456`) belonging to a specific user (`123`) (15:57).

### Advanced Concepts
Route Versioning (18:54): Including version numbers (e.g., `v1`, `v2`) in the URL path to manage breaking changes and allow clients time to migrate to new APIs (19:13).
Catch-All Route (22:18): A fallback route (`/*`) configured to handle any requests that do not match defined routes, typically returning a friendly "404 Not Found" message rather than a generic error.

Serialization and Deserialization for Backend Engineers:

1. Introduction to Client-Server Communication (0:00 - 1:24):
Front-end (Client): Typically a browser (like Chrome) running a JavaScript app (React, Angular, Vue).
Back-end (Server): Runs remotely (AWS, GCP, Azure) or locally, potentially built with languages like Rust.
Communication: Clients send HTTP requests (GET, POST) containing URLs, headers, and body data to the server, which then responds.

2. The Problem: Data Compatibility (2:29 - 6:01):
Different systems use different data types (e.g., JavaScript is dynamic, Rust is statically typed).
Challenge: How to transmit data from one language's memory structure to another machine over the internet so it remains understandable and usable.
OSI Model Overview: At a high level, data moves from the Application Layer (where data is structured) down to the Physical Layer (bits) for transmission, and reverses on the receiving side.

3. The Solution: Serialization Standards (6:03 - 9:15):
Definition: Serialization is converting data from a programming language format into a common, neutral format for transmission or storage.
Deserialization is the reverse process: converting that common format back into a usable data structure on the receiving end.
Goal: To be language-agnostic and machine-agnostic.

4. Popular Serialization Types (9:16 - 12:56):
Text-Based Formats: Human-readable. Popular examples include JSON (JavaScript Object Notation), YAML, and XML.
Binary Formats: Not human-readable, but more compact and efficient. Examples include Protobuf (Protocol Buffers) and Avro.
Note: The video focuses on JSON as it is used in ~80% of HTTP-based communication.

5. Deep Dive into JSON (13:00 - 16:08):
Structure: Uses opening and closing braces `{}`, similar to JavaScript objects.
Rules:
Keys must be strings enclosed in double quotes.
Values can be strings, numbers, booleans, arrays, or nested objects.
Example:
    
    {
      "name": "John",
      "age": 30,
      "address": {
        "country": "India",
        "phone": 123456
      }
    }
    

6. Demo: Practical Application (16:09 - 21:03):
Scenario: A POST request to `/api/books`.
Request Body (Serialization): The client converts a JS object into a JSON string and sends it.
OSI Mapping: Application layer data becomes JSON, then gets converted through network layers into packets, then bits for transmission (17:26).
Server Processing (Deserialization): The Rust server receives the data, converts it back from JSON into a Rust struct to perform business logic (19:04).
Response: The server serializes the result back into JSON to send to the client (19:41).

7. Summary (21:04 - end):
Serialization and Deserialization are essential techniques for ensuring data is understandable across different languages and environments.

Authentication and Authorization for backend engineers, covering their definitions, historical evolution, modern implementations, and best practices. The video emphasizes that these are foundational security concepts for building robust applications.

### 1. Fundamental Concepts (0:00 - 18:27)
Authentication (AuthN): The process of verifying who a user is within a given context (platform, operating system, etc.) (0:24-0:53).
Authorization (AuthZ): The process of determining what a user is allowed to do (permissions, capabilities) after they have been authenticated (0:59-1:22).
Evolution of Authentication:
Medieval Period: Relied on personal recognition and later, physical seals to vouch for identity independently of direct acquaintance (3:48-5:39).
Pre-Digital Era: Evolved into passwords/passphrases, relying on the principle of "something you know" (7:43-8:36).
Digital Era (Mainframes): Initiated in the 1960s. A pivotal moment occurred in 1961 at MIT when a plain-text password file was printed, highlighting the critical need for secure password storage, leading to the adoption of hashing (8:43-14:59).
Modern Era: Demand for advanced frameworks driven by cloud computing, mobile devices, and API-based architectures (15:00-16:50).

### 2. Core Technical Components (18:27 - 41:10)
Sessions: Since HTTP is stateless, sessions were developed to maintain user state across requests. The server creates a session on authentication and sends a Session ID to the client (19:04-20:11).
Cookies: Small pieces of data stored by the browser. They are used to automatically send tokens (like Session IDs or JWTs) back to the server with subsequent requests (20:13-22:50).
JSON Web Tokens (JWT): A stateless authentication mechanism. A JWT is a self-contained, signed token containing user data (payload), metadata (header), and a signature for verification (22:53-39:46).
Payload Fields: `sub` (subject/user ID), `iat` (issued at), and custom fields like `role` or `name` (30:00-30:57).

### 3. Types of Authentication (41:10 - 1:19:00)
Stateful Authentication: Server stores session data (often in Redis for speed). Pros: Centralized control, easy to revoke sessions. Cons: Scalability issues in distributed systems (42:04-46:27).
Stateless Authentication: Server does not store session data; the JWT itself contains necessary info. Pros: Highly scalable, no server-side storage costs. Cons: Difficult to revoke tokens immediately (46:28-48:05).
API Keys: Used for machine-to-machine communication where programmatic requests need identification without a human user interface (54:37-58:00).
OAuth 2.0 & OpenID Connect (OIDC): Solved the problem of delegation (allowing one app to access resources from another on behalf of a user) and authentication fatigue (58:01-1:11:00).
OAuth 2.0 is for Authorization (delegation).
OIDC is built on top of OAuth 2.0 to handle Authentication, introducing the ID Token (usually a JWT) (1:11:01-1:14:00).
Flow: Client redirects user to Auth Server -> User authenticates -> Auth Server sends Authorization Code -> Client exchanges code for Access Token and ID Token (1:14:03-1:18:00).

### 4. Authorization in Detail (1:19:00 - 1:35:57)
Role-Based Access Control (RBAC): Assigning permissions based on user roles (e.g., Admin, User, Moderator) rather than individual users (1:24:50-1:26:00).
Implementation: The server deduces the role from the token (JWT) or a database lookup in the request cycle and restricts access to specific resources based on that role (1:26:08-1:27:38).
Forbidden Errors: If a user lacks permission, the server returns a 403 Forbidden status code (1:27:25).
Security Best Practices:
Generic Error Messages: Avoid revealing specific reasons for authentication failure (e.g., use "Invalid email or password" instead of "User not found") to prevent attackers from enumerating valid users (1:28:02-1:29:15).
Timing Attacks: Attackers can measure how long a server takes to respond to infer if a username exists. Countermeasures include using constant-time comparison functions for hashes or simulating a response delay to normalize response times (1:34:40-1:35:46).

The critical role of validation and transformation pipelines in backend application development, focusing on data integrity and security. The speaker details the layered architecture of a backend app and how data flows through it (0:00 - 3:50).Backend Architecture Layers: (0:33)
Repository Layer (Bottom): Manages database connections, queries, insertions, and deletions (relational or NoSQL) (0:33-0:55).
Service Layer (Middle): Executes core business logic, calls repository methods, handles notifications, and triggers webhooks (0:59-1:44).
Controller Layer (Top): Handles HTTP-related stuff (error codes, success status), manages incoming client data, calls the service layer, and returns formatted data to the user (1:48-3:28).Where Validations & Transformations Occur: (3:53)
These processes happen at the entry point of the controller layer, immediately after the route is matched and before any business logic is executed (3:56-4:58).
The goal is to ensure incoming data (JSON payload, query/path parameters, headers) matches the expected format to prevent system failure (5:03-7:28).Types of Validation: (15:42)
1. Syntactic Validation: Checks if data follows a specific structure or pattern (e.g., email address format, phone number digits, date formats like YYYY-MM-DD) (15:58-17:59).
2. Semantic Validation: Checks if the data makes logical sense (e.g., date of birth cannot be in the future, age cannot be 365 years) (17:59-19:35).
3. Type Validation: Ensures the data type is correct (e.g., string, number, boolean, array) (19:38-20:38).Transformation and Casting: (20:42)
Transformation involves manipulating or converting data into a required format before validation or processing (21:24-21:38).
Example: Query parameters are received as strings by default, but need to be cast (type-casted) into numbers for validation or database queries (23:15-25:15).Advanced/Complex Validation Examples: (30:29)
Password Matching: Ensures the `password` and `confirmPassword` fields are identical (31:06-31:27).
Conditional Validation: If a `married` field is `true`, a `partnerName` field becomes mandatory (31:58-33:05).Frontend vs. Backend Validation: (37:24)
Frontend Validation: Essential for User Experience (UX); provides immediate feedback to the user (38:43-39:02).
Backend Validation: Mandatory for Security and Data Integrity; prevents malicious or corrupt data from reaching the database (39:04-39:35).
Crucial Takeaway: Never trust the client. Backend validation must exist independently of frontend validation, as direct API hits (via tools like Postman/Insomnia) bypass frontend checks (39:37-40:48).

The backend request lifecycle, explaining how a request travels from the client, through the server, and back. The instructor breaks down the responsibilities of controllers, services, repositories, middlewares, and request context.

### 1. Request Lifecycle & Architecture (0:00 - 3:42)
Goal: Understand what happens inside a server after receiving an HTTP request (1:37) and before sending a response.
Initial Entry: The request reaches the server via a specific port (3:08).
Routing: The server matches the incoming URL path (e.g., `/users`) to a specific Handler/Controller function (3:18).
Design Pattern: While not mandatory, separating code into Handlers, Services, and Repositories ensures a scalable, maintainable, and debuggable codebase (3:42).

### 2. Handlers/Controllers Layer (4:17 - 26:50)
Core Responsibility: Handling the HTTP protocol aspects (receiving input and sending output) (5:25).
Components: Receives `request` and `response` objects from the framework (5:03).
Data Extraction & Deserialization: Takes JSON from the request body or query parameters and converts it into a native data format (struct, class) (10:04).
Example: In Go, parsing JSON into a struct; in Node.js, body-parser usually handles this before the controller (10:13).
Error Handling: If parsing fails, the controller immediately returns a 400 Bad Request (11:15).
Validation & Transformation: Ensures the data is valid (missing fields, wrong formats) and shapes it for downstream layers (13:12).
Example: Setting default values for optional query parameters like sorting (`?sort=name` or `?sort=date`) (14:32).
Delegation: Calls the Service Layer with the prepared data (20:18).

### 3. Service Layer (18:00 - 20:30)
Core Responsibility: Business logic orchestration (20:30).
Functions:
Performs operations that don't require a database (e.g., sending emails or notifications) (20:20).
Orchestrates Repository Layer calls (fetching, combining, and processing data) (23:05).
Logic: This is where the actual functionality of the API resides (23:55).

### 4. Repository Layer (20:50 - 24:30)
Core Responsibility: Database interactions (21:10).
Functions: Constructs and executes database queries (SQL, NoSQL) to insert, fetch, or delete data (21:40).
Best Practice: Follows a single-responsibility principle—one method should do one thing (e.g., `GetAllBooks()` vs `GetBookById()`) (22:15).

### 5. Middlewares (26:50 - 50:57)
Core Responsibility: Executing common tasks for many routes before they reach the controller (35:32).
The `next()` Function: Middlewares accept `req`, `res`, and a `next` function to pass execution to the next layer (30:26).
Common Use Cases:
CORS (Cross-Origin Resource Sharing): Handles security headers to allow/block requests from different domains (37:15).
Authentication/Authorization: Verifies user tokens (JWT, session IDs) before allowing access to a resource (41:51).
Rate Limiting: Protects the server from excessive requests by checking IP addresses and returning 429 Too Many Requests if limits are exceeded (43:18).
Logging & Monitoring: Tracks request paths, methods, and status codes for debugging (45:47).
Global Error Handling: A specialized middleware that catches errors from any layer and returns a properly formatted response (49:50).
Order Matters: Security middlewares (like CORS) should run first to stop malicious requests early (50:18).

### 6. Request Context (50:57 - 59:57)
Core Responsibility: Sharing state/data across different layers and middlewares within a single request (51:56).
Functions:
User Information: Stores user ID or roles determined by the authentication middleware, making them available to the controller/service without passing them directly (55:18).
Security: Prevents clients from spoofing user IDs in database queries by extracting the ID from the trusted context rather than the raw request body (56:11).
Tracing: Stores a unique Request ID (UUID) to log and track the request across microservices (57:56).
Cancellation: Sends cancellation signals or deadlines to downstream services to prevent hanging requests (59:31).

Guide to REST API design from a backend engineering perspective, covering theoretical foundations, practical implementation patterns, and best practices for creating intuitive interfaces.

Introduction and Context (0:00 - 15:00)
Purpose: To standardize API design rules and guidelines to avoid common confusion among developers (0:46).
The Goal: Focus on business logic rather than worrying about REST standards during execution (4:01).
History of the Web: Tim Berners-Lee initiated the World Wide Web in 1990, inventing URIs, HTTP, and HTML (4:55).
Evolution of Standards: The transition from Multi-Page Applications (MPAs) to Single Page Applications (SPAs) changed how APIs are consumed, moving toward JSON-heavy, client-side rendering (2:30).

REST Architectural Style (10:00 - 20:41)
Coined by Roy Fielding in his PhD dissertation in 2000 (13:50).
Core Constraints:
    1. Resource Identification: Using URIs to identify resources (9:49).
    2. Manipulation Through Representations: Clients manipulate resources via representations (e.g., JSON) rather than accessing the database directly (9:51).
    3. Self-Descriptive Messages: Messages contain metadata explaining how to process them (9:52).
    4. HATEOAS: Hypermedia as the Engine of Application State (9:55).
    5. Uniform Interface: Consistent interface across services (10:01).
    6. Layered System: Allows for intermediate components like load balancers (10:11).
    7. Cache: Responses must define if they are cacheable to improve efficiency (10:46).
    8. Statelessness: Each request must contain all information necessary for the server to understand and process it (11:17).

URL Design Patterns (21:54 - 31:00)
Structure: `Scheme` (http/https), `Authority` (domain/IP), `Path` (resource hierarchy), `Query Parameters` (sorting/filtering) (21:56).
Best Practices: Use plural nouns for resources (e.g., `/books`, not `/book`) to represent collections (27:54).
Naming: Use lower-case, hyphen-separated words (kebab-case) for readability in URLs (29:36).
Hierarchy: Forward slashes indicate hierarchical relationships (e.g., `/books/123/reviews`) (29:51).

HTTP Methods and Idempotency (31:03 - 53:13)
Idempotency: The property where performing the same action multiple times has the same effect as performing it once (31:19).
CRUD Operations:
GET: Retrieve data (Idempotent) (32:53).
POST: Create a new resource (Not idempotent) (32:55).
PUT: Replace a resource (Idempotent) (32:58).
PATCH: Partially update a resource (Not strictly idempotent, but often treated as such) (33:00).
DELETE: Remove a resource (Idempotent) (33:02).

Practical API Design Workshop (53:13 - end)
Scenario: Designing an API for a Project Management SaaS (similar to Jira or Linear) (53:17).
Steps: Identify nouns (Organizations, Projects, Tasks), design database schema, and design API endpoints using Insomnia (58:02).
Organization Endpoints:
`POST /organizations` - Create (102:36).
`GET /organizations` - List all (including pagination parameters `limit` and `page`) (105:36).
`GET /organizations/:id` - Fetch one (107:05).
`PATCH /organizations/:id` - Partial update (124:17).
`DELETE /organizations/:id` - Delete (137:16).
Project Endpoints:
Consistent patterns applied to projects (139:35).
`POST /projects` - Create (140:12).
`GET /projects/:id` - Fetch one (150:09).
Custom Actions: `POST /projects/:id/clone` - Used for non-CRUD actions like cloning a project with all its tasks (153:48).

API Best Practices (196:00 - end)
Interactive Documentation: Use tools like Swagger/OpenAPI for testing and documentation (196:51).
Consistency: Maintain consistent payload structures (CamelCase for JSON) across all resources (197:34).
Sensible Defaults: Define default values on the server side (e.g., default status 'active') to make client requests simpler (199:53).
Avoid Abbreviations: Use clear, verbose field names (e.g., `description`, not `desc`) (200:35)

Introduction to databases and data persistence for backend development, using PostgreSQL as the primary example.

Introduction to Data Persistence (0:00 - 1:55)
What is a database? It is a way to persist information across different sessions so that data survives even after the application stops running (0:27).
Why is it crucial? Without persistence, users would lose all progress, such as completed tasks in a to-do list app, every time they closed the app (1:38).
Broad Definition: A database is simply a structured storage system that allows you to create, read, update, and delete (CRUD) data (3:25).
Examples of databases: Smartphone contact lists, browser `localStorage`, and even a simple text file for taking notes (2:10 - 3:11).

Disk-Based Databases vs. Caching (3:50 - 8:26)
Backend Databases: In backend engineering, we specifically refer to disk-based databases (hard drives or SSDs) (4:13).
Disk vs. RAM:
RAM (Main Memory): Extremely fast but expensive and volatile (loses data on power loss) (4:42).
Disk (Secondary Memory): Slower but cheaper and persistent (5:18).
Trade-off: We choose disk storage to handle massive amounts of data efficiently without high costs (7:18).
Caching: Technologies like Redis store data in RAM for extreme speed, used specifically for frequently accessed data, not as primary storage (8:00).

Database Management Systems (DBMS) (8:40 - 25:50)
Definition: A DBMS is software designed to efficiently manage data storage, retrieval, and manipulation (9:29).
Responsibilities:
    1.  Data Organization: Efficiently storing data for quick access (10:13).
    2.  Access: Providing CRUD operations (10:25).
    3.  Integrity: Ensuring the accuracy and validity of data (e.g., ensuring a payment field only accepts numbers, not text) (10:34).
    4.  Security: Protecting data from unauthorized access (12:09).
Why not just use files?
Parsing: Writing code to manually parse text files is slow and error-prone (13:05).
Lack of Structure: Text files cannot enforce data consistency (14:49).
Concurrency: Handling multiple users updating the same file simultaneously is complex (15:37).
Relational vs. Non-Relational (23:10): The video focuses on Relational Database Management Systems (RDBMS), which organize data into structured tables.

Why PostgreSQL? (26:30 - 32:45)
Open Source: Free to use and inspect (26:34).
SQL Standard: Sticks closely to SQL standards, making it easy to migrate to other systems like MySQL if necessary (26:58).
Extensible: Highly customizable with extensive documentation (28:01).
Json Support: Excellent support for Json and JsonB data types, offering flexibility similar to non-relational databases (28:36).

PostgreSQL Data Types Demo (32:45 - 53:23)
`serial` / `bigserial`: Auto-incrementing integers, typically used for primary key IDs (34:15).
`numeric` / `decimal`: Exact numeric types, essential for financial data where accuracy is critical (37:40).
`real` / `double precision`: Floating-point numbers, used for speed when exact precision isn't necessary (40:00).
`char` / `varchar` / `text`: String types. Character pads extra spaces, Varchar has a length limit, and Text has no limit. The video recommends using `text` for better performance and simplicity (40:38 - 45:00).
`boolean`: True or False values (50:18).
`date` / `time` / `timestamp`: For storing temporal data (50:24).
`json` / `jsonb`: For storing structured Json data. Jsonb is faster to process (53:04).

Database Migrations (56:00 - 1:02:22)
What are they? A version control system for your database schema (56:30).
Why use them? They track changes to the database structure (tables, columns, indexes) over time (56:56).
Up & Down Migrations: `up` applies changes, `down` reverts them (57:00).

Project Management Platform Modeling (1:02:22 - 1:41:00)
Tools: Using DbMate for migrations and TablePlus for GUI database management (1:02:30 - 32:50).
Defining `enum` Types: Creating custom types for constrained values like `userrole` (admin, member) or `taskstatus` (open, closed) (1:05:00).
Designing Tables:
`users`: Basic user information (1:09:00).
`projects`: Associated with a creator (1:15:30).
`tasks`: Connected to projects and assigned to users (1:20:00).

Seeding Test Data (1:41:00 - 1:44:00)
Seeding: The process of inserting dummy data into the database for development and testing purposes (1:41:20).

API Interaction & SQL Queries (1:52:30 - End)
Parameterized Queries: A crucial security mechanism to prevent SQL Injection attacks by separating SQL code from user-provided data (1:53:40).
Indexes: Database objects that drastically speed up data retrieval, similar to an index in a book (2:21:30).
Triggers: Automatic actions that occur when a specific event happens in the database, such as automatically updating a `updated_at` timestamp whenever a row is modified (2:41:00 - 2:43:40).
    
