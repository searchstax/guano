# d2fn/guano fork

This is a fork of the d2fn/guano repo which is under MIT license. We can use and edit this code freely as long as we carry the license file along.

    usage: guano

      -s,--server <arg>          the zookeeper remote server to connect to (ie
                                 "localhost:2181"
                                 
      -d,--dump-znode <arg>      the znode to dump (recursively)
      -o,--output-dir <arg>      the output directory to which znode
                                 information should be written (must be a
                                 normal, empty directory)
                                 
      -i,--input-dir <arg>       the input directory from which znode
                                 information should be read
      -r,--restore-znode <arg>   the znode into which read data should be
                                 restored

      -v,--verbose               enable debug output

## Code/Jar Build Instructions
Follow below steps to release a new version when any of the above mentioned changes are made.
1. Modify files as required.
2. Update the version no. in `pom.xml`.
3. From project root, execute: `mvn clean install -Dfindbugs.skip=true -DskipTests`
  a. This will generate `guano-<version>.jar` binary in `target/` directory.
