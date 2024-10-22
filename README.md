# Estadistica en R

## Table of content
1. [Variable Aleatoria](#Variable-Aleatoria)
2. [Algunos conceptos](#Algunos-conceptos)
3. [Distribuciones Discretas](#Distribuciones-Discretas)
4. [Distribuciones Continuas](#Distribuciones-Continuas)

## Variable Aleatoria

Una **variable aleatoria** es un valor que depende de eventos aleatorios. Es una función que asigna un valor numérico a cada resultado posible de un experimento aleatorio.

Existen dos tipos principales de variables aleatorias:

+ **Variable aleatoria discreta**: Toma un número finito o contable de valores distintos. Ejemplo: el número de caras que obtienes al lanzar dos monedas.

+ **Variable aleatoria continua**: Puede tomar un número infinito de valores dentro de un intervalo. Ejemplo: la altura de una persona o el tiempo que tarda en completarse una tarea.

## Algunos conceptos

El **PMF** es una manera de describir las probabilidades asociadas con una variable aleatoria discreta. Asigna una probabilidad a cada valor posible que puede asumir la variable aleatoria. (Las distribuciones continuas no tienen PMF)

PMF(X=x) = P(X=x) => Proporciona la probabilidad de que X tome un valor específico x.

La **CDF** de una distribución da la probabilidad acumulada de que la variable aleatoria X tome un valor menor o igual a un cierto valor x.

CDF(X<=x) = P(X<=x) = sum(k=0,x) P(X=k) => es la probabilidad de obtener hasta x éxitos en una serie de n ensayos con probabilidad de éxito p.

El **PDF**
**Memorylesseness**
**Mean**
**E(X)**
**V(X)**
**Estimador**

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

### Normal(Miù(media),Rò^2(desviacion estandar al cuadrado: varianza))
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


