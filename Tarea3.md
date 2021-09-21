## Tarea3

1. Baja con wget o curl los datos de covid nacional en la siguiente URL: https://archivo.datos.cdmx.gob.mx/casos_nacionales_covid-19.csv
~~~
wget https://archivo.datos.cdmx.gob.mx/casos_nacionales_covid-19.csv
~~~

2. Modifica a que todas las columnas estén en minúsculas ocupando tolower().
~~~
awk -F, '{ print tolower($0)}' casos_nacionales_covid-19.csv > aux.csv
mv aux.csv casos_nacionales_covid-19.csv
~~~

3. Modifica los acentos por la misma letra sin acento utilizando gsub() de awk. gsub.
~~~
awk -F, '{ gsub(/á/,"a"); print $0 }' casos_nacionales_covid-19.csv > aux.csv

awk -F, '{ gsub(/é/, "e"); print $0 }' aux.csv > aux1.csv

awk -F, '{ gsub(/í/, "i"); print $0 }' aux1.csv > aux2.csv

awk -F, '{ gsub(/ó/, "o"); print $0 }' aux2.csv > aux3.csv

awk -F, '{ gsub(/ú/, "u"); print $0 }' aux3.csv > aux4.csv

mv aux4.csv casos_nacionales_covid-19.csv

rm aux.csv
rm aux1.csv
rm aux2.csv
rm aux3.csv
rm aux4.csv
~~~

4. ¿Cuántas personas fallecieron menores de 20 años? [0-19]
~~~

 awk -F, 'BEGIN{count=0;} {if($17~/0[1-9]|1[0-9]/ && $14~/....-..-../)  count++
 }END{print count}' casos_nacionales_covid-19.csv

 241

~~~

5. ¿Cuántas personas embarazadas fallecieron entre julio y diciembre del 2020? (Revisa la operación ~ en los condicionales awk).
~~~
awk -F,  'BEGIN{count=0;} {if(($19 ~ "si") && ($14 ~ /2020-[7-9]|1[0-2]-../)) count++} END{print count}' casos_nacionales_covid-19.csv

6
~~~

6. De las personas entre 30 y 50 [30-50] años que fallecieron, ¿cuántas tenían diabetes?
~~~
awk -F, 'BEGIN{count=0;} {if (($17~/3[0-9]|4[0-9]|50/) && ($14 ~/....-..-../) && ($22 ~ "si")) count++} END{print count}' casos_nacionales_covid-19.csv

2676
~~~

7. De las personas que encontraste en la pregunta 6, ¿cuántas no residen en la "MICHOACÁN"?
~~~
awk -F, 'BEGIN{count=0;} {if (($17~/3[0-9]|4[0-9]|50/) && ($14 ~/....-..-../) && ($9!="michoacan") && ($22 ~ "si")) count++} END{print count}' casos_nacionales_covid-19.csv

2676
~~~

8. ¿Cuántas personas menores de 19 años [0-18] fallecieron en agosto del 2021?
~~~

awk -F, 'BEGIN{count=0;} {if($17~/0[0-9]|1[0-8]/ &&  $14~/2021-08-../)count++}
END{print count}' casos_nacionales_covid-19.csv

12
~~~

9. Verifica si la columna de fecha de defunción tiene una longitud de 10 caracteres. En caso de que no sea verifica si tiene números, de no ser así, imprime el siguiente mensaje El renglón <NR> no tiene asociada una fecha <$fecha_def>; si contiene números verifica que inicien con 2020 e imprime El renglón <NR> no tiene el formato adecuado de fecha <$fecha_def>. length
~~~
awk -F, '{
    if (length($14)!=10)
      if ($14!=/\d/) print "El renglón ",NR, " no tiene asociada una fecha ", $14;
      else  if ($14==/2020.*/) print "El renglón ", NR, " no tiene el formato adecuado de fecha", $14;
  }' casos_nacionales_covid-19.csv
~~~

10. Cuenta cuántos registros de fallecidos tenemos de cada entidad de residencia.
~~~
awk -F, '{
  if ($14~/....-..-../) arr[$9]++
}
END{
 for (element in arr)
   print "entidad de residencia: ", element, " registros: ", arr[element]   
}' casos_nacionales_covid-19.csv

entidad de residencia:  "sonora"  registros:  6
entidad de residencia:  "michoacan de ocampo"  registros:  75
entidad de residencia:  "san luis potosi"  registros:  20
entidad de residencia:  "tabasco"  registros:  4
entidad de residencia:  "hidalgo"  registros:  486
entidad de residencia:  "veracruz de ignacio de la llave"  registros:  106
entidad de residencia:  "zacatecas"  registros:  5
entidad de residencia:  "tlaxcala"  registros:  69
entidad de residencia:  "nuevo leon"  registros:  11
entidad de residencia:  "nayarit"  registros:  2
entidad de residencia:  "jalisco"  registros:  11
entidad de residencia:  "quintana roo"  registros:  12
entidad de residencia:  "queretaro"  registros:  50
entidad de residencia:  "guanajuato"  registros:  58
entidad de residencia:  "sinaloa"  registros:  6
entidad de residencia:  "guerrero"  registros:  171
entidad de residencia:  "yucatan"  registros:  5
entidad de residencia:  "tamaulipas"  registros:  18
entidad de residencia:  "morelos"  registros:  157
entidad de residencia:  "puebla"  registros:  271
entidad de residencia:  "oaxaca"  registros:  79
entidad de residencia:  na  registros:  50551
entidad de residencia:  "mexico"  registros:  15571
~~~

11. Cuenta cuántos registros tenemos de cada sector diferente, imprime:
~~~
awk -F, '{
  arr[$5]++
}
END{
 for (element in arr)
   print "sector: ", element, " registros: ", arr[element]   
}' casos_nacionales_covid-19.csv

sector:  "municipal"  registros:  1
sector:  "cruz roja"  registros:  643
sector:  "sedena"  registros:  13628
sector:  "imss"  registros:  480338
sector:  "issste"  registros:  40586
sector:  "dif"  registros:  3
sector:  "privada"  registros:  139594
sector:  "semar"  registros:  6244
sector:  "pemex"  registros:  14442
sector:  "sector"  registros:  1
sector:  "universitario"  registros:  23
sector:  "estatal"  registros:  1466
sector:  "imss-bienestar"  registros:  65
sector:  na  registros:  36
sector:  "ssa"  registros:  3317826
~~~
