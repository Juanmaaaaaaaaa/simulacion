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

#### Vista interaz general:

<img width="362" height="656" alt="image" src="https://github.com/user-attachments/assets/ad357bb7-6b02-4d77-8179-265207227b9e" />

#### Derrota:

<img width="555" height="281" alt="image" src="https://github.com/user-attachments/assets/63796fd5-514d-4202-a79b-2086c800fa44" />

#### Victoria:

<img width="342" height="172" alt="image" src="https://github.com/user-attachments/assets/c0f68a2c-12e9-4ad6-9d2c-2f008dcfd065" />


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

```
//==================================================
// VARIABLES
//==================================================

// Tiempo
let dias = 60;
let ultimoCambio = 0;
let duracionDia = 1000;

// Estado del juego
let gameOver = false;
let victoria = false;

// Vitalidad del embrión
let vitalidad = 100;

// Parámetros elegidos por el usuario
let temperatura;
let humedad;
let ventilacion;
let volteo;

// Parámetros ideales (la naturaleza)
let temperaturaIdeal = 37.5;
let humedadIdeal = 60;
let ventilacionIdeal = 5;
let volteoIdeal = 5;

// Sliders
let sliderTemp;
let sliderHum;
let sliderVent;
let sliderVolt;

// Movimiento del huevo
let anguloHuevo = 0;

// Tiempo para ruido Perlin
let tiempoRuido = 0;

// Tiempo del último cambio aleatorio
let ultimoCambioAmbiente = 0;

// Cada cuánto cambia el ambiente
let intervaloAmbiente = 1000;

// Fuerza de un evento extraño
let eventoExcepcion = false;

// Cantidad de error de los parámetros
let errorParametros = 0;

function setup() {

  createCanvas(450,800);

  textFont("Arial");

  //------------------------------------
  // Crear sliders
  //------------------------------------

  sliderTemp = createSlider(35,40,37.5,0.1);

  sliderHum = createSlider(40,80,60,1);

  sliderVent = createSlider(0,10,5,1);

  sliderVolt = createSlider(0,10,5,1);

  //------------------------------------
  // Posición de sliders
  //------------------------------------

  sliderTemp.position(270,620);

  sliderHum.position(270,670);

  sliderVent.position(270,720);

  sliderVolt.position(270,770);

}

function draw(){

  background(220,235,255);

  //------------------------------------
  // Si ganó
  //------------------------------------

  if(victoria){

    pantallaVictoria();

    return;

  }

  //------------------------------------
  // Si perdió
  //------------------------------------

  if(gameOver){

    pantallaDerrota();

    return;

  }

  //------------------------------------
  // Leer sliders
  //------------------------------------

  temperatura = sliderTemp.value();

  humedad = sliderHum.value();

  ventilacion = sliderVent.value();

  volteo = sliderVolt.value();

  //------------------------------------
  // Actualizar tiempo
  //------------------------------------
  
  actualizarTiempo();

  //------------------------------------
  // Actualizar comportamiento del ambiente
  //------------------------------------

  actualizarAmbiente();

  //------------------------------------
  // Actualizar actualizar vitalidad
  //------------------------------------

  actualizarVitalidad();

  //------------------------------------
  // Dibujar interfaz
  //------------------------------------

  dibujarTitulo();

  dibujarVitalidad();

  dibujarHuevo();

  dibujarEtiquetas();

}

function actualizarTiempo(){

  // Los últimos cinco días duran más

  if(dias > 5){

    duracionDia = 1000;

  }

  else{

    duracionDia = 4000;

  }

  if(millis() - ultimoCambio > duracionDia){

    dias--;

    ultimoCambio = millis();

  }

  if(dias <= 0){

    victoria = true;

  }

}

function dibujarVitalidad(){

  fill(0);

  textSize(18);

  textAlign(LEFT);

  text(
    "Vitalidad del embrión",
    25,
    70
  );


  stroke(0);

  noFill();

  rect(
    25,
    85,
    220,
    20
  );


  noStroke();


  if(vitalidad>60){

    fill(70,220,80);

  }

  else if(vitalidad>30){

    fill(240,200,50);

  }

  else{

    fill(240,70,70);

  }


  rect(
    25,
    85,
    vitalidad*2.2,
    20
  );


}

function dibujarTitulo(){

  fill(0);

  textAlign(CENTER);

  textSize(30);

  text("Día "+dias,width/2,40);

}

function dibujarHuevo(){

  push();

  translate(width/2,height/2);

  //-----------------------------------
  // Oscilación del huevo
  //-----------------------------------

  let velocidad = map(volteo,0,10,0,0.15);

  anguloHuevo = sin(frameCount*velocidad)*0.2;

  rotate(anguloHuevo);

  //-----------------------------------
  // Color según temperatura
  //-----------------------------------

  let rojo = map(temperatura,35,40,200,255);

  let verde = map(temperatura,35,40,220,180);

  let azul = map(temperatura,35,40,255,160);

  fill(rojo,verde,azul);

  stroke(80);

  strokeWeight(2);

  ellipse(0,0,170,220);

  pop();

  //-----------------------------------
  // Dibujar humedad
  //-----------------------------------

  dibujarGotas();

  //-----------------------------------
  // Dibujar viento
  //-----------------------------------

  dibujarViento();

}

function dibujarGotas(){

  let cantidad = int(map(humedad,40,80,0,10));

  fill(70,150,255);

  noStroke();

  for(let i=0;i<cantidad;i++){

    let x = random(width/2-50,width/2+50);

    let y = random(height/2-80,height/2+80);

    ellipse(x,y,8,8);

  }

}

function dibujarViento(){

  let cantidad = int(map(ventilacion,0,10,0,8));

  stroke(120);

  strokeWeight(2);

  noFill();

  for(let i=0;i<cantidad;i++){

    let y = height/2-120+i*30;

    arc(width/2+120,y,50,20,PI,TWO_PI);

  }

}

function dibujarEtiquetas(){

  fill(0);

  textAlign(LEFT);

  textSize(16);

  text("Temperatura: "+nf(temperatura,1,1)+" °C",20,635);

  text("Humedad: "+humedad+" %",20,685);

  text("Ventilación: "+ventilacion,20,735);

  text("Volteo: "+volteo,20,785);

}

function pantallaVictoria(){

  background(210,255,210);


  fill(0);

  textAlign(CENTER);


  textSize(35);

  text(
    "¡El huevo eclosionó!",
    width/2,
    height/2-40
  );


  textSize(20);

  text(
    "El cóndor logró nacer gracias al equilibrio",
    width/2,
    height/2+20
  );


}

function pantallaDerrota(){

  background(255,210,210);


  fill(0);

  textAlign(CENTER);


  textSize(35);

  text(
    "El huevo no logró eclosionar",
    width/2,
    height/2-40
  );


  textSize(20);

  text(
    "Las condiciones no fueron adecuadas",
    width/2,
    height/2+20
  );

}

function actualizarAmbiente(){

  if(millis()-ultimoCambioAmbiente > intervaloAmbiente){


    //----------------------------------
    // Distribución normal
    //----------------------------------

    temperaturaIdeal += randomGaussian(0,0.15);

    humedadIdeal += randomGaussian(0,0.5);

    ventilacionIdeal += randomGaussian(0,0.15);

    volteoIdeal += randomGaussian(0,0.15);



    //----------------------------------
    // Ruido Perlin
    //----------------------------------

    let cambioHumedad = map(
      noise(tiempoRuido),
      0,
      1,
      -0.5,
      0.5
    );


    humedadIdeal += cambioHumedad;


    tiempoRuido += 0.05;



    //----------------------------------
    // Limitar valores naturales
    //----------------------------------

    temperaturaIdeal = constrain(
      temperaturaIdeal,
     35,
     40
    );


    humedadIdeal = constrain(
      humedadIdeal,
     40,
     80
    );


    ventilacionIdeal = constrain(
      ventilacionIdeal,
     0,
     10
    );


    volteoIdeal = constrain(
      volteoIdeal,
     0,
     10
    );



    //----------------------------------
    // Evento excepcional
    //----------------------------------

    if(random(1)<0.02){

      eventoExcepcion=true;


      temperaturaIdeal += random(-3,3);

      humedadIdeal += random(-20,20);

    }


    else{

      eventoExcepcion=false;

    }



    ultimoCambioAmbiente = millis();

  }

}

function actualizarVitalidad(){


  //---------------------------------
  // Calcular diferencia con lo ideal
  //---------------------------------

  let errorTemperatura = abs(
    temperatura - temperaturaIdeal
  );


  let errorHumedad = abs(
    humedad - humedadIdeal
  );


  let errorVentilacion = abs(
    ventilacion - ventilacionIdeal
  );


  let errorVolteo = abs(
    volteo - volteoIdeal
  );



  //---------------------------------
  // Suma de errores
  //---------------------------------

  errorParametros =
  errorTemperatura +
  errorHumedad/10 +
  errorVentilacion +
  errorVolteo;



  //---------------------------------
  // Si está fuera del equilibrio
  //---------------------------------

  if(errorParametros > 5){

    vitalidad -= 0.15;

  }


  //---------------------------------
  // Si está bien cuidado
  //---------------------------------

  else{

    vitalidad += 0.05;

  }



  //---------------------------------
  // Limitar vitalidad
  //---------------------------------

  vitalidad = constrain(
    vitalidad,
    0,
    100
  );



  //---------------------------------
  // Derrota
  //---------------------------------

  if(vitalidad <= 0){

    gameOver=true;

  }

}
```

