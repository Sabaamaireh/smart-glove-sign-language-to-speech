# smart-glove-sign-language-to-speech
ESP32-based smart glove that converts sign language gestures into speech using flex sensors, MPU6050, and DFPlayer Mini.
#include <Wire.h>
#include <Adafruit_MPU6050.h>
#include <Adafruit_Sensor.h>
#include <HardwareSerial.h>
#include <DFRobotDFPlayerMini.h>

// ================= MPU6050 =================
Adafruit_MPU6050 mpu;

// ================= FLEX SENSOR PINS =================
#define FLEX1 34
#define FLEX2 35
#define FLEX3 32
#define FLEX4 33
#define FLEX5 25

// ================= DFPLAYER =================
HardwareSerial mySerial(1);
DFRobotDFPlayerMini player;

// ================= AUDIO CONTROL =================
bool isPlaying = false;

void setup() {

  Serial.begin(115200);

  // ================= MPU6050 =================
  Wire.begin(21, 22);
  Wire.setClock(100000);

  if (!mpu.begin()) {

    Serial.println("MPU6050 NOT Found");

    while (1);
  }

  Serial.println("MPU6050 Ready");

  // ================= DFPLAYER =================
  mySerial.begin(9600, SERIAL_8N1, 16, 17);

  delay(2000);

  if (!player.begin(mySerial)) {

    Serial.println("DFPlayer Error");

    while(true);
  }

  Serial.println("DFPlayer Ready");

  player.volume(30);
}

void loop() {

  // ================= FLEX READINGS =================
  int thumb  = analogRead(FLEX1);
  int index  = analogRead(FLEX2);
  int middle = analogRead(FLEX3);
  int ring   = analogRead(FLEX4);
  int pinky  = analogRead(FLEX5);

  // ================= MPU6050 READINGS =================
  sensors_event_t a, g, temp;

  mpu.getEvent(&a, &g, &temp);

  // ================= PRINT FLEX =================
  Serial.println("===== FLEX =====");

  Serial.print("Thumb: ");
  Serial.println(thumb);

  Serial.print("Index: ");
  Serial.println(index);

  Serial.print("Middle: ");
  Serial.println(middle);

  Serial.print("Ring: ");
  Serial.println(ring);

  Serial.print("Pinky: ");
  Serial.println(pinky);

  // ================= PRINT MPU =================
  Serial.println("===== MPU6050 =====");

  Serial.print("Accel X: ");
  Serial.println(a.acceleration.x);

  Serial.print("Accel Y: ");
  Serial.println(a.acceleration.y);

  Serial.print("Accel Z: ");
  Serial.println(a.acceleration.z);

  // =====================================================
  // ================= STOP ==============================
  // =====================================================

  if (

    thumb > 600 && thumb < 880 &&
    index > 1000 && index < 1300 &&
    middle > 700 && middle < 1000 &&
    ring > 800 && ring < 1100 &&
    pinky > 1900 && pinky < 2200 &&

    // Broad MPU Orientation
    // Broad MPU Orientation
a.acceleration.x > -11.0 &&
a.acceleration.x < -7.0 &&

a.acceleration.y > -5.0 &&
a.acceleration.y < 5.0 &&

a.acceleration.z > -4.0 &&
a.acceleration.z < 4.0

  )
  {

    Serial.println("Gesture Detected: STOP");

    if (!isPlaying) {

      isPlaying = true;

      delay(200);

      player.playMp3Folder(2);

      Serial.println("Playing STOP");

      delay(4000);

      isPlaying = false;
    }
  }

  // =====================================================
  // ================= NO ================================
  // =====================================================

  else if (

    thumb > 380 && thumb < 680 &&
    index > 280 && index < 390 &&
    middle > 300 && middle < 420 &&
    ring > 200 && ring < 380 &&
    pinky > 1550 && pinky < 1730 &&

    // Broad MPU Orientation
    a.acceleration.x > -2.0 &&
    a.acceleration.x < 5.0 &&

    a.acceleration.y > 8.0 &&
    a.acceleration.y < 11.5 &&

    a.acceleration.z > -2.0 &&
    a.acceleration.z < 5.0

  )
  {

    Serial.println("Gesture Detected: NO");

    if (!isPlaying) {

      isPlaying = true;

      delay(200);

      player.playMp3Folder(3);

      Serial.println("Playing NO");

      delay(4000);

      isPlaying = false;
    }
  }

  // =====================================================
  // ================= I HAVE A QUESTION =================
  // =====================================================

  else if (

    thumb > 80 && thumb < 180 &&
    index > 480 && index < 800 &&
    middle > 390 && middle < 560 &&
    ring > 220 && ring < 400 &&
    pinky > 1530 && pinky < 1800 &&

    // Broad MPU Orientation
// Broad MPU Orientation
a.acceleration.x > -11.0 &&
a.acceleration.x < -7.0 &&

a.acceleration.y > -5.0 &&
a.acceleration.y < 5.0 &&

a.acceleration.z > -4.0 &&
a.acceleration.z < 4.0
  )
  {

    Serial.println("Gesture Detected: I HAVE A QUESTION");

    if (!isPlaying) {

      isPlaying = true;

      delay(200);

      player.playMp3Folder(4);

      Serial.println("Playing QUESTION");

      delay(4000);

      isPlaying = false;
    }
  }

  // =====================================================
  // ================= I AM HUNGRY =======================
  // =====================================================

  else if (

    // FLEX CONDITIONS
    thumb > 70 && thumb < 420 &&
    index > 390 && index < 580 &&
    middle > 290 && middle < 500 &&
    ring > 270 && ring < 480 &&
    pinky > 1600 && pinky < 1820 &&

    // Broad MPU Orientation
    a.acceleration.x > -11.0 &&
    a.acceleration.x < -8.0 &&

    a.acceleration.y > -5.0 &&
    a.acceleration.y < 2.0 &&

    a.acceleration.z > -5.0 &&
    a.acceleration.z < 2

  )
  {

    Serial.println("Gesture Detected: I AM HUNGRY");

    if (!isPlaying) {

      isPlaying = true;

      delay(200);

      player.playMp3Folder(5);

      Serial.println("Playing I AM HUNGRY");

      delay(4000);

      isPlaying = false;
    }
  }

  // =====================================================
  // ================= OK ================================
  // =====================================================

  else if (

    thumb > 170 && thumb < 610 &&
    index > 340 && index < 425 &&
    middle > 270 && middle < 410 &&
    ring > 330 && ring < 390 &&
    pinky > 1570 && pinky < 1660 &&

    // Broad MPU Orientation
    a.acceleration.x > -6.0 &&
    a.acceleration.x < 2.0 &&

    a.acceleration.y > -11.0 &&
    a.acceleration.y < -7.0 &&

    a.acceleration.z > -4.0 &&
    a.acceleration.z < 4.0

  )
  {

    Serial.println("Gesture Detected: OK");

    if (!isPlaying) {

      isPlaying = true;

      delay(200);

      player.playMp3Folder(1);

      Serial.println("Playing OK");

      delay(4000);

      isPlaying = false;
    }
  }

  // =====================================================
  // ================= NO GESTURE ========================
  // =====================================================

  else {

    Serial.println("No Gesture Detected");
  }

  Serial.println("====================");
  Serial.println();

  delay(500);
}
