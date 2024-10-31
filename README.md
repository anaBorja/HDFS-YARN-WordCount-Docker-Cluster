# HDFS-YARN-WordCount-Docker-Cluster

Este repositorio proporciona una configuración de clúster de Docker para Hadoop, utilizando HDFS y YARN, que permite contar palabras en un archivo de texto. Esta configuración es ideal para aquellos que desean experimentar con Hadoop sin necesidad de instalarlo localmente.


### Requisitos

Docker Desktop, 
WSL2 (Windows Subsystem for Linux)

### Instrucciones de Uso

1. **Clonar el Repositorio**
    ```bash
   git clone https://github.com/anaBorja/HDFS-YARN-WordCount-Docker-Cluster.git
    
2. **entrar en la carpeta**
   ```bash
   cd hdfs-docker-cluster

3. **Iniciar el Clúster**
   ```bash
    docker-compose up -d
  
4. **Preparar el Archivo de texto en HDFS**
   ```bash
   docker exec -it namenode hadoop fs -mkdir -p /user/input
   docker cp tu_texto.txt namenode:/tmp/tu_texto.txt
   docker exec -it namenode hadoop fs -put /tmp/tu_texto.txt /user/input

5. **Contar Palabras**
    ```bash
    docker exec -it namenode hadoop jar /opt/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.5.jar wordcount /user/input /user/output
El comando ejecuta el hadoop-mapreduce-examples.jar que incluye el progrma de wordcount.
Parámetros:
-/user/input: Ruta en HDFS donde esta el archivo.
-/user/output: Ruta donde se guardará el resultado del conteo de palabras.

6. **Ver los resultados**
    ```bash
    docker exec -it namenode hadoop fs -cat /user/output/part-r-00000
  Al ejecutarse el anteior comando se crear part-r-00000 y te mostrara las palabras del texto que se repiten.

7. **Detener el clúster**
  ```bash
  docker-compose down