### Intención conceptual

Transformar un fenómeno biológico como la incubación del cóndor en una experiencia interactiva donde el usuario comprende que mantener un sistema vivo requiere adaptación constante y no solamente control.

### Decisión de diseño importante

Se decidió evitar que los parámetros fueran completamente aleatorios, ya que eso representaría caos. En cambio, se utilizaron diferentes modelos de aleatoriedad para crear comportamientos con patrones reconocibles.

### Dificultad

El principal reto fue encontrar un equilibrio entre permitir que el usuario tenga influencia y evitar que pueda controlar completamente el resultado.

### Solución

Se implementó una combinación entre interacción directa y cambios automáticos del ambiente, haciendo que el usuario tenga que adaptarse constantemente.


## Criterios

#### Nota: 5

### Encargo completo: Cumple
Interpreto los cinco momentos dentro de un mismo sistema visual. La experiencia representa la incubación de un huevo de cóndor en un único sistema. 
- Posibilidad: los parámetros pueden variar constantemente. 
- Tendencia: el ruido Perlin genera cambios graduales. 
- Normalidad: randomGaussian() mantiene los valores cerca del equilibrio. 
- Excepción: eventos aleatorios alteran significativamente las condiciones.
- Influencia: el usuario ajusta los parámetros mediante sliders para mantener la incubación.
  
### Simulación con intención: Cumple
Utilizo al menos tres conceptos de la unidad para comunicar las ideas del encargo.
Se implementan distribución normal (randomGaussian), ruido Perlin (noise) y distribuciones de probabilidad mediante eventos excepcionales con baja probabilidad de ocurrencia. Estos conceptos representan distintos tipos de incertidumbre en el ambiente de incubación.

### Interacción significativa: Cumple
La interacción modifica el comportamiento o las probabilidades del sistema, que también funciona sin intervención.
El usuario modifica temperatura, humedad, ventilación y volteo mediante sliders, pero el ambiente continúa cambiando automáticamente. El sistema sigue funcionando aunque el usuario no interactúe, lo que obliga a adaptarse constantemente a los cambios.

### Prototipo funcional: Cumple
La experiencia puede ejecutarse y recorrerse completa sin errores que impidan comprenderla.	
El prototipo permite recorrer toda la experiencia: el contador avanza desde el día 60 hasta la eclosión, los parámetros afectan el huevo, la vitalidad responde a las condiciones y existen estados de victoria y derrota.

### Proceso documentado: Cumple
La bitácora evidencia avances, decisiones, dificultades, soluciones, uso de IA y enlace al prototipo.
En la bitacora se evidencia la idea planeada, el uso en p5, la mayor dificultad que apareció, la ayuda de la ia y el enlace en el prototipo.
