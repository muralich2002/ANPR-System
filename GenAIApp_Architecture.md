```mermaid
%%{init: { "flowchart": { "useMaxWidth": false, "width": 100% }, "theme": "default", "themeVariables": { "fontSize": "20px", "nodeTextMargin": 10, "nodeBorder": 3 } }}%%
graph LR
    %% Title
    title["Beverage Company - Gen AI Data Modernization Architecture"]
    style title fill:none,stroke:none,font-size:24px,text-align:center

    %% Define styles for better visual appeal with larger text and boxes
    classDef source fill:#ff6b6b,stroke:#333,stroke-width:3px,color:white,stroke-dasharray: 5 5,font-size:18px
    classDef ingestion fill:#4ecdc4,stroke:#333,stroke-width:3px,color:white,stroke-dasharray: 5 5,font-size:18px
    classDef lakehouse fill:#45b7d1,stroke:#333,stroke-width:3px,color:white,stroke-dasharray: 5 5,font-size:18px
    classDef genai fill:#9b59b6,stroke:#333,stroke-width:3px,color:white,stroke-dasharray: 5 5,font-size:18px
    classDef consumption fill:#96ceb4,stroke:#333,stroke-width:3px,color:white,stroke-dasharray: 5 5,font-size:18px
    classDef governance fill:#ffd166,stroke:#333,stroke-width:3px,stroke-dasharray: 5 5,font-size:18px
    classDef orchestration fill:#ff9f1c,stroke:#333,stroke-width:3px,color:white,stroke-dasharray: 5 5,font-size:18px

    %% Legend
    subgraph Legend
        direction TB
        L1["Source Systems"]:::source
        L2["Ingestion & Processing"]:::ingestion
        L3["Data Lakehouse"]:::lakehouse
        L4["Gen AI Services"]:::genai
        L5["Consumption & Visualization"]:::consumption
        L6["Governance & Security"]:::governance
    end

    %% Source Systems
    subgraph "Source Systems"
        direction TB
        ERP[("ERP Systems")]
        POS[("POS Systems")]
        IOT[("IoT Devices")]
        CRM[("CRM Data")]
        SALES[("Sales Data")]
        MARKETING[("Marketing Data")]
    end

    %% Ingestion & Processing
    subgraph "Ingestion & Processing"
        direction TB
        GLUE[("AWS Glue")]
        LAMBDA[("AWS Lambda")]
        STEP[("AWS Step Functions")]
        KINESIS[("Amazon Kinesis")]
        SQS[("Amazon SQS")]
        EVENTBRIDGE[("Amazon EventBridge")]
    end

    %% Data Lakehouse
    subgraph "Data Lakehouse"
        direction TB
        RAW[("Raw Data Layer")]
        CLEANSED[("Cleansed Data Layer")]
        REFINED[("Refined Data Layer")]
        CATALOG[("AWS Glue Data Catalog")]
        BEDROCK[("Amazon Bedrock")]
        VECTOR[("Vector Database")]
        EMBEDDINGS[("Embeddings Store")]
    end

    %% Gen AI Services
    subgraph "Gen AI Services"
        direction TB
        BEDROCK_FOUNDATION[("Foundation Models")]
        BEDROCK_AGENTS[("Bedrock Agents")]
        BEDROCK_KNOWLEDGE[("Knowledge Bases")]
        SAGEMAKER[("Amazon SageMaker")]
        COMPREHEND[("Amazon Comprehend")]
        TRANSLATE[("Amazon Translate")]
    end

    %% Consumption & Visualization
    subgraph "Consumption & Visualization"
        direction TB
        AI_ASSISTANT[("AI Sales Assistant")]
        PRESCRIPTIVE[("Prescriptive Sales Recommender")]
        SENTIMENT[("Sentiment Analysis Tool")]
        ATHENA[("Amazon Athena")]
        QUICKSIGHT[("Amazon QuickSight")]
        APPS[("Internal Applications")]
        API_GATEWAY[("API Gateway")]
    end

    %% Governance & Security
    subgraph "Governance & Security"
        direction TB
        IAM[("AWS IAM")]
        KMS[("AWS KMS")]
        CLOUDTRAIL[("AWS CloudTrail")]
        GUARDDUTY[("Amazon GuardDuty")]
        MACIE[("Amazon Macie")]
        GLUE_CATALOG[("Data Catalog")]
    end

    %% Orchestration
    subgraph "Orchestration"
        direction LR
        AIRFLOW[("Apache Airflow")]
        MWAA[("Amazon MWAA")]
    end

    %% Data Flow - Source to Ingestion
    ERP -->|"Extract"| GLUE
    POS -->|"Stream"| LAMBDA
    IOT -->|"Process"| STEP
    CRM -->|"Batch"| KINESIS
    SALES -->|"Queue"| SQS
    MARKETING -->|"Event"| EVENTBRIDGE

    %% Data Flow - Ingestion to Lakehouse
    GLUE -->|"ETL"| RAW
    LAMBDA -->|"Transform"| CLEANSED
    STEP -->|"Orchestrate"| REFINED
    KINESIS -->|"Real-time"| RAW
    SQS -->|"Process"| CLEANSED
    EVENTBRIDGE -->|"Trigger"| REFINED

    %% Data Flow - Lakehouse Processing
    RAW -->|"Quality Check"| CLEANSED
    CLEANSED -->|"Model"| REFINED
    REFINED -->|"Catalog"| CATALOG
    REFINED -->|"Generate"| EMBEDDINGS
    EMBEDDINGS -->|"Store"| VECTOR

    %% Gen AI Integration
    BEDROCK -->|"Access Models"| BEDROCK_FOUNDATION
    BEDROCK -->|"Create Agents"| BEDROCK_AGENTS
    BEDROCK -->|"Build Knowledge"| BEDROCK_KNOWLEDGE
    VECTOR -->|"Retrieve"| BEDROCK_KNOWLEDGE
    CATALOG -->|"Query"| BEDROCK_AGENTS

    %% AI Services Integration
    SAGEMAKER -->|"Train Models"| BEDROCK_FOUNDATION
    COMPREHEND -->|"Analyze Text"| SENTIMENT
    TRANSLATE -->|"Multi-language"| AI_ASSISTANT

    %% Consumption Flow
    BEDROCK_AGENTS -->|"Power"| AI_ASSISTANT
    BEDROCK_KNOWLEDGE -->|"Enable"| PRESCRIPTIVE
    SAGEMAKER -->|"Deploy"| PRESCRIPTIVE
    REFINED -->|"Query"| ATHENA
    ATHENA -->|"Visualize"| QUICKSIGHT
    ATHENA -->|"Consume"| APPS
    API_GATEWAY -->|"Expose"| AI_ASSISTANT
    API_GATEWAY -->|"Expose"| PRESCRIPTIVE

    %% Governance Integration
    IAM -->|"Secure"| BEDROCK
    IAM -->|"Control Access"| SAGEMAKER
    KMS -->|"Encrypt"| VECTOR
    KMS -->|"Encrypt"| EMBEDDINGS
    CLOUDTRAIL -->|"Audit"| BEDROCK
    CLOUDTRAIL -->|"Monitor"| SAGEMAKER
    GUARDDUTY -->|"Protect"| GENAI
    MACIE -->|"Classify"| REFINED
    GLUE_CATALOG -->|"Govern"| CATALOG

    %% Orchestration Flow
    AIRFLOW -->|"Schedule"| GLUE
    AIRFLOW -->|"Trigger"| LAMBDA
    MWAA -->|"Orchestrate"| STEP
    AIRFLOW -->|"Monitor"| BEDROCK
    AIRFLOW -->|"Deploy"| SAGEMAKER

    %% Apply Styles
    class ERP,POS,IOT,CRM,SALES,MARKETING source
    class GLUE,LAMBDA,STEP,KINESIS,SQS,EVENTBRIDGE ingestion
    class RAW,CLEANSED,REFINED,CATALOG,BEDROCK,VECTOR,EMBEDDINGS lakehouse
    class BEDROCK_FOUNDATION,BEDROCK_AGENTS,BEDROCK_KNOWLEDGE,SAGEMAKER,COMPREHEND,TRANSLATE genai
    class AI_ASSISTANT,PRESCRIPTIVE,SENTIMENT,ATHENA,QUICKSIGHT,APPS,API_GATEWAY consumption
    class IAM,KMS,CLOUDTRAIL,GUARDDUTY,MACIE,GLUE_CATALOG governance
    class AIRFLOW,MWAA orchestration

    %% Style for subgraph labels
    style "Source Systems" fill:#f5f5f5,stroke:#333,stroke-width:2px,font-size:20px
    style "Ingestion & Processing" fill:#f5f5f5,stroke:#333,stroke-width:2px,font-size:20px
    style "Data Lakehouse" fill:#f5f5f5,stroke:#333,stroke-width:2px,font-size:20px
    style "Gen AI Services" fill:#f5f5f5,stroke:#333,stroke-width:2px,font-size:20px
    style "Consumption & Visualization" fill:#f5f5f5,stroke:#333,stroke-width:2px,font-size:20px
    style "Governance & Security" fill:#f5f5f5,stroke:#333,stroke-width:2px,font-size:20px
    style "Orchestration" fill:#f5f5f5,stroke:#333,stroke-width:2px,font-size:20px
    style "Legend" fill:#f5f5f5,stroke:#333,stroke-width:2px,font-size:20px
```

