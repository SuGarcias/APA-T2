# Segunda tarea de APA 2023: Manejo de números primos

## ORIOL GARCIA VILA

## Fichero `primos.py`

- El alumno debe escribir el fichero `primos.py` que incorporará distintas funciones relacionadas con el manejo
  de los números primos.

- El fichero debe incluir una cadena de documentación que incluirá el nombre del alumno y los tests unitarios
  de las funciones incluidas.

- Cada función deberá incluir su propia cadena de documentación que indicará el cometido de la función, los
  argumentos de la misma y la salida proporcionada.

- Se valorará lo pythónico de la solución; en concreto, su claridad y sencillez, y el uso de los estándares marcados
  por PEP-8. También se valorará su eficiencia computacional.

### Determinación de la *primalidad* y descomposición de un número en factores primos

Incluya en el fichero `primos.py` las tres funciones siguientes:

- `esPrimo(numero)`   Devuelve `True` si su argumento es primo, y `False` si no lo es.
- `primos(numero)`    Devuelve una **tupla** con todos los números primos menores que su argumento.
- `descompon(numero)` Devuelve una **tupla** con la descomposición en factores primos de su argumento.

### Obtención del mínimo común múltiplo y el máximo común divisor

Usando las tres funciones del apartado anterior (y cualquier otra que considere conveniente añadir), escriba otras
dos que calculen el máximo común divisor y el mínimo común múltiplo de sus argumentos:

- `mcm(numero1, numero2)`:  Devuelve el mínimo común múltiplo de sus argumentos.
- `mcd(numero1, numero2)`:  Devuelve el máximo común divisor de sus argumentos.

Estas dos funciones deben cumplir las condiciones siguientes:

- Aunque se trate de una solución sub-óptima, en ambos casos deberá partirse de la descomposición en factores
  primos de los argumentos usando las funciones del apartado anterior.

- Aunque también sea sub-óptimo desde el punto de vista de la programación, ninguna de las dos funciones puede
  depender de la otra; cada una debe programarse por separado.

### Obtención del mínimo común múltiplo y el máximo común divisor para un número arbitrario de argumentos

Escriba las funciones `mcmN()` y `mcdN()`, que calculan el mínimo común múltiplo y el máximo común divisor para un
número arbitrario de argumentos:

- `mcmN(*numeros)`:  Devuelve el mínimo común múltiplo de sus argumentos.
- `mcdN(*numeros)`:  Devuelve el máximo común divisor de sus argumentos.

### Tests unitarios

La cadena de documentación del fichero debe incluir los tests unitarios de las cinco funciones. En concreto, deberán
comprobarse las siguientes condiciones:

- `esPrimo(numero)`:  Al ejecutar `[ numero for numero in range(2, 50) if esPrimo(numero) ]`, la salida debe ser
                      `[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47]`.
- `primos(numeor)`: Al ejecutar `primos(50)`, la salida debe ser `(2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47)`.
- `descompon(numero)`: Al ejecutar `descompon(36 * 175 * 143)`, la salida debe ser `(2, 2, 3, 3, 5, 5, 7, 11, 13)`.
- `mcm(num1, num2)`: Al ejecutar `mcm(90, 14)`, la salida debe ser `630`.
- `mcd(num1, num2)`: Al ejecutar `mcd(924, 780)`, la salida debe ser `12`.
- `mcmN(numeros)`: Al ejecutar `mcm(42, 60, 70, 63)`, la salida debe ser `1260`.
- `mcdN(numeros)`: Al ejecutar `mcd(840, 630, 1050, 1470)`, la salida debe ser `210`.

### Entrega

#### Ejecución de los tests unitarios

Inserte a continuación una captura de pantalla que muestre el resultado de ejecutar el fichero `primos.py` con la opción
*verbosa*, de manera que se muestre el resultado de la ejecución de los tests unitarios.

#### Código desarrollado

Inserte a continuación el contenido del fichero `primos.py` usando los comandos necesarios para que se realice el
realce sintáctico en Python del mismo.

#### Subida del resultado al repositorio GitHub ¿y *pull-request*?

El fichero `primos.py`, la imagen con la ejecución de los tests unitarios y este mismo fichero, `README.md`, deberán
subirse al repositorio GitHub mediante la orden `git push`. Si los profesores de la asignatura consiguen montar el
sistema a tiempo, la entrega se formalizará realizando un *pull-request* al propietario del repositorio original.

El fichero `README.md` deberá respetar las reglas de los ficheros Markdown y visualizarse correctamente en el repositorio,
incluyendo la imagen con la ejecución de los tests unitarios y el realce sintáctico del código fuente insertado.

## TESTS UNITARIOS:
<image src="/tests_unitarios.png" alt="Tests unitarios">

