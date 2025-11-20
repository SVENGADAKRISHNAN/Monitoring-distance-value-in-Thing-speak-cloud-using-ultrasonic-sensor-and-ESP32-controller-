# Monitoring-distance-value-in-Thing-speak-cloud-using-ultrasonic-sensor-and-ESP32-controller

# Uploading ultrasonic sensor data in Thing Speak cloud

# NAME: S.VENGADA KRISHNAN
# REG:NO: 212223110061
# AIM:
To monitor the distance of the obstacle in the Thing speak cloud using ultrasonic sensor and ESP32 controller.
# Apparatus required:
@@ -96,8 +97,66 @@ Prototype and build IoT systems without setting up servers or developing web sof


# PROGRAM:
```
#include "ThingSpeak.h"
#include <WiFi.h>
char ssid[] = "vivo Y22"; //SSID
char pass[] = "12345678"; // Password
const int trigger = 2;
const int echo = 26;
long T;
float distanceCM;
WiFiClient client;
unsigned long myChannelField = 3172665; // Channel ID
const int ChannelField = 1; // Which channel to write data
const char * myWriteAPIKey = "JX41703K8UTKIAKC"; // Your write API Key
void setup()
{
  Serial.begin(115200);
  pinMode(trigger, OUTPUT);
  pinMode(echo, INPUT);
  WiFi.mode(WIFI_STA);
  ThingSpeak.begin(client);
}
void loop()
{
  if (WiFi.status() != WL_CONNECTED)
  {
    Serial.print("Attempting to connect to SSID: ");
    Serial.println(ssid);
    while (WiFi.status() != WL_CONNECTED)
    {
      WiFi.begin(ssid, pass);
      Serial.print(".");
      delay(5000);
    }
    Serial.println("\nConnected.");
  }
  digitalWrite(trigger, LOW);
  delay(1);
  digitalWrite(trigger, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigger, LOW);
  T = pulseIn(echo, HIGH);
  distanceCM = T * 0.034;
  distanceCM = distanceCM / 2;
  Serial.print("Distance in cm: ");
  Serial.println(distanceCM);
  ThingSpeak.writeField(myChannelField, ChannelField, distanceCM, myWriteAPIKey);
  delay(1000);
}
```
# CIRCUIT DIAGRAM:
<img width="624" height="536" alt="image" src="https://github.com/user-attachments/assets/38642c8d-99b2-4595-a1f0-6b8b4e8947ea" />

# OUTPUT:
<img width="1408" height="752" alt="exp7wind" src="https://github.com/user-attachments/assets/d1106d7f-0f44-447c-946e-de404ae42d5c" />

<img width="1328" height="800" alt="exp7graph" src="https://github.com/user-attachments/assets/db288c25-c3fa-4533-b9d8-3af1eab482c0" />


# RESULT:
Thus the distance values are updated in the Thing speak cloud using ESP32 controller.
