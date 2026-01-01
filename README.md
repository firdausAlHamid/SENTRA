## 🏛️ Arsitektur Platform SENTRA

```mermaid
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
    %% NORMALIZATION
    %% =====================
    subgraph Normalization["Normalization & Validation"]
        N1[Schema Mapper]
        N2[Data Validator]
        N3[Data Enricher]
    end

    IG1 --> N1
    IG2 --> N1
    IG4 --> N1

    N1 --> N2 --> N3

    %% =====================
    %% STORAGE
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
        A1[Trend Analysis]
        A2[Anomaly Detection]
        A3[Sentiment Analysis]
        A4[Risk Scoring]
    end

    DB2 --> A1
    DB2 --> A2
    DB2 --> A3
    DB2 --> A4

    %% =====================
    %% DELIVERY
    %% =====================
    subgraph Delivery["Delivery Layer"]
        D1[Government Dashboard]
        D2[Early Warning System]
        D3[Reports & Export]
    end

    A1 --> D1
    A2 --> D2
    A4 --> D2
    DB2 --> D3
