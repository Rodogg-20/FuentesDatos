##Tarea2

1. Con wget o curl baja el archivo de nombres desde 1880 hasta 2014 de censos de Estados Unidos de la siguiente URL:https://www.dropbox.com/s/ezrp0t7uwyg7vgi/NationalNames.zip?dl=0
  ~~~
  wget https://www.dropbox.com/s/ezrp0t7uwyg7vgi/NationalNames.zip?dl=0
  ~~~

2. Descomprime el archivo con unzip
  ~~~
  unzip 'NationalNames.zip?dl=0'
  ~~~

3. Cambia el nombre del archivo a census_names.csv
  ~~~
  mv NationalNames.csv census_names.csv
  ~~~

Utilizando sed y/o grep responde las siguientes preguntas:
Las modificaciones se realizan en el archivo original.

4. Modifica los nombres de las columnas para que estén todas en minúsculas.
  ~~~
  sed -E -i '1s/([A-Z])/\L&/g' census_names.csv
  ~~~

5. Anna o Ana
  a. ¿Cuántos registros hay que tenga el nombre Anna o Ana?
    ~~~
    grep -ic 'Anna,' census_names.csv
    13691

    grep -ic 'Ana,' census_names.csv
    20268
    ~~~
    si sumamos ambos tendríamos 33959

  b. Modifica los registros que tengan Anna o Ana por el que aparezca más veces (imputación), es decir, si Anna aparece más veces que Ana entonces hay que cambiar las Ana por Anna -> Respeta la mayúscula inicial.
    Por el inciso anterior sabemos que 'Ana'aparece más veces, por lo tanto vamos a cambiar todas las 'Anna' por 'Ana'
    ~~~
    sed -i 's/ana,/Ana,/g' census_names.csv
    sed -i 's/ANA,/Ana,/g' census_names.csv

    sed -i 's/Anna,/Ana,/g' census_names.csv
    sed -i 's/anna,/Ana,/g' census_names.csv
    sed -i 's/ANNA,/Ana,/g' census_names.csv
    ~~~
    Aplicamos estos 3 seds por todas las posibles combinaciones con mayúsculas y minúsculas

  c.Verifica que tienes el mismo número de registros para ahora todas las Anna o Ana
    ~~~
    grep -c 'Ana,' census_names.csv
    33959
    ~~~
    demostrando que fueron correctas las modificaciones

6. Emma o Ema
  a. ¿Cuántos registros hay que tenga el nombre Emma o Ema?
    ~~~
    grep -ic 'Emma,' census_names.csv
    480

    grep -ic 'Ema,' census_names.csv
    1937
    ~~~
    un total de 2417 registros

  b. Modifica los registros que tengan Emma o Ena por el que aparezca más veces (imputación), es decir, si Emma aparece más veces que Ema entonces hay que cambiar las Ema por Emma -> Respeta la mayúscula inicial
    Sabiendo que aparece más veces 'Ema', aplicamos lo mismo que el ejercicio anterior
    ~~~
    sed -i 's/ema/Ema/g' census_names.csv
    sed -i 's/EMA/Ema/g' census_names.csv

    sed -i 's/Emma/Ema/g' census_names.csv
    sed -i 's/emma/Ema/g' census_names.csv
    sed -i 's/EMMA/Ema/g' census_names.csv
    ~~~
  c. Verifica que tienes el mismo número de registros para ahora todas las Emma o Ema
    ~~~
    grep -c 'Ema,' census_names.csv
    2417
    ~~~

