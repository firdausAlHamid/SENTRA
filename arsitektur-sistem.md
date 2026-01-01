flowchart LR
    %% =====================
    %% ACTORS / DATA SOURCES
    %% =====================
    subgraph Sumber_Data["Sumber Data"]
        DS1[UMKM / Operasional]
        DS2[Pasar & Distribusi]
        DS3[Media Sosial]
        DS4[Laporan Manual]
        DS5[API Eksternal]
    end

    %% =====================
    %% INGESTION LAYER
    %% =====================
    subgraph Ingestion["Data Ingestion Layer"]
        IG1[HTTP / API Adapter]
        IG2[File Adapter]
        IG3[Message Queue Adapter]
        IG4[Social Media Adapter]
    end

    DS1 --> IG1
    DS2 --> IG1
    DS3 --> IG4
    DS4 --> IG2
    DS5 --> IG1

    %% =====================
    %% NORMALIZATION LAYER
    %% =====================
    subgraph Normalization["Normalization & Validation"]
        N1[Schema Mapper]
        N2[Data Validator]
        N3[Data Enricher]
    end

    IG1 --> N1
    IG2 --> N1
    IG3 --> N1
    IG4 --> N1

    N1 --> N2 --> N3

    %% =====================
    %% STORAGE LAYER
    %% =====================
    subgraph Storage["Data Storage"]
        DB1[(Operational DB)]
        DB2[(Analytical DB)]
        DB3[(Data Lake)]
    end

    N3 --> DB1
    N3 --> DB2
    N3 --> DB3

    %% =====================
    %% INTELLIGENCE CORE
    %% =====================
    subgraph Intelligence["Intelligence Core"]
        A1[Trend Analysis Engine]
        A2[Anomaly Detection Engine]
        A3[Sentiment Analysis Engine]
        A4[Risk Scoring Engine]
    end

    DB2 --> A1
    DB2 --> A2
    DB2 --> A3
    DB2 --> A4

    %% =====================
    %% ALERT & GOVERNANCE
    %% =====================
    subgraph Governance["Governance & Control"]
        G1[Rule Engine]
        G2[Threshold Engine]
        G3[Audit & Logging]
        G4[Data Lineage]
        G5[Access Policy]
    end

    A2 --> G1
    A4 --> G2
    A1 --> G3
    A3 --> G4

    %% =====================
    %% DELIVERY LAYER
    %% =====================
    subgraph Delivery["Delivery & Visualization"]
        D1[Government Dashboard]
        D2[Reports & Export]
        D3[Early Warning System]
        D4[Public Transparency Portal]
    end

    G1 --> D3
    G2 --> D3
    DB2 --> D1
    DB2 --> D2
    DB2 --> D4

