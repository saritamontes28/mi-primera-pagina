Desafío de la Tortuga en Consola (Retos 1 - 5)
El objetivo principal es simular el comportamiento de la biblioteca gráfica turtle (avance y giro) utilizando solamente print() para dibujar y funciones básicas para encapsular la lógica.

-----

##  Reto 1: Simula el comportamiento de la tortuga (Avance)

El objetivo es simular el comando `t.forward(10)` usando solo `print()` e `input()`.

###  Código (Reto 1)

```python
# Reto 1: Simula el avance horizontal
def simular_avance(n):
    """Simula el avance horizontal (t.forward) en la consola."""
    print("-" * n + ">")
    
    # input() simula la pausa gráfica y el requerimiento de usar input().
    input(f"Tortuga simulada avanzó {n} pasos. Presiona Enter para continuar.")

# Ejecución
simular_avance(10)
```

###  Explicación (Reto 1)

  * **`def simular_avance(n):`**: Define una función que toma la longitud del movimiento (`n`) como argumento.
  * **`print("-" * n + ">")`**: Dibuja el rastro. El truco es multiplicar la cadena `"-"` por la variable `n`. El `>` representa la punta de la flecha o la cabeza de la tortuga.
  * **`input(...)`**: Se usa para forzar una pausa en la consola, simulando la espera de un evento en la ventana gráfica de `turtle`.

### Resultado
<img width="463" height="43" alt="image" src="https://github.com/user-attachments/assets/d343d0a0-3a93-408f-90da-f30657d41cbd" />

-----

##  Reto 2: Tortuga bajando (Vertical)

El objetivo es simular el rastro de la tortuga moviéndose **hacia abajo** (giro de 90 grados y avance vertical).

###  Código (Reto 2)

```python
# Reto 2: Simula el movimiento vertical hacia abajo
def simular_bajada(n):
    """Simula el movimiento vertical (hacia abajo) en la consola."""
    
    # Bucle para dibujar la longitud del trazo
    for _ in range(n):
        print("|")
        
    # Dibuja la flecha final
    print("V")
    
    input(f"Tortuga simulada bajó {n} pasos. Presiona Enter para continuar.")

# Ejecución
simular_bajada(5)
```

###  Explicación (Reto 2)

  * **`for _ in range(n):`**: Un bucle `for` repite la impresión del carácter vertical.
  * **`print("|")`**: Dibuja la línea vertical (`|`) en su propia línea, simulando el avance hacia abajo.
  * **`print("V")`**: Se usa la letra `V` para representar la dirección final del movimiento (hacia abajo).
    
### Resultado
<img width="449" height="123" alt="image" src="https://github.com/user-attachments/assets/ce35e55f-2397-49e2-8aa3-662511b3d289" />

-----

##  Reto 3: Girar y dibujar (La 'L' alineada)

El objetivo es simular un avance y un giro (`t.forward(100); t.right(90); t.forward(100)`), lo que requiere alinear el segmento vertical con el horizontal.

###  Código (Reto 3)

```python
# Reto 3: Simulación de la forma "L" con alineación

def simular_l(n_h, n_v):
    """Dibuja un patrón en forma de L, alineando el vertical con el horizontal."""
    
    # 1. Movimiento horizontal
    print("-" * n_h + ">")
    
    # Calculamos el margen necesario para alinear la bajada con la punta del ">".
    margen_vertical = n_h 
    
    # 2. Movimiento vertical (alineado)
    for _ in range(n_v):
        print(" " * margen_vertical + "|")
        
    print(" " * margen_vertical + "V")
    
    input("Patrón en 'L' dibujado. Presiona Enter.")

# Ejecución: 5 pasos horizontales y 3 verticales
simular_l(5, 3)
```

###  Explicación (Reto 3)

  * **`margen_vertical = n_h`**: Esta variable es crucial. Almacena la longitud del trazo horizontal.
  * **`print(" " * margen_vertical + "|")`**: Se utiliza el margen (espacios) antes del carácter vertical (`|`). Esto **empuja** el trazo vertical hacia la derecha, alineándolo justo debajo del final del trazo horizontal (`>`), simulando el giro correcto de 90 grados.

