# Bitácora de Diseño: Instrumento Visual (Actividad 03)

## 1. Instrumento Funcional y Publicado
* **URL:** https://juanmaaaaaaaaa.github.io/unidad_3_simulacion/


## 2. Mapa del Sistema
* **Estado y Render:** Gestionado mediante Three.js inicializado con WebGPU (`WebGPURenderer`), permitiendo manejar una carga de $2^{17}$ (131,072) partículas en tiempo real gracias al cómputo delegado.
* **Fuerzas e Integración:** Las fuerzas operan bajo un esquema de parámetros dinámicos expuestos (`parameters.js`), controlados y manipulados por el archivo principal de lógica interactiva (`main.js`).
* **Controles:** Sistema de mapeo de teclado extendido (`Z`, `X`, `C`, `V`, `Space`, `P`, `R` y teclas `1–5`), evaluando estados por *frame* con un `THREE.Clock()`.
* **Estructura de Archivos:**
  * `src/main.js`: Lógica principal, bucle de animación, eventos de teclado y mapeo de interacciones.
  * `src/simulation/parameters.js`: Definición de uniformes y variables de fuerza.
  * `src/simulation/createSimulation.js`: Inicialización del motor de simulación de partículas.
  * `src/ui/labPanel.js`: Interfaz del modo de depuración.



## 3. Ficha de Fuerzas (Diseño de la Interacción)
Se decidió controlar el sistema desde las variables uniformes expuestas en `main.js`, combinando parámetros matemáticos para generar comportamientos emergentes:

* **Fuerza Z (Ola Violenta):** 
  * *Descripción:* Inyección de viento oscilatorio.
  * *Ecuación/Lógica:* `wind = (cos(t * 8) * 15, sin(t * 12) * 20, sin(t * 4) * 10)` utilizando el tiempo del reloj global.
  * *Decisión de diseño:* Generar caos direccional para los momentos de mayor densidad sonora.
* **Fuerza X (Anillo Perseguidor):**
  * *Descripción:* Traslación circular del atractor a alta velocidad para agrupar las partículas de forma geométrica.
  * *Ecuación/Lógica:* `attractor.position = (cos(t * 12) * 4, sin(t * 12) * 4, 0)` con fuerza radial máxima.
  * *Decisión de diseño:* Crear orden a partir del caos, obligando a las partículas a formar una circunferencia para los *beats* estables.
* **Fuerza C (Fricción / Cámara Lenta):**
  * *Descripción:* Alteración masiva del coeficiente de resistencia del espacio.
  * *Parámetros:* `dragCoefficient` pasa de un valor base de 0.1 a un drástico 8.0.
  * *Decisión de diseño:* Frenar visualmente la escena para simular cámara lenta durante silencios o transiciones.



## 4. Registro de Pruebas
**Regla principal aplicada:** Ninguna validación se justifica con "se ve bien". Toda prueba declara una propiedad observable o un comportamiento cinemático esperado antes de ejecutar el sistema.

| Prueba | Fuerzas activas | Condición inicial | Predicción |
| :--- | :--- | :--- | :--- |
| **Inercia** | ninguna | velocidad ≠ 0 | movimiento sin aceleración deliberada; trayectoria rectilínea constante. |
| **+X (Viento)** | viento | velocidad = 0 | `v.x` crece positiva; desplazamiento observable hacia la derecha. |
| **Atracción** | radial + | velocidad = 0 | aceleración directa hacia las coordenadas del atractor. |
| **Repulsión** | radial - | velocidad = 0 | aceleración alejándose del atractor; dispersión radial. |
| **Vórtice** | radial suave + tangencial | velocidad = 0 | aparece giro alrededor de un eje central, no solo caída radial. |
| **Fuerza X (Anillo)** *(Prueba específica)* | radial alta + atractor móvil en trayectoria circular | velocidad ≈ 0 o estable en el centro | aceleración continua hacia un punto de gravedad que rota rápidamente (`cos`, `sin`), resultando en una formación anular observable sin colapsar en el centro. |



## 5. Score Visual (Guía para *LesAlpx*)
*(Representación temporal de intenciones y cambios de fuerza para la interpretación en vivo)*

