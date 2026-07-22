# Reto de diseño

En este reto de diseño pensé en la eclosión de los huevos del cóndor, con la intención de preservar esta especie en vía de extinción que su principal problema es la reproducción lenta dado que una pareja pone solo un huevo cada dos o tres años. Esta experiencia interactiva busca que el usuario encuentre los parámetros ideales para la eclosión, mientras pasan los 60 días para que eclosione.

Cada día se demoraría 1 segundo hasta los 55 días porque los parámetros cambian a 5 días de eclosionar, por lo que los últimos cinco días pueden demorarse 4 segundos cada uno. La idea es que sea como un contador en la parte superior de la pantalla que vaya reduciendo desde 60 hasta 0 que es cuando eclosiona el huevo.

En el centro de la pantalla aparecería el huevo y cambiaria el color a un color más cálido cuando sea una mayor la temperatura y un color mas frio cuando sea menor la temperatura. El huevo también cambia si el volteo es mayor o menor, si es mayor oscila el huevo más rápido si es menor menos rápido y si es cero no se mueve. También cambia el huevo a que tenga gotas de agua y mas gotas de agua si hay más humedad y si hay menos humedad menos gotas de agua. Por último, la ventilación, que aparecería ráfagas de viento y a más ventilación más ráfagas y a menos ventilación menos ráfagas.

Abajo a la derecha aparecerían los parámetros para deslizar y cambiarlos 

A medida de que pasa el tiempo los parámetros cambia de forma aleatoria utilizando randomGauss  
