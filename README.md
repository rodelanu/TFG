# Trabajo de Fin de Grado - Computación Cuántica

# Implementación de reglas metamórficas para distintos algoritmos cuánticos

Realizado por:
- Rodrigo de la Nuez Moraleda
- Sinhué García Gil

< explicación del concepto de reglas metamórficas >

- Suma Modular.
  * R0: x (+m) 0 = x
  * RS: x (+m) s(y) = s(x (+m) y), donde s es el sucesor modular.

<br>

# Algoritmo de Deutsch-Jozsa 

`Deutsch_Jozsa_Rules.ipynb`
- Deutsch-Josza (DJ). El programa P toma un oráculo para una función f: {0,1}^n -> {0,1} que es constante (P -> 1) o bien es equilibrada (P -> 0).
  * Sean g un automorfismo de {0,1}^n y f una función como la del enunciado, se cumple que P(f) = P(f(g)).
  * Dada f: {0,1}^n -> {0,1} una función constante o equilibrada, siempre se verifica que P(f) = P(1 - f).
  * Sean f una función f como la del enunciado y f' otra función que resulta de mantener fijos la mitad de 0's e intercambiar la otra mitad de 0's por 1's.
    De forma análoga, f' no afecta a la mitad de valores x para los que f(x) = 1 y para el resto de esos valores se tiene f'(x) = 0.
    Al considerar esta nueva función, resultado de perturbar exactamente la mitad de asignaciones de f, se tiene que P(f') = 1 para cualquier f escogida.

<br>

# Algoritmo de Bernstein-Vazirani

`Bernstein_Vazirani_Rules.ipynb`
- Bernstein-Vazirani (BV). Dada una función f_s = s*x (mod 2), el programa P nos devolverá el valor de la cadena de bits s.
  * Si t es la cadena resultante de aplicar X (0 -> 1, 1 -> 0) bit a bit en s, entonces P(f_(s+t)) = |1...1⟩.
  * P(f_(s+t)) = P(f_s) + P(f_t).
  * P(f_(s*t)) = P(f_s) * P(f_t).

<br>

# Algoritmo de Simon

`Simon_Rules.ipynb`
- Al efectuar la suma bit a bit sobre el estado cuántico que comprende todos los
posibles resultados del programa P, se obtiene de nuevo el conjunto inicial de soluciones S.
- Aplicar la implementación del algoritmo con cierta cadena de bits b e invertir las
cadenas de bits resultantes, equivale a aplicar el programa asociado a la cadena b invertida.
