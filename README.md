# Sensor de Estacionamento

## Alunos


## Tabela de Gastos


## Simulação no Tinkerkad

Link da Simulação: <>


## Projeto Físico


## Código Usado

```C++
//C++ Code

// Pinagem
const int trigPin = 13;
const int echoPin = 12;
const int buzzerPin = 10;

// Variáveis para o sensor
long duration;
int distance;

void setup() { //Configurando pinos de saída e entrada
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(buzzerPin, OUTPUT);
  Serial.begin(9600); //Para debug
}

void loop() {
  // Medindo a distância
  digitalWrite(trigPin, LOW); //Sem pulso por 2 microseg
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH); //Envia pulso por 10 microseg
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  //Quanto tempo o impulso ultrassônico 
  //demora para retornar ao sensor
  duration = pulseIn(echoPin, HIGH);
  
  //Distância baseada na duração e velocidade do som
  distance = duration * 0.034 / 2;

  // Limita o mapeamento da distância de 0 a 100 cm
  int distLimit = constrain(distance, 0, 100);

  // Mapeando a distância para valor PWM
  int volume = map(distLimit, 0, 100, 5, 255);
  // 5 é o valor mínimo do buzzer (evitar silêncio do buzzer)
  //255 é o máximo (menor distância = maior frequência)
  //Objeto mais próximo = PWM menor = buzzer com maior volume
  
  // Fazendo o Buzzer apitar em intervalos de 10 ms
  analogWrite(buzzerPin, volume); 
  delay(10);                      // Duração do buzz
  analogWrite(buzzerPin, 0);      // Off
  delay(50);                      // Espera até próximo ciclo

  // --- Para debugar, é possível ver essas info no simulador ---
  Serial.print("Distância: ");
  Serial.print(distance);
  Serial.print(" cm | Volume: ");
  Serial.println(volume);
}
```
