## <a name="typical-output"></a>Finden Sie ein Ausgabebeispiel

Es folgt ein Beispiel für die Ausgabe im Beispiel "Hello World" in die Protokolldatei geschrieben. Zeilenvorschub und Tabulatorzeichen wurden für Lesbarkeit hinzugefügt:

```
[{
    "time": "Mon Apr 11 13:48:07 2016",
    "content": "Log started"
}, {
    "time": "Mon Apr 11 13:48:48 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:48:55 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:01 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:04 2016",
    "content": "Log stopped"
}]
```

## <a name="code-snippets"></a>Codeausschnitte

In diesem Abschnitt werden einige wichtige Teile des Codes in diesem Beispiel "Hello World".

### <a name="gateway-creation"></a>Gateway-Erstellung

Der Entwickler muss das *Gateway-Prozess*schreiben. Dieses Programm erstellt die interne Infrastruktur (der Broker), lädt die Module und richtet alles ordnungsgemäß funktioniert. Das SDK enthält die **Gateway_Create_From_JSON** -Funktion, um ein Gateway aus einer Datei JSON bootstrap zu aktivieren. Um die **Gateway_Create_From_JSON** -Funktion verwenden, müssen Sie ihr den Pfad in eine JSON-Datei übergeben, die angibt, die Module geladen werden. 

Suchen Sie den Code für den Gatewayprozess, in dem Beispiel "Hello World", in der [main.c] [ lnk-main-c] Datei. Im folgenden Codeausschnitt zeigt für Lesbarkeit eine verkürzte Version des Codes Prozess Gateway. Dieses Programm erstellt ein Gateway und klicken Sie dann den Benutzer auf **die EINGABETASTE** drücken, bevor es Sie das Gateway sonstige Hilfsmittel wartet. 

```
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed to create the gateway from JSON\n");
    }
    else
    {
        printf("gateway successfully created from JSON\n");
        printf("gateway shall run until ENTER is pressed\n");
        (void)getchar();
        Gateway_LL_Destroy(gateway);
    }
    return 0;
}
```

Die Einstellungsdatei JSON enthält eine Liste der Module geladen werden. Jedes Modul muss a: angeben.

- **Modulname**: einen eindeutigen Namen für das Modul an.
- **Module_path**: der Pfad zu der Dokumentbibliothek, die das Modul enthält. Für Linux Dies ist eine Datei .so, Windows ist dies eine DLL-Datei.
- **Args**: alle Konfigurationsinformationen das Modul muss.

Die JSON-Datei enthält außerdem die Verknüpfungen zwischen den Modulen, die an dem Broker übergeben werden. Eine Verknüpfung verfügt über zwei Eigenschaften:
- **Quelle**: einem Modulnamen aus der `modules` Abschnitt oder "\*".
- **Empfänger**: eine Modulnamen aus der `modules` Abschnitt

Jede Verknüpfung definiert eine Weiterleitung der Nachricht und die Richtung an. Nachrichten von Modul `source` werden an das Modul übermittelt werden `sink`. Die `source` kann festgelegt werden, um "\*", was bedeutet, dass Nachrichten von allen Modulen nach empfangen werden `sink`.

Das folgende Beispiel zeigt die JSON-Einstellungsdatei verwendet, um das Beispiel "Hello World" unter Linux zu konfigurieren. Jede Nachricht von Modul erzeugt `hello_world` behandelt werden vom Modul `logger`. Gibt an, ob ein Modul erfordert, dass der Entwurf des Moduls Argument abhängt. In diesem Beispiel wird das Modul für die Protokollierung ein Argument, der Pfad zur Ausgabedatei ist, und das Modul "Hello World" ist keine Argumente:

```
{
    "modules" :
    [ 
        {
            "module name" : "logger",
            "module path" : "./modules/logger/liblogger_hl.so",
            "args" : {"filename":"log.txt"}
        },
        {
            "module name" : "hello_world",
            "module path" : "./modules/hello_world/libhello_world_hl.so",
            "args" : null
        }
    ],
    "links" :
    [
        {
            "source" : "hello_world",
            "sink" : "logger"
        }
    ]
}
```

### <a name="hello-world-module-message-publishing"></a>Hello World Modul Nachricht Veröffentlichung

Sie finden den Code von "Hello World" Modul verwendet, um Nachrichten in der ['hello_world.c'] veröffentlichen[ lnk-helloworld-c] Datei. Im folgenden Codeausschnitt zeigt eine geänderte Version mit zusätzlichen Kommentare und einige Fehlerbehandlungscode, um die Lesbarkeit entfernt:

```
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);
    
    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" to a set of message properties that
    // will be appended to the message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set the content for the message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set the properties for the message
    msgConfig.sourceProperties = propertiesMap;
    
    // create a message based on the msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of the thread*/
        }
        else
        {
            // publish the message to the broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="hello-world-module-message-processing"></a>Hello World Modul die Verarbeitung von Nachrichten

Das Modul "Hello World" nie Nachrichten verarbeiten muss, die anderen Modulen in der Broker veröffentlichen. Dadurch wird die Implementierung des Rückrufs, der Nachricht im Modul "Hello World" eine Funktion keine Aktion ausgeführt.

```
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a>Protokollierung Modul Nachricht veröffentlichen und verarbeiten

Das Modul Protokollierung empfängt Nachrichten aus der Broker und schreibt sie in eine Datei. Es werden alle Nachrichten nie veröffentlicht. Aus diesem Grund ruft der Code des Moduls Protokollierung nie die **Broker_Publish** -Funktion.

Die **Logger_Recieve** -Funktion in der [logger.c] [ lnk-logger-c] Datei ist der Rückruf der Broker zum Übermitteln von Nachrichten an das Modul Protokollierung aufgerufen. Im folgenden Codeausschnitt zeigt eine geänderte Version mit zusätzlichen Kommentare und einige Fehlerbehandlungscode, um die Lesbarkeit entfernt:

```
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get the message properties from the message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert the collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode the message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start the construction of the final string to be logged by adding
    // the timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add the message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add the content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write the formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a>Nächste Schritte

Informationen zur Verwendung des IoT Gateway SDK finden Sie Folgendes:

- [IoT Gateway SDK – senden Gerät-Cloud-Nachrichten mit einem simulierten Gerät mit Linux][lnk-gateway-simulated].
- [Azure IoT Gateway SDK] [ lnk-gateway-sdk] auf GitHub.

<!-- Links -->
[lnk-main-c]: https://github.com/Azure/azure-iot-gateway-sdk/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/azure-iot-gateway-sdk/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/azure-iot-gateway-sdk/blob/master/modules/logger/src/logger.c
[lnk-gateway-sdk]: https://github.com/Azure/azure-iot-gateway-sdk/
[lnk-gateway-simulated]: ../articles/iot-hub/iot-hub-linux-gateway-sdk-simulated-device.md