# Beverage Company - Gen AI Data Modernization Architecture

## Overview
This enhanced architecture diagram illustrates the comprehensive Gen AI-powered data modernization journey for a leading beverage manufacturer, focusing on AWS Bedrock and related AI services to create intelligent sales and marketing solutions.

## Key Components

### Source Systems
- **ERP Systems**: Enterprise resource planning data
- **POS Systems**: Point-of-sale transaction data
- **IoT Devices**: Connected device data
- **CRM Data**: Customer relationship management data
- **Sales Data**: Historical and real-time sales information
- **Marketing Data**: Campaign and customer interaction data

### Ingestion & Processing
- **AWS Glue**: ETL processing for structured data
- **AWS Lambda**: Serverless processing for real-time data
- **AWS Step Functions**: Workflow orchestration
- **Amazon Kinesis**: Real-time data streaming
- **Amazon SQS**: Message queuing for asynchronous processing
- **Amazon EventBridge**: Event-driven processing

### Data Lakehouse
- **Raw Data Layer**: Unprocessed source data storage
- **Cleansed Data Layer**: Quality-checked and standardized data
- **Refined Data Layer**: Business-modeled data with semantic meaning
- **AWS Glue Data Catalog**: Centralized metadata management
- **Amazon Bedrock**: Foundation model service for AI applications
- **Vector Database**: Storage for embeddings and semantic search
- **Embeddings Store**: Vector representations of data for AI processing

