# MQTT.js Client Example

## Overview
This is an MQTT client example project that showcases how you can use HiveMQ Cloud with the MQTT.js Client. The example project covers the basic MQTT functionality: Connecting MQTT clients to your HiveMQ Cloud cluster, subscribing to topics and publishing data (sending and receiving messages using the MQTT protocol).

The Javascript client used here supports MQTT v3.1, v3.1.1 and v5.
You can find documentation for this client library here: https://www.hivemq.com/blog/mqtt-client-library-mqtt-js/.

This example repository is easily and clearly structured, so you can start quickly:
This readme file is your starting point. Here we will describe what you have to do step-by-step to get started with this example.
[``example.js``](example.js) is a simple implementation that demonstrates the core functionality of an MQTT Client.
Follow the instructions in the following paragraphs to get started yourself.

## HiveMQ Cloud
[HiveMQ](https://www.hivemq.com/) is the industry leader for enterprise-ready, beautifully scalable, large-scale IoT deployments with MQTT. We help companies connect things to the Internet. Our MQTT-based messaging platform ensures fast, reliable, and secure movement of data to and from connected IoT devices for companies around the world. HiveMQ Cloud is our fully-managed, cloud-native IoT messaging platform that makes trustworthy and scalable IoT device connectivity simple. You can learn more about HiveMQ Cloud on our [website](https://www.hivemq.com/mqtt-cloud-broker/), [documentation](https://www.hivemq.com/docs/hivemq-cloud/introduction.html)  and our [blog posts](https://www.hivemq.com/tags/cloud/).

## Getting started
[By signing up](https://console.hivemq.cloud) for HiveMQ Cloud you will automatically get access to a HiveMQ Cloud Basic cluster. HiveMQ Cloud Basic is our smallest package that allows you to connect up to 100 MQTT clients for free and test the full MQTT functionality. 

The [HiveMQ Cloud Quick Start Guide](https://www.hivemq.com/docs/hivemq-cloud/introduction.html#guide) gives you step-by-step instructions on how to set up your HiveMQ Cloud account, create clusters, and connect MQTT clients.


### Prerequisites 
After signing up, you have a running HiveMQ Cloud cluster, that you can use in this example.
Now clone this repository into your local IDE.

For using the code examples, you need to install [MQTT.js](https://github.com/mqttjs/MQTT.js).
Execute this command in the terminal of your IDE to install all dependencies.
```sh
npm install
```

### Broker credentials
To define the HiveMQ Cloud cluster which should be targeted, you need to fill the placeholders in the code with your host name, username and password.
The <b>host name</b> can be found in the <b>Details</b> section of the <b>Overview</b> tab of your cluster.
![cluster overview](/img/hivemq-cloud-cluster-overview.png)

After the cluster is created, add a set of credentials that you can use in this example or future implementations.
Use any secure username and password you desire.
The <b>username</b> and <b>password</b> are the values used as <b>Client Credentials</b> that you just created.
![credentials](/img/hivemq-cloud-credentials.png)

### Code Examples
This example project covers the core functionality of an MQTT client interacting with HiveMQ Cloud.
To securely connect the MQTT client with HiveMQ Cloud you need to enable TLS.
Use your username and password, to authenticate your MQTT client at HiveMQ Cloud.
To connect the client, use the port 8883 that is standard for secure MQTT communication. 

```js
const options = {
  username: '<your_username>',
  password: '<your_password>',
  rejectUnauthorized: false
};
```
```js
const client = mqtt.connect('tls://your_host:port', options);
```

The code located inside the ``example.js`` connects to the configured HiveMQ Cloud Broker.
This is a ready-set example that can simply be run after inputting your credentials by executing this command in the terminal of your IDE.
```sh
node example.js
```

The code first subscribes to the topic filter ``'messages'``.  
That means the MQTT client receives all messages that are published to this [topic filter](https://www.hivemq.com/blog/mqtt-essentials-part-5-mqtt-topics-best-practices/).
```js
client.subscribe('messages');
```

Then the code publishes a message to the same topic.
```js
client.publish('messages', 'Hello, this message was received!');
```

The callback gets triggered when a message is received and prints it to the console.
```js
client.on('message', function(topic, message) {
  console.log(String.fromCharCode.apply(null, message)); // need to convert the byte array to string
});
```
There are also callbacks for a successful connection and when an error occurs. 


## Learn more
If you want to learn more about MQTT, visit the [MQTT Essentials](https://www.hivemq.com/mqtt-essentials/) guide, that explains the core of MQTT concepts, its features and other essential information. Learn about MQTT.js at the [official Github repository](https://github.com/mqttjs).

## Contributing

Please see our [contributing guidelines](./CONTRIBUTING.adoc) and [code of conduct](./code-of-conduct.md).

## License

[Apache 2.0](./LICENSE).
