<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "acd4010e430da00946a154f62847a169",
  "translation_date": "2025-06-18T09:45:44+00:00",
  "source_file": "03-GettingStarted/06-http-streaming/solution/java/README.md",
  "language_code": "ne"
}
-->
# Calculator HTTP Streaming Demo

यस प्रोजेक्टले Server-Sent Events (SSE) प्रयोग गरी Spring Boot WebFlux मार्फत HTTP स्ट्रिमिङ कसरी गर्ने देखाउँछ। यसमा दुईवटा एप्लिकेसनहरू छन्:

- **Calculator Server**: एक प्रतिक्रियाशील वेब सेवा जसले गणना गर्छ र SSE मार्फत परिणाम स्ट्रिम गर्छ
- **Calculator Client**: स्ट्रिमिङ इन्डपोइन्ट प्रयोग गर्ने क्लाइन्ट एप्लिकेसन

## पूर्व आवश्यकताहरू

- Java 17 वा माथि
- Maven 3.6 वा माथि

## प्रोजेक्ट संरचना

```
java/
├── calculator-server/     # Spring Boot server with SSE endpoint
│   ├── src/main/java/com/example/calculatorserver/
│   │   ├── CalculatorServerApplication.java
│   │   └── CalculatorController.java
│   └── pom.xml
├── calculator-client/     # Spring Boot client application
│   ├── src/main/java/com/example/calculatorclient/
│   │   └── CalculatorClientApplication.java
│   └── pom.xml
└── README.md
```

## यो कसरी काम गर्छ

1. **Calculator Server** ले `/calculate` endpoint that:
   - Accepts query parameters: `a` (number), `b` (number), `op` (operation)
   - Supported operations: `add`, `sub`, `mul`, `div`
   - Returns Server-Sent Events with calculation progress and result

2. The **Calculator Client** connects to the server and:
   - Makes a request to calculate `7 * 5` इन्डपोइन्ट प्रदान गर्छ
   - स्ट्रिमिङ प्रतिक्रिया ग्रहण गर्छ
   - प्रत्येक इभेन्टलाई कन्सोलमा प्रिन्ट गर्छ

## एप्लिकेसनहरू चलाउने तरिका

### विकल्प १: Maven प्रयोग गरी (सिफारिस गरिएको)

#### १. Calculator Server सुरु गर्नुहोस्

टर्मिनल खोल्नुहोस् र server डाइरेक्टरीमा जानुहोस्:

```bash
cd calculator-server
mvn clean package
mvn spring-boot:run
```

सर्भर `http://localhost:8080` मा सुरु हुनेछ

तपाईंले यस्तो आउटपुट देख्नुहुनेछ:
```
Started CalculatorServerApplication in X.XXX seconds
Netty started on port 8080 (http)
```

#### २. Calculator Client चलाउनुहोस्

नयाँ टर्मिनल खोल्नुहोस् र client डाइरेक्टरीमा जानुहोस्:

```bash
cd calculator-client
mvn clean package
mvn spring-boot:run
```

क्लाइन्ट सर्भरसँग जडान हुनेछ, गणना गर्नेछ र स्ट्रिमिङ परिणाम देखाउनेछ।

### विकल्प २: Java सिधै प्रयोग गरी

#### १. सर्भर कम्पाइल र चलाउनुहोस्:

```bash
cd calculator-server
mvn clean package
java -jar target/calculator-server-0.0.1-SNAPSHOT.jar
```

#### २. क्लाइन्ट कम्पाइल र चलाउनुहोस्:

```bash
cd calculator-client
mvn clean package
java -jar target/calculator-client-0.0.1-SNAPSHOT.jar
```

## सर्भर म्यानुअली परीक्षण गर्ने तरिका

तपाईं वेब ब्राउजर वा curl प्रयोग गरेर पनि सर्भर परीक्षण गर्न सक्नुहुन्छ:

### वेब ब्राउजर प्रयोग गरी:
भिजिट गर्नुहोस्: `http://localhost:8080/calculate?a=10&b=5&op=add`

### curl प्रयोग गरी:
```bash
curl "http://localhost:8080/calculate?a=10&b=5&op=add" -H "Accept: text/event-stream"
```

## अपेक्षित आउटपुट

क्लाइन्ट चलाउँदा तपाईंले यस्तो स्ट्रिमिङ आउटपुट देख्नुहुनेछ:

```
event:info
data:Calculating: 7.0 mul 5.0

event:result
data:35.0
```

## समर्थित अपरेसनहरू

- `add` - Addition (a + b)
- `sub` - Subtraction (a - b)
- `mul` - Multiplication (a * b)
- `div` - Division (a / b, returns NaN if b = 0)

## API Reference

### GET /calculate

**Parameters:**
- `a` (required): First number (double)
- `b` (required): Second number (double)
- `op` (required): Operation (`add`, `sub`, `mul`, `div`)

**Response:**
- Content-Type: `text/event-stream`
- गणनाको प्रगति र परिणाम सहित Server-Sent Events फिर्ता गर्छ

**उदाहरण अनुरोध:**
```
GET /calculate?a=7&b=5&op=mul HTTP/1.1
Host: localhost:8080
Accept: text/event-stream
```

**उदाहरण प्रतिक्रिया:**
```
event: info
data: Calculating: 7.0 mul 5.0

event: result
data: 35.0
```

## समस्या समाधान

### सामान्य समस्या

1. **पोर्ट 8080 पहिले नै प्रयोगमा छ**
   - पोर्ट 8080 प्रयोग गरिरहेका अन्य एप्लिकेसनहरू बन्द गर्नुहोस्
   - वा `calculator-server/src/main/resources/application.yml`

2. **Connection refused**
   - Make sure the server is running before starting the client
   - Check that the server started successfully on port 8080

3. **Parameter name issues**
   - This project includes Maven compiler configuration with `-parameters` flag
   - If you encounter parameter binding issues, ensure the project is built with this configuration

### Stopping the Applications

- Press `Ctrl+C` in the terminal where each application is running
- Or use `mvn spring-boot:stop` मा सर्भर पोर्ट परिवर्तन गर्नुहोस् यदि ब्याकग्राउन्डमा चलिरहेको छ भने

## प्रविधि स्ट्याक

- **Spring Boot 3.3.1** - एप्लिकेसन फ्रेमवर्क
- **Spring WebFlux** - प्रतिक्रियाशील वेब फ्रेमवर्क
- **Project Reactor** - प्रतिक्रियाशील स्ट्रिम लाइब्रेरी
- **Netty** - नन-ब्लकिङ I/O सर्भर
- **Maven** - बिल्ड टुल
- **Java 17+** - प्रोग्रामिङ भाषा

## अर्को कदमहरू

कोडमा परिवर्तन गरेर प्रयास गर्नुहोस्:
- थप गणितीय अपरेसनहरू थप्नुहोस्
- अमान्य अपरेसनको लागि त्रुटि ह्यान्डलिङ समावेश गर्नुहोस्
- अनुरोध/प्रतिक्रिया लगिङ थप्नुहोस्
- प्रमाणीकरण लागू गर्नुहोस्
- युनिट टेस्टहरू थप्नुहोस्

**अस्वीकरण**:  
यो दस्तावेज AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरी अनुवाद गरिएको हो। हामी शुद्धताका लागि प्रयासरत छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादमा त्रुटि वा अशुद्धता हुन सक्छ। मूल दस्तावेज यसको मूल भाषामा आधिकारिक स्रोत मानिनु पर्छ। महत्वपूर्ण जानकारीका लागि व्यावसायिक मानवीय अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न कुनै पनि गलतफहमी वा गलत व्याख्याका लागि हामी जिम्मेवार छैनौं।