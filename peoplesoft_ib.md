# PeopleSoft Integration Broker (IB) Cheatsheet

PeopleSoft Integration Broker is a middleware technology within PeopleTools that facilitates synchronous and asynchronous messaging between PeopleSoft applications and external systems, or between different PeopleSoft systems.

## Core Concepts & Terminology

*   **Message**: The data structure defining the payload being exchanged. Can be:
    *   **Rowset-based**: XML messages structured according to a PeopleSoft Rowset definition. Most common for PeopleSoft-to-PeopleSoft integrations.
    *   **Non-Rowset-based (XML, JSON, etc.)**: For integrating with third-party systems using standard XML, JSON, or other formats. Often uses `Documents` (see below).
    *   **Predefined Messages**: PeopleSoft delivers many messages for its modules.
*   **Service**: A logical grouping of service operations.
*   **Service Operation (formerly Message Definition in older versions)**: Defines a specific transaction or business event. Key components:
    *   **Type**: Synchronous, Asynchronous Request/Response, Asynchronous One-Way.
    *   **Message**: The message definition (e.g., `PERSON_BASIC_SYNC`) associated with the request/response.
    *   **Handlers**: PeopleCode application classes that process the message content.
    *   **Routings**: Define the direction (inbound/outbound) and transformation of messages between nodes.
    *   **Queues (for Asynchronous Operations)**: Ensure ordered and guaranteed delivery.
*   **Node**: Represents a PeopleSoft system, an external system, or a logical entity involved in an integration.
    *   **Local Node**: The current PeopleSoft system.
    *   **Remote Node**: An external system or another PeopleSoft instance.
    *   Contains connection information (e.g., URL for HTTP, WSDL for web services).
*   **Gateway**: The entry/exit point for messages into/out of a PeopleSoft system. Handles protocol-level communication (HTTP, JMS, etc.). Usually configured on a PeopleSoft web server.
    *   `Gateway URL`: e.g., `http://<server>/PSIGW/PeopleSoftListeningConnector` (for HTTP listening)
*   **Application Server Domains**: Handle the processing of messages, including executing Handler PeopleCode. Integration Broker runs within specific application server processes (e.g., `PSAPPSRV`, `PSAESRV` for async).
*   **Connectors (Target Connectors)**: Software modules responsible for transmitting messages to external systems using specific protocols (e.g., `HTTPTargetConnector`, `JMSTargetConnector`, `SOAPTargetConnector`, `RESTTargetConnector`).
*   **Handlers (PeopleCode Application Classes)**: Contain the business logic to process messages.
    *   Implement specific Integration Broker interfaces (e.g., `PT_INTEGRATION:IRequestHandler`, `PT_INTEGRATION:INotificationHandler`).
    *   Common methods: `OnRequest()`, `OnNotify()`, `OnError()`.
*   **Transformations**: Convert message structure or data format (e.g., XSLT for XML transformations, PeopleCode for data mapping).
*   **Documents (PeopleTools 8.50+)**: Allow defining arbitrary message structures (XML, JSON, file layouts) independent of PeopleSoft rowsets. Useful for third-party integrations.
    *   **Document Builder**: Tool to create and manage Document definitions.
*   **REST Services (PeopleTools 8.52+)**: Integration Broker provides robust support for creating and consuming RESTful web services.
    *   Service operations can be exposed as REST resources.
    *   URI templates, HTTP methods (GET, POST, PUT, DELETE) are configured.
*   **SOAP Services**: Support for creating and consuming SOAP-based web services (WSDL).

## Message Structure Examples

*   **Rowset-based XML Message (Simplified)**:
    ```xml
    <?xml version="1.0"?>
    <MY_MESSAGE_NAME> <!-- Corresponds to the Message Name -->
      <FieldTypes>
        <EMPLID class="R" type="CHAR"/>
        <NAME class="R" type="CHAR"/>
      </FieldTypes>
      <MsgData>
        <Transaction>
          <PSCAMA class="R"/> <!-- PeopleSoft Common Application Message Attributes -->
          <MY_RECORD class="R"> <!-- Corresponds to a Record Name in the Message -->
            <EMPLID>12345</EMPLID>
            <NAME>John Doe</NAME>
          </MY_RECORD>
        </Transaction>
      </MsgData>
    </MY_MESSAGE_NAME>
    ```
*   **Non-Rowset (Document-based) JSON Example**:
    If you define a Document for a JSON structure, the message payload would be that JSON.
    ```json
    {
      "orderId": "ORD789",
      "customer": {
        "id": "CUST001",
        "name": "Jane Smith"
      },
      "items": [
        {"sku": "PROD-A", "quantity": 2},
        {"sku": "PROD-B", "quantity": 1}
      ]
    }
    ```

## Handler PeopleCode Examples (Conceptual)

Handlers are typically Application Classes implementing specific IB interfaces.