7. Kateleen o Katilynn o Katelyn o Katelynn o Katelin o Katelynne o Katelyne o Katelinn
  a. ¿Qué implicación consideras relevante en hacer estos cambios en los nombres? Considera que estamos tratando con datos de un censo.
    Siempre hay que tomar en cuenta que estamos trabajando con información de personas, al modificar sus nombres o cualquier otro dato para facilitar su análisis o simplificar nuestro trabajo  realmente estamos alterando datos personales, siempre hay que hacerlo con ética y responsabilidad
  b. ¿Cuántos registros hay que tengan todas las combinaciones de katelyn?
    ~~~
    grep -ic 'Kateleen,' census_names.csv
    17
    grep -ic 'Katilynn,' census_names.csv
    26
    grep -ic 'Katelyn,' census_names.csv
    63
    grep -ic 'Katelynn,' census_names.csv
    38
    grep -ic 'Katelin,' census_names.csv
    38
    grep -ic 'Katelynne,' census_names.csv
    31
    grep -ic 'Katelyne,' census_names.csv
    27
    grep -ic 'Katelinn,' census_names.csv
    20

    un total de 260 variantes
    ~~~
  c. Modifica los registros que tengan el nombre de katelyn con todas su variantes por el que aparezca más veces (imputación), es decir, si Katelyn aparece más veces que todas las demás combinaciones, modifica todas las combinaciones a la mayor. -> Respeta la mayúscula inicial.
    ~~~
    sed -i 's/Kateleen,/Katelyn,/g' census_names.csv
    sed -i 's/kateleen,/Katelyn,/g' census_names.csv
    sed -i 's/KATELEEN,/Katelyn,/g' census_names.csv

    sed -i 's/Katilynn,/Katelyn,/g' census_names.csv
    sed -i 's/katilynn,/Katelyn,/g' census_names.csv
    sed -i 's/KATILYNN,/Katelyn,/g' census_names.csv

    sed -i 's/katelyn,/Katelyn,/g' census_names.csv
    sed -i 's/KATELYN,/Katelyn,/g' census_names.csv

    sed -i 's/Katelynn,/Katelyn,/g' census_names.csv
    sed -i 's/katelynn,/Katelyn,/g' census_names.csv
    sed -i 's/KATELYNN,/Katelyn,/g' census_names.csv

    sed -i 's/Katelin,/Katelyn,/g' census_names.csv
    sed -i 's/katelin,/Katelyn,/g' census_names.csv
    sed -i 's/KATELIN,/Katelyn,/g' census_names.csv

    sed -i 's/Katelynne,/Katelyn,/g' census_names.csv
    sed -i 's/katelynne,/Katelyn,/g' census_names.csv
    sed -i 's/KATELYNNE,/Katelyn,/g' census_names.csv

    sed -i 's/Katelyne,/Katelyn,/g' census_names.csv
    sed -i 's/katelyne,/Katelyn,/g' census_names.csv
    sed -i 's/KATELYNE,/Katelyn,/g' census_names.csv

    sed -i 's/Katelinn,/Katelyn,/g' census_names.csv
    sed -i 's/katelinn,/Katelyn,/g' census_names.csv
    sed -i 's/KATELINN,/Katelyn,/g' census_names.csv
    ~~~

  d. Verifica que tienes el mismo número de registros una vez que hiciste la modificación.
    ~~~
    grep -c 'Katelyn,' census_names.csv
    260
    ~~~
8. Jennie o Jenni o Jeni o Yenni o Yeni o Yennie
  a. ¿Cuántos registros hay que tengan todas las combinaciones de Jennie?
    ~~~
      grep -ic 'Jennie,' census_names.csv
      195
      grep -ic 'Jenni,' census_names.csv
      70
      grep -ic 'Jeni,' census_names.csv
      69
      grep -ic 'Yenni,' census_names.csv
      11
      grep -ic 'Yeni,' census_names.csv
      37
      grep -ic 'Yennie,' census_names.csv
      1

      un total de 383
    ~~~
  b. Modifica los registros que tengan el nombre de Jennie con todas su variantes por el que aparezca más veces (imputación), es decir, si Jeni aparece más veces que todas las demás combinaciones, modifica todas las combinaciones a la mayor. -> Respeta la mayúscula inicial.
  ~~~
  sed -i 's/jennie,/Jennie,/g' census_names.csv
  sed -i 's/JENNIE,/Jennie,/g' census_names.csv

  sed -i 's/Jenni,/Jennie,/g' census_names.csv
  sed -i 's/jenni,/Jennie,/g' census_names.csv
  sed -i 's/JENNI,/Jennie,/g' census_names.csv

  sed -i 's/Jeni,/Jennie,/g' census_names.csv
  sed -i 's/jeni,/Jennie,/g' census_names.csv
  sed -i 's/JENI,/Jennie,/g' census_names.csv

  sed -i 's/Yenni,/Jennie,/g' census_names.csv
  sed -i 's/yenni,/Jennie,/g' census_names.csv
  sed -i 's/YENNI,/Jennie,/g' census_names.csv

  sed -i 's/Yeni,/Jennie,/g' census_names.csv
  sed -i 's/yeni,/Jennie,/g' census_names.csv
  sed -i 's/YENI,/Jennie,/g' census_names.csv

  sed -i 's/Yennie,/Jennie,/g' census_names.csv
  sed -i 's/yennie,/Jennie,/g' census_names.csv
  sed -i 's/YENNIE,/Jennie,/g' census_names.csv

  ~~~

  c. Verifica que tienes el mismo número de registros una vez que hiciste la modificación.

  ~~~
  grep -c 'Jennie,' census_names.csv
  383
  ~~~
