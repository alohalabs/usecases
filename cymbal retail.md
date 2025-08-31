```mermaid
graph TD
    %% Define the main components and subgraphs
    subgraph "1. User-Facing Applications"
        direction LR
        A[Customer Website/App]
        B[Real-Time Events]
    end

    subgraph "2. Data Ingestion & Storage"
        direction LR
        C[Product Catalog]
        D[Cloud Storage]
        E[Pub/Sub]
        F[BigQuery]
        G[Cloud Spanner]
    end

    subgraph "3. AI & Analytics Services"
        direction LR
        H[Vertex AI Search for commerce]
        I[Vertex AI Agent Builder]
        J[Vertex AI Gemini Models]
        K[Vertex AI Forecasting]
        L[Looker]
    end

    subgraph "4. E-commerce Platform"
        direction LR
        M[Global Load Balancer]
        N[Cloud Run / GKE]
    end

    subgraph "5. Monitoring & Security"
        direction LR
        O[Cloud Monitoring / Logging]
        P[Cloud DLP]
        Q[IAM]
        R[VPC Service Controls]
    end

    %% Define the data and control flows
    A -- User Interaction --> B
    A -- API Calls --> M
    B -- Streaming Events --> E
    C -- Ingestion Pipeline --> F
    C -- Product Images --> D
    D -- New Images --> J
    E -- Processed Events --> F
    H -- Recommendations/Search API --> M
    I -- Chatbot API --> M
    J -- Product Metadata --> F
    J -- Automated Descriptions --> C
    K -- Forecasts --> F
    F -- BI Queries --> L
    L -- Dashboard Access --> A
    M -- Routing --> N
    N -- Read/Write --> G
    N -- Call AI Services --> H
    N -- Call AI Services --> I
    F -- DLP Scan --> P
    G -- DLP Scan --> P

    %% Expand grouped edges for Q (IAM)
    Q -- Access Control --> H
    Q -- Access Control --> I
    Q -- Access Control --> J
    Q -- Access Control --> K
    Q -- Access Control --> L
    Q -- Access Control --> O
    Q -- Access Control --> P
    Q -- Access Control --> F
    Q -- Access Control --> G
    Q -- Access Control --> D

    %% Expand grouped edges for R (VPC Service Controls)
    R -- Security Perimeter --> H
    R -- Security Perimeter --> I
    R -- Security Perimeter --> J
    R -- Security Perimeter --> K
    R -- Security Perimeter --> P
    R -- Security Perimeter --> F
    R -- Security Perimeter --> G

    O -- Log Analysis --> Q
    O -- Metrics/Alerts --> Q

    %% Connect the layers
    subgraph "Overall Flow"
        direction TB
        subgraph "Data & Analytics Pipeline"
            direction LR
            "1. User-Facing Applications" --> "2. Data Ingestion & Storage"
            "2. Data Ingestion & Storage" --> "3. AI & Analytics Services"
            "3. AI & Analytics Services" --> "2. Data Ingestion & Storage"
        end
        subgraph "Customer Journey"
            direction LR
            "1. User-Facing Applications" --> "4. E-commerce Platform"
            "4. E-commerce Platform" --> "3. AI & Analytics Services"
        end
        subgraph "Security & Operations"
            direction LR
            "5. Monitoring & Security" --> "1. User-Facing Applications"
            "5. Monitoring & Security" --> "2. Data Ingestion & Storage"
            "5. Monitoring & Security" --> "3. AI & Analytics Services"
            "5. Monitoring & Security" --> "4. E-commerce Platform"
        end
    end
```
