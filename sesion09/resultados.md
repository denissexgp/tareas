# Sesión 09: Comparación de alineamientos múltiples

## Dónde no se pusieron de acuerdo los métodos

**R-spondinas (referencia RSPO2_human).** Clustal Omega y MAFFT L-INS-i discrepan en dos regiones. La primera es el arranque del péptido señal (posiciones 1–7), con acuerdo por columna de ~0.35–0.41. Es una región hidrofóbica sin homología real entre especies, así que no hay señal que ancle el alineamiento. La segunda es la cola C-terminal básica (211–243), de composición sesgada y longitud variable, con acuerdo medio de 0.35 y 82 % de posiciones por debajo de 0.5. Ambas coinciden con las letras de baja confianza de MUSCLE5 (posiciones 18–19 en el péptido señal y 227–233 en la cola, con LC de 2 a 6) y con lo que recortó trimAl (10 residuos del péptido señal y 17 de la cola). En cambio, los dominios FU1+FU2 (40–141) y TSP1 (145–203) tienen acuerdo de 0.99 y LC de 9, porque los andamios de cisteínas anclan el alineamiento, y trimAl los conservó casi por completo.

**Receptores LGR (referencia LGR5_human).** Las dos regiones de mayor desacuerdo son el ectodominio LRR (1–234, con corridas de acuerdo bajo en 1–87, 93–168 y 193–234) y la cola C-terminal (841–907). En el LRR el problema es de registro: son repeticiones en tándem de ~24 aa con el mismo consenso, y correr una secuencia una repetición completa da un alineamiento casi igual de bueno, por lo que cada programa elige un registro distinto. El acuerdo medio del LRR es 0.61 y 45 % de sus posiciones quedan por debajo de 0.5. La cola es de baja complejidad y longitud variable (acuerdo medio 0.40, 74 % por debajo de 0.5). Ambas regiones coinciden con la baja confianza de MUSCLE5 (corridas aproximadas en 5–28, 164–306 y 848–897, con LC medio de 4.7 en la cola) y con lo que eliminó trimAl (357 de 454 residuos del LRR y 82 de 87 de la cola). El 7TM es la región donde los programas coinciden (acuerdo 0.96, LC 9.0), y trimAl casi no lo tocó.

## Tabla por dominio

**rspo (RSPO2_human, 243 aa)**

| Dominio | Posiciones | Acuerdo medio | LC medio | Residuos eliminados por trimAl |
|---|---|---|---|---|
| Péptido señal | 1–21 | 0.49 | 8.2 | 10 de 21 |
| Enlace N | 22–39 | 0.50 | – | 6 de 18 |
| FU1+FU2 | 40–141 | 0.99 | 9.0 | 3 de 102 |
| Enlace | 142–144 | 0.96 | – | – |
| TSP1 | 145–203 | 0.99 | 9.0 | 0 de 59 |
| Cola C-terminal | 204–243 | 0.35 | 7.9 | 17 de 40 |

**lgr (LGR5_human, 907 aa)**

| Dominio | Posiciones | Acuerdo medio | LC medio | Residuos eliminados por trimAl |
|---|---|---|---|---|
| LRR | 1–454 | 0.61 | 7.2 | 357 de 454 |
| Bisagra | 455–573 | 0.78 | 7.5 | 87 de 119 |
| 7TM | 574–820 | 0.96 | 9.0 | 32 de 247 |
| Cola C-terminal | 821–907 | 0.40 | 4.7 | 82 de 87 |

## ¿Se puede usar el .dnd de Clustal como la filogenia de un gen?

No, el .dnd es solo el orden en que Clustal Omega fue fusionando las secuencias, calculado con distancias entre k-meros y agrupado por UPGMA, sin modelo evolutivo ni medidas de apoyo. Sirve para alinear, pero la filogenia debe inferirse con un método como IQ-TREE sobre un alineamiento recortado, con selección de modelo y apoyos por nodo.

