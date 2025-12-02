Desafío de la Tortuga en Consola (Retos 1 - 5)
El objetivo principal es simular el comportamiento de la biblioteca gráfica turtle (avance y giro) utilizando solamente print() para dibujar y funciones básicas para encapsular la lógica.

-----

##  Reto 1: Simula el comportamiento de la tortuga (Avance)

El objetivo es simular el comando `t.forward(10)` usando solo `print()` e `input()`.

###  Código (Reto 1)

```python
# Reto 1: Simula el avance horizontal
print("-" * 10 + ">")
input("Tortuga simulada avanzó 10 pasos. Presiona Enter para continuar.")
```

###  Explicación (Reto 1)

* **`print("-" * 10 + ">")`**: Dibuja el rastro. El truco clave es multiplicar la cadena **`"-"`** por el número de pasos (**`10`**), lo que repite el guion diez veces. El **`+ ">"`** añade la punta de la flecha, representando la cabeza de la tortuga o la dirección del movimiento.
* **`input(...)`**: Se usa para forzar una **pausa** en la consola. Esto simula la espera de un evento o la actualización de la ventana gráfica que se requiere después de cada movimiento en un entorno como `turtle`, asegurando que el usuario vea el avance antes de que el programa finalice.

### Resultado
<img width="463" height="43" alt="image" src="https://github.com/user-attachments/assets/d343d0a0-3a93-408f-90da-f30657d41cbd" />

-----

##  Reto 2: Tortuga bajando (Vertical)

El objetivo es simular el rastro de la tortuga moviéndose **hacia abajo** (giro de 90 grados y avance vertical).

###  Código (Reto 2)

```python
# Simulación de los 5 pasos verticales
print("|")
print("|")
print("|")
print("|")
print("|")

# Dibuja la punta de la flecha
print("V")

# Simula la pausa y la interacción
input("Tortuga simulada bajó 5 pasos. Presiona Enter para continuar.")
```

###  Explicación (Reto 2)

* Líneas Verticales: Cada instrucción print("|") representa **un paso hacia abajo**. Al repetir el print la cantidad de veces necesaria (en este caso, 5), se simula la longitud del trazo vertical del movimiento.
* Punta de Flecha: La instrucción print("V") dibuja el indicador final del movimiento, actuando como la **punta de la flecha** que marca la dirección final.
* Pausa: La función input(...) detiene la ejecución del programa. Esto simula la **pausa gráfica** necesaria para que el usuario pueda ver el movimiento antes de que la consola siga o finalice.
    
### Resultado
<img width="449" height="123" alt="image" src="https://github.com/user-attachments/assets/ce35e55f-2397-49e2-8aa3-662511b3d289" />

-----

##  Reto 3: Girar y dibujar (La 'L' alineada)

El objetivo es simular un avance y un giro (`t.forward(100); t.right(90); t.forward(100)`), lo que requiere alinear el segmento vertical con el horizontal.

###  Código (Reto 3)

```python
# Reto 3: Simulación de la forma "L" con alineación

# 1. Movimiento Horizontal (5 pasos: 5 guiones + 1 >)
print("-----" + ">")

# El margen necesario para alinear la bajada es de 5 espacios (" " * 5)

# 2. Movimiento Vertical (3 pasos hacia abajo, alineados con el margen)
print("     " + "|")
print("     " + "|")
print("     " + "|")

# Dibuja la punta de flecha 'V' alineada
print("     " + "V")

# Simula la pausa
input("Patrón en 'L' dibujado. Presiona Enter.")
```

###  Explicación (Reto 3)

* **Trazo Horizontal**: Se usa `print("-----" + ">")`. El truco de multiplicar la cadena (`"-" * 5`) se usa manualmente (escribiendo 5 guiones) para dibujar la línea base.
* **Alineación Vertical**: Para alinear la línea vertical, se utiliza la **multiplicación de la cadena de espacio** (`" " * 5`) antes del símbolo vertical (`|`). La cantidad de espacios es **igual a la longitud** del trazo horizontal (5).
* **Repetición Manual**: Como no podemos usar bucles, la instrucción `print("     " + "|")` debe repetirse **manualmente 3 veces** para simular los 3 pasos verticales.

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

# --- DEFINICIÓN DE FUNCIONES ---
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
# --- FIN DEFINICIÓN DE FUNCIONES ---

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

### 1. `def adelante(n):` (Movimiento Horizontal)

Esta función se encarga de dibujar el peldaño del escalón y de actualizar la "memoria" horizontal para el siguiente movimiento.

* **Dibujo (`print`)**: 
    * `print(" " * posicion_h + "-" * n + ">")`
    * Usa **`" " * posicion_h`** para crear un margen de espacios que **alinea** el nuevo trazo justo donde terminó el anterior.
    * Dibuja el trazo (`"-" * n`) y la punta de flecha (`>`).
* **Actualización de Memoria**: 
    * `posicion_h += n + 1`
    * La posición se actualiza sumando la longitud del trazo (`n`) más el carácter de la punta (`+ 1`). Esto prepara `posicion_h` para el inicio del siguiente segmento.

---

### 2. `def abajo(n):` (Movimiento Vertical)

Esta función dibuja la altura del escalón, alineándola con precisión, y luego ajusta la "memoria" para el siguiente peldaño.

* **Cálculo del Margen**: 
    * `margen_vertical = posicion_h - 1`
    * El margen se calcula restando **`- 1`** a la posición actual. Esto es esencial para que la línea vertical comience exactamente debajo de la punta (`>`) del trazo horizontal anterior.
* **Dibujo Vertical**:
    * Usa un bucle (`for _ in range(n)`) para dibujar **`n`** líneas verticales (`|`).
    * Cada línea se imprime con el margen calculado: `print(" " * margen_vertical + "|")`.
    * Dibuja la punta `V` final alineada.
* **Conservación de Memoria (Clave)**: 
    * `posicion_h = margen_vertical`
    * La posición horizontal se establece en el margen (`posicion_h - 1`). Esto asegura que el próximo llamado a `adelante(n)` comience el nuevo peldaño justo en la base de la pared vertical, cerrando la forma del escalón correctamente.

### Resultado
<img width="300" height="216" alt="image" src="https://github.com/user-attachments/assets/fc6759ca-20e2-492b-b16d-96e7d4424158" />

-----
