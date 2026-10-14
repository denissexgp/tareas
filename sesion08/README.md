# Sesión 08: BLAST+ local (D. laeve, módulo WNT–RSPO–LGR)

## Versiones de software
- blastp: 2.16.0+ (Package: blast 2.16.0, build Nov 27 2024 09:40:57)
- mafft: v7.526 (2024/Apr/26)

## Origen de los datos
Copiados en el cluster ken desde `/mnt/data/bioinfo1/jmiranda/sesion08/datos`
(`proteoma_dlaeve_v1.2.faa`, `consultas_wnt.faa`, `mapa_mrna.tsv`).

## Archivos entregados
- `top5.sh`: script que corre blastp y reporta los 5 mejores hits por consulta.
- `top5_lgr5.md`: salida de `./top5.sh referencias_lgr5.faa proteoma_dlaeve`.
- `lgr_candidatos_ids.txt`: 6 candidatos (LGR5, E-value < 1e-30 y qcovs >= 60).
- `tabla_candidatos.tsv`: cromosoma, posición y símbolo de cada candidato (ej. 8).
- `mejores.tsv`: mejor hit por consulta (ej. 5).
- `familia_lgr.aln.faa`: alineamiento MAFFT de 10 secuencias (6 candidatos + 4 referencias LGR5), 2,099 columnas.
- `acusado_909458.tsv`, `reciproco.tsv`: evidencia del párrafo.

`datos/`, la base `proteoma_dlaeve.p*` y `hits.tsv` no se suben; se regeneran con los comandos de la práctica.

## Conclusión

**¿Cuántos receptores LGR completos tiene la babosa?** *D. laeve* tiene **dos** receptores LGR tipo-B completos: `dlaeveM00000441839` en **chr6** (30.9 Mb) y `dlaeveM00000727719` en **chr10** (23.7 Mb). Ambos están anotados como LGR4 en `mapa_mrna.tsv`. Los 6 candidatos que pasaron los filtros de LGR5 (E-value < 1e-30 y cobertura >= 60 %) están en la tabla siguiente. Solo los de chr6 y chr10 regresan a LGR5 como mejor hit en el BLAST recíproco contra las 72 consultas (83.2 % de identidad con LGR5 de *Bradybaena* para chr10 y 56.8 % para chr6, con 99 % y 82 % de cobertura). Los otros cuatro prefieren RXFP1 o FSHR de *Bradybaena* con identidades de 53 a 73 %, así que son receptores LGR de otros subtipos (relaxina y FSH/TSH): chr2 (x2, símbolo GPRGPH), chr4 (TSHR) y chr5 (GPRGPH). Además, en el top5 de las referencias LGR5 (`top5_lgr5.md`) los genes de chr6 y chr10 son siempre los dos primeros hits en las cuatro consultas, con bit scores muy superiores al resto (por ejemplo, 1621 y 1444 con la referencia de *Bradybaena*, contra 346 del tercero).

**¿Por qué `dlaeveM00000909458` (chr13) no es uno de ellos?** Aunque alinea con LGR5 con E-values de hasta 8.4e-14 (humano) y 1.0e-15 (*Bradybaena*), lo hace con identidades de solo 25-31 % y una cobertura de la consulta de 43 % (LGR5 humano) y 31 % (*Bradybaena*), contra 79-99 % de cobertura y mucha mayor identidad en los dos LGR reales. Por eso no pasa los filtros del ejercicio 7 (E-value < 1e-30 y cobertura >= 60 %) y no está en `lgr_candidatos_ids.txt`. Este E-value solo indica homología parcial: el parecido proviene del ectodominio de repeticiones ricas en leucina (LRR), un motivo presente en muchas familias de proteínas, y el par LGR5-humano aparece en dos líneas porque son dos HSP, dos bloques alineados separados dentro del mismo par. Según la anotación genómica descrita en la práctica, este gen solo tiene LRR y carece del dominio de siete hélices transmembranales (7TM), por lo que no es un receptor completo y no puede transducir señal como un LGR. Las sondas diseñadas como "lgr5" con el transcriptoma apuntaban en realidad a este gen.

## Tablas de evidencia

### Candidatos: cromosoma (ej. 8) y mejor hit de vuelta (parte 5)

| Gen | Cromosoma | Posición | Símbolo | Mejor hit de vuelta | % id | qcovs | Recíproco a LGR5 |
|---|---|---|---|---|---|---|---|
| dlaeveM00000132191 | chr2 | 15.7 Mb | GPRGPH | RXFP1 (*Bradybaena*) | 53.3 | 94 | no |
| dlaeveM00000134217 | chr2 | 17.7 Mb | GPRGPH | RXFP1 (*Bradybaena*) | 73.2 | 99 | no |
| dlaeveM00000308285 | chr4 | 45.9 Mb | TSHR | FSHR (*Bradybaena*) | 67.8 | 100 | no |
| dlaeveM00000351276 | chr5 | 18.7 Mb | GPRGPH | RXFP1 (*Bradybaena*) | 70.8 | 99 | no |
| **dlaeveM00000441839** | **chr6** | 30.9 Mb | LGR4 | LGR5 (*Bradybaena*) | 56.8 | 82 | **sí** |
| **dlaeveM00000727719** | **chr10** | 23.7 Mb | LGR4 | LGR5 (*Bradybaena*) | 83.2 | 99 | **sí** |

### Gen dlaeveM00000909458 (chr13) contra las consultas

| Consulta | % id | E-value | qcovs |
|---|---|---|---|
| LGR5\|human\|NP_003658.1 | 26.6 | 8.39e-14 | 43 |
| LGR5\|human\|NP_003658.1 | 30.7 | 2.60e-12 | 43 |
| LGR5\|mollusc\|Pomacea_canaliculata\|XP_025085505.1 | 25.9 | 6.65e-10 | 31 |
| LGR5\|mollusc\|Bradybaena_similaris\|BFZ05148.1 | 26.6 | 1.04e-15 | 31 |
| LGR5\|mollusc\|Bradybaena_similaris\|BFZ05148.1 | 25.4 | 5.74e-10 | 31 |
| LGR6\|human\|NP_001017403.1 | 26.8 | 3.50e-14 | 40 |
| LGR6\|human\|NP_001017403.1 | 30.1 | 2.45e-09 | 40 |
| LGR6\|mollusc\|Pomacea_canaliculata\|XP_025085505.1 | 25.9 | 6.65e-10 | 31 |
| LGR6\|mollusc\|Bradybaena_similaris\|BFZ05148.1 | 26.6 | 1.04e-15 | 31 |
| LGR6\|mollusc\|Bradybaena_similaris\|BFZ05148.1 | 25.4 | 5.74e-10 | 31 |
| RXFP1\|mollusc\|Magallana_gigas\|XP_011430344.3 | 29.0 | 2.99e-08 | 18 |

### Alineamiento
`familia_lgr.faa`: 10 secuencias, longitud 892-1,682 aa. `familia_lgr.aln.faa`: 10 secuencias de 2,099 columnas cada una (MAFFT inserta gaps para que todas midan lo mismo).
