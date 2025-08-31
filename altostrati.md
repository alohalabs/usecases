
graph TD
    %% Define the main components
    subgraph "1. Data Sources"
        direction LR
        A[Legacy Media Library] -->|Migration| C
        B[External Data Feeds] -->|Ingestion| D
        E[User Events] -->|Real-time| F
    end

    subgraph "2. Ingestion & Processing"
        direction LR
        C[Cloud Storage] --> G{Cloud Functions / Cloud Run}
        B --> G
        E --> G
        G --> H[BigQuery]
        H --> J[Vertex AI]
    end

    subgraph "3. AI & Analytics"
        direction LR
        J[Vertex AI]
        J -- Model Garden --> K[GenAI for Content Creation]
        J -- Prediction --> L[Dynamic Pricing Model]
        J -- Search for Media --> M[Recommendations/Search]
        J -- Agent Builder --> N[Chatbot]
        J -- Fairness Indicators --> O[Bias Monitoring]
        H --> P[Looker]
    end

    subgraph "4. User-Facing Applications"
        direction LR
        Q[Website/Mobile Apps]
        Q -->|API| M
        Q -->|API| L
        Q -->|API| N
        Q -- GKE --> R[Microservices]
        R -- Identity Platform --> S[User Auth]
        S --> Q
    end

    subgraph "5. Monitoring & Security"
        direction LR
        T[Cloud Monitoring]
        U[Cloud Logging]
        V[IAM]
        W[Cloud DLP]
    end

    %% Define the data and control flows
    A -- Content Migration --> C
    B -- Market Data --> G
    E -- User Actions --> G
    G -- Processed Data --> H
    H -- Analytics Data --> P
    H -- Training Data --> J
    J -- Model Inference --> L
    J -- Recommendations --> M
    L -- Price API --> R
    M -- Search API --> R
    N -- Chatbot API --> R
    K -- AI Content --> C
    P -- Insights --> |Marketing| X[Marketing Platforms]
    C --> V
    H --> V
    T -- Monitoring Metrics --> T
    U -- Log Data --> U
    V -- Access Control --> {C, H, J, T, U, W}
    W -- Data Protection --> {C, H}
    X[Marketing Platforms] -- GA4/Ad Manager Integration --> Q
    Q -- User Data --> E

    %% Connect the layers
    subgraph "Overall Flow"
        style Overall Flow fill:#f9f,stroke:#333,stroke-width:2px
        direction TB
        subgraph "Data Pipeline"
            direction LR
            "1. Data Sources" --> "2. Ingestion & Processing"
        end
        subgraph "AI & Analytics Flow"
            direction LR
            "2. Ingestion & Processing" --> "3. AI & Analytics"
        end
        subgraph "Application Flow"
            direction LR
            "3. AI & Analytics" --> "4. User-Facing Applications"
        end
        subgraph "Monitoring & Security Flow"
            direction LR
            "5. Monitoring & Security" --> "1. Data Sources"
            "5. Monitoring & Security" --> "2. Ingestion & Processing"
            "5. Monitoring & Security" --> "3. AI & Analytics"
            "5. Monitoring & Security" --> "4. User-Facing Applications"
        end
    end
