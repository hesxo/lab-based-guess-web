Here’s your complete documentation for the Coconut Beetle Indicator – FFT-Based Prototype, now including a configurable sound frequency range, threshold level, and tree height parameter – all implemented as easily adjustable configuration values in the Arduino sketch.

⸻

🐞 Coconut Beetle Indicator – FFT-Based Prototype

Using Arduino Nano + MAX4466 Microphone + LED Alerts

⸻

📌 1. Project Purpose

This prototype aims to detect Coconut Rhinoceros Beetles by analyzing their acoustic signatures using Fast Fourier Transform (FFT) on an Arduino Nano. The system processes ambient sound and identifies beetle presence based on frequency-domain analysis, triggering LED indicators for visual alerts.

⸻

🧪 2. Design Assumptions (For Prototype)
	•	No sound loss through air or materials (ideal conditions)
	•	The microphone is placed securely near the base of the coconut tree
	•	Tree height and sound frequency parameters are user-configurable
	•	Beetle activity produces sound in a target frequency range (e.g., 3–6 kHz)
	•	The FFT is performed in software using Arduino resources only

⸻

🔩 3. Required Hardware

Component	Quantity	Description
Arduino Nano	1	Main microcontroller
MAX4466 Mic Module	1	Electret mic with analog waveform output
Red LED	1	Indicates confirmed beetle presence
Yellow LED	1	Indicates possible beetle activity
Green LED	1	Indicates system is active
Push Button	1	For manual reset
Resistors (220Ω, 10kΩ)	~4	For LEDs and pull-down for button
Breadboard & Wires	–	For prototyping connections


⸻

📐 4. Wiring Schematic

Arduino Pin	Connection
A0	MAX4466 OUT (audio analog)
D2	Green LED (via 220Ω to GND)
D3	Yellow LED (via 220Ω to GND)
D4	Red LED (via 220Ω to GND)
D5	Push Button (to GND w/ pull-up)
5V	MAX4466 VCC
GND	MAX4466 GND + all components


⸻

⚙️ 5. Software Configuration Parameters

These are defined at the top of the Arduino sketch and are easy to adjust for calibration:

// ---------------------- CONFIGURABLE PARAMETERS ----------------------
float treeHeightMeters = 10.0;        // Coconut tree height in meters
double detectionMinFreq = 3000.0;     // Minimum frequency to detect (Hz)
double detectionMaxFreq = 6000.0;     // Maximum frequency to detect (Hz)
double detectionThreshold = 100.0;    // FFT magnitude threshold
// ---------------------------------------------------------------------


⸻

🧠 6. Detection Logic

✅ FFT (Fast Fourier Transform)
	•	Converts 64 audio samples (time domain) into frequency data (frequency domain)
	•	Sampling rate: ~10 kHz (sufficient for 5kHz signal analysis)
	•	FFT is used to isolate sound within the beetle’s frequency band

✅ Time Frames
	•	5 seconds = 1 analysis window (called a frame)
	•	If beetle-like sound is detected in:
	•	1 frame → Yellow LED (possible beetle)
	•	3 consecutive frames (15 seconds) → Red LED (confirmed beetle)

⸻

💡 7. LED Behavior Summary

Condition	LED Indicator
System running	Green LED ON
Beetle detected (1 frame)	Yellow LED ON
Beetle confirmed (3 frames)	Red LED ON
Reset button pressed	All LEDs OFF, system restarted


⸻

🧮 8. Full Arduino Sketch (Final Version)

#include <arduinoFFT.h>

// ---------------------- CONFIGURABLE PARAMETERS ----------------------
float treeHeightMeters = 10.0;        // Coconut tree height in meters
double detectionMinFreq = 3000.0;     // Minimum frequency to detect (Hz)
double detectionMaxFreq = 6000.0;     // Maximum frequency to detect (Hz)
double detectionThreshold = 100.0;    // FFT magnitude threshold
// ---------------------------------------------------------------------

arduinoFFT FFT = arduinoFFT();
const uint16_t samples = 64;
double vReal[samples];
double vImag[samples];

// Pins
const int micPin = A0;
const int greenLED = 2;
const int yellowLED = 3;
const int redLED = 4;
const int resetButton = 5;

// Time and state
unsigned long lastFrameTime = 0;
const unsigned long frameDuration = 5000; // 5s frame
int frameCount = 0;

void setup() {
  Serial.begin(9600);
  pinMode(greenLED, OUTPUT);
  pinMode(yellowLED, OUTPUT);
  pinMode(redLED, OUTPUT);
  pinMode(resetButton, INPUT_PULLUP);
  digitalWrite(greenLED, HIGH); // System is ON
}

void loop() {
  if (digitalRead(resetButton) == LOW) {
    resetSystem();
    return;
  }

  unsigned long currentMillis = millis();
  if (currentMillis - lastFrameTime >= frameDuration) {
    lastFrameTime = currentMillis;

    captureAudio();
    FFT.Windowing(vReal, samples, FFT_WIN_TYP_HAMMING, FFT_FORWARD);
    FFT.Compute(vReal, vImag, samples, FFT_FORWARD);
    FFT.ComplexToMagnitude(vReal, vImag, samples);

    bool beetleDetected = checkFrequencyBand(detectionMinFreq, detectionMaxFreq);

    if (beetleDetected) {
      frameCount++;
    } else {
      frameCount = 0;
    }

    updateLEDs();
  }
}

void captureAudio() {
  for (int i = 0; i < samples; i++) {
    vReal[i] = analogRead(micPin);
    vImag[i] = 0;
    delayMicroseconds(100); // 10kHz sampling
  }
}

bool checkFrequencyBand(double minFreq, double maxFreq) {
  double samplingFrequency = 10000.0; // Hz
  double binResolution = samplingFrequency / samples;
  int startBin = (int)(minFreq / binResolution);
  int endBin = (int)(maxFreq / binResolution);

  for (int i = startBin; i <= endBin; i++) {
    if (vReal[i] > detectionThreshold) {
      Serial.print("Beetle sound detected at bin ");
      Serial.print(i);
      Serial.print(" (~");
      Serial.print(i * binResolution);
      Serial.println(" Hz)");
      return true;
    }
  }
  return false;
}

void updateLEDs() {
  digitalWrite(yellowLED, LOW);
  digitalWrite(redLED, LOW);

  if (frameCount >= 3) {
    digitalWrite(redLED, HIGH);  // Confirmed Beetle
  } else if (frameCount == 1) {
    digitalWrite(yellowLED, HIGH);  // Possible Beetle
  }
}

void resetSystem() {
  frameCount = 0;
  digitalWrite(yellowLED, LOW);
  digitalWrite(redLED, LOW);
  digitalWrite(greenLED, LOW);
  delay(200);
  digitalWrite(greenLED, HIGH);
}


⸻

🧪 9. Calibration Tips
	•	Use a frequency generator app to simulate beetle frequencies via a speaker
	•	Monitor Serial output for detection feedback
	•	Tune:
	•	detectionThreshold → lower for more sensitivity, higher for noise rejection
	•	detectionMinFreq / detectionMaxFreq → adjust based on research or recordings
	•	delayMicroseconds() → defines sampling frequency (~10kHz here)

⸻

📈 10. Future Enhancements

Feature	Benefit
I2S or MEMS mic	Higher resolution sound
Data logging (SD)	Trend analysis
LoRa/ESP8266 module	Remote farmer alert system
Machine learning	Detect multiple pest species
Battery + solar	Field deployment


⸻

Would you like a PDF export, a Fritzing wiring diagram, or a starter GitHub repository with the code and documentation?