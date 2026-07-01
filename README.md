# Be-ConnectUrPet

Dual-backend ecosystem designed to power [ConnectUrPet mobile application](https://github.com/AriSV05/fe-ConnectUrPet). To test the entire core logic was independently implemented across two distinct architectural paradigms:

1.  **Microservice/Monolith:** Built with **Spring Boot** and backed by **PostgreSQL**.
2.  **Serverless Architecture:** Built with **Google Cloud Functions** and backed by **Firebase/Firestore**.

Both services achieve **100% feature parity** and operate completely independent of each other, though their modular design allows for inter-service communication if required.

-> [ConnectUrPet - frontend service and specifications](https://github.com/AriSV05/fe-ConnectUrPet) <-

---
### Tech Stack & Internal Architecture

### 1. Spring Boot Service
Engineered following **Clean Architecture** and layered design principles to guarantee high maintainability and clear separation of concerns.

*   **Database & Persistence:** **PostgreSQL** handles complex relational data modeling. Managed via the **Repository Pattern** for decoupled data access.
*   **Data Isolation (Entities vs. DTOs):** Strict separation between database representation (`Entities`) and API contracts (`DTOs`). Built custom **Mappers** to isolate the data layer from external network delivery.
*   **Business Logic:** Encapsulated entirely within isolated `Services`.

### 2. Google Cloud Functions (Serverless Layer)
A highly scalable, low-maintenance implementation designed to handle unpredictable spike loads without infrastructure overhead.

*   **BaaS Integration:** Leverages **Firebase** for cloud data storage and real-time document synchronization.
*   **Event-Driven Execution:** Fully decoupled cloud functions triggered via HTTPS requests, mirroring every endpoint available in the Spring Boot counterpart.

---
> [!NOTE]
> While both backends live independently to serve as alternative data sources for the mobile frontend, they are designed with **inter-service communication** readiness. Thanks to standard REST/JSON protocols and shared DTO contracts, migrating this setup into a distributed microservices cluster (e.g., Spring Boot handling core logic while Cloud Functions handle specific event triggers) requires zero architectural refactoring.

---
### Deployment & DevOps Strategy

To ensure continuous delivery and automated hosting, both environments feature production-ready cloud deployment pipelines.

### Spring Boot on Heroku
The service includes a pre-configured deployment blueprint tailored for Heroku container or buildpack execution:
Includes environment variable routing for secure PostgreSQL credentials and database connection pooling.

### Serverless on Google Cloud Platform (GCP)
The serverless stack utilizes the Google Cloud CLI (`gcloud`) and Firebase Tools for automated deployment:
Functions are containerized natively by GCP and deployed to independent cloud endpoints.
