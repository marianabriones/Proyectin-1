# Proyectin-1
CASHFLOW MATCHING
## <p style="text-align: center;">  Proyecto del modulo 1
### <p style="text-align: center;"> CASH FLOW MATCHING 
#### <span style="color:red"> Mariana Briones  

#### <span style="color:green"> Patricia Buenrostro

#### <span style="color:blue"> Marta Martínez 
    
    
![alt text](http://www.descifrado.com/wp-content/uploads/2017/11/Bonos-2-6-696x464.jpg)
CONCEPTO 

Cash Flow Matching: El cash flow matching trata de invertir de forma que en cada momento, los flujos de caja que se obtengan con las inversiones permitan hacer frente a las coberturas aseguradas. 

Bonos: Los bonos son instrumentos financieros de deuda utilizados tanto por entidades privadas como por entidades de gobierno. El bono es una de las formas de materializarse los títulos de deuda, de renta fija o variable. El emisor se compromete a devolver el capital principal junto con los intereses.
Como podemos ver en nuestra vida diaria, todos tenemos ciertas obligaciones futuras, relacionadas con el dinero, y tenemos que ser previsores para ver como podemos llegar a cumplir esas obligaciones e incluso además de cumplirlas y sobrepasar el objetivo y ahorrar.

En nuestro proyecto vamos a suponer que tenemos ciertas obligaciones que tenemos que cumplir para el plazo de unos años y que tenemos ciertos tipos de bonos con ciertos intereses. Nuestro objetivo es saber cuanto dinero depositar en cada bono para que al final de los años nos alcance para pagar todas nuestras obligaciones o incluso nos sobre como ya comentamos en la parte de arriba 
Matemáticamente, podemos formular este problema de la siguiente manera...

$$
\begin{array}{ll}
\min_{x_1,\dots,x_n} &amp; \sum_{j=1}^{m} p_jx_j \\
\text{s. a. }        &amp; \sum_{j=1}^{m}c_{i,j}x_j\geq y_i \text{ para } 1\leq i\leq n \\
                     &amp; x_j \text{ para } 1\leq j\leq m,
\end{array}
$$
donde:

$x_j$ es la cantidad del bono $j$ a ser comprada ($j=1,2,\dots,m$),

$p_j$ es el precio del bono $j$,

$y_i$ es la obligación en el periodo $i$ ($i=1,2,\dots,n$), y

$c_{i,j}$ es el cupón del bono $j$ en el periodo $i$.

Queremos atender obligaciones de efectivo sobre un periodo de 6 años.

Seleccionamos 10 bonos.

La estructura de flujo de efectivo de cada bono se muestra en la columna correspondiente de la tabla.

Los precios de cada bono están dados en el vector $p$.

Las obligaciones están dadas en el vector $y$.

Se supone que se pueden comprar fracciones de bono.

import pandas as pd
import numpy as np

table = pd.DataFrame(index=np.arange(6)+1, columns=np.arange(10)+1)
table.iloc[:,0] = [10,10,10,10,10,110]
table.iloc[:,1] = [7,7,7,7,7,107]
table.iloc[:,2] = [8,8,8,8,8,108]
table.iloc[:,3] = [6,6,6,6,106,0]
table.iloc[:,4] = [7,7,7,7,107,0]
table.iloc[:,5] = [5,5,5,105,0,0]
table.iloc[:,6] = [10,10,110,0,0,0]
table.iloc[:,7] = [8,8,108,0,0,0]
table.iloc[:,8] = [7,107,0,0,0,0]
table.iloc[:,9] = [100,0,0,0,0,0]
table

C = table.values
p = np.array([109, 94.8, 99.5, 93.1, 97.2, 92.9, 110, 104, 102, 95.2])
y = np.array([107, 190, 990, 80, 900, 1400])

from scipy.optimize import linprog

res = linprog(p, A_ub=-C, b_ub=-y)
res

res.x

C.dot(res.x)

y
