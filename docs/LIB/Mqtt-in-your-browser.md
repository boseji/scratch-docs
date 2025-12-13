# MQTT in your browser

Source <https://gist.github.com/narutaro/6461c0524f7d7ff01e21c2ecb0be84ca#file-mqtt-in-your-browser-md>

MQTT is probably best known as a lightweight messaging protocol implemented for small sensors, but there is actually a JavaScript implementation called `MQTT.js`. It's a JavaScript implementation, so of course it works in a browser. I think it's a great option for front-end engineers who are working with MQTT/IoT-related projects (for example, creating a dashboard to visualize MQTT data). In this article, I'd like to write about what I did when I tried to connect `MQTT.js` to the test server (broker) of `Mosquitto™`.

- [MQTT.js](https://github.com/mqttjs/MQTT.js)
- [Mosquitto™](https://test.mosquitto.org/)

#### References for MQTT using WebPages

- How to communicate an ESP32 with a web page via MQTT

    <https://www.luisllamas.es/en/how-to-communicate-an-esp32-with-a-web-page-through-mqtt/>

- MQTT Web dashboard | MQTT Web App using HTML , CSS and Java Script (Video)

    <https://www.youtube.com/watch?v=rlnhd67PV-M>

    ![type:video](https://www.youtube.com/embed/rlnhd67PV-M)

## Sample code for MQTT in HTML Page

It's very simple, but the following code should work. You should see `{"name": "sensor1", "temp": 10}` in your browser console. As a scenario, I made it so that `sensor1` in `floor1/room1` is sending the temperature. MQTT topics are generally hierarchical with `/`.

```html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>MQTT</title>.
  <script src="https://unpkg.com/mqtt/dist/mqtt.min.js"></script>
</head>
<body>

<script>
let client = mqtt.connect('wss://test.mosquitto.org:8081');
let topic = "floor1/room1"
let metric = '{"name": "sensor1", "temp": 10}'

client.subscribe(topic);
client.publish(topic, metric);

client.on('message', function (topic, message) { // message is Buffer
  console.log(message.toString());
});

client.end();
</script>

</body
</html>
```

* When throwing MQTT from a browser, it is common to use `MQTT over WebSocket` since you can't throw it directly.
* Therefore, the protocol specification in the URI should be `wss://test.mosquitto.org:8081`.

### MQTT Publish periodically, like a sensor from HTML Page

Change the code to send data periodically.

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="utf-8">
  <title>MQTT DASH</title>.
  <script src="https://unpkg.com/mqtt/dist/mqtt.min.js"></script>
</head>

<body>

<script>
let client = mqtt.connect('wss://test.mosquitto.org:8081');
let topic = "floor1/room1"

client.subscribe(topic);

pubLoop = setInterval(() => {
  const time = Date.now().toString();
  const temp = Math.floor( Math.random() * 11 );
  let metric = '{"time":' + time + ', "name": "sensor1", "temp":' + temp + '}'
  client.publish(topic, metric);
}, 1000);

client.on('message', function (topic, message) { // message is Buffer
  console.log(message.toString());
});

setTimeout(function() { clearInterval( pubLoop ); }, 10000); // stop after 10sec

</script>

</body>
</html>
```

Console output. Well, it's starting to look like sensor data.

```json
{"time":1588127649527, "name": "sensor1", "temp":6}
{"time":1588127650532, "name": "sensor1", "temp":4}
{"time":1588127651530, "name": "sensor1", "temp":6}
{"time":1588127652529, "name": "sensor1", "temp":1}
{"time":1588127653531, "name": "sensor1", "temp":3}
{"time":1588127654530, "name": "sensor1", "temp":8}
{"time":1588127655528, "name": "sensor1", "temp":10}
{"time":1588127656529, "name": "sensor1", "temp":10}
{"time":1588127657530, "name": "sensor1", "temp":4}
```

### Separate `pub` / `sub` for MQTT on HTML Page

It might be easier to separate the pub and sub instances like this:

```html

<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="utf-8">
  <title>MQTT DASH</title>.
  <script src="https://unpkg.com/mqtt/dist/mqtt.min.js"></script>
</head>

<body>

<script>

let pub = mqtt.connect('wss://test.mosquitto.org:8081');
let sub = mqtt.connect('wss://test.mosquitto.org:8081');
let topic = "floor1/room1"


sub.subscribe(topic);

pubLoop = setInterval(() => {
  const time = Date.now().toString();
  const amp = Math.floor( Math.random() * 11 );
  const tem = Math.floor( Math.random() * 11 );
  const hum = Math.floor( Math.random() * 11 );
  let metric = '{"time":' + time + ', "name": "sensor1", "amp":' + amp + ', "temp":' + tem + ', "hum":' + hum + '}'
  pub.publish(topic, metric);
  console.log("pub: " + metric);
}, 1000);

sub.on('message', function (topic, message) { // message is Buffer
  console.log("sub: " + message.toString());
});

setTimeout(function() {
  clearInterval( pubLoop );
  pub.end();
  sub.end();
}, 10000); // stop after 10sec

</script>

</body
</html>
```

Now your browser should work as sensors which do publish and subscription

----
<!-- Footer Begins Here -->
## Links

- [Back to Root Document](../README.md)

