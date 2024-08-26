# ESP-NOW Communications

Reference:

- Why ESPNow is awesome - hint: ACKs & Retries!

	<https://www.youtube.com/watch?v=Xmzk6v5qIjo>

	Video talks about Retires and Broadcast mode.
	Which one is more reliable and why.

- ESP-NOW - Peer to Peer ESP32 Network

	<https://www.youtube.com/watch?v=bEKjCDDUPaU>

	Basic Introduction to ESP-NOW but missing the important
	point about channels and key differences between the ESP8266
	and ESP32 implementations of ESP-NOW.

	<https://dronebotworkshop.com/esp-now/>

	Companion website for the Video.

-  ESPNOW for beginners! #ESP32 #ESP8266 

	<https://www.youtube.com/watch?v=Ydi0M3Xd_vs>

	Specifically Focused on ESP32 and
	explains the trick to Auto detect the ESP Slave MAC ID
	directly from its AP.
	Does not go over the issues with Channel in ESP8266.

	<https://github.com/programming-electronics-academy/espnow-minimum>

	Source code for the Video.

-  ESPNOW mix with #ESP32 and #ESP8266 

	<https://www.youtube.com/watch?v=_eHe7ViXyY8>

	How to migrate the ESP32 examples over to ESP8266.
	But still does not talk about the Channel Gotcha.

## ESP8266 as ESP-NOW Master (Send Only)

This is a Send only configuration for ESP8266. It needs another board to be in the role as a Receiver to get the data sent.

**Note:** We are not selecting any **CHANNEL** here in the code its assumed to
be `1` since there is no way to change this in Master.

#### Includes and Globals

```c
// Includes
#include <ESP8266WiFi.h>
#include <espnow.h>

// REPLACE WITH YOUR RECEIVER MAC Address
uint8_t broadcastAddress[] = {0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF};
// uint8_t broadcastAddress[] = {0x01, 0x02, 0x03, 0x04, 0x05, 0x06};

String myData = "Test";
```

#### Basic Setup

```c
// Setup

// For Maximum Message length of ESP-NOW + 1
myData.reserve(251);

// Set device as a Wi-Fi Station
WiFi.mode(WIFI_STA); // Selects Channel 0 by default

// Initialize ESP-NOW
if (esp_now_init() != 0) {
  Serial.println("Error initializing ESP-NOW");
  return;
} else {
  Serial.println("Initialized ESP-NOW");
}
```

#### Configure ESP-NOW

```c
// Setup continued

  // Once ESPNow is successfully Init, we will register for Send CB to
  // get the status of Transmitted packet
  esp_now_set_self_role(ESP_NOW_ROLE_CONTROLLER);
  esp_now_register_send_cb(OnDataSent);
```
Here `OnDataSent` is a Call Back function.

This call back function is called when the transmission completes.

#### Address Registration

```c
// Global

// REPLACE WITH YOUR RECEIVER MAC Address
uint8_t broadcastAddress[] = { 0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF };
// uint8_t broadcastAddress[] = {0x01, 0x02, 0x03, 0x04, 0x05, 0x06};
```

```c
// Setup continued

// Add peer - Channel 0 Password NULL Password_Length 0
if (esp_now_add_peer(broadcastAddress, ESP_NOW_ROLE_SLAVE, 0, NULL, 0) != 0) {
Serial.println("Failed to add peer");
return;
} else {
Serial.println("Added peer");
}

if (esp_now_is_peer_exist(broadcastAddress)) {
    Serial.println("Peer exists");
} else {
    Serial.println("No exists");
}
```

Here we are using a **Broadcast address** means that every node listening
on the ESP-NOW network will receive the data being transmitted.

This can be changed to a Specific MAC address to select 
a particular destination.

#### Sending Messages

```c
// Send message via ESP-NOW
int result = esp_now_send(broadcastAddress, (uint8_t *)myData.c_str(),
							myData.length());

if (result == 0) {
	Serial.println("Sent with success");
} else {
	Serial.println("Error sending the data");
}
```

#### Callback for Transmit Complete

```c
// Callback function called when data is sent
void OnDataSent(uint8_t *mac_addr, uint8_t status) {
  Serial.print("\r\nLast Packet Send Status:\t");
  Serial.println(status == 0 ? "Delivery Success" : "Delivery Fail");
}
```

## ESP8266 as ESP-NOW Slave (Receive Only)

