# Axieva_Product_Order_Management
Product Order Management

A simple full-stack Product Order Management application providing user authentication (JWT), product browsing with search/filter/pagination, and order creation/management. The project contains a Spring Boot backend and a React frontend.

Tech stack

	•  Backend: Java 17, Spring Boot (Web, Data JPA, Security, Validation), Maven
	•  Database: H2 (embedded) by default;
	•  Frontend: React 18, Redux, CSS
	•  HTTP client: Axios

Project structure (high level)

	•  src/main/java/... — Spring Boot backend sources (controllers, services, security)
	•  src/main/resources — application properties and data.sql (seed data)
	•  frontend/ — React frontend project
	•  pom.xml — Maven project file
	•  HELP.md — docs

Prerequisites

	•  Java 17+ and JAVA_HOME configured
	•  Node.js 18+ and npm 9+ (to run frontend)
	•  Maven (or use included Maven wrapper)
	•  (Optional) Postman or curl for API testing

Configuration notes

Important properties in src/main/resources/application.properties:

	•  server.port (default 8081)
	•  spring.datasource.* (H2 by default)
	•  jwt.secret and jwt.expiration-ms (development secret present;)
	•  spring.sql.init.mode=always ensures data.sql seeds DB at startup
Default frontend dev server: http://localhost:3000. If the frontend needs to talk to the backend, configure the API base URL in frontend/src/lib/api.js (defaults to http://localhost:8081/api).

CORS: backend is configured to allow cross-origin requests from frontend dev server.
Other API endpoints (summary)

	•  GET /api/products/{id} — Get product details
	•  POST /api/products — Create product (validated body)
	•  PUT /api/products/{id} — Update product
	•  DELETE /api/products/{id} — Delete product
	•  POST /api/orders — Create order (authenticated user)
	•  GET /api/orders — List orders (user-specific; admin sees all)

All non-/api/auth/** endpoints require a valid JWT Bearer token.

Data seeding

src/main/resources/data.sql inserts sample products. Useful for testing product listing and pagination.

Assumptions & design notes

	•  JWT tokens are returned on register/login and should be used as Bearer tokens for subsequent requests.
	•  Product stock and payment are modeled simply for demonstration purposes (no real payment provider).
	•  Admin-level behavior: orders endpoint returns all orders if user has ROLE_ADMIN; otherwise user sees own orders.

Troubleshooting & common issues

	•  401 Unauthorized: ensure Authorization: Bearer <token> header is present and token is valid (get token from /api/auth/login).
	•  Database errors: check application.properties and the console logs for schema or SQL initialization errors.
	•  Change server port with --server.port=PORT on startup if port conflicts occur.
	•  To clear and re-seed H2: stop server, delete H2 files (if any), and restart; data.sql will run on startup.

