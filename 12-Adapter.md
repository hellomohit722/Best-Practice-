
# Adapter

<img width="906" height="662" alt="image" src="https://github.com/user-attachments/assets/957f95b8-b233-42c7-9902-5a46202ca47d" />

- Adapter convert the interface of the cass into another inteface that client accepts, Adapter lets classes work together that could not otherwise because of in compatible interfaces.

```java
// 1. Target Interface
interface IReports {
    String getJsonData(String data);
}

// 2. Adaptee
class XmlDataProvider {

    // Input format: "Alice:42"
    public String getXmlData(String data) {

        String[] parts = data.split(":");

        String name = parts[0];
        String id = parts[1];

        return "<user>"
                + "<name>" + name + "</name>"
                + "<id>" + id + "</id>"
                + "</user>";
    }
}

// 3. Adapter
class XmlDataProviderAdapter implements IReports {

    private XmlDataProvider xmlProvider;

    public XmlDataProviderAdapter(XmlDataProvider provider) {
        this.xmlProvider = provider;
    }

    @Override
    public String getJsonData(String data) {

        // Step 1: Get XML from Adaptee
        String xml = xmlProvider.getXmlData(data);

        // Step 2: Extract Name
        int startName = xml.indexOf("<name>") + 6;
        int endName = xml.indexOf("</name>");
        String name = xml.substring(startName, endName);

        // Step 3: Extract ID
        int startId = xml.indexOf("<id>") + 4;
        int endId = xml.indexOf("</id>");
        String id = xml.substring(startId, endId);

        // Step 4: Convert XML -> JSON
        return "{\"name\":\"" + name + "\", \"id\":" + id + "}";
    }
}

// 4. Client
class Client {

    public void getReport(IReports report, String rawData) {

        System.out.println("Processed JSON:");
        System.out.println(report.getJsonData(rawData));
    }
}

// 5. Main Class
public class AdapterPatternDemo {

    public static void main(String[] args) {

        // Create Adaptee
        XmlDataProvider xmlProvider = new XmlDataProvider();

        // Create Adapter
        IReports adapter = new XmlDataProviderAdapter(xmlProvider);

        // Raw Data
        String rawData = "Alice:42";

        // Client
        Client client = new Client();
        client.getReport(adapter, rawData);
    }
}
```

- object adapter -> composition
- class adapter -> inheritance
- Composition over inheritence in real world application.

# Usecase
- Third party like Notification, payment
- legacy code
