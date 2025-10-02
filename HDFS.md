---
layout: default
title: Introdución ao Big Data
---

# HDFS
## Uso básico
Para interactuar co almacenamento utilízase o comando hdfs. Isto admite un parámetro ou subcomando con diferentes opcións.
```bash
hdfs comando
```
Para interactuar co sistema de ficheiros Hadoop, utilízase o parámetro dfs, que require outro argumento (que comeza por "-") que se corresponderá con algúns dos comandos básicos de bash.
```bash
hdfs dfs -comando_linux
```
Exemplo:
```bash
hdfs dfs ls
```
Comandos mais usados:
- **-put**: coloca un ficheiro en *HDFS*.
- **-get** (ou *copyToLocal*): recupera un ficheiro de *HDFS* ao noso sistema local.
- **-cat** / **-text**: amosa o contido dun ficheiro.
- **-head**: amosa o principio dun ficheiro.
- **-tail**: amosa o final dun ficheiro.
- **-mkdir**: crea un directorio.
- **-rmdir**: elimina un directorio.
- **-count**: conta o número de elementos (número de cartafoles/ficheiros...).
- **-cp**: copia un ficheiro.
- **-mv**: move ou renomea un ficheiro.
- **-rm**: elimina un ficheiro.

## Namenodes e Datanodes
Esquema da arquitectura de *HDFS*:
![Arquitectura de HDFS](images/hdfs-arquitectura.png)
### Namenode
Como mencionamos, hai dous tipos de *namenodes*. O primeiro é coñecido como **Namenode principal**. Só hai un, e actúa como servidor principal.
- Nodo ao que os clientes teñen que conectarse para realizar lecturas/escrituras.
- Mantén a árbore do sistema de ficheiros (espazo de nomes) e os metadatos de todos os ficheiros e directorios da árbore, polo que sabe en que nodo do clúster está cada bloque de información (mapa de bloques).
- Os metadatos gárdanse tanto na memoria (para axilizar o seu uso) como no disco ao mesmo tempo, polo que é un nodo que require moita memoria RAM.
- Os bloques nunca pasan polo NameNode, transfírense entre DataNodes e/ou o cliente. É dicir, o Namenode non é responsable de almacenar ou transferir os datos.
- Se cae, non hai acceso a HDFS, polo que é fundamental manter as copias de seguridade.

O segundo tipo é coñedido como **Namenode Secundario** (*Secondary Namenode*):
- A súa función principal é gardar unha copia dos seguintes metadatos:
  - *FSImage*: instantánea dos metadatos do sistema de ficheiros.
  - *EditLog*: rexistro de transaccións que contén información sobre cada cambio que se produce nos *metadatos* do sistema de ficheiros.
- Non é unha copia do *Namenode*.
- Adoita executarse nunha máquina distinta.
### Datanode
Haberá máis dun nodo deste tipo en cada clúster. Para cada Namenode podemos ter miles de Datanodes.
- Almacena e le bloques de datos.
- Recuperado