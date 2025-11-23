Aquí tienes las instrucciones concisas para calibrar la cama (nivelación y planitud) de tu impresora Delta.

Dado que Delta Auto Calibration está desactivado en tu firmware pero tienes EEPROM activado, haremos esto manualmente ajustando los Endstops (Torres) y el Radio (Centro).

1. Preparación
Ejecuta estos comandos para iniciar:

gcode
M501      ; Cargar valores guardados
M503      ; Ver valores actuales (anota los valores de M666 y M665)
G28       ; Home
2. Calibrar Torres (Nivelación) - Comando M666
El objetivo es que la boquilla esté a altura Z=0 justo enfrente de cada torre. Usa la prueba del papel.

Torre X (Frontal Izquierda): G1 X-65 Y-37.5 Z0
Torre Y (Frontal Derecha): G1 X65 Y-37.5 Z0
Torre Z (Trasera): G1 X0 Y75 Z0
Ajuste: Si la boquilla está muy alta o choca en una torre, ajusta los "Endstop Offsets" con M666.

Comando: M666 X<valor> Y<valor> Z<valor> (Ej: M666 X-0.5)
Regla:
Si la boquilla está ALTA (pasa mucho papel): REDUCE el valor (hazlo más negativo).
Si la boquilla CHOCA (aprieta el papel): AUMENTA el valor (hazlo más positivo).
Nota: Haz ajustes pequeños (0.1 o 0.2 mm) y repite G28 y la prueba.
3. Calibrar Centro (Planitud/Radio) - Comando M665
Una vez que las 3 torres estén perfectas a Z=0, verifica el centro.

Centro: G1 X0 Y0 Z0
Ajuste: Si el centro no está a la misma altura que las torres, ajusta el "Delta Radius" (R) con M665.

Comando: M665 R<valor> (Ej: M665 R105.5)
Regla:
Si el centro está ALTO (Cóncavo/Domo, la boquilla no toca): AUMENTA el Radio (R).
Si el centro CHOCA (Convexo/Cuenco, la boquilla aprieta): DISMINUYE el Radio (R).
Nota: Al cambiar el Radio, las alturas de las torres cambiarán ligeramente. Es posible que debas repetir el paso 2 y 3 un par de veces.
4. Guardar
Cuando todo esté nivelado:

gcode
M500      ; Guardar configuración en memoria permanente
Tip: Tienes activado DELTA_CALIBRATION_MENU en tu firmware, por lo que si tienes pantalla LCD, también puedes buscar la opción "Delta Calibration" en el menú para que la impresora se mueva a estos puntos automáticamente.

Instrucciones Concisas de Calibración (Ciclo de Ajuste)
Repite este ciclo para cada torre (X, Y, Z) y luego para el Centro:

Mover: Ve al punto de prueba (Ej: G1 X-65 Y-37.5 Z0 para Torre X).
Comprobar: Usa el papel.
Muy alto: Papel suelto.
Muy bajo: Papel atrapado.
Ajustar: Envía el comando M666 (Torres) o M665 (Radio).
Ej: M666 X-0.2 (Baja la boquilla 0.2mm en X).
REINICIAR (CRÍTICO): Envía G28. <-- Sin esto, el cambio no surte efecto.
Verificar: Vuelve al paso 1 para ver si ahora está bien.
Resumen de Ajustes
Nivelación (Torres) - M666:
Boquilla Alta (no toca): Haz el valor MÁS NEGATIVO (Resta).
Boquilla Baja (choca): Haz el valor MÁS POSITIVO (Suma).
Recuerda: M666 X... Y... Z...
Planitud (Centro) - M665 R...:
Centro Alto (Domo): AUMENTA el Radio (R).
Centro Bajo (Cuenco): DISMINUYE el Radio (R).
Al finalizar todo: M500 para guardar.