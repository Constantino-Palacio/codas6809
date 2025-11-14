# Codas-09

<div align="center"><img src="https://github.com/user-attachments/assets/4c347d36-96e3-46b3-8146-0538222a51dc"  width="50%" height="50%"></div>

El Codas-09 es un kit de desarrollo del procesador 6809E de Motorola. Esencialmente es una SBC (_Single Board Computer_) que presenta un conector de bus (para backplane) y dos salidas del integrado R6522AP (_Versatile Interface Adapter_, VIA): una reservada para la placa de teclado (puerto B) y otra para aplicaciones del usuario (puerto A).

La placa del procesador contiene la RAM (2KiB) y la ROM (4KiB) del sistema, además de un zócalo para agregar otros 2KiB de RAM/ROM. La memoria ROM contiene el programa "básico" que hace la interfaz con la placa de teclado: un debugger bastante completo y un programa de calculadora RPN en hexadecimal y BCD con y sin signo en ambos casos.

La placa del teclado contiene un teclado sencillo para el ingreso de la información y un conjunto de LEDs y displays de 7 segmentos para visualización. Además, presenta una interfaz de cassette para E/S, aunque sólo se implementa en hardware: el usuario es el responsable de implementar el protocolo de comunicación con el grabador.

El kit se monta en una tabla de madera, con lugar para ambas placas y el circuito de alimentación. Se requiere de una fuente con tensión mayor a 8V, pues ambos módulos contienen un regulador de tensión interno que convierte la entrada (de hasta 18V) a 5V.

## Documentación

El kit se incluye con su manual correspondiente, que explica en forma breve cada una de las funciones de ambos módulos y cómo utilizar el programa incluido. Además, se incluye la hoja de datos del MC6809E y un apéndice con el conjunto de instrucciones del procesador.

<div align="center"><img src="https://github.com/user-attachments/assets/a5081c0b-7475-44e3-929d-b370e318fd87"  width="50%" height="50%"></div>

## Puesta a punto

Inicialmente, dos kits Codas fueron encontrados, y se tomó uno de ellos (Nº1) para su restauración, junto a los manuales del MC6809. En la imagen se muestra el kit Nº2, representativo del estado de ambos kits al momento de su hallazgo.

<div align="center"><img src="https://github.com/user-attachments/assets/f449d468-3e90-4c1d-a773-f8533aa700eb"  width="50%" height="50%"></div>

Ambas placas fueron limpiadas (no perfectamente) por ambos lados utilizando alcohol y un cepillo dental (lo que provocó una reacción con el flux de la placa, resultando en un residuo blanco removido con alcohol y un hisopo). El teclado y el plástico que cubre los LEDs y displays fueron limpiados con agua jabonosa. La tabla fue lustrada por separado.

Se probó el regulador con una fuente de 12V conectada al módulo de teclado, dejando aislado el módulo del MPU. Al observarse una reacción positiva (LEDs encendidos), se procedió a probar el circuito completo. Como el módulo de MPU no posee ninguna entrada de alimentación además del conector de backplane, se tomó un pad sin utilizar conectado a la línea de alimentación y se soldó un terminal para la conexión de la fuente. Para el conector de tierra se usó el terminal presente en el puerto A la VIA. Esta solución no es permanente. En tal caso se buscará una forma más sólida de conexión, como soldar los cables de +12V y GND directamente a la fuente o a un conector dentro de la misma.

Conectada la alimentación, se comprobó que ambos módulos funcionan: se reinició el sistema y la palabra `CODAS` apareció en el display. Para probar el programa del kit se recurrió al manual de instrucciones y se pudo verificar su correcto funcionamiento.

La siguiente imagen ilustra el funcionamiento del kit Nº1 luego del proceso de restauración.

<div align="center"><img src="https://github.com/user-attachments/assets/70ba176d-e672-4fbc-bbab-517f7f474152"  width="50%" height="50%"></div>

Se reemplazó también la conexión de alimentación por una llave de encendido conectada a una fuente de 12V tipo cargador de baterías. Esto resulta en una forma más conveniente de encendido y apagado del sistema.

## Mapa de memoria
- 0000:DFFF   56KiB libres para ampliación (backplane)
- E000:EFFF   4KiB RAM (zócalos M3 y M4, integrados 6116 2K*8)
- F000:FFFF   4KiB ROM monitor (zócalos M2 y M1, integrados 2716 2K*8)

Direcciones especiales:
- FFE0:FFEF   VIA
- FFF2:FFFF   Vector de Reset/Interrupción
