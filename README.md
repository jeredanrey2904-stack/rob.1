# rob.1
El sistema posee cinco LEDs, un pulsador y un buzzer. Mientras el botón permanece presionado, los LEDs se encienden de forma secuencial simulando una ruleta. Cuando el usuario suelta el botón, la ruleta se detiene, suena el buzzer y queda encendido el LED seleccionado.

Componentes

Arduino Uno R3
Protoboard
5 LEDs
5 resistencias de 220 Ω
Pulsador
Buzzer piezoeléctrico
Cables jumper
Funcionamiento

Se presiona el botón.
Los LEDs comienzan a moverse de un extremo al otro.
Al soltar el botón:
Suena el buzzer.
Se apagan todos los LEDs.
Queda encendido únicamente el LED donde terminó la ruleta.
Archivo INO
// Variables
int buzzer = 3;
int btn = 2;

int t = 200;
int leds;

void setup() {
  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(7, OUTPUT);
  pinMode(8, OUTPUT);
  pinMode(9, OUTPUT);

  pinMode(buzzer, OUTPUT);
  pinMode(btn, INPUT);

  randomSeed(analogRead(A0));
}

void rebote() {
  if (digitalRead(btn) == HIGH) {

    int sonido = random(300, 2000);

    tone(buzzer, sonido);
    delay(500);
    noTone(buzzer);

    t = t - 20;

    if (t < 50) {
      t = 200;
    }
  }
}

void loop() {

  for (leds = 5; leds <= 9; leds++) {
    digitalWrite(leds, HIGH);

    rebote();

    delay(t);

    digitalWrite(leds, LOW);
  }

  for (leds = 8; leds >= 6; leds--) {
    digitalWrite(leds, HIGH);

    rebote();

    delay(t);

    digitalWrite(leds, LOW);
  }

}
<img width="1354" height="698" alt="image" src="https://github.com/user-attachments/assets/dda5c6e7-b5b8-4288-af2a-7e98e5d67c98" />

