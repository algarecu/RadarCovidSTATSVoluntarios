# Radar COVID – Documentación
## Respuesta a Preguntas Frecuentes (FAQ)
 
 #### <a name="FAQ-E-5"></a>E.5. Cómo sube Radar Covid los identificadores aleatorios cuando alguien comunica un positivo. Cómo Radar STATS estima el número de las personas que han comunicado un positivo.

Cuando alguien comunica un positivo se "suben" al servidor de diagnósticos una "clave de exposición temporal" TEK (Temporary Exposure Key) por día y no todos los identificadores aleatorios (aproximadamente uno cada 10 minutos, 6 x 24 = 144 al día). Este TEK es la semilla de todos los identificadores aleatorios (ID aleatorio) que mi móvil ha generado a lo largo del día. Estos ID aleatorios se puede generar a partir del TEK de ese día [mediante fórmulas matemáticas](https://covid19-static.cdn-apple.com/applications/covid19/current/static/contact-tracing/pdf/ExposureNotification-CryptographySpecificationv1.2.pdf). Este mecanismo se describe [aquí](https://github.com/pvieito/Radar-STATS#documentation).

Vamos a suponer que una persona comunica su positivo el 20 octubre de 2020, alrededor de las 11:00. Se suben al servidor los TEK de los dias 19, 18, 17, 16, 15 [5 dias de acuerdo con lo que indica la cuestión I.7 de este documento](https://www.mscbs.gob.es/en/profesionales/saludPublica/ccayes/alertasActual/nCov/documentos/Preguntas_y_respuestas_RADAR-COVID.pdf) aunque en mi móvil haya TEK de 14 días previos.

¿Se sube el TEK del día 20? No siempre es así. Depende de Google Play y de la librería que se esté utilizando. @pvieito lo cuenta [aqui](https://twitter.com/pvieito/status/1315710081908998147), [aqui](https://twitter.com/pvieito/status/1310190919224881153) y [aqui](https://twitter.com/pvieito/status/1310190926082514944). Los TEK de liberación temprana, en que la fecha de generación coincide con la que se suben (en nuestro ejemplo, el 20 de octubre) no siempre se suben.

Vamos a suponer que en nuestro ejemplo, al comunicar un positivo, no hay liberación temprana: no se sube el del día 20 de cotubre.

De esta manera se suben 5 TEK cuya "fecha de subida" (Upload Date) es el 20/10/2020 y cuyas "fechas de generación" (Generation Date) son respectivamente 19/10, 18/10, 17/10, 16/10, 15/19.

Lo ilustramos son el siguiente ejemplo.


https://twitter.com/RadarCOVIDSTATS/status/1318649766356582401

```
#RadarCOVID Report – 2020-10-20@20

Today:
- Uploaded TEKs: 722 (+56 last hour)
- Shared Diagnoses: =128 (+7 last hour)
- TEKs per Diagnosis: =5.6
- Usage Ratio: =1.05%

Week:
- Shared Diagnoses: =970
- Usage Ratio: =1.25%
```

Y recogimos este enlace a esa misma hora (2020-10-20@20)  https://github.com/pvieito/Radar-STATS#multi-region-summary-table

```
Shared TEKs by Generation Date
Backend Region	B	CH	ES	ES@PRE	IT	PT	(aumento)
2020-10-20	0	182	140	3	0	0	+9
2020-10-19	0	699	270	34	454	66	+7
2020-10-18	171	1084	381	44	468	118 +7
2020-10-17	342	1472	523	47	496	139 +7
2020-10-16	487	1832	578	54	508	180 +6
2020-10-15	595	2167	646	50	567	206 +5
2020-10-14	666	2312	612	383	598	205 +5
2020-10-13	664	2356	551	375	625	198 +3
2020-10-12	609	2236	504	410	632	182 +2
2020-10-11	510	2045	462	84	634	165 +2
2020-10-10	428	1800	429	81	616	148 +1
2020-10-09	386	1603	421	77	600	134 +1
2020-10-08	349	1467	414	81	585	112	+1
2020-10-07	297	1361	375	90	568	109
```

https://twitter.com/RadarCOVIDSTATS/status/1318633946930872320
...

#RadarCOVID Report – 2020-10-20@19

Today:
- Uploaded TEKs: 666 (+0 last hour)
- Shared Diagnoses: =121 (+0 last hour)
- TEKs per Diagnosis: =5.5
- Usage Ratio: =0.99%

Week:
- Shared Diagnoses: =963
- Usage Ratio: =1.24%
...

...
https://github.com/pvieito/Radar-STATS#multi-region-summary-table
Shared TEKs by Generation Date
Backend Region	BE CH   ES  ES@PRE IT PT
Sample Date (UTC)						
2020-10-20	0	172	    131	2	0	0
2020-10-19	0	670	    263	11	330	65
2020-10-18	171	1056	374	22	361	117
2020-10-17	342	1447	516	27	393	138
2020-10-16	487	1812	572	34	409	179
2020-10-15	595	2151	641	29	469	206
2020-10-14	666	2301	607	363	509	205
2020-10-13	664	2347	548	358	541	198
2020-10-12	609	2229	502	395	553	182
2020-10-11	510	2040	460	71	560	165
2020-10-10	428	1795	428	72	549	148
2020-10-09	386	1601	420	70	537	134
2020-10-08	349	1467	413	77	525	112
2020-10-07	297	1361	375	86	510	109
...



