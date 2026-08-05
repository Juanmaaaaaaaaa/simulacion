# Reto de diseño 

## p5

https://editor.p5js.org/Juanmaaaaaaaaa/sketches/YHGEim_6G


## Tensión e intención

### Tensión

Quiero explorar la tensión entre **integración y exclusión**.

### Intención

Mi intención es representar un sistema en el que algunas partículas pueden colaborar y formar estructuras estables, mientras que otras desean unirse a esas estructuras pero son rechazadas cuando se acercan demasiado. Además, espero que esta contradicción se manifieste como un movimiento continuo de **acercamiento, rechazo y nuevo intento de integración**.

## Tipos y cantidades

| Tipo | Cantidad | Función |
|---|---:|---|
| A | 45 | Núcleo cooperativo |
| B | 45 | Núcleo cooperativo compatible con A |
| C | 70 | Partículas que buscan integrarse |

Hay una cantidad moderada de partículas para que el comportamiento fuera legible y para poder observar claramente las trayectorias de aproximación y expulsión.

## Reglas del sistema

- A atrae a A.
- B atrae a B.
- A y B se atraen entre sí.
- C es atraída por A y B.
- A y B repelen a C cuando está cerca.
- C evita ligeramente a otras C.

## Matriz de relaciones

| Desde / hacia | A | B | C |
|---|---:|---:|---:|
| **A** | +0.42 | +0.22 | -0.50 |
| **B** | +0.22 | +0.42 | -0.50 |
| **C** | +0.58 | +0.58 | -0.08 |


## Parámetros y justificación

### Distancias de interacción

| Relación | Distancia |
|---|---:|
| A-A y B-B | 72 px |
| A-B | 88 px |
| C hacia A/B | 118 px |
| A/B hacia C | 54 px |

Las partículas C detectan los grupos desde lejos, pero el rechazo ocurre únicamente cuando entran en una zona cercana. Esto crea la secuencia:

**atracción lejana → acercamiento → rechazo cercano → escape**

### Parámetros físicos

| Parámetro | Valor |
|---|---:|
| Fricción | 0.93 |
| Velocidad máxima A/B | 2.0 |
| Velocidad máxima C | 3.2 |

Las partículas A y B se comportan de manera más estable y pesada, mientras que las partículas C son más rápidas e inestables.

## Justificación de las decisiones

### A → A y B → B

Elegí una atracción positiva fuerte porque quiero hacer perceptible la **cohesión interna**. Espero que produzca grupos compactos pero móviles.

### A ↔ B

Elegí una atracción moderada porque quiero que los dos núcleos puedan colaborar sin perder completamente su identidad. Espero que produzca fusiones parciales y agrupaciones más grandes.

### C → A y C → B

Seleccioné una atracción alta porque quiero que las partículas C busquen activamente integrarse al grupo. Espero que produzca persecución y aproximación constante.

### A/B → C

Seleccioné una repulsión fuerte de corto alcance porque quiero incorporar el rechazo en la regla del sistema. Espero que produzca expulsiones, rebotes y trayectorias de escape.

### C → C

Elegí una ligera repulsión para evitar que las partículas excluidas formen una comunidad propia. Espero que permanezcan dispersas y en búsqueda constante.


# Invariantes y variables

## Invariantes

Estos elementos permanecen en todas las ejecuciones y definen la identidad del sistema:

- Existencia de tres poblaciones (A, B y C).
- Cooperación entre A y B.
- Búsqueda de integración por parte de C.
- Rechazo cercano de C por parte del grupo.
- Movimiento emergente basado en fuerzas locales.

## Variables

Estos elementos cambian en cada ejecución sin destruir la identidad del sistema:

- Posiciones iniciales.
- Trayectorias individuales.
- Forma de los grupos.
- Momentos de fusión entre A y B.
- Lugares y direcciones de expulsión de C.

# Distribución inicial

- A se ubica inicialmente en la mitad izquierda.
- B se ubica inicialmente en la mitad derecha.
- C se distribuye aleatoriamente en todo el espacio.

Esta distribución permite observar cómo A y B tienden a acercarse y formar un supergrupo móvil, mientras que C intenta incorporarse desde múltiples direcciones.


# Registro de pruebas

## Versión 1

- A y B se repelían.
- Resultado: dos comunidades separadas y poco intercambio.

<img width="1847" height="807" alt="image" src="https://github.com/user-attachments/assets/9af76dcc-765c-4fb6-8b2b-d47e3ab1e327" />


## Versión 2

- A y B se atraían demasiado.
- Resultado: un único grupo muy compacto y poco dinámico.

<img width="1841" height="817" alt="image" src="https://github.com/user-attachments/assets/a0452708-d687-4726-bb34-e7ed3ea9c2fe" />


## Versión seleccionada

- Atracción moderada entre A y B.
- Atracción fuerte de C hacia el grupo.
- Repulsión cercana del grupo hacia C.
- Resultado: ciclos claros de aproximación, expulsión y reintento.

<img width="1857" height="872" alt="image" src="https://github.com/user-attachments/assets/fcf17cad-b14d-4dc8-a4a6-0d2364f287d3" />


# Hallazgos

- La asimetría es esencial: C debe querer unirse más de lo que el grupo quiere aceptarla.
- El alcance largo de la atracción y el alcance corto de la repulsión generan bordes activos.
- Una cantidad excesiva de partículas dificulta percibir la contradicción.


# Descartes

- Trayectorias predefinidas.
- Diferencias de tamaño muy grandes.
- Repulsión constante entre A y B.
- Atracción entre C y C.

Estas opciones reducían la claridad o producían patrones menos relacionados con la intención.


