
<br>

# Trabajo de Fin de Grado - Computación Cuántica

Realizado por:
- Rodrigo de la Nuez Moraleda
- Sinhué García Gil
<br>

# Implementación de reglas metamórficas para comprobar la corrección de algoritmos cuánticos

**Def:** Sea f una función objetivo o algoritmo. Se considera que R es una ***regla metamórfica*** si es una relación entre una secuencia de entrada y su salida, que se puede deducir de forma lógica desde el algoritmo. Es decir, es una propiedad necesaria de f.

Desde esta definición de relación (regla) metamórfica, podemos definir lo que se considera como testing metamórfico.

**Def:** Dada f un algoritmo, P la implementación de f y R una regla metamórfica para una secuencia <x<sub>1</sub>, x<sub>2</sub>, ..., x<sub>n</sub>>. Para realizar ***testing metamórfico*** sobre P, seguiremos los siguiente pasos:
  * Creamos R', sustituyendo la f por su implementación P.
  * Seguimos construyendo R' con la secuencia de test que hemos elegido <x<sub>n+1</sub>,...,x<sub>k</sub>> -> <P(x<sub>n+1</sub>), ..., P(x<sub>k</sub>)>
  * Comprobamos los resultados, si alguno no se cumpliera, R' no se satisface y por lo tanto consideraríamos que P no es correcto.

Ejemplo de reglas metamórficas:
> Suma Modular:
>  * R0: x (+m) 0 = x
>  * RS: x (+m) s(y) = s(x (+m) y), donde s es el sucesor modular.

Para la implementación de las reglas que hemos obtenido, seguiremos el mismo esquema:
  * Implementaremos el algoritmo P
  * Probaremos para unos valores de test
  * Comprobaremos los resultados

Esta comprobación se realizará manualmente o con ayuda de puertas añadidas tras el algoritmo. Si bien es cierto, que debido a intentar usar el menor número de qubits posibles para se probados en ordenadores cuánticos reales, la comprobación de los ejemplos propuestos a continuación se hará de forma manual (visual)? (Obs: Ya que realmente comprobamos nosotros que da lo debe dar, no sé si habría otra forma mejor de ponerlo, lo dejo así por ahora).

<br>

## Algoritmo de Deutsch-Jozsa 

[1. Deutsch Jozsa Rules](1_Deutsch_Jozsa_Rules.ipynb)
- Deutsch-Josza (DJ). El programa P toma un oráculo para una función f: {0,1}<sup>n</sup> -> {0,1} que es constante (P -> 1) o bien es equilibrada (P -> 0).
  * Sean g un automorfismo de {0,1}<sup>n</sup> y f una función como la del enunciado, se cumple que P(f) = P(f(g)).
  * Dada f: {0,1}<sup>n</sup> -> {0,1} una función constante o equilibrada, siempre se verifica que P(f) = P(1 - f).
  * Sean f una función f como la del enunciado y f' otra función que resulta de mantener fijos la mitad de 0's e intercambiar la otra mitad de 0's por 1's.
    De forma análoga, f' no afecta a la mitad de valores x para los que f(x) = 1 y para el resto de esos valores se tiene f'(x) = 0.
    Al considerar esta nueva función, resultado de perturbar exactamente la mitad de asignaciones de f, se tiene que P(f') = 1 para cualquier f escogida.

<br>

## Algoritmo de Bernstein-Vazirani

[2. Bernstein Vazirani Rules](2_Bernstein_Vazirani_Rules.ipynb)
- Bernstein-Vazirani (BV). Dada una función f<sub>s</sub> = s*x (mod 2), el programa P nos devolverá el valor de la cadena de bits s.
  * Si t es la cadena resultante de aplicar X (0 -> 1, 1 -> 0) bit a bit en s, entonces P(f<sub>s+t</sub>) = |1...1⟩.
  * P(f<sub>s+t</sub>) = P(f<sub>s</sub>) + P(f<sub>t</sub>).
  * P(f<sub>s*t</sub>) = P(f<sub>s</sub>) * P(f<sub>t</sub>).

<br>

## Algoritmo de Simon

[3. Simon Rules](3_Simon_Rules.ipynb)
- Al efectuar la suma bit a bit sobre el estado cuántico que comprende todos los
posibles resultados del programa P, se obtiene de nuevo el conjunto inicial de soluciones S.
- Aplicar la implementación del algoritmo con cierta cadena de bits b e invertir las
cadenas de bits resultantes, equivale a aplicar el programa asociado a la cadena b invertida.