*   **`OnRequest` Handler (for Synchronous Service Operations)**:
    ```peoplecode
    import PT_INTEGRATION:IRequestHandler;

    class MySyncHandler implements PT_INTEGRATION:IRequestHandler
       method OnRequest(&requestMessage As Message) Returns Message;
       // Optional: method OnError(&requestMessage As Message) Returns string;
    end-class;

    method OnRequest
       /+ &requestMessage as Message +/
       /+ Returns Message +/
       /+ Extends/implements PT_INTEGRATION:IRequestHandler.OnRequest +/

       Local Message &responseMessage;
       Local Rowset &requestRowset, &responseRowset;
       Local string &emplid;
       Local Record &requestRec, &responseRec;

       &responseMessage = CreateMessage(Message.MY_RESPONSE_MESSAGE_NAME); // Create response message
       &requestRowset = &requestMessage.GetRowset(); // Get input data
       &requestRec = &requestRowset.GetRow(1).GetRecord(Record.MY_REQUEST_RECORD);
       &emplid = &requestRec.EMPLID.Value;

       // ... Process the request using &emplid ...
       // ... Populate &responseRowset or &responseMessage directly ...

       &responseRowset = &responseMessage.GetRowset();
       &responseRec = &responseRowset.GetRow(1).GetRecord(Record.MY_RESPONSE_RECORD);
       &responseRec.STATUS.Value = "SUCCESS";
       &responseRec.DETAILS.Value = "Processed EMPLID: " | &emplid;

       Return &responseMessage;
    end-method;
    ```

*   **`OnNotify` Handler (for Asynchronous One-Way Service Operations)**:
    ```peoplecode
    import PT_INTEGRATION:INotificationHandler;

    class MyAsyncHandler implements PT_INTEGRATION:INotificationHandler
       method OnNotify(&requestMessage As Message);
       // Optional: method OnError(&requestMessage As Message) Returns string;
    end-class;

    method OnNotify
       /+ &requestMessage as Message +/
       /+ Extends/implements PT_INTEGRATION:INotificationHandler.OnNotify +/

       Local Rowset &dataRowset;
       Local string &valueToProcess;

       &dataRowset = &requestMessage.GetRowset();
       &valueToProcess = &dataRowset.GetRow(1).GetRecord(1).GetField(1).Value;

       // ... Process the incoming asynchronous data ...
       // No response message is typically returned for OnNotify.
       // Handle errors by throwing exceptions or using OnError.

       If &someErrorCondition Then
          throw CreateException(0, 0, "Error processing notification: " | &valueToProcess);
       End-If;

    end-method;
    ```

*   **Accessing Non-Rowset Data (e.g., JSON from a Document)**:
    ```peoplecode
    // In an OnRequest or OnNotify handler
    // Assuming &requestMessage is a Document-based message
    Local Document &requestDoc;
    Local JsonParser &jsonParser;
    Local string &jsonString;
    Local boolean &parseSuccess;

    &requestDoc = &requestMessage.GetDocument();
    &jsonString = &requestDoc.GetContentString(); // Get JSON string

    &jsonParser = CreateJsonParser(&jsonString);
    Local any &jsonData = &jsonParser.Parse(); // Parses into PeopleCode any type (often nested arrays/objects)

    If &jsonData.IsObject() Then
       Local string &orderId = &jsonData.GetProperty("orderId").GetStringValue();
       // ... process jsonData ...
    End-If;

    // For sending a JSON response using a Document:
    // Local Document &responseDoc = CreateDocument("MY_JSON_RESPONSE_DOC", "application/json");
    // Local JsonBuilder &jsonBuilder = CreateJsonBuilder();
    // Local any &responsePCodeObject = CreateObject("PS_PT:Json"); // Build your response object
    // &responsePCodeObject.SetProperty("status", "success");
    // &responseDoc.SetContentString(&jsonBuilder.ToString(&responsePCodeObject));
    // &responseMessage.SetDocument(&responseDoc);
    ```

## Configuration Steps (PIA Navigation - General Flow)

Navigation paths can vary slightly by PeopleTools version.
**PeopleTools > Integration Broker > ...**

1.  **Nodes**: (Integration Setup > Nodes)
    *   Define local and remote nodes.
    *   Configure connectors for remote nodes (e.g., HTTPTargetConnector URL, WSDL URL).
    *   Set authentication options (e.g., password, certificates).
2.  **Gateways**: (Integration Setup > Gateways)
    *   Define the gateway ID and URL.
    *   Load connectors (HTTP, JMS, etc.).
    *   Ping Gateway to test connectivity.
3.  **Service Operations (Messages)**: (Integration Setup > Service Operations)
    *   Define service operation name, type (Sync, Async), request message, response message.
    *   **Handlers Tab**: Add PeopleCode handlers (Application Class) and set status to Active.
    *   **Routings Tab**: Define inbound or outbound routings.
        *   Specify Sender Node and Receiver Node.
        *   Optionally add transformations (XSLT, PeopleCode).
        *   Activate the routing.
    *   **Security Tab**: Define permission list(s) that have access to this service operation.
