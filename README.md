# Deep-Learning
Implementación del algoritmo DQN para el problema del Lunar Lander (automatización y optimización).

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1bf2n2bd7ib8v-ZdYjMNfGXS8byCFup9v?usp=sharing)
> **Nota:** Haz clic en el botón de arriba para abrir el notebook directamente en Google Colab.

---

## Descripción General

Este proyecto aborda el clásico problema de **Lunar Lander** (entorno Gymnasium) mediante la implementación del algoritmo **Deep Q-Learning (DQN)**.  El objetivo es entrenar un agente de Inteligencia Artificial para que aterrice un módulo lunar de manera óptima y suave, **minimizando el consumo de combustible** y contrarrestando las fuerzas de gravedad y el movimiento lateral.

El proyecto es un claro ejemplo de aplicación de **Aprendizaje por Refuerzo (Reinforcement Learning)** con Redes Neuronales Profundas.

## Objetivo y Desafío

* **Objetivo:** Conseguir que el agente logre una puntuación promedio de **+200** puntos en los 30 episodios del test final.
* **Desafío:** El Lunar Lander es un problema de control óptimo donde el agente debe aprender la secuencia de acciones (motores izquierdo, derecho o principal) basándose en un espacio de estado continuo (posición, velocidad, ángulo).

---

## Tecnología y Metodología (DQN)

### 1. Arquitectura del Modelo
* **Modelo:** Deep Neural Network (DNN) implementada con **TensorFlow** y **Keras**.
* **Estructura:** Tres capas densas de **128 neuronas** cada una, utilizando la función de activación **ReLU** y un inicializador de pesos `he_normal`.
* **Output:** Cuatro salidas correspondientes a las cuatro posibles acciones del agente (no hacer nada, motor izquierdo, motor principal, motor derecho).

### 2. Estabilización y Optimización (Estrategias Avanzadas)
Para mejorar la estabilidad y convergencia del entrenamiento, se implementaron varias técnicas clave del Aprendizaje por Refuerzo:

* **Replay Memory (`ReplayMemory`):** Se utiliza un búfer de experiencia de gran tamaño (`100,000` transiciones) para romper la correlación secuencial de los datos y estabilizar el entrenamiento.
* **Epsilon-Greedy Policy:** Se implementa un mecanismo de exploración que decae exponencialmente (`EXPLORATION_RATE_DECAY = 0.96`), asegurando que el agente explore inicialmente y luego explote su conocimiento.
* **Planificador de Tasa de Aprendizaje:** La tasa de aprendizaje (`LEARNING_RATE`) se reduce progresivamente, comenzando en $0.001$ y decreciendo cada 5,000 transiciones para afinar la convergencia.
* **Función de Pérdida Adaptativa:** El entrenamiento comienza con **MSE** (Error Cuadrático Medio) y cambia a la **Función de Pérdida de Huber** después de **25,000 transiciones**, lo que hace que el modelo sea más robusto a las recompensas atípicas (outliers).

### 3. Entorno
* **Entorno:** `gymnasium` (anteriormente `OpenAI Gym`) — LunarLander-v3.
* **Estado (8 dimensiones):** Posición (x, y), Velocidad (vx, vy), Ángulo, Velocidad Angular, Contacto con el suelo (pata izq., pata der.).

---

## Resultados y Visualización

* **Convergencia:** El modelo logra alcanzar y mantener el objetivo de una puntuación promedio de **+200** puntos, demostrando un rendimiento óptimo.
* **Visualización:** El notebook genera **videos (`.mp4`)** del agente aterrizando cada $10$ episodios, permitiendo una mirada visual al progreso del aprendizaje y al comportamiento final del modelo.
* **Prueba Final:** El agente es evaluado con una política puramente **Greedy** para confirmar la calidad de las Q-Values aprendidas, obteniendo una puntuación promedio de **244** superando el objetivo de +200 puntos.
