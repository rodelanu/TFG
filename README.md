
<br>

# Trabajo de Fin de Grado - Computación Cuántica

Repositorio común realizado por:
- Rodrigo de la Nuez Moraleda
- Sinhué García Gil
<br>

# Implementación de reglas metamórficas para comprobar la corrección de algoritmos cuánticos

**Definición.** Sea *f* una función objetivo o algoritmo, diremos que *R* es una ***regla metamórfica*** si es una relación entre una o varias secuencias de entrada y/o salida, y que se puede deducir de forma lógica a paritr del procedimiento el algoritmo. Esto quiere decir que *R* siempre será una propiedad necesaria de la función *f*.

**Definición.** Sea *f* la función que se desea computar, *P* la implementación de *f* y *R* una regla metamórfica para una secuencia <x<sub>1</sub>, x<sub>2</sub>, ..., x<sub>n</sub>>. Para realizar pruebas de ***testing metamórfico*** sobre *P*, se procederá como sigue:
  * Partiendo de la regla *R* se crea *R'*, sustituyendo en *R* la función *f* por su implementación *P*.
  * Consideramos una secuencia de test a elección <*x*<sub>*1*</sub>, ... , *x*<sub>*n*</sub>> &rarr; <*P*(*x*<sub>*1*</sub>), ... , *P*(*x*<sub>*n*</sub>)>
  * Si *R'* no se satisface con los valores obtenidos, se concluye que *P* no es una implementación válida de *f*.

A continuación, se presentan varias reglas metamórficas para la suma módulo *m*, con *m* cierto entero positivo.
>  * R0: x +<sub>m</sub> 0 = x
>  * RS: x +<sub>m</sub> s(y) = s(x <sub>m</sub> y), donde *s* denota el sucesor modular.

Para la implementación de las reglas que hemos obtenido, seguiremos el mismo esquema:
  * Se realiza una implementación *P* del algoritmo cuántico correspondiente.
  * Consideramos ciertos valores de prueba y ejecutamos el circuito creado para la implementación de *P*.
  * Comprobaremos que las reglas metamórficas definidas se comprueban para los valores de entrada seleccionados.

"""
Esta comprobación se realizará manualmente o con ayuda de puertas añadidas tras el algoritmo. Si bien es cierto, que debido a intentar usar el menor número de qubits posibles para se probados en ordenadores cuánticos reales, la comprobación de los ejemplos propuestos a continuación se hará de forma manual (visual)? (Obs: Ya que realmente comprobamos nosotros que da lo debe dar, no sé si habría otra forma mejor de ponerlo, lo dejo así por ahora).
"""

<br>

## Algoritmo de Deutsch-Jozsa 

[1. Deutsch-Jozsa Rules](1_Deutsch_Jozsa_Rules.ipynb)

El algoritmo de Deutsch-Jozsa busca clasificar una función desconocida *f* : {0,1}<sup>n</sup> &rarr; {0,1} según si es constante o equilibrada (cuando para la mitad de valores de entrada *f* devuelva 0 y 1 para la otra mitad). 

Este algoritmo devolverá la cadena de bits nula 0...0 si y sólo si *f* es constante.

Si *P* es el programa que implementa el algoritmo de Deutsch-Josza, de forma que si *f* es constante (*P* &rarr; 0) y si es equilibrada (*P* &rarr; 1), entonces se tienen las siguientes reglas metamórficas:

  * Sean *g* un automorfismo de {0,1}<sup>n</sup> y *f* una función como la del enunciado, se cumple que *P(f) = P(f o g)*.
  * Dada *f* : {0,1}<sup>n</sup> &rarr; {0,1} una función constante o equilibrada, siempre se verifica que *P(f) = P(1 - f)*.

<br>

## Algoritmo de Bernstein-Vazirani

[2. Bernstein-Vazirani Rules](2_Bernstein_Vazirani_Rules.ipynb)

Sea *P* el algortimo de Bernstein-Vazirani (BV). Dada una función f<sub>s</sub> = s*x (mod 2), P nos devolverá el valor de la cadena de bits s.

Reglas metamórficas que una implementación correcta del algoritmo de BV debería cumplir:
  * P(f<sub>s+t</sub>) = P(f<sub>s</sub>) + P(f<sub>t</sub>).
  * Si t es la cadena resultante de aplicar X (0 -> 1, 1 -> 0) bit a bit en s, entonces P(f<sub>s+t</sub>) = |1...1⟩. Este es un caso particular de la regla anterior, que aunque es más débil, cualquier contraejemplo de esta regla sirve para la primera.
  * Si aplicamos al algoritmo ambas funciones, f<sub>s</sub> y f<sub>s1</sub>, sucesivamente en estado de superposición, se obtiene como resultado s +<sub>b</sub> s1. 
  * P(f<sub>s*t</sub>) = P(f<sub>s</sub>) * P(f<sub>t</sub>).

<br>

## Algoritmo de Simon

[3. Simon Rules](3_Simon_Rules.ipynb)

El algoritmo de Simon busca encontrar una cadena *b* que caracteriza una función *f* : {0,1}<sup>n</sup> &rarr; {0,1} que es inyectiva o *dos a uno*, si para cada valor *y* del dominio imagen hay dos valores de entrada que evalúan a *y*, que siempre serán de la forma *x* y *x + b* (mod 2<sup>n</sup>), al considerar que ambas cadenas de bits se corresponden con valores de Z<sub>2<sup>n</sup></sub>. En el caso de que la función *f* sea inyectiva se tendrá que *b =* 0...0.

Este algoritmo encontrará las posibles cadenas *z* tales que *b***z* = 0 (mod 2), con las que se podrá hallar el valor de *b* mediante métodos de resolución de sistemas de ecuaciones lineales. 

Dada una implementación correcta de este algoritmo se tendrán las siguientes reglas metamórficas:

  * Al efectuar la suma bit a bit sobre el estado cuántico que comprende todos los posibles resultados *z* del programa, se obtiene de nuevo el conjunto inicial de soluciones.
  
  * Aplicar la implementación del algoritmo con cierta cadena de bits *b* e invertir las soluciones obtenidas, tiene el mismo efecto que aplicar el programa asociado a la cadena *b* invertida.
