1.1 Los cuatro defectos. Para cada uno: qué está mal, en qué archivo y en qué líneas se
manifiesta, y qué consecuencia tiene. Un defecto no es "falta una línea": es qué garantía se
pierde por no tenerla

1. En el .yml el pipeline de validar y publicar artefacto se ejecutan al mismo tiempo.
2. No cuenta con archivos de bloqueo
3. En la linea 32: Analisis de calidad. Se genera un reporte de cobertura en XML (--cov-report=xml), pero no se pasa a SonarCloud en sus argumentos.
4. No se usa un sistema cache para la instalacion de dependencia, relentizando la ejecucion por cada pipeline.


4.1 Medición posterior. El valor del proxy después de la intervención, junto al de la línea
base. Qué cambió y en qué proporción.
Se implementó el sistema de cache para las dependencias, el analisis de calidad quedon en funcionamiento, se tiene un job de bloqueo previo a publicación, y para ejecutar la publicación se necesita una previa ejecución del job de validación. El tiempo de ejecución aumentó en un total de 1m 21s, sin embargo; para la ejecución del job de publicación se demora apenas 15s, mejorando la tasa de falla de cambios.

4.2 Justificación de la versión. Qué versión declararon y qué commits del historial la
sustentan.
Se declaró la versión 1.2.1 debido a que en commits previos, se correcciones o fix del proyecto. El ultimo commit previo en ese archivo fue: 017bdcfa82c55d6a619d9c932f75ea16607b7fed

4.3 Lo que no se resolvió. El pipeline sigue teniendo limitaciones. Nombren una y
expliquen qué haría falta para resolverla.
El archivo de reporte coverage.xml no se guarda en archivos historicos cuando se genera el analisis de calidad.Para resolverlo se debería agregar un paso para siempre descargar ese archivo, para tener los logs de pruebas en caso fallen.

4.4 Declaración de uso de IA generativa, conforme al sílabo.
Se utilizó IA para:
- la generación de una función en la rama "falla" con el siguiente prompt: genera una una función nueva de al menos 15 líneas, con lógica real —condicionales, no un return fijo en python.
- Consulta del enunciado con el siguiente prompt: a que se refiere con "Sobre el quality gate. Configuren sonar-project.properties con su organization keyy su project key antes de la primera ejecución."
- Para la consulta de versiones: Como consulto que versión actualizar en el archivo VERSION
- Como colocar la condicion 3 en el pipeline: Como coloco esta condición? Condición 3: Fuerza al pipeline a esperar y detenerse si falla el Quality Gate en mi pipeline.yml
- Como colocar la condicion 4: Como coloco esta condición?  El artifact publicado debe llamarse despachos-<versión>, solo desde main, y solo si la validación pasó en mi pipeline.yml
- Se uso IA generativa para la descripción y el titulo de los commits.