4.  **Queues (for Asynchronous Operations)**: (Integration Setup > Queues)
    *   Define message queues. Service operations are assigned to queues.
    *   Queues are processed by dedicated IB processes in the application server.
5.  **Services**: (Integration Setup > Services)
    *   Group related service operations.
    *   Provide WSDL for web services.
    *   Configure REST service URI templates and HTTP methods.
6.  **Documents (for Non-Rowset Messages)**: (PeopleTools > Documents > Document Builder)
    *   Define the structure of non-PeopleSoft messages (XML, JSON, CSV, etc.).
    *   Can be used in service operations instead of rowset-based messages.
7.  **Security**:
    *   **Permission Lists**: Grant access to service operations. (PeopleTools > Security > Permissions & Roles > Permission Lists)
    *   **Web Service Security (WSS)**: For SOAP services, configure username tokens, X.509 certificates, etc.
    *   **Node Authentication**: Passwords, PSFTTARGET, certificates.

## Monitoring and Troubleshooting (PIA Navigation)

**PeopleTools > Integration Broker > Service Operations Monitor > ...**

*   **Monitor Overview**: Dashboard of IB activity.
*   **Synchronous Services**: Monitor synchronous message transactions. View request/response XML, errors.
*   **Asynchronous Services**:
    *   **Publication Contracts**: Monitor outgoing asynchronous messages.
    *   **Subscription Contracts**: Monitor incoming asynchronous messages.
    *   View message status (New, Working, Done, Error, Timeout).
    *   Drill down to see message XML, error details.
    *   Manage queues (pause, resume).
*   **Gateway Log Files**: Located on the web server hosting the gateway (e.g., `msgLog.html`, `errorLog.html`).
*   **Application Server Log Files**: Contain IB processing details and errors for specific domains/processes.

## Common Integration Scenarios

*   **Exposing a PeopleSoft Component as a Web Service (SOAP or REST)**:
    1.  Create service operation(s) with rowset-based messages reflecting the component interface.
    2.  Write `OnRequest` PeopleCode handler to interact with the Component Interface.
    3.  Configure node(s) and routing(s).
    4.  Provide WSDL (for SOAP) or REST endpoint URL to consumers.
*   **Consuming an External Web Service (SOAP or REST)**:
    1.  Import WSDL (for SOAP) or define messages/documents (for REST).
    2.  Use PeopleCode `IntBroker` class methods or `ConnectorRequest` methods to invoke the external service.
        ```peoplecode
        // Example: Consuming a Rowset-based Synchronous SOAP service
        // Local Message &request, &response;
        // &request = CreateMessage(Message.MY_REQUEST_MSG);
        // // ... populate &request ...
        // &response = %IntBroker.SyncRequest(&request, Node.EXTERNAL_SOAP_NODE);
        // If &response.ResponseStatus = %IB_Status_Success Then
        //   // Process &response
        // Else
        //   // Handle error
        // EndIf;

        // Example: Consuming a REST GET service (Document-based)
        // Local Message &restRequest, &restResponse;
        // &restRequest = CreateMessage(Operation.MY_REST_GET_OPER, %IntBroker_Request);
        // &restRequest.SetDocumentRequest(CreateDocument("MY_REQUEST_DOC", "application/json", "{}")); // Empty body for GET
        // &restResponse = %IntBroker.SyncRequest(&restRequest, Node.EXTERNAL_REST_NODE, False, False, ["param1Value", "param2Value"]); // Pass URI template params
        // If &restResponse.ResponseStatus = %IB_Status_Success Then
        //    Local Document &responseDoc = &restResponse.GetDocument();
        //    Local string &jsonResp = &responseDoc.GetContentString();
        //    // Parse &jsonResp
        // End-If;
        ```
*   **File-Based Integrations**:
    *   Use `File Layout` definitions to parse/generate flat files.
    *   Use `FILETARGET` connector for writing files or `FTPTARGET` for FTP.
    *   Can be triggered by Application Engine programs.
*   **JMS Integrations**:
    *   Use `JMSTargetConnector` or `JMSListeningConnector`.
    *   Configure JMS specific node properties.

## Best Practices

*   Use descriptive names for messages, service operations, nodes, etc.
*   Thoroughly test integrations in development/test environments.
*   Implement robust error handling in PeopleCode handlers.
*   Use the Integration Broker Monitor for troubleshooting.
*   Secure your integrations (authentication, authorization, SSL/TLS).
*   For REST services, follow RESTful design principles.
*   Use Documents for non-PeopleSoft message formats.

This provides a more detailed conceptual overview and some code structure examples for PeopleSoft Integration Broker. I'll proceed with `vscode.md`.The `peoplesoft_ib.md` cheatsheet has been successfully updated with a more detailed conceptual overview, examples of message structures (XML/JSON), conceptual PeopleCode handler structures, typical PIA configuration points, and common integration scenarios.

Next, I will enhance `vscode.md`, focusing on providing common keyboard shortcuts, useful settings, and examples of how to use features like the command palette, integrated terminal, and extensions.
