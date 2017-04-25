# Assignment-15.3
Deployment :
It is important to have a standard deployment that results from installing the packages regardless of the package manager. Here are the top level directories and a sample of what would be under each. Note that all of the packages are installed "flattened" into the prefix directory. For compatibility reasons, we should create "share/hadoop" that matches the old HADOOP_HOME and set the HADOOP_HOME variable to that.

        $PREFIX/ bin / hadoop
               |     | mapred
               |     | pig -> pig7
               |     | pig6
               |     + pig7
               |
               + etc / hadoop / core-site.xml
               |              | hdfs-site.xml
               |              + mapred-site.xml
               |
               + include / hadoop / Pipes.hh
               |         |        + TemplateFactory.hh
               |         + hdfs.h
               |
               + lib / jni / hadoop-common / libhadoop.so.0.20.0
               |     |
               |     | libhdfs.so -> libhdfs.so.0.20.0
               |     + libhdfs.so.0.20.0
               |
               + libexec / task-controller
               |
               + man / man1 / hadoop.1
               |            | mapred.1
               |            | pig6.1
               |            + pig7.1
               |
               + share / hadoop-common 
               |       | hadoop-hdfs
               |       | hadoop-mapreduce
               |       | pig6
               |       + pig7
               |
               + sbin / hdfs-admin
               |      | mapred-admin
               |
               + src / hadoop-common
               |     | hadoop-hdfs
               |     + hadoop-mapreduce
               |
               + var / lib / data-node
                     |     + task-tracker
                     |
                     | log / hadoop-datanode
                     |     + hadoop-tasktracker
                     |
                     + run / hadoop-datanode.pid
                           + hadoop-tasktracker.pid
        
Note that we must continue to honor HADOOP_CONF_DIR to override the configuration location, but that it should default to $prefix/etc.
User facing binaries and scripts go into bin. Configuration files go into etc with multiple configuration files having a directory. JNI
shared libraries go into lib/jni/$tool since Java does not allow to specify the version of the library to load. Libraries that aren't
loaded via System.loadLibrary are placed directly under lib. 64 bit versions of the libraries for platforms that support them should be
placed in lib64. All of the architecture-independent pieces, including the jars for each tool will be placed in share/$tool. The default
location for all the run time information will be in var. The storage will be in var/lib, the logs in var/log and the pid files in
var/run.
