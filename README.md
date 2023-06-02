# code_elctrovanne
```
int sensorPin = A0; // Pin du capteur
int valvulaPin = 8; // Pin de l'électrovanne

int seuil = 600; // Valeur de référence du capteur
int fuiteEau = 0; // Indicateur de fuite d'eau

void setup() {
pinMode(sensorPin, INPUT); // Configure le pin du capteur comme une entrée
pinMode(valvulaPin, OUTPUT); // Configure le pin de l'électrovanne comme une sortie
digitalWrite(valvulaPin, LOW); // Initialement, l'électrovanne est ouvert
Serial.begin(9600); // Configuration de la communication série
Serial.println("BEGIN");
}

void loop() {
int valeurCapteur = analogRead(sensorPin); // Lecture de la valeur du capteur
if (valeurCapteur < seuil) { // Si la valeur du capteur est supérieure au seuil 
  fuiteEau = 1; // Indiquer qu'il y a une fuite d'eau
  digitalWrite(valvulaPin, HIGH); // fermer l'électrovanne pour couper le flux d'eau
  Serial.println("désactivation de la vanne");
  Serial.println("Une fuite d'eau a été détectée !"); // Notifier la détection de la fuite
}
else if (fuiteEau == 1) { // Si une fuite a été détectée précédemment et maintenant le niveau d'eau a baissé
  fuiteEau = 0; // Réinitialiser l'indicateur de fuite d'eau
  digitalWrite(valvulaPin, LOW); // Ouvrir l'électrovanne pour permettre à l'eau de s'écouler à nouveau
  Serial.println("La fuite d'eau a été réparée !"); // Notifier la réparation de la fuite
}
delay(1000); // Délai d'une seconde avant de réaliser la prochaine lecture

}
```
