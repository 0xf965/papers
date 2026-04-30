# Snake Game – Guía del Juego (Game of Prompts)

## Descripción

Este juego es una versión automatizada de Snake.
El jugador no controla directamente la serpiente, sino que crea un solver que decide cada movimiento en función del estado actual del juego.

El objetivo es obtener la mayor puntuación posible.

---

## Objetivo

* Comer manzanas normales suma +1 punto
* Comer manzanas venenosas resta -2 puntos (mínimo 0)
* El juego termina si la serpiente:

  * Choca con los bordes
  * Choca consigo misma
  * Recibe un movimiento inválido o no responde

---

## Cómo funciona el juego

El juego avanza en pasos. En cada paso ocurre lo siguiente:

1. El Game Service envía el estado actual
2. El solver decide un movimiento
3. El Game Service aplica ese movimiento
4. Se actualiza el estado y la puntuación
5. Se repite el proceso

---

## Qué información recibe el solver

En cada paso, el solver recibe:

* Posición completa de la serpiente (la cabeza es el primer elemento)
* Posición de la manzana
* Posiciones de las manzanas venenosas
* Tamaño del tablero

Ejemplo conceptual:

snake = [[10,10], [10,9], [10,8]]
apple = [12,15]
poison_apples = [[11,15]]
board_rows = 60
board_cols = 120

---

## Qué debe responder el solver

El solver debe devolver exactamente un movimiento:

UP
DOWN
LEFT
RIGHT

Solo uno por turno.

---

## Ejemplo simple

Estado:

* Cabeza en (10,10)
* Manzana en (10,15)

Interpretación:

* RIGHT acerca a la manzana
* LEFT puede ser inválido si hay cuerpo
* UP o DOWN pueden alejar

El solver debe elegir el movimiento más conveniente en ese contexto.

---

## Puntuación

* Manzana normal: +1
* Manzana venenosa: -2 (mínimo 0)

Número de manzanas venenosas en el tablero:

poison_apples = floor(score / 10)

A mayor puntuación, mayor dificultad.

---

## Restricciones del solver

* El solver se ejecuta de forma aislada
* No puede conectarse a internet ni a servicios externos
* La imagen completa del solver (incluyendo dependencias) debe tener un tamaño máximo de 1 GB

---

## Qué hace bueno a un solver

Un buen solver no solo busca la manzana. También debe:

* Evitar colisiones en todo momento
* No tomar decisiones que lo dejen sin salida
* Manejar correctamente espacios reducidos
* Evitar el veneno cuando sea necesario
* Ser consistente y no fallar ni devolver movimientos inválidos

En muchos casos, ir directamente hacia la manzana no es la mejor decisión.

---

## Reproducibilidad

El juego puede ejecutarse con una semilla (seed):

mismo solver + misma seed = mismo resultado

Esto permite comparar solvers de forma justa.

---

## Resumen

El problema que debe resolver el solver es:

Dado un estado del juego, decidir el mejor movimiento posible en ese instante.

Este proceso se repite continuamente hasta que el juego termina.