### Resultado
<img width="286" height="107" alt="image" src="https://github.com/user-attachments/assets/068a9805-4529-430e-8d41-45ffd2e2e6ba" />

-----

##  Reto 4: Encapsula los comportamientos usando funciones

El objetivo es refactorizar los movimientos en las funciones **`adelante(n)`** y **`abajo(n)`** usando una variable global para conservar la posición y preparar la simulación de múltiples segmentos.

###  Código (Reto 4)

```python
# **LA CLAVE:** Variable global para mantener la "memoria" de la posición horizontal.
posicion_h = 0

def adelante(n):
    """Dibuja el avance horizontal y actualiza la posición global."""
    global posicion_h
    
    # Imprime con el margen y el trazo
    print(" " * posicion_h + "-" * n + ">")
    
    # Actualiza la posición: suma n (pasos) + 1 (la punta ">").
    posicion_h += n + 1 

def abajo(n):
    """Dibuja el descenso vertical, alineado con el trazo anterior, y conserva la posición."""
    global posicion_h
    
    # Margen para alinear con el final del trazo anterior.
    margen_vertical = posicion_h - 1
    
    # Dibuja la línea vertical
    for _ in range(n):
        print(" " * margen_vertical + "|")
        
    # Dibuja la flecha 'V'
    print(" " * margen_vertical + "V")
    
    # Conserva la posición: el siguiente 'adelante' debe empezar aquí.
    posicion_h = margen_vertical 
    

# Ejecución de prueba (Patrón en L)
print("--- Ejecución Reto 4 (Patrón L) ---")
adelante(5)
abajo(3)
```

###  Explicación (Reto 4)

  * **`posicion_h = 0`**: La variable **global** almacena la posición en la consola.
  * **`global posicion_h`**: Esta palabra clave dentro de las funciones es necesaria para poder **modificar** la variable global. Sin ella, Python asumiría que estás creando una variable local.
  * **`adelante(n)`**: Es responsable de **aumentar** `posicion_h`, moviendo la tortuga hacia la derecha.
  * **`abajo(n)`**: Es responsable de **calcular** la alineación (`posicion_h - 1`) y de **establecer** la nueva posición horizontal para el siguiente avance.

### Resultado
<img width="92" height="82" alt="image" src="https://github.com/user-attachments/assets/83100b24-e376-40b8-a7b8-58c465f4a94f" />

-----

##  Reto 5: La tortuga baja las escalas

El objetivo es usar las funciones del Reto 4 repetidamente para dibujar múltiples escalones, probando que la conservación de posición funciona.

###  Código (Reto 5)

*(Usamos las mismas funciones `adelante` y `abajo` del Reto 4)*

```python
# Reiniciamos la posición para la simulación
posicion_h = 0 

# (Aquí se define de nuevo el código de adelante(n) y abajo(n))

# --- Ejecución del Reto 5: Bajar 3 escalones (adelante 5, abajo 2) ---

print("--- Comportamiento Esperado: Bajando 3 Escalones ---")

# Escalón 1
adelante(5)
abajo(2)

# Escalón 2
adelante(5)
abajo(2)

# Escalón 3
adelante(5)
abajo(2)
```

###  Explicación (Reto 5)

  * **Lógica en Secuencia:** La solución simplemente consiste en llamar a las dos funciones, `adelante(n)` seguido de `abajo(n)`, para dibujar un escalón completo.
  * **Efecto de Escalera:** Gracias a la lógica de `posicion_h`:
    1.  `adelante(5)` incrementa la posición.
    2.  `abajo(2)` se alinea con el nuevo punto y luego establece la posición para el siguiente avance.
    3.  La segunda llamada a `adelante(5)` comienza en una posición más a la derecha que la primera, creando el efecto visual de un **escalón descendente**.

### Resultado
<img width="300" height="216" alt="image" src="https://github.com/user-attachments/assets/fc6759ca-20e2-492b-b16d-96e7d4424158" />

-----
