
<br>

# Trabajo de Fin de Grado - Computación Cuántica

Repositorio común realizado por:
- Rodrigo de la Nuez Moraleda
- Sinhué García Gil

<br>

Se ha utilizado la librería `qiskit` para la creación del siguiente código de programación cuántica:
* `1_Deutsch_Jozsa_Rules.ipynb` &rarr; Algoritmo de Deutsch-Jozsa y sus reglas metamórficas
* `2_Bernstein_Vazirani_Rules.ipynb` &rarr; Algoritmo de Bernstein-Vazirani y sus reglas metamórficas
* `3_Simon_Rules.ipynb` &rarr; Algoritmo de Simon y sus reglas metamórficas

<br>

# Implementación de reglas metamórficas para comprobar la corrección de algoritmos cuánticos

**Definición.** Sea *f* una función objetivo o algoritmo, diremos que *R* es una ***regla metamórfica*** si es una relación entre varios valores de entrada y/o salida, y que se puede deducir de forma lógica a partir del procedimiento del algoritmo. Esto quiere decir que *R* siempre será una propiedad necesaria de la función *f*.

<br>

**Definición.** Sea *f* la función que se desea computar, *P* la implementación de *f* y *R* una regla metamórfica para una secuencia (*x*<sub>1</sub>,*x*<sub>2</sub>, ... ,*x*<sub>*n*</sub>). Para realizar pruebas de ***testing metamórfico*** sobre *P*, se procederá como sigue:
  * Partiendo de la regla *R* se crea *R'*, sustituyendo en *R* la función *f* por su implementación *P*.
  * Consideramos una secuencia de test a elección (*x*<sub>1</sub>, ... ,*x*<sub>*n*</sub>) &rarr; (*P*(*x*<sub>1</sub>), ... ,*P*(*x*<sub>*n*</sub>)).
  * Si *R'* no se satisface con los valores obtenidos, se concluye que *P* no es una implementación correcta de *f*.

<br>

A continuación, se presentan varias reglas metamórficas para la suma módulo *m*, con *m* cierto entero positivo.
>  * *R*<sub>0</sub> :=  *x* +<sub>*m*</sub> 0 = *x*
>  * *R*<sub>*s*</sub> :=  *x* +<sub>m</sub> *s*(*y*) = *s*(*x* +<sub>*m*</sub> *y*), donde *s* denota el sucesor modular.

<br>

Para la implementación de las reglas que hemos definido, seguiremos el mismo esquema:
  * Se crea un programa *P* con el objetivo de computar el algoritmo cuántico correspondiente.
  * Consideramos ciertos valores de prueba y ejecutamos el circuito creado para la implementación *P*.
  * Comprobamos que la regla metamórfica definida se verifica para los valores de entrada seleccionados.


<br>

## Algoritmo de Deutsch-Jozsa 

[1. Deutsch-Jozsa Rules](1_Deutsch_Jozsa_Rules.ipynb)

El algoritmo de Deutsch-Jozsa busca clasificar una función de caja negra *f* : {0,1}<sup>n</sup> &rarr; {0,1} según si es constante o equilibrada (cuando para la mitad de valores de entrada *f* devuelva 0 y 1 para la otra mitad). 

Este algoritmo devolverá la cadena de bits nula 0...0 si y sólo si *f* es constante (suponiendo que cumpla las condiciones del enunciado: si no es constante es equilibrada). De esta forma, puede entenderse el resultado del algoritmo como un valor binario (por ejemplo, tomando el máximo valor de la cadena de bits medida).

Si *P* es el programa que implementa el algoritmo de Deutsch-Jozsa interpretamos que si *f* es constante (*P* &rarr; 0) y si es equilibrada (*P* &rarr; 1), entonces se tienen las siguientes reglas metamórficas:

  * Sean *g* un automorfismo de {0,1}<sup>n</sup> y *f* una función como la del enunciado, se cumple que *P(f) = P(f o g)*.
  * Dada *f* : {0,1}<sup>n</sup> &rarr; {0,1} una función constante o equilibrada, siempre se verifica que *P(f) = P(1 - f)*.

<br>

## Algoritmo de Bernstein-Vazirani

[2. Bernstein-Vazirani Rules](2_Bernstein_Vazirani_Rules.ipynb)

El algoritmo de Bernstein-Vazirani busca la obtención de una cadena de bits *s* que caracteriza una función de caja negra *f<sub>*s*</sub>(x)* = *s* * *x* (mod 2), donde (*) es el producto escalar. Sea *P* el programa que implementa este algoritmo y devuelve *s*, si (+<sub>*b*</sub>) denota la suma (módulo 2) bit a bit de dos cadenas, se tienen las siguientes reglas metamórficas:

  * Si *s'* es la cadena resultante de aplicar *X* (0  &rarr;  1, 1  &rarr;  0) bit a bit sobre *s*, entonces *P*(*f*<sub>*s +<sub>*b*</sub> s'*</sub>) = *P*(*f*<sub>*s*</sub>) +<sub>*b*</sub> *P*(*f*<sub>*s'*</sub>) = |1...1⟩.

  * El programa aplicado a la suma bit a bit de dos cadenas *s* y *s'* (de igual longitud) da el mismo resultado que al aplicar los programas asociados a *s* y *s'*, y hacer la suma bit a bit con los resultados: *P*(*f*<sub>*s +<sub>*b*</sub> s'*</sub>) = *P*(*f*<sub>*s*</sub>) +<sub>*b*</sub> *P*(*f*<sub>*s'*</sub>). Esta regla es una generalización de la primera y, por tanto, cualquier contraejemplo de la anterior servirá para esta.

  * Al aplicar en el algoritmo los oráculos de ambas funciones *f*<sub>*s*</sub> y *f*<sub>*s'*</sub> sucesivamente, se obtiene como resultado la suma bit a bit de las cadenas *s* y *s'*, esto es la cadena *s* +<sub>*b*</sub> *s'*. 

<br>

## Algoritmo de Simon

[3. Simon Rules](3_Simon_Rules.ipynb)

El algoritmo de Simon busca encontrar una cadena *b* que caracteriza una función *f* : {0,1}<sup>n</sup> &rarr; {0,1}<sup>n</sup> que es inyectiva o *dos a uno*, si para cada valor *y* del dominio imagen hay dos valores de entrada que evalúan a *y*, que siempre serán de la forma *x*, *x + b* (mod 2<sup>n</sup>), al considerar que ambas cadenas de bits se corresponden con valores de Z<sub>2<sup>n</sup></sub>. En el caso de que la función *f* sea inyectiva se tendrá que *b =* 0...0.

Este algoritmo encontrará todas las posibles cadenas *z* tales que *b* * *z* = 0 (mod 2), con las que se podrá hallar el valor de la cadena *b* a partir del sistema de ecuaciones asociado.

Dada una implementación correcta de este algoritmo se cumplirán las siguientes reglas metamórficas:

  * Al efectuar la suma bit a bit sobre el estado cuántico que comprende todos los posibles resultados *z* del programa consigo mismo, se obtiene de nuevo el conjunto inicial de soluciones (con las mismas probabilidades).
  
  * Aplicar la implementación del algoritmo con cierta cadena de bits *b* e invertir las soluciones obtenidas, tiene el mismo efecto que aplicar el programa asociado a la cadena *b* invertida.
