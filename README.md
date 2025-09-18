# Proyecto Corto I — Diseño Digital Combinacional en FPGA (Hamming SEC-DED)

**Curso:** EL-3307 Diseño Lógico — II Semestre 2025  
**Escuela:** Escuela de Ingeniería Electrónica, ITCR  
**Autores:** José Andrés Acosta Sosa, Fabiola Solano Guillén 

---

## Introducción  
La creciente complejidad de los sistemas digitales modernos exige el uso de metodologías de diseño asistidas por computadora. En este proyecto se abordó la implementación de un sistema de corrección y detección de errores mediante el algoritmo de Hamming, aplicando conceptos de diseño digital sincrónico en una FPGA TangNano.  

La meta principal consistió en diseñar, codificar, simular y verificar un circuito digital capaz de codificar palabras binarias, detectar errores introducidos en la transmisión, corregirlos cuando sea posible y desplegar los resultados tanto en LEDs como en displays de 7 segmentos.  

El proyecto se desarrolló en un lapso de dos semanas, dividido en fases de diseño, codificación, pruebas y documentación, con un esquema de trabajo colaborativo entre dos integrantes utilizando control de versiones.

---

## Objetivo general  
Introducir al estudiante en el desarrollo de sistemas digitales utilizando lenguajes de descripción de hardware, enfatizando en la codificación, verificación y despliegue de resultados en dispositivos programables.

---

## Objetivos específicos  
1. Implementar un diseño digital en FPGA utilizando SystemVerilog.  
2. Construir testbenches básicos para validar las especificaciones del diseño.  
3. Implementar el algoritmo de Hamming (SEC-DED) para corrección de un error y detección de dos errores.  
4. Visualizar retrasos de señal y formas de onda mediante simulación.  
5. Coordinar el trabajo en equipo con control de versiones.  
6. Practicar la planificación de tareas en grupos pequeños.  

---

## Especificación del diseño  
El circuito se estructuró en subsistemas interconectados, siguiendo una arquitectura modular:  

- **Lectura y codificación de la palabra transmitida:** generación de bits de paridad a partir de una palabra de 4 bits.  
- **Lectura y decodificación de la palabra recibida:** entrada de 8 bits con posibilidad de errores intencionados.  
- **Verificador de paridad y detector de error:** identificación de un error corregible o detección de doble error.  
- **Corrección de error:** corrección de la palabra recibida o despliegue de error múltiple.  
- **Despliegue en LEDs:** representación de la palabra corregida y señalización de doble error.  
- **Despliegue en display de 7 segmentos:** visualización en notación hexadecimal de la palabra transmitida o de la posición del error.  

---

## Metodología de desarrollo  
### Fase 1 – Diseño conceptual  
- Análisis del algoritmo de Hamming SEC-DED.  
- Definición de la arquitectura del sistema.  
- Bocetos de diagramas de bloques.  

### Fase 2 – Implementación en HDL  
- Codificación en SystemVerilog con estilo estructural.  
- Redacción de ecuaciones booleanas simplificadas para algunos submódulos.  
- Organización de los módulos según subsistemas.  

### Fase 3 – Simulación y verificación  
- Creación de testbenches para cada subsistema.  
- Simulaciones a nivel RTL y post-síntesis.  
- Análisis de tiempos y verificación funcional de las salidas en LEDs y 7 segmentos.  

### Fase 4 – Integración y despliegue en hardware  
- Alambrado en protoboard de conmutadores y displays.  
- Configuración de pines de la FPGA TangNano.  
- Validación de comportamiento en laboratorio.  

### Fase 5 – Documentación  
- Elaboración de bitácora con avances diarios.  
- Redacción del presente informe en formato README.md.  

---

## Montaje físico en protoboard  
Para comprobar el funcionamiento en hardware, se realizaron conexiones físicas entre la FPGA TangNano y una protoboard. El montaje se organizó de la siguiente manera:  

