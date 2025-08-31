graph TD
    %% Define the main components and subgraphs
    subgraph "1. Data Sources"
        direction LR
        A[Legacy Media Library]
        B[External Data Feeds]
        E[User Events]
    end

    subgraph "2. Ingestion & Processing"
        direction LR
        C[Cloud Storage]
        G{Cloud Functions / Cloud Run}
        H[BigQuery]
    end

    subgraph "3. AI & Analytics"
        direction LR
        J[Vertex AI]
        K[GenAI for Content Creation]
        L[Dynamic Pricing Model]
        M[Recommendations/Search]
        N[Chatbot]
        O[Bias Monitoring]
        P[Looker]
    end

    subgraph "4. User-Facing Applications"
        direction LR
        Q[Website/Mobile Apps]
        R[Microservices]
        S[User Auth]
    end

    subgraph "5. Monitoring & Security"
        direction LR
        T[Cloud Monitoring]
        U[Cloud Logging]
        V[IAM]
        W[Cloud DLP]
        X[Marketing Platforms]
    end

    %% Define the data and control flows
    A -- Content Migration --> C
    B -- Market Data --> G
    E -- User Actions --> G
    G -- Processed Data --> H
    H -- Analytics Data --> P
    H -- Training Data --> J
    J -- Model Garden --> K
    J -- Prediction --> L
    J -- Search for Media --> M
    J -- Agent Builder --> N
    J -- Fairness Indicators --> O
    L -- Price API --> R
    M -- Search API --> R
    N -- Chatbot API --> R
    K -- AI Content --> C
    P -- Insights --> X
    C --> V
    H --> V
    J --> V
    T -- Monitoring Metrics --> T
    U -- Log Data --> U
    V -- Access Control --> {C, H, J, T, U, W, X}
    W -- Data Protection --> {C, H}
    S -- Auth Data --> R
    S -- Auth Requests --> Q
    X -- GA4/Ad Manager Integration --> Q
    Q -- User Data --> E

    %% Connect the layers
    A -- Content Migration --> C
    B -- Ingestion --> G
    E -- Real-time --> G
    G -- Transformed Data --> H
    H -- Analytics Data --> P
    H -- Training Data --> J
    J -- Model Serving --> Q
    K -- Generated Content --> C
    P -- BI --> X
    Q -- User Interface --> Q
    R -- API --> Q
    S -- Authentication --> R
    T -- Observability --> V
    U -- Logging --> V
    V -- Security --> W
    W -- DLP --> H
    X -- Marketing Campaigns --> Q