## CÓDIGO primos.py
```python
import doctest

#DEFINICIÓN de Número Primo:
#Número entero que solamente es divisible por él mismo y por la unidad (1)
#############################################################################
def esPrimo (numero):
    """
    Devuelve True si su argumento es primo, y False si no lo es
    >>> [ numero for numero in range(2, 50) if esPrimo(numero) ]
    [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47]
    """
    if numero < 2: 
        return False
    else:
        for aux in range(2,numero):
            if numero % aux == 0:
                return False
        return True

#############################################################################
def primos(numero):
    """
    Devuelve una tupla con todos los números primos menores que su argumento.
    >>> primos(50)
    (2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47)
    """
    tupla_primos = tuple([item for item in range(numero) if esPrimo(item)])
    return tupla_primos

#############################################################################
def descompon(numero):
    """
    Devuelve una tupla con la descomposición en factores primos de su argumento.
    >>> descompon(36 * 175 * 143)
    (2, 2, 3, 3, 5, 5, 7, 11, 13)
    """
    # He intentado hacerlo usando en vez de range(2,numero+1), 
    # la tupla con los primos hasta numero primos(numero),
    # pero me ocupaba mucho tiempo de cálculo y nunca me llegaba a terminar.
 
    factors = []
    for i in range(2,numero+1):
        while numero % i == 0:
            factors.append(i)
            numero //= i
        if numero < 2:
            break
    return tuple(factors)


#############################################################################
    #mcd con algoritmo de euclides.
    #No lo he usado para la entrega, pero lo hice antes de saber que tenian que usar-se
    #las funciones creadas y pues no lo iba a borrar. Lo he usado para comparar resultados.
def mcd_eucleides(numero1, numero2):  
    if numero1*numero2 == 0: 
        return 0
    elif int(numero1)!= numero1 or int(numero2)!= numero2:
        print("No se admiten valores NO enteros")
    elif (numero1 or numero2) < 0  :
        return 1
    else:
        while numero1 != numero2:
            if numero1 > numero2:
                numero1 -= numero2
            else:
                numero2-=numero1
        return numero1

#############################################################################
    #Función que devuelve una lista de listas con cada sublista una pareja de:
        #Valor, nº de veces que aparece en la lista pasada por parametros
        #La hice porque he intentado hacer las funciones mcm y mcd sin diccionarios (para hacerlo diferente que en clase)
        # y necesitaba de una función así.
def n_veces_lista (lista):
    cont =[]
    for i in set(lista):
            c= lista.count(i)
            cont.append([i,c])
    return cont

#############################################################################
    #Cómo he dicho anteriormente, he intentado hacer mcm y mcd 
    # de una forma alternativa al uso de los diccionarios, 
    # más que nada porqué intenté hacerlo antes de ser explicado en clase y no la iba a borrar
def mcm (numero1, numero2):
    """
    Devuelve el mínimo común múltiplo de sus argumentos.
    >>> mcm(90, 14)
    630
    """
    desc1 = descompon(numero1)
    desc2 = descompon(numero2)
    primos_cont1 = n_veces_lista(desc1)
    primos_cont2 = n_veces_lista(desc2)

    resultat = 1
    for i in range(0, len(primos_cont1)):

        if primos_cont1[i][0] not in set(desc2):
            resultat*= (primos_cont1[i][0]**primos_cont1[i][1])

        for y in range(0, len(primos_cont2)):

            if primos_cont1[i][0] == primos_cont2[y][0]:
                
                if primos_cont1[i][1] > primos_cont2[y][1]:
                    resultat *= (primos_cont1[i][0]**primos_cont1[i][1])
                else:
                    resultat *= (primos_cont1[y][0]**primos_cont1[y][1])
    
    for y in range(0,len(primos_cont2)):
        if primos_cont2[y][0] not in set(desc1):
            resultat *= (primos_cont2[y][0]**primos_cont2[y][1])
                
            
    return resultat

#############################################################################
    #En esta, le he introducido casos particulares para ahorrar recorrer listas de listas y hacer calculos o evitar errores
def mcd (numero1, numero2):
    """
    Devuelve el mínimo común múltiplo de sus argumentos.
    >>> mcd(924, 780)
    12
    """
    # Caso de que alguno de los dos valores sea 0:
    if numero1*numero2 == 0: 
        return 0 # mcd = 0
        
    
    #caso valores no enteros:
    elif int(numero1)!= numero1 or int(numero2)!= numero2: 
        print("No se admiten valores NO enteros")
        return 0
    
    #caso valores negativos:
    elif (numero1 or numero2) < 0 : 
        return 1
    
    #Otros casos:
    else:
        #listas con los primos repetidos en la descomposición del otro numero
        primos_aux =[item for item in descompon(numero1) if item in descompon(numero2)]
        primos_aux2 =[item for item in descompon(numero2) if item in descompon(numero1)]
        
        #lista de listas con valores [[n_primo, n_veces que aparece],[n_primo2, n_veces que aparece2],...]
        primos_cont1 = n_veces_lista(primos_aux)
        primos_cont2 = n_veces_lista(primos_aux2)

        resultat = 1
        for i in range(0, len(primos_cont1)):
            if primos_cont1[i][1] < primos_cont2[i][1]: 
                resultat *= (primos_cont1[i][0]**primos_cont1[i][1])
            else:
                resultat *= (primos_cont2[i][0]**primos_cont2[i][1])

        return resultat
#############################################################################
    #Al introducior una serie indefinida de elementos, ya he optado por hacer uso de los diccionarios,
    #ya que la sintaxis y el ahorro de tener que recorrer listas de listas y comparar valores me parecian más óptimos.

def mcmN (*numeros):
    """
    Devuelve el mínimo común múltiplo de sus argumentos.
    >>> mcmN(42, 60, 70, 63)
    1260
    """
    factor_dict = {}
    for num in numeros:
        for factor, count in n_veces_lista(descompon(num)):
            factor_dict[factor] = max(factor_dict.get(factor, 0), count)
    mcm = 1
    for factor, count in factor_dict.items():
        mcm *= factor ** count
    return mcm

#############################################################################
def mcdN (*numeros):
    """
    Devuelve el mínimo común múltiplo de sus argumentos.
    >>> mcdN(840, 630, 1050, 1470)
    210
    """
    factor_dict = {}
    for num in numeros:
        num_factor_dict = n_veces_lista(descompon(num))
        for factor, count in num_factor_dict:
            if factor not in factor_dict:
                factor_dict[factor] = [count]
            else:
                factor_dict[factor].append(count)
            #print(factor_dict)

    mcd = 1
    for factor, counts in factor_dict.items():
        if len(counts) == len(numeros):
            mcd *= factor ** min(counts)
    #print(factor_dict.items())
    return mcd

doctest.testmod()
```