This is the counter part of the ESP-NOW for the Transmit only example
[above](#esp8266-as-esp-now-master-send-only). This example is designed
for Receive only operation. This program if loaded on multiple boards will
receive message from the Master sending on **Broadcast Address**.

**Note:** We are not selecting any **CHANNEL** here in the code its assumed to
be `1` since there is no way to change this in Master.

#### Includes and Globals

```c
// Includes
#include <ESP8266WiFi.h>
#include <espnow.h>

// Maximum Size of 250 Bytes for ESP-NOW
#define MAX_SIZE 251
char myData[MAX_SIZE];
```

#### Basic Setup

```c
// Setup

// Set device as a Wi-Fi Station
WiFi.mode(WIFI_STA); // Defaults to Channel 0

// Initilize ESP-NOW
if (esp_now_init() != 0) {
Serial.println("Error initializing ESP-NOW");
return;
} else {
Serial.println("Initialized ESP-NOW");
}

// Once ESPNow is successfully Init, we will register for recv CB to
// get recv packer info
esp_now_set_self_role(ESP_NOW_ROLE_SLAVE);
esp_now_register_recv_cb(OnDataRecv);
```

Here `OnDataRecv` is a call back function that is called in the
slave upon receiving data from the Master.

#### Callback for Received Data

```c
// Callback function called when data is Received
void OnDataRecv(uint8_t *mac, uint8_t *incomingData, uint8_t len) {
  Serial.print("\r\nReceived From MAC Address = ");
  Serial.printf("%02x:%02x:%02x:%02x:%02x:%02x",
    mac[0],mac[1],mac[2],mac[3],mac[4],mac[5]);
  Serial.print("\r\nReceived Packet:\t");
  memcpy(myData, incomingData, len);
  Serial.print("len(");
  Serial.print(len);
  Serial.print(") \"");
  Serial.print(myData);
  Serial.print("\"");
}
```

## ESP8266 as ESP-NOW Master with Auto Address detection

```c
// Slave MAC Auto-Populated 
uint8_t broadcastAddress[6]={
    0xFF, 0xFF, 0xFF, 
    0xFF, 0xFF, 0xFF
};
```

#### Auto populate the MAC ID of Slave

```c
// Find a Single slave to talk to directly
bool ScanForSlave() {
  int8_t scanResults = WiFi.scanNetworks();

  // Find the Networks
  for (int i = 0; i < scanResults; ++i) {
    String SSID = WiFi.SSID(i);
    String BSSIDstr = WiFi.BSSIDstr(i);

    // Identifier for the Slave
    if (SSID.indexOf("RX_") == 0) {
      Serial.print("Found Slave -> ");
      Serial.println(BSSIDstr.c_str());
      int mac[6];
      if ( 6 == sscanf(BSSIDstr.c_str(), "%x:%x:%x:%x:%x:%x",  
        &mac[0], &mac[1], &mac[2], &mac[3], &mac[4], &mac[5] ) ) {
        for (int ii = 0; ii < 6; ++ii ) {
          broadcastAddress[ii] = (uint8_t) mac[ii];
        }
      }

      return true;
    }
  }
  return false;
}
```

#### New Initialization Step

```c
// Detect the Slaves
do{
	Serial.println("...Scanning for Slaves...");
	delay(2000);
}while(!ScanForSlave());

// Add peer - Channel 0 Password NULL Password_Length 0
if (esp_now_add_peer(broadcastAddress, ESP_NOW_ROLE_SLAVE, 0, NULL, 0) != 0) {
...
```

Rest everything remains same.

**Note:** Here only one Slave is auto detected but the 
[function](#auto-populate-the-mac-id-of-slave) shown can
be expanded to cover more Slaves in the same way.

## ESP8266 as ESP-NOW Slave with support for Auto Detection

```c
// Globals

// Prepare the Access Point Name ('RX_' + Last 3 MAC)
char apName[9+4+1];
```

```c
// Update Setup

// Set device as a Wi-Fi AP For easier Identification
WiFi.mode(WIFI_AP);
// Build the AP Name
String mac = WiFi.macAddress();
sprintf(apName, "RX_%s", mac.substring(9));
// Start the AP - Non-Hidden AP, Channel 0, Max Connections 0
WiFi.softAP(apName, "RX_1_Password", 0, 0, 0);

```

The AP Here helps to get detected on the Master Side easily.

And would generate a AP Name unique to the specific ESP8266.

----
<!-- Footer Begins Here -->
## Links

- [Back to Root Document](../README.md)
