graph TD
    A[Client/API Request] --> B{Flask Endpoint}

    %% Endpoints
    B --> B1[upload_urls.py]
    B --> B2[upload_docs.py]
    B --> B3[chat.py]
    B --> B4[status.py]

    %% upload_urls.py
    B1 --> C1[Extract & Validate URLs]
    C1 --> C2[Download & Parse Content]
    C2 --> C3[Split Text Chunks]
    C3 --> C4[Embed via HuggingFace]
    C4 --> C5[Store in VectorStore (ChromaDB)]

    %% upload_docs.py
    B2 --> D1[Load Files (PDF/DOCX)]
    D1 --> D2[Split Text Chunks]
    D2 --> D3[Embed via HuggingFace]
    D3 --> D4[Store in VectorStore (ChromaDB)]

    %% chat.py
    B3 --> E1[User Query Received]
    E1 --> E2[Embed Query]
    E2 --> E3[Search VectorStore for Matches]
    E3 --> E4[Retrieve Context Chunks]
    E4 --> E5[Generate Answer (LLM)]
    E5 --> E6[Log Conversation]

    %% status.py
    B4 --> F1[System Health & ChromaDB Check]

    %% Shared utils
    C5 --> G1[utils/vectorstore.py]
    D4 --> G1
    E3 --> G1

    C1 --> G2[utils/config_loader.py]
    D1 --> G2
    F1 --> G2

    E6 --> G3[utils/chat_logs.py]

    %% Logs & Output
    C5 --> H1[upload_results_*.json]
    D4 --> H2[upload_results_*.json]
    E6 --> H3[chat_logs/*.json]
