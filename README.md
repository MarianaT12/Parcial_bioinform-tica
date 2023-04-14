# Parcial_bioinformatica
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

##Análisis:
