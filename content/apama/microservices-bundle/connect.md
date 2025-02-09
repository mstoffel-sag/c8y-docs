---
weight: 30
title: Connecting to the Cumulocity IoT platform
layout: redirect
---

To support making these requests, we provide a helper event with actions to automatically connect to the {{< product-c8y-iot >}} platform and then create requests which can be used to call other microservices. This helper event is called `CumulocityRequestInterface` and is within the `com.apama.cumulocity` package. This helper event provides a static action which will connect to {{< product-c8y-iot >}} and return an instance of the event. It can automatically connect either from within a microservice or the {{< product-c8y-iot >}} platform itself, or from a remote correlator. That instance has an action which will create a request to call a specific microservice.

To create the connection from your own code, simply call the `connectToCumulocity` method and store the result:

```java
CumulocityRequestInterface cumulocity := CumulocityRequestInterface.connectToCumulocity();
```

This will automatically create a connection using the credentials and connection details provided to your microservice, or using the configuration for the {{< product-c8y-iot >}} transport when connecting from an external Apama instance.
