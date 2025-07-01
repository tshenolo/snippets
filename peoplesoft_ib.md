# PeopleSoft Integration Broker Cheatsheet

*   **Purpose**: PeopleSoft's framework for synchronous and asynchronous messaging between PeopleSoft systems and third-party applications.
*   **Key Components**:
    *   Gateway: Acts as the entry point for messages (listens for HTTP/S, JMS, etc.). Connects to Application Server(s).
    *   Application Server Domains: Handle message processing (routing, transformation, execution of PeopleCode).
    *   Messages: Data structures defining the payload (Rowset-based, Non-Rowset/XML, Document).
    *   Service Operations (formerly known as Message Definitions in older versions): Defines the transaction (e.g., request/response, one-way). Includes:
        *   Message: The data structure.
        *   Handlers: PeopleCode programs that process the message (OnRequest, OnResponse, OnError, etc.).
        *   Routings: Define the direction of the message (inbound/outbound) and transformation rules.
    *   Nodes: Represent PeopleSoft systems or external systems involved in integration. Contain connection information.
    *   Queues: For asynchronous messaging, ensures ordered and guaranteed delivery.
    *   Connectors: Adapters for different protocols (HTTP, JMS, FTP, File, etc.).
*   **Handlers (PeopleCode)**:
    *   Application Classes or Functions implementing specific interfaces (e.g., `PS_PT:Integration:IRequestHandler`).
    *   `OnRequest`: Processes incoming synchronous requests.
    *   `OnNotify`: Processes incoming asynchronous messages.
    *   `Transform` programs (XSLT or PeopleCode) for data mapping.
*   **Service Configuration**: Done through PIA (PeopleSoft Internet Architecture) navigation: PeopleTools > Integration Broker > ...
*   **Monitoring**: Integration Broker Monitor provides tools to view message status, errors, and logs.
*   **Common Use Cases**: Exposing PeopleSoft components as web services (REST/SOAP), consuming external web services, EIPs (Enterprise Integration Patterns).
*   **Security**: WS-Security for web services, node authentication, SSL/TLS.