1. **Entradas de la palabra transmitida (4 bits):**  
   - Se conectaron 4 switches en la protoboard, cada uno con resistencia de pull-down.  
   - Cada salida del switch se conectó a las entradas correspondientes de la FPGA (según el archivo de constraints).  

2. **Entradas de la palabra recibida (8 bits):**  
   - Se colocaron 8 switches adicionales que representan la palabra recibida con errores intencionales.  
   - Estas entradas se cablearon directamente a la FPGA, con resistencias de pull-down para asegurar niveles lógicos definidos.  

3. **Displays de 7 segmentos:**  
   - Se utilizaron en lugar de dos módulos de display de 7 segmentos, un solo módulo para mayor facilidad en la protoboard.  
   - Los ánodos fueron controlados mediante transistores PNP conectados a la FPGA, de modo que se activara un display u otro según el selector.  
   - Los cátodos se cablearon directamente a las salidas de la FPGA.

4. **Alimentación:**  
   - La protoboard se alimentó con 3.3 V desde la FPGA TangNano, asegurando compatibilidad de niveles lógicos.  

El resultado del montaje fue un sistema interactivo: al variar los switches se podían introducir datos y errores, y las correcciones eran reflejadas en tiempo real tanto en LEDs como en los displays.

---

## Ejercicio 2: Oscilador en anillo
Oscilador con 5 inversores 
<img width="800" height="480" alt="DS0001" src="https://github.com/user-attachments/assets/8a05bd29-9f15-4bd6-81bd-ebd978f978a6" />
Oscilador con 3 inversores 
<img width="800" height="480" alt="DS0010" src="https://github.com/user-attachments/assets/7027a929-9625-473f-a973-96af887a93d3" />
El periodo de osilacion en la practica es de 16,7 ms
Oscilado con un 1 metro de alambre 
<img width="800" height="480" alt="DS0007" src="https://github.com/user-attachments/assets/158c6cae-1aef-4e30-a077-cc3db4b9a46d" />
La amplitud y el ruido se ven afectado por la longitud del cable a comparacion de las medidas antesrios hechas con puentes cortos 
Tension estable 
<img width="800" height="480" alt="DS0008" src="https://github.com/user-attachments/assets/d377f2b0-11ba-4cde-9fd8-2fd5117c228e" /> 
medicion sin el capacitor 
<img width="800" height="480" alt="DS0006" src="https://github.com/user-attachments/assets/9d88f8a3-df3b-40be-ba76-4737af28ed3c" />
Medicion con el capacitor 
Hay un cambio de 8V a 100mV esto devido a la carga capacitiva y la velocidad maxima de operacion de circuito.

---

## Resultados  
- **Funcionamiento del sistema:** Se logró la codificación de palabras de 4 bits con paridad extendida, la detección de un error sencillo, la corrección automática del mismo y la identificación de errores dobles.  
- **Simulación:** Se verificaron transiciones de entrada y salida, confirmando la robustez del diseño.  
- **Recursos utilizados:** El diseño empleó LUTs y FFs en proporciones moderadas, sin comprometer el rendimiento de la FPGA.  
- **Despliegue:** Los LEDs mostraron la palabra corregida y los displays de 7 segmentos representaron tanto la palabra transmitida como el síndrome de error.  

---

## Principales problemas encontrados  
1. **Codificación inicial del algoritmo de Hamming:** Requirió ajustes debido a discrepancias entre la teoría y la implementación en HDL.  
2. **Sincronización de señales:** Algunos problemas de latencia obligaron a introducir registros intermedios.  
3. **Alambrado de los displays:** Fue necesario implementar transistores PNP para la correcta activación de los segmentos.  
4. **Compatibilidad de voltajes:** Se debió ajustar el VDD a 3.3 V para garantizar el funcionamiento seguro.  

---

## Conclusiones  
El proyecto permitió afianzar competencias en diseño digital, simulación y uso de FPGA. La implementación modular y el uso de control de versiones facilitaron la organización del trabajo. A pesar de los retos técnicos, el sistema cumplió con las especificaciones propuestas y se logró un funcionamiento completo tanto en simulación como en hardware.  

---