# Varias manifestaciones del mismo sistema

## Manifestación 1 – Semilla 11

- A y B forman dos grupos que luego se conectan mediante cadenas temporales.
- C orbita alrededor del borde del grupo combinado.

## Manifestación 2 – Semilla 27

- El grupo principal se desplaza por el espacio.
- C es expulsada en ráfagas hacia diferentes direcciones.

## Manifestación 3 – Semilla 84

- A y B permanecen parcialmente separados.
- C alterna entre ambos grupos y nunca logra estabilizarse.

En todas las manifestaciones se conserva la identidad del sistema: **cooperación interna y exclusión externa**.


# Relación con Motion 101 y Particle Life

El sistema utiliza:

- posición,
- velocidad,
- aceleración,
- fuerzas dependientes de la distancia,
- múltiples poblaciones,
- relaciones asimétricas,
- comportamiento emergente.

No existen trayectorias predefinidas; el movimiento surge de las interacciones locales entre partículas.
te ese intento permanente es lo que mantiene el movimiento y hace visible la tensión conceptual del proyecto.

# Código:

    let particles = [];
    
    const counts = {
      A: 45,
      B: 45,
      C: 70
    };
    
    const colors = {
      A: [90, 173, 226],  // azul
      B: [88, 214, 141],  // verde
      C: [245, 176, 65]   // naranja
    };
    
    // Matriz de relaciones
    const matrix = {
      A: { A: 0.42, B: 0.22, C: -0.50 },
      B: { A: 0.22, B: 0.42, C: -0.50 },
      C: { A: 0.58, B: 0.58, C: -0.08 }
    };
    
    function setup() {
      createCanvas(900, 600);
      background(8, 10, 18);
    
      // A en la izquierda
      createGroup('A', counts.A, 0, width * 0.45);
    
      // B en la derecha
      createGroup('B', counts.B, width * 0.55, width);
    
      // C en todo el espacio
      createGroup('C', counts.C, 0, width);
    }
    
    function createGroup(type, amount, x1, x2) {
      for (let i = 0; i < amount; i++) {
        particles.push(
          new Particle(
            random(x1, x2),
            random(height),
            type
          )
        );
      }
    }
    
    function draw() {
      // Fondo con transparencia para dejar rastros suaves
      background(8, 10, 18, 35);
    
      // Interacciones
      for (let p of particles) {
        p.interact(particles);
      }
    
      // Actualización y dibujo
      for (let p of particles) {
        p.update();
        p.edges();
        p.display();
      }
    }
    
    class Particle {
      constructor(x, y, type) {
        this.pos = createVector(x, y);
        this.vel = p5.Vector.random2D().mult(random(0.5, 1.5));
        this.acc = createVector();
        this.type = type;
      }
    
      interact(others) {
        for (let o of others) {
          if (o === this) continue;
    
          let d = p5.Vector.dist(this.pos, o.pos);
    
          // Rango base
          let range = 72;
    
          // Atracción entre A y B
          if (
            (this.type === 'A' && o.type === 'B') ||
            (this.type === 'B' && o.type === 'A')
          ) {
            range = 88;
          }
    
          // C detecta grupos desde lejos
          if (this.type === 'C' && (o.type === 'A' || o.type === 'B')) {
            range = 118;
          }
    
          // El grupo rechaza a C solo cuando está cerca
          if ((this.type === 'A' || this.type === 'B') && o.type === 'C') {
            range = 54;
          }
    
          if (d > 0 && d < range) {
            let force = matrix[this.type][o.type];
    
            let dir = p5.Vector.sub(o.pos, this.pos);
    
            // Fuerza suave según la distancia
            let strength = force * (1 - d / range);
    
            dir.setMag(strength * 0.28);
    
            this.acc.add(dir);
          }
        }
      }
    
      update() {
        this.vel.add(this.acc);
    
        // Velocidad máxima
        let maxV = this.type === 'C' ? 3.2 : 2.0;
        this.vel.limit(maxV);
    
        this.pos.add(this.vel);
    
        // Fricción
        this.vel.mult(0.93);
    
        // Reiniciar aceleración
        this.acc.mult(0);
      }
    
      edges() {
        // Mundo toroidal
        if (this.pos.x < 0) this.pos.x += width;
        if (this.pos.x > width) this.pos.x -= width;
        if (this.pos.y < 0) this.pos.y += height;
        if (this.pos.y > height) this.pos.y -= height;
      }
    
      display() {
        noStroke();
    
        if (this.type === 'C') {
          fill(...colors[this.type], 170);
          circle(this.pos.x, this.pos.y, 3);
        } else {
          fill(...colors[this.type], 220);
          circle(this.pos.x, this.pos.y, 5);
        }
      }
    }

# Autoevaluación

| Criterio | Peso | Valoración | Aporte |
|---|---:|---:|---:|
| La intención es clara y perceptible en el comportamiento. | 20% | 95% | 19.0 |
| Los tipos, cantidades, matriz y parámetros están justificados desde la intención. | 25% | 90% | 22.5 |
| Comprendo y puedo modificar el funcionamiento técnico del sistema. | 20% | 90% | 18.0 |
| El sistema produce variaciones con una identidad reconocible. | 15% | 95% | 14.25 |
| Experimenté, comparé, seleccioné y descarté con criterios claros. | 10% | 90% | 9.0 |
| Puedo distinguir y sustentar lo diseñado y lo emergente. | 10% | 85% | 8.5 |
| **Total** | **100%** |  | **91.25** |

## Nota propuesta

**Puntaje total:** 91.25

**Nota propuesta:** 4.56 / 5.0

