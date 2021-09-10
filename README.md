<h1 align="center">Organización de Computadoras </h1>
<div align="center">
<img src="https://media.giphy.com/media/11LK0CKzYtkaic/giphy.gif?cid=ecf05e47q1771mvp65emyjz7yd60iq2d0jy5awmuqxxdrr6q&rid=giphy.gif&ct=g"/>
 </div>

<div>
<table >
  <thead>
    <tr>
      <th>Registro</th>
      <th>Funcionamiento</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>AX</td>
      <td>Madrid</td>
    </tr>
    <tr>
      <td>BX</td>
      <td>Ciudad de México</td>
    </tr>
    <tr>
      <td>CX</td>
      <td>Buenos Aires</td>
    </tr>
   <tr>
      <td>CX</td>
      <td>Buenos Aires</td>
    </tr>
  </tbody>
  
</table>
</div>
 
 
 
1 - El Programa 1 utiliza una instrucción de transferencia de datos (instrucción MOV) con diferentes modos de direccionamiento para hacer referencia a sus operandos. Ejecutar y analizar cada instrucción en el Simulador MSX88 observando el flujo de información a través del BUS DE DATOS, el BUS DE DIRECCIONES, el BUS DE CONTROL, el contenido de los REGISTROS, de las posiciones de MEMORIA accedidas, de las operaciones en la ALU, etc...

a) Explicar detalladamente qué hace cada instrucción MOV del programa anterior, en función de sus operandos y su modo de direccionamiento.

b) Confeccionar una tabla que contenga todas las instrucciones MOV anteriores, el modo de direccionamiento y el contenido final del operando destino de cada una de ellas.

c) Notar que durante la ejecución de algunas instrucciones MOV aparece en la pantalla del simulador un registro temporal denominado “ri”, en ocasiones acompañado por otro registro temporal denominado “id”. Explicar con detalle que función cumplen estos registros.
```Assembly
;Variables
org 1000h
NUM0 DB 0CAH ;1000h
NUM1 DB 0  ;1001h
NUM2 DW ? ; 1002h y 1003h
NUM3 DW 0ABCDH ;1004h y 1005h
NUM4 DW ?  ;1006h y  1007h

;Programa
org 2000h
mov BL, NUM0  ;BL = CA
mov BH, 0FFH    ;BH = FF
mov CH, BL      ;CH  = CA
mov AX, BX     ; AX = BX(BL:CA,BH:FF)  = CA,FF
mov NUM1, AL ;1001h = CA
mov NUM2, 1234h ;1002h = 34h y 1003H = 12h
mov BX, OFFSET NUM3 ;BX = 1004h
mov DL, [BX] ;DL = CD (Lo que apunta 1004h)
mov AX, [BX] ; AH=AB, AL=CD
mov BX, 1006h ;BX = 1006h
mov WORD PTR [BX], 0CDEFH ;1007h=CD, 1006h = EF
HLT
end
```
2 - El Programa 2 utiliza diferentes instrucciones de procesamiento de datos (instrucciones aritméticas y lógicas). Analice y ejecute el comportamiento de ellas en el MSX88.
a) ¿Cuál es el estado de los FLAGS después de la ejecución de las instrucciones ADD y SUB del programa anterior? Justificar el estado de cada uno de ellos (¿por qué quedaron en 0 ó en 1?).

¿Dan alguna indicación acerca de la correctitud de los resultados?

b) ¿Qué cadenas binarias representan a NUM1 y NUM2 en la memoria del simulador? ¿En qué sistemas binarios están expresados estos valores?

c) Confeccionar una tabla que indique para cada operación aritmética o lógica del programa, el valor de sus operandos, en qué registro o dirección de memoria se almacenan y el resultado obtenido luego de realizar cada operación

```Assembly
ORG 1000H
  NUM0 DB 80H
  NUM1 DB 200
  NUM2 DB -1
  Bts0 DB 01111111B
  Bts1 DB 10101010B
ORG 2000H
  MOV AL, NUM0 ; AL = 80
  ADD AL, AL ;80+80 en binario  C=1, O=1, S=0, Z=1
  INC NUM1 ;200 + 1
  MOV BH, NUM1 ;BH=C9h
  MOV BL, BH ;BL=C9h
  DEC BL ; BL = C8h
  SUB BL, BH ;-1(decimal), FFFFH
  MOV CH, Bts1
  AND CH, Bts0 ;Bts1 and Bts2
  NOT Bts0
  OR CH, Bts0
  XOR CH, 11111111B
  HLT
END
```
3 - El Programa 3 implementa un contador utilizando una instrucción de transferencia de control. Analice el funcionamiento de cada instrucción, poniendo atención en las del lazo repetitivo que provoca la cuenta.

a) ¿Cuántas veces se ejecuta el lazo? ¿De qué variables depende esto en el caso general?

b) Analice y ejecute el programa reemplazando la instrucción de salto condicional JNZ por las siguientes, indicando en cada caso el contenido final del registro AL:
1. JS
2. JZ
3. JMP

```Assembly

ORG 1000H
  INI DB 0
  FIN DB 15
ORG 2000H
  MOV AL, INI ;0
  MOV AH, FIN ;Fh (15)
  SUMA: INC AL; AL + 1
  CMP AL, AH ;FIN - AL
  JNZ SUMA ;Se repite hasta que sea 0
  HLT ;Termina con AL = 15
END

```