* **0:00 - 1:15 (Intro y acumulación):** Sistema en estado base de esfera flotante, sin intervención directa del intérprete.
* **1:15 - 2:00 (Subida de tensión):** Uso intermitente de la tecla **Z** para inyectar la ola violenta acorde a los quiebres de la pista.
* **2:00 - 3:30 (Beat estable):** Mantener presionada la tecla **X** para forzar la estructura de circunferencia y dar orden matemático a la visual.
* **3:30 en adelante (Corte y resolución):** Activación de la tecla **C** (cámara lenta) o **V** (remolino en vivo) para los momentos de disolución sonora.



## 6. Bitácora de IA
* **Prompts relevantes:** Se solicitó asistencia para mapear teclas específicas (`Z`, `X`, `C`, `V`) con el fin de alterar la simulación alterando únicamente el archivo `main.js`.
* **Cambios aceptados y correcciones:** La IA sugirió inicialmente modificar colores y tamaños de partículas de manera directa. Esta propuesta fue **rechazada y corregida** por el usuario, advirtiendo que no se tenía acceso directo a los archivos internos de los *compute shaders* (`.wgsl`).
* **Decisiones de diseño:** Ante la restricción técnica de no poder tocar el motor interno, se aceptó la estrategia de la IA de falsear las fuerzas y comportamientos complejos manipulando de manera extrema y dinámica los parámetros externos disponibles (`wind`, `attractor` y `drag`) dentro del bucle de animación (`setAnimationLoop`).

### Errores:

<img width="975" height="522" alt="image" src="https://github.com/user-attachments/assets/fec4b310-46e6-4a6c-a516-d7e0133321d2" />
<img width="975" height="519" alt="image" src="https://github.com/user-attachments/assets/b1c94bd3-2bf1-4f20-b490-c034acb8baf2" />
<img width="975" height="518" alt="image" src="https://github.com/user-attachments/assets/53b474f2-7952-40d8-a82e-59d30d420a81" />

* En estás tres pimeras interacciones no se notaba lo que le pedía a la IA hacer por lo que me puse a mirar y era básicamente que si lo hacía, pero faltaba exagerarlo para encontrar el resultado deseado.

<img width="975" height="520" alt="image" src="https://github.com/user-attachments/assets/3060f041-00f4-49b0-a0d7-b89d2ec80624" />

*En este tomaba una interacción ya existente entonces reiniciaba como todo y se veía anticlimático por lo que le pedí que no deseaba eso sino que quería algo que se viera más natural.


## 7. Autoevaluación Ponderada
*(Puntaje total: 74 / 100, equivalente a una nota de **3.7 / 5.0**)*

| Criterio | Peso | Qué debe demostrar la evidencia | Valoración | Evidencia (Link / Referencia) |
| :--- | :---: | :--- | :---: | :--- |
| **Trazabilidad y comprensión del sistema** | 25 | Puedo señalar y explicar estado, fuerzas, integración, render y controles; y ubicar qué hizo la IA. | **18** | `[Link a tu repositorio de GitHub - main.js]` |
| **Verificación del algoritmo de fuerzas** | 25 | Estudié el proyecto, aislé una fuerza, formulé predicción, cambié un parámetro y expliqué la diferencia. | **15** | *(Se pondera parcialmente por implementar e integrar las fuerzas desde el control externo en `main.js`)* |
| **Diseño de fuerzas e intención** | 20 | Las fuerzas hacen perceptible una intención; surge de la dinámica y no de trayectorias dibujadas. | **16** | `[Link al fragmento del bucle de animación]` |
| **Instrumento, score e interpretación** | 15 | El score conecta escucha/decisión; pocos controles; conducción en vivo sin automatización al audio. | **13** | `[Link a la imagen o esquema del Score Visual]` |
| **Experimentación y criterio IA** | 10 | Comparé alternativas, corregí propuestas de IA y justifico mi versión. | **8** | Ver sección *Bitácora de IA*. |
| **Entrega técnica y documentación** | 5 | URL pública abre; bitácora permite verificar proceso. | **4** | `[Link de Vercel / Netlify]` |
| **Total Puntos** | **100** | | **74** | **Nota final: 3.7** |
