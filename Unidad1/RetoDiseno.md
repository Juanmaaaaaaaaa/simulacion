# Reto de diseño

## P5:

https://editor.p5js.org/Juanmaaaaaaaaa/sketches/ucCX7oXIX

### Idea:

En este reto de diseño pensé en representar la eclosión de un huevo de cóndor, con la intención de generar conciencia sobre la conservación de esta especie, que se encuentra en vía de extinción debido, entre otros factores, a su lenta reproducción, ya que una pareja pone únicamente un huevo cada dos o tres años. Esta experiencia interactiva busca que el usuario encuentre y mantenga las condiciones ideales para la incubación mientras transcurren los 60 días necesarios para que el huevo eclosione.

Cada día de incubación durará un segundo hasta llegar al día 55. A partir de ese momento, como los últimos cinco días son los más críticos para el desarrollo del embrión, cada uno durará cuatro segundos. En la parte superior de la pantalla habrá un contador que disminuirá desde 60 hasta 0, momento en el que el huevo eclosionará si el usuario ha logrado mantener las condiciones adecuadas.

En el centro de la pantalla aparecerá el huevo, cuya apariencia cambiará según los parámetros de incubación. Su color se volverá más cálido cuando la temperatura aumente y más frío cuando disminuya. Además, el huevo oscilará según el nivel de volteo: a mayor frecuencia de volteo, más rápida será la oscilación; a menor frecuencia, el movimiento será más lento, y si el volteo es nulo, el huevo permanecerá inmóvil. La humedad se representará mediante gotas de agua sobre la superficie del huevo: a mayor humedad aparecerán más gotas, mientras que a menor humedad habrá menos. Finalmente, la ventilación se visualizará mediante ráfagas de viento alrededor del huevo; una mayor ventilación generará más ráfagas y una menor ventilación, menos.

En la parte inferior derecha de la pantalla se ubicarán los controles deslizantes que permitirán al usuario modificar los parámetros de temperatura, humedad, ventilación y volteo para intentar mantener el ambiente de incubación dentro de los valores adecuados.

A medida que transcurra el tiempo, los parámetros ambientales cambiarán de forma automática utilizando una distribución normal (randomGaussian), simulando las variaciones naturales del entorno. Si el usuario no corrige estos cambios y alguno de los parámetros permanece fuera de su rango óptimo, la vitalidad del embrión comenzará a disminuir, representada mediante una barra de vitalidad visible en la interfaz. Si el usuario logra restablecer las condiciones adecuadas, la barra podrá recuperarse gradualmente; sin embargo, si la vitalidad llega a cero, el embrión no sobrevivirá y la experiencia finalizará con la pérdida.

### Proyecto: Incubación del cóndor

Esta experiencia interactiva representa el proceso de eclosión de un huevo
de cóndor, una especie en vía de extinción cuya principal dificultad para
su conservación es su lenta reproducción.

El objetivo del usuario es mantener las condiciones adecuadas de incubación
durante 60 días simulados para lograr que el huevo eclosione.

El sistema no está completamente controlado por el usuario, ya que los
parámetros ambientales cambian constantemente utilizando diferentes tipos
de aleatoriedad, representando que la incertidumbre también posee reglas
y comportamientos.

### Código

El código está dividido en diferentes funciones para separar las
responsabilidades del sistema.

Las funciones principales controlan:

- El tiempo de incubación.
- La actualización de las condiciones ambientales.
- La representación visual del huevo.
- La interacción del usuario mediante sliders.
- La evaluación de la vitalidad del embrión.

Esto permite modificar cada parte del sistema sin afectar las demás.

Por otro lado:

randomGaussian() representa las variaciones normales del ambiente,
manteniendo los parámetros cerca de valores ideales con pequeños cambios.

noise() genera tendencias progresivas y naturales, evitando cambios bruscos
en los parámetros como la humedad.

Los eventos excepcionales representan cambios poco probables que alteran
el sistema, simulando situaciones inesperadas.

El usuario no controla completamente el sistema, solo modifica sus
probabilidades mediante los sliders y debe adaptarse a los cambios.

La barra de vitalidad muestra el estado del embrión, disminuyendo cuando
las condiciones son incorrectas y recuperándose cuando el equilibrio se
mantiene.

### Intención conceptual

Transformar un fenómeno biológico como la incubación del cóndor en una experiencia interactiva donde el usuario comprende que mantener un sistema vivo requiere adaptación constante y no solamente control.

### Decisión de diseño importante

Se decidió evitar que los parámetros fueran completamente aleatorios, ya que eso representaría caos. En cambio, se utilizaron diferentes modelos de aleatoriedad para crear comportamientos con patrones reconocibles.

### Dificultad

El principal reto fue encontrar un equilibrio entre permitir que el usuario tenga influencia y evitar que pueda controlar completamente el resultado.

### Solución

Se implementó una combinación entre interacción directa y cambios automáticos del ambiente, haciendo que el usuario tenga que adaptarse constantemente.
