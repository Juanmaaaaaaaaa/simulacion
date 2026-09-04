# Unidad 4: Oscilación

Código: https://editor.p5js.org/Juanmaaaaaaaaa/sketches/YLFZ0ya04

## Idea
Me basé en la idea del Pokémon Wishiwashi, el cual, por sí solo, es un pescadito nada más, muy inofensivo, pero cuando muchos se juntan, muchos como que se logran agrupar de cierta forma, y causan que se transforme en otra forma el Wishiwashi, que se llama forma banco, el cual es un monstruo muy temible a comparación del Wishiwashi común, que es un Pokémon muy débil.

Quería mostrar que cuando muchos pescaditos se sincronizan, por así decirlo, forman algo mucho mejor y pues mucho más temible, lo cual hace que aunque tengan diferentes sonidos y apariencias, todos terminen volviéndose no solo con una apariencia temible y un sonido temible.

## Traducción del Modelo de Kuramoto y Variables
El sistema implementa el modelo dinámico de Kuramoto adaptado a un entorno audiovisual en p5.js:
* **Fase ($\theta$):** Representa el temporizador o ciclo interno de cada agente Wishiwashi individual, determinando cuándo parpadea en rojo brillante y emite su pulso sonoro.
* **Frecuencia natural ($\omega$):** La velocidad base a la que oscila cada agente de manera aislada (`omegaBase` con ligera variación aleatoria).
* **Fuerza de acoplamiento ($K$):** Controla qué tanto se influyen los agentes vecinos entre sí. Al aumentar $K$ mediante el control deslizante, la atracción de fases se acelera.
* **Parámetro de orden global ($R$):** Calcula matemáticamente la coherencia de la población ($\sqrt{\sum \cos(\theta)^2 + \sum \sin(\theta)^2} / N$), midiendo en tiempo real cuán sincronizado está el sistema.

##  Cumplimiento de Requisitos Mínimos en la Aplicación
* **Agentes simultáneos:** El sistema inicializa con 10 agentes gobernados por el sistema dinámico, permitiendo añadir más mediante clics hasta superar el mínimo de 8.
* **4 personalidades audiovisuales diferentes:** Cada agente se clasifica aleatoriamente en uno de 4 tipos (`personalityType`), manifestándose tanto visualmente (formas geométricas únicas: pez ovalado, rombo, circular con aletas o torpedo) como sonoramente (frecuencias específicas de audio: 330Hz, 440Hz, 554Hz y 659Hz).
* **Modificación de variables en tiempo real:** Se implementaron dos controles deslizantes interactivos en la interfaz para modificar en vivo la **Fuerza de Acoplamiento ($K$)** y la **Frecuencia Natural ($\omega$)**.
* **Interacciones performativas (Global e Individual):** 
  * *Global:* Modificación de parámetros con sliders o alteración de todo el sistema mediante la tecla `ESPACIO`.
  * *Individual:* Hacer clic directamente sobre un agente específico para perturbar su fase de manera aislada.
* **Mecanismo de perturbación:** Presionar la barra espaciadora descoloca abruptamente las fases de todos los agentes, permitiendo observar cómo el colectivo absorbe el caos y se reorganiza.
* **3 Estados colectivos reconocibles:** El sistema evalúa permanentemente el parámetro de orden $R$ para reflejar de forma explícita en pantalla los estados de **Desorden (Caos)**, **Organización Parcial** y **Organización Estable (Sincronizados)**.
* **Comunicación perceptible del estado:** Se comunica mediante un indicador de texto dinámico con código de colores, cambios de color en los agentes, destellos de pulso sincronizados y una respuesta sonora en unísono que escala hacia la transformación final en la **Forma Banco**.

## Proceso

A medida de que probaba con la IA sentía que la IA no me entendía o yo no me explicaba bien con mi idea por lo que pase por algunos fallos que no me gustaban.

<img width="1862" height="817" alt="image" src="https://github.com/user-attachments/assets/dfa1c803-a7c2-48f1-be61-f4e93b9a70cd" />
Acá solo se enloquecían y ya

<img width="1861" height="832" alt="image" src="https://github.com/user-attachments/assets/ec4eb542-dd3c-4b21-adaa-70b958e0c2c0" />

<img width="1862" height="822" alt="image" src="https://github.com/user-attachments/assets/43d9f158-39ea-487f-a949-5d58134e3eb0" />


Pero finalmente lo logre y llegue a lo que mi mente pensaba (despues de mucho)

<img width="1857" height="872" alt="image" src="https://github.com/user-attachments/assets/45a4ddb9-5333-4d1b-b3bd-fcfb7f40df9f" />

<img width="1861" height="832" alt="image" src="https://github.com/user-attachments/assets/187a4829-ff0d-426e-a1a3-2edba3bb4343" />
