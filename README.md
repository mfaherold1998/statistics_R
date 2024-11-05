# Estadistica en R

## Table of content
1. [Variable Aleatoria](#Variable-Aleatoria)
2. [Algunos conceptos](#Algunos-conceptos)
3. [Distribuciones Discretas](#Distribuciones-Discretas)
4. [Distribuciones Continuas](#Distribuciones-Continuas)
5. [Percentiles](#Percentiles)
6. [Quantiles](#Quantiles)
7. [Teorema del limite central](#Teorema-del-limite-central)
8. [Ley de los Grandes Números](#Ley-de-los-Grandes-Números)
9. [Momentos](#Momentos)
10. [Estimadores](#Estimadores)
11. [Maximum Likelihood Stimator(MLE)](#Maximum-Likelihood-Stimator(MLE))
12. [Intervalos de Confianza](#Intervalos-de-Confianza)

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

## Ley de los Grandes Números
Es un principio fundamental en la teoría de la probabilidad que describe el resultado de realizar el mismo experimento aleatorio un número muy grande de veces. Esta ley establece que, a medida que aumenta el número de repeticiones de un experimento, la media muestral de los resultados observados se aproximará a la media real o esperada de la distribución de la variable aleatoria.

Hay dos versiones principales de la Ley de los Grandes Números:
+ Ley de los Grandes Números Débil
+ Ley de los Grandes Números Fuerte

Importancia de la Ley de los Grandes Números:
+ **Inferencia Estadística**: La Ley de los Grandes Números justifica la idea de que los promedios muestrales se aproximan a la media poblacional a medida que aumenta el tamaño de la muestra. Esto es crucial en la inferencia estadística.
+ **Pruebas y Experimentos**: Ayuda a entender por qué las muestras grandes proporcionan estimaciones más confiables y estables de los parámetros poblacionales.
+ **Seguros y Finanzas**: Se utiliza en el cálculo de primas de seguros y en modelos financieros, donde se asume que los resultados promedio se estabilizarán a medida que se observen más eventos.


## Momentos

Proporcionan información sobre las características de la distribución, como la tendencia central, la dispersión y la forma.

Para una variable aleatoria X el r-esimo momento alrededor del origen se define como: Miu(r) = E(X^r)

### Momentos centrales
Además de los momentos alrededor del origen, a menudo se utilizan los momentos centrales, que se centran en la media de la distribución.

Miu(r) = E((X-miu)^r)

Los momentos centrales son útiles porque reflejan cómo se distribuyen los valores de 
X alrededor de su media.

### Importancia de los Momentos
**Tendencia Central**: El primer momento (media) describe la tendencia central de la distribución.

**Dispersión**: El segundo momento (varianza) describe cuán dispersos están los datos en relación con la media.

**Forma**: Los momentos de orden superior (como el tercero y el cuarto) proporcionan información sobre la forma de la distribución, como su asimetría y su curtosis.

## Estimadores
> Un estimador es una regla o fórmula que se aplica a cualquier muestra para obtener una estimación del parámetro.
>
> Una estimación es el valor numérico que se obtiene al aplicar el estimador a una muestra específica.

### Estimador Insesgado
T is unbiased cuando E(T) = verdadero valor de la medida estimada

### Eficiencia (small sensibility)
Si se conoce la media, el mejor estimador es el de menor varianza.

Si no se conoce la media hay que calcular el error cuadratico medio y el que tenga menor error es mejor.

Un estimador con menor varianza es considerado más eficiente porque proporciona estimaciones más consistentes y cercanas al verdadero valor del parámetro.

Un estimador se considera eficiente si cumple con las siguientes propiedades:
+ **Incorruptibilidad**: El estimador debe ser insesgado, lo que significa que su valor esperado debe ser igual al verdadero valor del parámetro que está estimando.
+ **Varianza Mínima**: Entre todos los estimadores insesgados, un estimador eficiente tiene la menor varianza posible. Esta es la condición que se establece en el Teorema de Cramer-Rao, que establece un límite inferior para la varianza de estimadores insesgados.

Eficiencia relativa = V(T2)/V(T1) => Si esta razon es menor que uno T2 es mas eficiente

Casos en los que un estimador sesgado con menor varianza puede ser preferible a uno insesgado:
+ Cuando se trabaja con muestras pequeñas
+ Cuando la eficiencia computacional es crucial
+ En el aprendizaje automático y la estadística aplicada, a veces se utilizan estimadores sesgados porque pueden mejorar el rendimiento predictivo en datos no vistos.
+ En modelos estadísticos complejos (como modelos de regresión no lineales o modelos mixtos), puede ser difícil obtener estimadores insesgados debido a la complejidad de la función de verosimilitud.
+ En finanzas, un estimador sesgado puede ser preferido si ayuda a reducir la varianza de las estimaciones de rendimiento de activos.
+ Cuando se requiere realizar inferencias bajo ciertas condiciones o restricciones.
+ En estudios de rendimiento, como la evaluación de la efectividad de tratamientos médicos, a veces se utilizan estimadores sesgados si se ha comprobado que ofrecen resultados más robustos y útiles en situaciones específicas.

### Consistencia
Un estimador es consistente si, al aumentar el número de observaciones, las estimaciones se acercan cada vez más al valor real que se desea estimar.

> Cuando la varianza tiende a 0 en caso de ser un estimador insesgado.

> Cuando el MSE tiende a 0 en caso de ser un estimador sesgado.

Propiedades de la Consistencia:
+ **Insesgamiento**: Un estimador consistente no tiene que ser insesgado, pero todos los estimadores insesgados son consistentes. Sin embargo, la consistencia es una propiedad más general que no depende de que el estimador sea insesgado.
+ **Varianza**: Para que un estimador sea consistente, la varianza del estimador debe tender a cero a medida que el tamaño de la muestra aumenta.

Importancia de la Consistencia:
+ **Inferencia Estadística**: La consistencia es una propiedad crucial en la inferencia estadística porque garantiza que, con suficientes datos, los estimadores proporcionarán resultados cercanos a los verdaderos parámetros de la población.
+ **Toma de Decisiones**: Los estimadores consistentes son más confiables para la toma de decisiones, ya que su precisión mejora con el tamaño de la muestra.
+ **Validez de Modelos**: En modelos estadísticos y de aprendizaje automático, la consistencia de los estimadores contribuye a la validez de las conclusiones extraídas de los datos.

### Estimador Asintóticamente Insesgado
Un estimador se considera asintóticamente insesgado si su valor esperado se aproxima al verdadero valor del parámetro que estima a medida que el tamaño de la muestra aumenta. En otras palabras, aunque el estimador pueda ser sesgado para muestras pequeñas, este sesgo disminuye y tiende a cero a medida que el tamaño de la muestra se hace muy grande.

Importancia del Insesgamiento Asintótico:
+ **Pruebas de Hipótesis**: En contextos donde se requiere hacer inferencias basadas en muestras grandes, los estimadores asintóticamente insesgados son útiles porque permiten suponer que los resultados se aproximan a la realidad.
+ **Confiabilidad en Grandes Muestras**: Proporciona una justificación teórica para confiar en las estimaciones a partir de muestras grandes, incluso si el estimador tiene un sesgo en muestras pequeñas.
+ **Modelos Estadísticos**: En modelos más complejos, se utiliza la propiedad de insesgamiento asintótico para validar estimadores en contextos donde se tienen limitaciones en los datos.

### Error Cuadratico Medio (MSE)
El error cuadrático medio (ECM) es una medida de la precisión de un estimador o modelo, que cuantifica la diferencia promedio entre los valores estimados y los valores reales. O sea mide la diferencia entre el estimador y lo que se estima.

Se utiliza comúnmente en estadística y aprendizaje automático para evaluar el rendimiento de modelos de predicción.

ECM => 1/n * sum(i=1,n)(yi-y^i)2 (el promedio de los cuadrados del valor real menos el valor estimado)

Interpretación:
+ **Valores Bajos**: Un ECM bajo indica que el modelo está haciendo buenas predicciones, ya que las estimaciones están cerca de los valores reales.
+ **Valores Altos**: Un ECM alto sugiere que hay un gran error en las estimaciones, lo que significa que el modelo no está ajustando bien los datos.

Propiedades del ECM:
+ **No Negativo**: El ECM siempre es mayor o igual a cero, ya que los cuadrados de las diferencias son no negativos.
+ **Sensibilidad a Errores Grandes**: Debido a que se eleva al cuadrado la diferencia, el ECM es más sensible a errores grandes. Esto puede ser útil en algunas aplicaciones donde los errores grandes son especialmente indeseables.
+ **Comparación de Modelos**: El ECM se puede utilizar para comparar diferentes modelos de predicción; el modelo con el ECM más bajo generalmente se considera el mejor.

## Maximum Likelihood Stimator(MLE)
El Estimador de Máxima Verosimilitud es un método estadístico utilizado para estimar los parámetros de un modelo probabilístico. La idea fundamental detrás de este enfoque es encontrar los parámetros que maximizan la "verosimilitud" de observar los datos dados esos parámetros.

### Verosimilitud
La verosimilitud se refiere a la probabilidad de observar los datos que tenemos, dado un conjunto específico de parámetros. Formalmente, si tenemos un conjunto de datos X = {x1, x2, ... xn} y un modelo parametrico que depende de un parametro ZETA, La funcion de verosimilitud L(ZETA|X) = P(X|ZETA).

L(ZETA|X) = productoria(1,n) f(xi,ZETA)

> **Probability vs Likelihood**
>
> La *probabilidad* es el area debajo de una distribucion fija => pr(data|distribucion)
>
> El *likelihood* son los valores e las y para valores fijos de datos => pr(distribucion|data)


### Para Obtener un MLE (Procedimiento)
+ Funcion de Verosimilitud: Productoria(1,n)f(x) = Q
+ ln Q
+ Maximizar ln Q derivando con respecto al parametro
+ Igualar a 0 la expresion resultante
+ Con un solo parametro se tiene una sola ecuacion (con n parametros n ecuaciones)
+ Se resuelve el sistema
+ Los puntos obtenidos son los MLE

Propiedades del MLE:
+ **Incorruptibilidad**: Los MLE son insesgados o asintóticamente insesgados, especialmente en muestras grandes.
+ **Consistencia**: A medida que el tamaño de la muestra aumenta, el MLE converge al verdadero valor del parámetro.
+ **Eficiencia**: En muchos casos, el MLE tiene la menor varianza posible entre los estimadores insesgados, lo que se conoce como la propiedad de ser el estimador más eficiente.
+ **Distribución Asintótica Normal**: Para muestras grandes, la distribución del MLE se aproxima a una distribución normal, lo que permite realizar inferencias.

Si los datos son independientes y estan identicamente distribuidos:
+ l^(ZETA|X) = 1/n sum(1,n) ln f(xi|ZETA)
+ MLE consistente
+ sqrt(n)-eficiente y asintoticamente eficiente
+ l(ZETA|X) = log L(ZETA|X) = sum log f(xi,ZETA)


## Intervalos de Confianza

Un intervalo de confianza es un rango de valores que se utiliza para estimar un parámetro poblacional con un nivel de confianza específico. En lugar de proporcionar un solo valor de estimación (como una media muestral), un intervalo de confianza da un rango en el cual es probable que se encuentre el parámetro real de la población.

Componentes de un Intervalo de Confianza:
+ **Estimador puntual**: Es el valor calculado a partir de la muestra, como la media muestral, que actúa como el centro del intervalo.
+ **Margen de error**: Es la cantidad que se suma y resta al estimador puntual para construir el intervalo. Este depende de:
  + El **nivel de confianza** deseado (por ejemplo, 95%, 99%).
  + La distribución de los datos.
  + El tamaño de la muestra.
+ **Nivel de confianza**: Es la probabilidad de que el intervalo calculado contenga el verdadero parámetro poblacional. Por ejemplo, un intervalo de confianza del 95% implica que, si repetimos el estudio muchas veces, el 95% de los intervalos construidos contendrán el valor verdadero del parámetro.

### Interpretación de un Intervalo de Confianza

Un intervalo de confianza del 95% para la media, por ejemplo, significa que estamos 95% seguros de que el verdadero valor de la media poblacional se encuentra dentro de ese rango. En otras palabras, si construyéramos 100 intervalos de confianza a partir de 100 muestras diferentes, esperaríamos que aproximadamente 95 de esos intervalos contengan la media verdadera.

### Como calcular un intervalo de confianza

Supongamos que tienes una muestra con una media muestral de 100 y una desviación estándar de 15, y quieres calcular un intervalo de confianza del 95% para la media poblacional. Con un tamaño de muestra de n=25:
+ Encuentras el valor crítico para el nivel de confianza del 95%
+ Calculas el margen de error
+ Construyes el intervalo de confianza


Esto significa que estás 95% seguro de que la verdadera media poblacional está entre los dos valores extremos obtenidos. CI\[a,b]

### Usos de los Intervalos de Confianza
**Estimación de parámetros**: Para estimar rangos posibles para parámetros desconocidos.

**Toma de decisiones**: En estudios de mercado, pruebas de hipótesis y evaluaciones científicas, un intervalo de confianza ayuda a evaluar la precisión de las estimaciones.
