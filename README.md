# Как писать на Scala и не умереть.
## Курс того, как я учил scala

> Это моя личная история боли и радости. Всё написанное дальше - это то, что я делал на момент изучения. Я не хочу, чтобы вы учили или делали так же. Просто рассказываю о том, что я делал. Вы можете пойти по этому пути, но за результат я ответственность не беру.


### Jupyter + Any Lang = Love
Для изучения этого языка я решил использовать Jupyter. Потому что в нём можно как и поиграться с языком, так и поделать боевые задачи по ML (по крайней мере на python).

Начнём с установки. После того, как вы скачали [Anaconda](https://www.continuum.io/downloads) или руками собрали всё вам нужное с помощью setupweels и магии... Нужно запилить Kernel (это ядро jupyter). Ядро - это по сути язык, на котором вы можете писать, если вы действительно хотите погрузиться в мир jupyter и python ML, то вам [сюда](https://github.com/goto-ru/AD_starter). Ну а мы продолжаем.

По скольку конечной целью моего обучения является ML. Мы будем ставить [Toree](https://github.com/apache/incubator-toree). Это ядро позволяет использовать не только Scala, но и Apache Spark, которым на Python я уже овладел.

Прежде чем установить само ядро, придётся позабавиться с настройкой Spark, потому что Toree без него не установится. Не знаю, что там с другими системами, но в Arch есть AUR пакет ``` apache-spark```. Его мы и установим.

```
[tvorogme@localhost projects]$ yaourt -S  apache-spark
```

Далее добавим ```spark-home```:

```
export SPARK_HOME=/opt/apache-spark
```

Далее установим kernel:

```
[tvorogme@localhost projects]$ pip install https://dist.apache.org/repos/dist/dev/incubator/toree/0.2.0/snapshots/dev1/toree-pip/toree-0.2.0.dev1.tar.gz
[tvorogme@localhost projects]$ jupyter toree install --spark_home=$SPARK_HOME
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

Вроде бы всё хорошо, но тут:

```
[I 06:12:32.516 NotebookApp] Kernel started: 03f845fb-0f19-40b4-a43a-24d2a0b27b33
Starting Spark Kernel with SPARK_HOME=/opt/apache-spark
Setting default log level to "WARN".
To adjust logging level use sc.setLogLevel(newLevel). For SparkR, use setLogLevel(newLevel).
(Scala,org.apache.toree.kernel.interpreter.scala.ScalaInterpreter@6731787b)
(PySpark,org.apache.toree.kernel.interpreter.pyspark.PySparkInterpreter@16f7b4af)
(SparkR,org.apache.toree.kernel.interpreter.sparkr.SparkRInterpreter@7adf16aa)
(SQL,org.apache.toree.kernel.interpreter.sql.SqlInterpreter@34a1d21f)
17/05/20 06:12:35 WARN toree.Main$$anon$1: No external magics provided to PluginManager!
Exception in thread "main" java.lang.IncompatibleClassChangeError: class org.clapper.classutil.asm.ASMEmptyVisitor has interface org.objectweb.asm.ClassVisitor as super class
	at java.lang.ClassLoader.defineClass1(Native Method)
	at java.lang.ClassLoader.defineClass(ClassLoader.java:763)
	at java.security.SecureClassLoader.defineClass(SecureClassLoader.java:142)
	at java.net.URLClassLoader.defineClass(URLClassLoader.java:467)
	at java.net.URLClassLoader.access$100(URLClassLoader.java:73)
	at java.net.URLClassLoader$1.run(URLClassLoader.java:368)
	at java.net.URLClassLoader$1.run(URLClassLoader.java:362)
	at java.security.AccessController.doPrivileged(Native Method)
	at java.net.URLClassLoader.findClass(URLClassLoader.java:361)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:424)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:357)
	at java.lang.ClassLoader.defineClass1(Native Method)
	at java.lang.ClassLoader.defineClass(ClassLoader.java:763)
	at java.security.SecureClassLoader.defineClass(SecureClassLoader.java:142)
	at java.net.URLClassLoader.defineClass(URLClassLoader.java:467)
	at java.net.URLClassLoader.access$100(URLClassLoader.java:73)
	at java.net.URLClassLoader$1.run(URLClassLoader.java:368)
	at java.net.URLClassLoader$1.run(URLClassLoader.java:362)
	at java.security.AccessController.doPrivileged(Native Method)
	at java.net.URLClassLoader.findClass(URLClassLoader.java:361)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:424)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:357)
	at org.clapper.classutil.asm.ClassFile$.load(ClassFinderImpl.scala:250)
	at org.clapper.classutil.ClassFinder.org$clapper$classutil$ClassFinder$$classData(ClassFinder.scala:427)
	at org.clapper.classutil.ClassFinder$$anonfun$2.apply(ClassFinder.scala:385)
	at org.clapper.classutil.ClassFinder$$anonfun$2.apply(ClassFinder.scala:385)
	at scala.collection.immutable.Stream.map(Stream.scala:418)
	at org.clapper.classutil.ClassFinder.processOpenZip(ClassFinder.scala:385)
	at org.clapper.classutil.ClassFinder.processJar(ClassFinder.scala:340)
	at org.clapper.classutil.ClassFinder.findClassesIn(ClassFinder.scala:329)
	at org.clapper.classutil.ClassFinder.find(ClassFinder.scala:320)
	at org.clapper.classutil.ClassFinder.getClasses(ClassFinder.scala:311)
	at org.apache.toree.plugins.PluginSearcher$$anonfun$1.apply(PluginSearcher.scala:73)
	at org.apache.toree.plugins.PluginSearcher$$anonfun$1.apply(PluginSearcher.scala:73)
	at scala.util.Try$.apply(Try.scala:192)
	at org.apache.toree.plugins.PluginSearcher.loadClassMap(PluginSearcher.scala:73)
	at org.apache.toree.plugins.PluginSearcher.internalClassInfo$lzycompute(PluginSearcher.scala:35)
	at org.apache.toree.plugins.PluginSearcher.internalClassInfo(PluginSearcher.scala:34)
	at org.apache.toree.plugins.PluginSearcher.internal$lzycompute(PluginSearcher.scala:38)
	at org.apache.toree.plugins.PluginSearcher.internal(PluginSearcher.scala:38)
	at org.apache.toree.plugins.PluginManager.internalPlugins$lzycompute(PluginManager.scala:45)
	at org.apache.toree.plugins.PluginManager.internalPlugins(PluginManager.scala:44)
	at org.apache.toree.plugins.PluginManager.initialize(PluginManager.scala:80)
	at org.apache.toree.boot.layer.StandardComponentInitialization$class.initializePlugins(ComponentInitialization.scala:221)
	at org.apache.toree.boot.layer.StandardComponentInitialization$class.initializeComponents(ComponentInitialization.scala:86)
	at org.apache.toree.Main$$anon$1.initializeComponents(Main.scala:35)
	at org.apache.toree.boot.KernelBootstrap.initialize(KernelBootstrap.scala:101)
	at org.apache.toree.Main$.delayedEndpoint$org$apache$toree$Main$1(Main.scala:40)
	at org.apache.toree.Main$delayedInit$body.apply(Main.scala:24)
	at scala.Function0$class.apply$mcV$sp(Function0.scala:34)
	at scala.runtime.AbstractFunction0.apply$mcV$sp(AbstractFunction0.scala:12)
	at scala.App$$anonfun$main$1.apply(App.scala:76)
	at scala.App$$anonfun$main$1.apply(App.scala:76)
	at scala.collection.immutable.List.foreach(List.scala:381)
	at scala.collection.generic.TraversableForwarder$class.foreach(TraversableForwarder.scala:35)
	at scala.App$class.main(App.scala:76)
	at org.apache.toree.Main$.main(Main.scala:24)
	at org.apache.toree.Main.main(Main.scala)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.spark.deploy.SparkSubmit$.org$apache$spark$deploy$SparkSubmit$$runMain(SparkSubmit.scala:743)
	at org.apache.spark.deploy.SparkSubmit$.doRunMain$1(SparkSubmit.scala:187)
	at org.apache.spark.deploy.SparkSubmit$.submit(SparkSubmit.scala:212)
	at org.apache.spark.deploy.SparkSubmit$.main(SparkSubmit.scala:126)
	at org.apache.spark.deploy.SparkSubmit.main(SparkSubmit.scala)
```

Просидев над этим часок, я понял, что ему не хватает для счасться! Просто выполните ```/etc/hadoop/hadoop-env.sh``` и всё станет хорошо. 

Поздравляю ```kernel ready```!

Все дальнейшие штуки я буду делать в тетрадках. Они будут разделены по папочкам, а когда я закончу я опишу их тут.



