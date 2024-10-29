# Estadistica en R

## Table of content
1. [Variable Aleatoria](#Variable-Aleatoria)
2. [Algunos conceptos](#Algunos-conceptos)
3. [Distribuciones Discretas](#Distribuciones-Discretas)
4. [Distribuciones Continuas](#Distribuciones-Continuas)
5. [Percentiles](#Percentiles)
6. [Quantiles](#Quantiles)
7. [Teorema del limite central](#Teorema-del-limite-central)

## Variable Aleatoria

Una **variable aleatoria** es un valor que depende de eventos aleatorios. Es una función que asigna un valor numérico a cada resultado posible de un experimento aleatorio.

Existen dos tipos principales de variables aleatorias:

+ **Variable aleatoria discreta**: Toma un número finito o contable de valores distintos. Ejemplo: el número de caras que obtienes al lanzar dos monedas.

+ **Variable aleatoria continua**: Puede tomar un número infinito de valores dentro de un intervalo. Ejemplo: la altura de una persona o el tiempo que tarda en completarse una tarea.

## Algunos conceptos

### Cumulative Distribution Function

LA CDF de una distribución da la probabilidad acumulada de que la variable aleatoria X tome un valor menor o igual a un cierto valor x: 

+ F(x)= P(X<=x) = P(X<=x) = sum(k=0,x)P(X=k) **caso discreto**
+ F(x) = integral(-inf, x) f(x) **caso continuo**

> Gráficamente, la CDF de una distribución continua suele tener una forma de "S" o sigmoide, mientras que para distribuciones discretas, es una función escalonada.

+ Monotona no decreciente
+ Continua por la izquierda
+ F(-inf) = 0
+ F(+inf) = 1

> Que sea continua por la izquierda significa que en cualquier punto x, el valor de la CDF F(x) es igual al límite de la función cuando nos acercamos a x desde valores menores.

### Probability Mass Function

El PMF es una manera de describir las probabilidades asociadas con una variable aleatoria discreta. Asigna una probabilidad a cada valor posible que puede asumir la variable aleatoria. 

f(x) = P(X=x) => Proporciona la probabilidad de que X tome un valor específico x.

+ La P de un valor x especifico siempre es mayor que 0
+ La suma de las probabilidades de todos los posibles valores de x es igual a 1

### Probability Density function

El PDF es una función que describe la probabilidad relativa de que una variable aleatoria continua tome un valor específico. A diferencia de las variables aleatorias discretas, donde se utilizan probabilidades exactas, en el caso de las continuas, se trabaja con densidades.

f(x) = P(a<=x<=b) = integral(a,b)f(x)

+ Para cada valor de x en el dominio f(x)>=0
+ La integral total en todo su dominio debe ser igual a 1

> El valor del PDF en un punto x no representa la probabilidad de que la variable tome ese valor exacto (ya que la probabilidad de que tome un valor exacto es 0 en una distribución continua), sino la densidad de probabilidad en ese punto. Es decir, indica cuán probable es que la variable aleatoria se encuentre cerca de x.

### Propiedad de Memorylesseness

Es una característica específica de ciertas distribuciones de probabilidad como la distribución **exponencial** y la distribución **geométrica**.

Esto significa que la probabilidad de que el evento ocurra después de un tiempo 
s+t, dado que ya ha pasado un tiempo 
s, es igual a la probabilidad de que el evento ocurra después de un tiempo 
t. 
En otras palabras, el tiempo que ya ha pasado no proporciona ninguna información sobre el tiempo que queda hasta que ocurra el evento.

Si se conoce que han sucedido m eventos, la propabilidad de que ocurra m+x solo depende de x y no se ve afectada por m.

> En el caso de la **distribución exponencial**, que a menudo se utiliza para modelar el tiempo entre eventos en un proceso de Poisson, si el tiempo de espera hasta el próximo evento sigue una distribución exponencial con parámetro λ, la propiedad de memorylessness se puede entender de la siguiente manera:
>
> Si has esperado ya 5 minutos, la probabilidad de que tengas que esperar más de otros 3 minutos es la misma que si no hubieras esperado nada en absoluto.

> En la distribución geométrica, que modela el número de ensayos hasta el primer éxito en una serie de ensayos de Bernoulli (por ejemplo, lanzar una moneda hasta obtener cara), también se aplica la propiedad de memorylessness:
>
> Si ya has lanzado la moneda 4 veces sin éxito, la probabilidad de que necesites 3 lanzamientos adicionales para obtener el primer éxito es la misma que si comenzaras a lanzar la moneda desde cero.

### Valor esperado E(X)

Es una medida de tendencia central que representa el valor promedio de una variable aleatoria.

Es una forma de cuantificar el "centro" de la distribución.

**Caso discreto**: E(x) = sum(i) xi*P(X=xi)

**Caso continuo**: E(x) = integral(-inf,inf) x * f(x)

Propiedades:
+ E(c) = c
+ Si x >= 0 entonces E(x) >= 0
+ x<=y  E(x)<=E(y)
+ a<=x<=b  b<=E(x)<=b
+ Si X y Y son independientes E(XY)= E(X)*E(Y)
+ E(X+Y) = E(X) + E(Y)
+ E(cX) = c*E(X)
+ **Linealidad**: E(a+bX) = a + b*E(x)  la media de una combinación lineal de variables aleatorias se puede calcular directamente a partir de las medias individuales.
+ **Interpretación**: La media puede interpretarse como el "punto de equilibrio" de la distribución, donde si se distribuyeran pesos en torno a la media, el sistema estaría equilibrado.

### Varianza V(X)
Es una medida que indica la dispersión o variabilidad de los valores de una variable aleatoria en torno a su media.

V(X) = E(\[X - EX]^2) = EX^2 - E^2X

**Caso discreto**: V(X) = sum(Rx)(x - EX)^2 * P(X=x)

**Caso continuo**: V(X) = integral(Rx)(x - EX)^2 * f(x)

Propiedades:
+ **No negatividad**: es una suma de cuadrados, nunca puede ser negativa
+ V(c) = 0
+ V(a+bX) = b^2 * V(X)
+ Si X y Y son independientes entonces V(X+Y) = V(X) + V(Y)
+ Si X y Y no son independientes entonces V(X+Y) = V(X) + V(Y) + 2Cov(X,Y)
+ La desviacion estandar es la raiz cuadrada de la varianza

### Mediana
La mediana es una medida de tendencia central que representa el valor que divide un conjunto de datos ordenado en dos partes iguales. Es decir, es el punto medio de un conjunto de datos, donde el 50% de los valores son menores o iguales a la mediana, y el 50% son mayores o iguales a ella.

Para calcular la mediana, es necesario primero ordenar los datos de menor a mayor.

En una distribución simétrica, como la distribución normal, la mediana coincide con la media (el valor central).

### Estimador
Es una función o regla matemática que se utiliza para inferir o aproximar un parámetro desconocido de una población, utilizando datos muestrales.

Estimadores comunes:
+ Media muestral: X_
+ Varianza muestral: S^2
+ Proporcion muestral: p^

Propiedades:
+ **Sesgado**: Un estimador es insesgado si su valor esperado es igual al parámetro poblacional que está estimando: E(P^)=P
+ **Consistencia**: Un estimador es consistente si, a medida que el tamaño de la muestra aumenta, el estimador converge al valor verdadero del parámetro poblacional.
+ **Eficiencia**: Un estimador es eficiente si tiene la varianza más baja posible entre todos los estimadores insesgados.
+ **Suficiencia**: Un estimador es suficiente si captura toda la información relevante de la muestra acerca del parámetro.

> Un estimador es una regla o fórmula que se aplica a cualquier muestra para obtener una estimación del parámetro.
>
> Una estimación es el valor numérico que se obtiene al aplicar el estimador a una muestra específica.

## Distribuciones Discretas

Distribución de probabilidad que describe el comportamiento de una variable aleatoria discreta.

Algunas caracteristicas son:
+ **Valores discretos**
+ **Probabilidad acumulada**: Para cada valor de xi hay una probabilidad P(X = xi). La suma de todas las probabilidades de todas las xi es igual a 1.
+ **Funcion de probabilidad**: Funcion de masa de probabilidad, que asigna una probabilidad a cada valor de xi.

### Bernoulli(p)
+ Evento simple que puede ser exito o fallo
+ P(X=x) = p^x(1-p)^1-x
+ X {0,1} **Exito (p) o Fallo (p-1)**
+ PMF { q = 1-p  x=0; p  x=1}
+ CDF {0  x<0; 1-p 0<x<1; 1 x>1}
+ Mean: p
+ Estimador: p^ = x_
+ E(x) = p
+ V(x) = p(1-p)

### Binomial(n,p)
+ Experimento Bernoulli repetido n veces.
+ P(X=x) = C(n,x) p^x(1-p)^n-x
+ X {0,1...n} **Cuantas veces ocurre el exito en n experimentos?**
+ PMF {Cnx p^x*q^n-x}
+ CDF {Iq(n-x,1+x)}
+ Mean: np
+ Estimador: p^ = x/n (x-> el numero de exitos)
+ E(x) = np
+ V(x) = npq

### Poisson(lambda{0,inf+})
+ Eventos raros que se presentan con poca frecuencia
+ P(X=x) = e^-lambda(lambda^x/fact(x)); lambda = n(#experimentos)*p(probabilidad)
+ P(X=x) = e^-lambda(lambda^x/fact(x)); lambda = lambda * t
+ X {N} **Cuantas veces ocurre un evento en un intervalo determinado de tiempo**
+ lambda **intensidad por unidad de tiempo**
+ PMF {P(X=x) = (lambda^x * e^-lambda)/fact(x)}
+ CDF {P(X<=x) = sum(k=0,x)P(X=k)}
+ Mean: lambda
+ Estimador: lambda^ = 1/n * sum(i=1,n)xi
+ E(x) = lambda
+ V(x) = lambda

Para que un fenómeno sea modelado por una distribución de Poisson, debe cumplir con los siguientes requisitos:
+ **Los eventos son independientes**: La ocurrencia de un evento no afecta la probabilidad de que ocurra otro evento.
+ **La tasa promedio de ocurrencia es constante**: El número promedio de eventos que ocurren en un intervalo es constante, y esta tasa es denotada por lambda.
+ **Los eventos ocurren de manera aleatoria**: No hay patrones que afecten la probabilidad de que ocurra un evento.

### Geometrica (p)
+ Cuantas veces se repite el experimento bernoulli antes de optener el primer exito
+ P(X=x) = (1-p)^x-1*p (cantidad de veces a repetir el experimento antes de obtener el primer exito)
+ P(Y=y) = (1-p)^y * p (cantidad de fallos antes del primer exito)
+ X {0,1,2,3...} **cantidad de fallos antes del primer exito**
+ PMF {}
+ CDF {1-(1-p)^k  k>=1; 0  k<1}
+ Mean: 1/p (x) 1-p/p (y)
+ Estimador: P^= n / sum(i=1,n)xi
+ E(x) = 1/p
+ V(x) = (1-p)/p^2

### Binomial negativa
+ Generaliza la distribución geométrica y modela el número de ensayos necesarios para obtener k éxitos.
+ P(X=x) = C(x-1,r-1)(1-p)^x-r*p^r (cantidad de veces a repetir el experimento para obtener r exitos) X{r...inf+}
+ P(Y=y) = C(m+r-1,r-1)(1-p)^m * p^r (cantidad de fallos antes de obtener el r-esimo exito) X{0...inf+}
+ PMF {}
+ CDF {}
+ Mean: r(1-p)/p
+ Estimador: p^ = r/r+k (sesgado) p^ = r+k/r (insesgado)
+ E(x) = rp/(1-p)
+ V(x) = r(1-p)/p^2

### Hipergeometrica
+ Modela el número de éxitos en una muestra sin reemplazo de una población finita.
+ Parámetros: N (tamaño de la población), k (número de éxitos en la población), y n (tamaño de la muestra).

### Uniforme
+ Todos los resultados posibles tienen la misma probabilidad.
+ P(X=x) = 1/n
+ X{a...b}
+ PMF {}
+ CDF {P(X<=x) = x-a+1/n  a<=x<=b}
+ Mean: a+b/2
+ Estimador: n = b-a+1
+ E(x) = a+b/2
+ V(x) = (b-a+1)^2 -1/ 12

## Distribuciones Continuas
Distribución de probabilidad que describe el comportamiento de una variable aleatoria continua.

Caracteristicas:
+ **Intervalos de Valores**: número infinito de valores en un rango específico.
+ **Función de Densidad de Probabilidad (PDF)**: En lugar de tener una PMF, utilizan una PDF que describe la probabilidad de que la variable aleatoria tome un valor en un intervalo específico. La probabilidad de que una variable continua tome un valor exacto es siempre cero; en cambio, se considera la probabilidad de que caiga dentro de un rango.
+ **Integración**: Para encontrar la probabilidad de que una variable aleatoria continua caiga dentro de un intervalo, se calcula el área bajo la curva de la PDF en ese intervalo. Esto se realiza mediante la integración de la PDF en los límites del intervalo.
+ **CDF**: la probabilidad de que la variable aleatoria sea menor o igual a un cierto valor. Se calcula integrando la PDF desde el límite inferior hasta el valor específico.

### Exponencial(lambda)
+ Caracteriza el tiempo transcurrido entre eventos raros (poisson)
+ PDF {f(x)=lambda * e^  -(lambda*x)  x>=0} lambda->tasa de eventos
+ CDF {F(x)= 1-e^-lambda*x  x>=0}
+ X: tiempo transcurrido entre eventos
+ Mean: 1/lambda
+ Estimador: lambda^ = 1/x_ (sesgado) lambda^ = n-2/sum(i) xi
+ E(x) = 1/lambda
+ V(x) = 1/lambda^2
+ MemoryLessenses: Pr(T>t) = e^-lambda*t

### Gamma(lambda(intensidad),alpha(#de tareas))
+ dado un proceso se tiene que ejecutar el evento de interes en bloques, el resultado se obtiene despues de haber ejecutado todos los bloques
+ X: todos los tiempos que demoraron todos los bloques en ejecutarse

### Normal o Gaussiana(Miù(media),Rò^2(desviacion estandar al cuadrado: varianza))
+ X{inf-,inf+} 
+ PDF {}
+ CDF {}
+ Mean: miù
+ Estimador: m^= x_ = 1/n * sum(i=1,n)xi  r^2^= 1/n * sum(i=1,n)(xi-x_)^2 
+ E(x) = miù
+ V(x) = rò^2

### T-student(n(grados de libertad))
+ Cuando X sigue una distribucion normal pero n es pequena y la desviacion estandar es desconocida
+ X{inf-,inf+}
+ PDF {}
+ CDF {}
+ Mean: 0 n>0
+ Estimador: 
+ E(x) = 0 n>0
+ V(x) = n/n-2  n>2

### X^2(k(grados de libertad))
+ Surge cuando la variables e puede representar como una suma de variables estandarizadas independientes al cuadrado
+ X: suma de las variables independientes estandarizadas
+ PDF {}
+ CDF {} 
+ Mean: k
+ Estimador: 
+ E(x) = k
+ V(x) = 2k

### F de Fisher(k(grados de libertad del numerador),p(del denumerador))
+ Surge cuando la variable aleatoria es el cociente de dos variables aleatorias que siguen una distribucion X^2
+ PDF {}
+ CDF {} 
+ Mean: 
+ Estimador: 
+ E(x) = 
+ V(x) = 


## Percentiles

Los percentiles son valores que dividen un conjunto de datos en cien partes iguales, permitiéndote ver en qué posición relativa está un dato dentro de esa distribución. En otras palabras, el percentil indica el valor bajo el cual se encuentra un cierto porcentaje de observaciones.

+ **Percentil 25 (P25)**: representa el valor por debajo del cual se encuentra el 25% de los datos. También es el primer cuartil.
+ **Percentil 50 (P50)**: marca el valor por debajo del cual está el 50% de los datos y coincide con la mediana.
+ **Percentil 75 (P75)**: indica el valor debajo del cual está el 75% de los datos, y se conoce como el tercer cuartil.

Los percentiles se utilizan para interpretar mejor la posición de un valor en una muestra, como decir que "tu puntaje en el examen está en el percentil 90", lo que indica que superaste al 90% de las personas que tomaron ese examen.

**Propiedades**: 
+ P( Z < a ) = 0.5 (percentil 50)
+ P( Z < a ) = 0.9 (percentil 90)
+ P( Z < a) = 0.025 (percentil 2.5)
+ P( Z < a) = 0.975 (percentil 97.5)
  
+ Z(0.975 -> valor del percentil) = 1.96 -> valor de la a

Para Z -> N(0,1):
+ P(Z>a) = 1-P(Z<=a)
+ P(Z<-a) = P(Z<a)
+ P(Z<0) = 0,5

**Calcular el percentil**:

+ Datos Ordenados: 5,10,15,20,25,30,35,40,45,50
+ Formula: Pk = (k/100)*(n+1)  k:percentil  n:cantidad de datos
+ P25 = 25/100 * 10+1 = 0.25*11 = 2,75  (El percentil 25 se encuentra entre el 2 y el 3 valor)
+ Iterpolar para encontrar el valor exacto: El segundo valor es 10 y el tercero es 15. Al estar en el 2.75, tomamos un 75% del camino entre 10 y 15: P25 = 10 + (0.75 * (15-10)) = 10 + 3.75 = 13.75
+ Resultado: el percentil 25 (P25) es aproximadamente 13.75, lo que significa que el 25% de los datos son menores o iguales a 13.75.


## Quantiles

Los quantiles son valores que dividen un conjunto de datos en intervalos iguales, donde cada intervalo contiene el mismo número de observaciones.

Los quantiles se clasifican según el número de partes en las que dividen los datos:
+ **Cuartiles**: Dividen los datos en 4 partes iguales.
  + 1er cuartil (Q1) = percentil 25
  + 2do cuartil (Q2) = percentil 50, también conocido como la mediana
  + 3er cuartil (Q3) = percentil 75
+ **Deciles**: Dividen los datos en 10 partes iguales.
  + El decil 1 (D1) corresponde al percentil 10, el decil 2 al percentil 20, y así sucesivamente.
+ **Percentiles**: Dividen los datos en 100 partes iguales.
  + Cada percentil representa el 1% de los datos (P1, P2, ..., P99). 

### Funcion Quantile
Función matemática y estadística que se usa para calcular el valor de un quantil específico en un conjunto de datos.

> *¿Cuál es el valor en el conjunto de datos tal que cierto porcentaje de los datos es menor o igual a él?*

Conocida como la inversa de CDF para una variable aleatoria continua:
+ F^-1 = Fx(X) = P(X<=x) = p

En el calculo del percentil:
+ **Para datos discretos**: A veces necesitamos interpolar entre posiciones.
+ **Para distribuciones continuas**: Podemos obtener el valor exacto del percentil directamente mediante la función quantile, sin interpolación.

## Teorema del limite central 
Este teorema establece que, bajo ciertas condiciones, la suma (o promedio) de un gran número de variables aleatorias independientes y identicamente distribuidas (i.i.d.) se aproximará a una distribución normal, independientemente de la forma de la distribución original.

El TLC es aplicable cuando el tamaño de la muestra 
n es lo suficientemente grande.

Las variables aleatorias deben ser independientes; esto significa que el resultado de una variable no afecta a las demás.

El TLC es poderoso porque permite que la distribución de la suma o el promedio de variables aleatorias se normalice, incluso si las variables originales no siguen una distribución normal (pueden ser sesgadas o tener otra forma).

Imagina que lanzas un dado muchas veces (digamos, 100 veces) y registras los resultados. Aunque la distribución de los resultados de un solo lanzamiento de un dado es uniforme y no normal, si calculas el promedio de esos 100 lanzamientos, la distribución de ese promedio se acercará a una distribución normal a medida que aumentes el número de lanzamientos.

