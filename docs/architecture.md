# Platform architecture

The platform separates ingestion, storage, transformation, and validation so each layer can scale and fail independently.

```mermaid
flowchart TB
    subgraph Control
      CFG[(Source configuration)]
      KV[Managed secrets]
      OBS[Observability]
    end
    subgraph Ingestion
      FN[Serverless functions]
      AUTH[Pluggable authentication]
      API[REST and SOAP clients]
    end
    subgraph Data
      RAW[Immutable raw zone]
      SPARK[Distributed processing]
      DQ[Validation rules]
      CUR[Curated datasets]
    end
    CFG --> FN
    KV --> AUTH --> API --> FN
    FN --> RAW --> SPARK --> DQ --> CUR
    OBS -.-> FN
    OBS -.-> SPARK
```

The ingestion service resolves source configuration and authentication at runtime. Raw payloads are stored before distributed jobs apply schema and business transformations. Validation is a separate gate before curated delivery.
