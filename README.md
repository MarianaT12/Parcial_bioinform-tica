# Parcial_bioinformatica
### PUNTO 1
Haciendo uso de las herramientas suministradas, descarguen del NCBI las secuencias correspondientes al Popset:1776322181
También descarguen una secuencia query de este enlace.

Haciendo uso de expresiones regulares modifique el encabezado fasta de todas las secuencias, de tal manera que solo quede el código de la secuencia, el nombre del gen, género y epíteto específico separado por guiones bajos. Anexe la expresión de búsqueda y reemplazo en su archivo de respuesta.

Find:(\>\w+\.\w+)(\s)(\w+)(\s)(\w+)(\s)(\w+)(\s)(\w+\-\w+)(.*)
Replace:$1_$3_$5_COI_mitochondrial

Construya una base de datos tipo Blastn con las lista de secuencias descargadas.
#crear blast
module load blast/2.7.1
makeblastdb -in secuenciassodoptera -dbtype nucl -parse_seqids -out trans_Noctuidae -title "Noctuidae_transcriptome"

Usando la secuencia query realice un Blast para saber la identidad de la especie y gen. Anexe el código.

blastn -query query.fasta -task megablast -db trans_Noctuidae -outfmt 7 -word_size 7 -out blast_COI -num_threads 1

Interprete el resultado del BLAST de acuerdo a los parámetros vistos en clase.

![image](https://user-images.githubusercontent.com/130588298/232135544-f7a7bef6-a991-4fb8-a62e-8c126687c771.png)

# Análisis: 

A partir del blast se puede decir que hay una alta probabilidad de que las secuencias que se utilizaron sean del género Spodoptera y la probabilidad de que las secuencias se hayan alineado al azar es 0.

### PUNTO 2

Concatene las secuencias del Popset y la query en un solo archivo fasta.
cat query.fasta secuenciassodoptera > secuencias_noctuidae.fasta

Realice un alineamiento múltiple utilizando el programa de su preferencia (Adjunte el código o los pasos seguidos en el archivo de respuesta).
Pedir el salloc
- module load clustalw/2 = cargar el clustal en la terminal
- clustalw2 = abrir el clustal
    - Opción 1 = Copiar el nombre del archivo que tenga las secuencias.
    - Opción 2 = Hacer el alineamiento,  enter
    - Opción 9 = Cambiar las formas del output .fasta
    - Opción F
    - Opción 4, enter
    - Opción 1 = hacer el alineamiento
    - Ponerle nombre a todas las opciones
    - con el GUIDE TREE tambien puedo cambiarle el nombre y me muestra el formato del alineamiento en .cluster
    - Oprimir enter para que me muestre todo y me devuelva al menú principal y después x para salir.
Realice un árbol de máxima verosimilitud bajo el modelo GTR+I+G y con un valor de bootstrap de 1000 (Nota: Recuerde utilizar el parámetro ultrafast bootstrap para agilizar el proceso).
iqtree -s FcC_supermatrix.phy -m GTR+I+G -bb 1000 -pre secuenciasCLUSTAL
Visualice el árbol resultante en su herramienta de preferencia, agregue la imagen en el Readme file y discuta las relaciones filogenéticas identificadas. (Árboles que no estén enraizados no se califican).

![image](https://user-images.githubusercontent.com/130588298/232136063-fae718a6-e0bd-4b67-92fd-6a3e2f36b7ba.png)

# Discusión:
Lo que se puede ver a partir del árbol de máxima verosimilitud es que la familia Noctuidae puede ser monofilética y que _Mythimna_ y _Peridroma_ tienen un ancestro en común. Ahora, el género Spodoptera tuvo eventos de especiación más tardíos con respecto al grupo de _Mythimna_ y _Peridroma_ 

### Punto 3 (Valor 1.0)
1.	Descargue usando las herramientas vistas en clase el siguiente archivo
-Descargar: curl https://raw.githubusercontent.com/paula-torres/bioinformatica_ur/main/files/archivo1.csv > archivo1.csv
2.	Dígame cuántas filas, número de caracteres y columnas tiene. Anexe código.
Numero de filas: wc -L archivo1.csv (me arroja el número de palabras, líneas y caracteres )= tiene 20 filas
Numero de columnas: awk -F "\," '{print NF; exit}'archivo1.csv (tiene 4)
3.	Modifique la palabra chrom por Cromosoma y reemplace las comas , por tabs \t. guárdelo en un archivo de nombre result_file.bed.

1.	sed -i 's/chr/cromosoma/' archivo1.csv (me reemplaza chrom por cromosoma)
2.	cambiar a tabla
sed -i 's/\,/\t/' archivo1.csv
sed -i2 's/\,/\t/' archivo1.csv
sed -i3 's/\,/\t/' archivo1.csv
sed -i4 's/\,/\t/' archivo1.csv

Todo eso me crea 4 archivos distintos, el cuarto que ya tenia todo por \t entonces lo renombré con mv archivo1.csv4 result_file.bed

4.	Guarde las filas que contengan el patrón coding en un archivo con el nombre result_file_coding.bed

grep -e "\scoding" result_file.bed > result_file_coding.bed
Punto 4 (Valor 1.0)
1.	Comprima la carpeta con todos los archivos resultantes que están en el cluster.
2.	Descárguela a su computador.
3.	Carguen el archivo zip a su repositorio.
Zip PARCIAL1_MARIANATRESPALACIOS.ZIP parcial1_MarianaTrespalacios
Lo muevo a mi compu
scp -r -i bio.pt.pem -P 37022 bio.pt@172.25.255.10:/home/bio.pt/data/Parcial1/PARCIAL1_MARIANATRESPALACIOS.zip /mnt/c/Users/Mary/Documents/'Septimo semestre'/Bioinformatica/parcial_marianatrespalacios
descomprimo en la carpeta de parcial