### Gen AI Services
- **Foundation Models**: Pre-trained large language models via Bedrock
- **Bedrock Agents**: Autonomous AI agents for specific tasks
- **Knowledge Bases**: RAG (Retrieval-Augmented Generation) systems
- **Amazon SageMaker**: Machine learning model development and deployment
- **Amazon Comprehend**: Natural language processing and sentiment analysis
- **Amazon Translate**: Multi-language support for global operations

### Consumption & Visualization
- **AI Sales Assistant**: Intelligent chatbot for sales support
- **Prescriptive Sales Recommender**: ML-powered sales recommendations
- **Sentiment Analysis Tool**: Customer sentiment monitoring
- **Amazon Athena**: Serverless query service
- **Amazon QuickSight**: Business intelligence and visualization
- **Internal Applications**: Custom applications consuming AI insights
- **API Gateway**: Secure API access to AI services

### Governance & Security
- **AWS IAM**: Identity and access management
- **AWS KMS**: Encryption key management
- **AWS CloudTrail**: API call logging and auditing
- **Amazon GuardDuty**: Threat detection
- **Amazon Macie**: Data classification and protection
- **Data Catalog**: Metadata governance

### Orchestration
- **Apache Airflow**: Workflow orchestration
- **Amazon MWAA**: Managed Airflow service

## Detailed Data Flow

### 1. Data Ingestion Pipeline
- Multiple source systems feed into various AWS processing services
- Real-time and batch processing paths for different data types
- Event-driven architecture for responsive data processing

### 2. Data Lakehouse Processing
- Raw data undergoes quality checks and transformation
- Business logic applied in refined layer
- Vector embeddings generated for AI processing
- Centralized catalog for data discovery

### 3. Gen AI Integration
- Bedrock provides access to foundation models
- Knowledge bases built from vector embeddings
- Autonomous agents created for specific business tasks
- SageMaker models deployed for custom AI solutions

### 4. AI-Powered Applications
- AI Sales Assistant provides intelligent customer support
- Prescriptive Sales Recommender offers data-driven recommendations
- Sentiment analysis monitors customer satisfaction
- APIs expose AI capabilities to internal applications

### 5. Governance & Security
- End-to-end security with IAM and KMS
- Comprehensive auditing with CloudTrail
- Data protection with Macie and GuardDuty
- Metadata governance through data catalog

## Key Benefits

### Business Impact
- **AI Sales Assistant**: 24/7 intelligent customer support
- **Prescriptive Sales Recommender**: Data-driven sales optimization
- **Sentiment Analysis**: Real-time customer satisfaction monitoring
- **Self-Serve Analytics**: Democratized data access

### Technical Benefits
- **Scalable Architecture**: Cloud-native design for growth
- **Cost Optimization**: Pay-per-use pricing model
- **Security**: Enterprise-grade security and compliance
- **Innovation Ready**: Foundation for future AI initiatives

### Operational Benefits
- **Single Source of Truth**: Centralized data lakehouse
- **Automated Processing**: Reduced manual intervention
- **Real-time Insights**: Immediate access to business intelligence
- **Global Reach**: Multi-language support for international operations

## Success Metrics
- Improved sales team productivity through AI assistance
- Enhanced customer satisfaction via intelligent recommendations
- Reduced time-to-insight for business decisions
- Increased data democratization across the organization
- Foundation for future AI innovation and competitive advantage
