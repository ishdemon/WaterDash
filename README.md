# WaterDash
Water monitoring system that automatically controls Motor Pump using Android &amp; ESP32 & MQTT.


<h3> Why? </h3>
<i>Lets be real who doesn't hates this 😁👉</i>  <br><br>



https://user-images.githubusercontent.com/13925683/173885864-31b2fc91-7812-45ce-8751-cfe405e3365e.mp4



<br>
Jokes aside, traditional systems in market are pretty dumb and not at all smart. It uses a contact based sensor to know whether tank is full or not..<br>
- doesn't tell you how much water is there in tank<br>
- doesn't have App/remote access<br>
- not smart at all<br>

<h1> Software </h1>
<h3>DashBoard</h3>
<img src="/images/DashApp.png" height=300>
<br><br>
<img src="https://github.com/mqtt/mqttorg-graphics/blob/master/mqtt-logo-250.png">
ESP32 also communicates with an MQTT Broker. It publishes all the data to the broker. In my case https://mosquitto.org/ locally hosted in a RaspberryPi. Since my users will just be under 10 at most, i chose to host it local but one can use a Cloud MQTT service if need to handle large users.
<br><br><img src="https://mqtt.org/assets/img/mqtt-publish-subscribe.png" height= 200>
<h3>Companion Phone App</h3>
<img src="/images/22-06-08-00-22-33_AdobeExpress.gif"> 




<h1> Hardware </h1>
<h3></h3>
<h3>ESP32 Module</h3>
ESP32 board is the MCU that controls the pump & collects data from various sensors ( Energy, LPG/Smoke, etc). It communicates with an Android device over USB Serial communication to display all the data.
<h3></h3>
<h3>Android Phone(5.0+) with USB OTG supported</h3>
Android phone maintains a serial connection with the ESP32 board & recieves data (JSON payload) every second. Its a full duplex connection so it also sends controls commands back to the board. I have used a rooted Samsung galaxy S4 with lineage OS to keep it light as possible.<br>
<br>
<img src="/images/diagram.png">


<h2> Features</h2>
1) Calculates Percentage of water in tank(I used Cylindrical)<br>
2) Modes : Auto & Direct(Manual) to cover all the general usecases in typical home.<br>
3) Automatically fills the overhead tank and turns off the Pump based on water availability.<br>
4) Calculates Load(power) connected, AC voltage, current, power factor, frequency.<br>
5) Temperature/ Humidity.<br>
6) LPG Gas leakage alarm.<br>
7) Shows Everything in a cool UI based on Android.

<h3> Pump Protection</h3>
Using Flow sensor in the outlet line of Pump, it detects the waterflow & accordingly switches off to avoid dry running of motor pump.
<h3></h3>

Flow             |  No Flow
:-------------------------:|:-------------------------:
<img src="/images/flow.gif">  |  <img src="/images/noflow.gif">

<h1> Case Design </h1>
<img src="/images/1.png" height=300>
<img src="/images/2.png" height=300>
<img src="/images/3.png" height=300>
<img src="/images/4.png" height=300>

<h2>Challenges faced</h2>
Since USB will be occupied for communicating with ESP32 MCU, you can't really charge the phone. I had to figure out to run the phone without USB power. 
Tried using a Li-ion charger board to directly charge the battery but it got heated up quite a bit.
Managed to run the device directly without battery by supplying a ~4.4v directly onto terminals. Phone detects it as a battery & it always shows 100%. Great success!


