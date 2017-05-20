# Как писать на Scala и не умереть.
## Как я scala учил 
### Для себя вы тут можете найти много интересных вещей, если вы хотите работать со scala, но пока не очень можете в него =)

> Это моя личная история боли и радости. Всё написанное дальше - это то, что я делал на момент изучения. Я не хочу, чтобы вы учили или делали так же. Просто рассказываю о том, что я делал. Вы можете пойти по этому пути, но за результат я ответственность не беру.


### Jupyter + Any Lang = Love
Для изучения этого языка я решил использовать Jupyter. Потому что в нём можно как и поиграться с языком, так и поделать боевые задачи по ML (по крайней мере на python).

Начнём с установки. После того, как вы скачали [Anaconda](https://www.continuum.io/downloads) или руками собрали всё вам нужное с помощью setupweels и магии... Нужно запилить Kernel (это ядро jupyter). Ядро - это по сути язык, на котором вы можете писать, если вы действительно хотите погрузиться в мир jupyter и python ML, то вам [сюда](https://github.com/goto-ru/AD_starter). Ну а мы продолжаем.

Прежде чем установить само ядро, придётся позабавиться с настройкой Spark, потому что хочется Machine Learning во всей красе. Не знаю, что там с другими системами, но в Arch есть AUR пакет ``` apache-spark```. Его мы и установим.

```
[tvorogme@localhost projects]$ yaourt -S  apache-spark
```

Далее добавим ```spark-home```:

```
export SPARK_HOME=/opt/apache-spark
```

Теперь нужно поставить Scala.

По скольку это большая машина JRE то нужно всё это ставить: 

```
[tvorogme@localhost ~]$ pacman -S jre8-openjdk scala
```

Но установив, я не смог запустить scala, потому что [БАЦ](https://github.com/NixOS/nixpkgs/issues/22439)! 

Решаем эту проблему.
```
[tvorogme@localhost ~]$ sudo archlinux-java set java-8-openjdk/jre
```

#### Вместо 1.000 слов:
```
[tvorogme@localhost ~]$ scala
Welcome to Scala 2.12.2-20170419-092530-unknown (OpenJDK 64-Bit Server VM, Java 1.8.0_121).
Type in expressions for evaluation. Or try :help.

scala> 
```
Дальше продолжаем ставить зависимости ядра:

```
[tvorogme@localhost ~]$ yaourt -S hadoop
```
Добавим JAVA_HOME:
```
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk/jre/
```

Победа:
```
[tvorogme@localhost ~]$ hadoop
Usage: hadoop [--config confdir] [COMMAND | CLASSNAME]
  CLASSNAME            run the class named CLASSNAME
 or
  where COMMAND is one of:
  fs                   run a generic filesystem user client
  version              print the version
  jar <jar>            run a jar file
                       note: please use "yarn jar" to launch
                             YARN applications, not this command.
  checknative [-a|-h]  check native hadoop and compression libraries availability
  distcp <srcurl> <desturl> copy file or directories recursively
  archive -archiveName NAME -p <parent path> <src>* <dest> create a hadoop archive
  classpath            prints the class path needed to get the
                       Hadoop jar and the required libraries
  credential           interact with credential providers
  daemonlog            get/set the log level for each daemon
  trace                view and modify Hadoop tracing settings

Most commands print help when invoked w/o parameters.
```

Дальше идём побеждать:
Ставим ядро!
```
[tvorogme@localhost scala]$ bash <(curl https://raw.githubusercontent.com/alexarchambault/jupyter-scala/master/jupyter-scala)>
```
Поздравляю ```kernel ready```!

Все дальнейшие штуки я буду делать в тетрадках. Они будут разделены по папочкам, а когда я закончу я опишу их тут.



