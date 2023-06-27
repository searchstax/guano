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
2. Update the version no. in `pom.xml`. (Upstream project uses three digit version no to track the changes. We append another digit to track SearchStax related changes).
3. From project root, execute: `mvn clean install -Dfindbugs.skip=true -DskipTests`
  a. This will generate `guano-<version>.jar` binary in `target/` directory.

## Upload Jar to s3
#### QA: 
https://s3.console.aws.amazon.com/s3/buckets/ss-deployment-artifacts-qa?prefix=searchstax/solr/&region=us-east-1
#### Staging: 
https://s3.console.aws.amazon.com/s3/buckets/ss-deployment-artifacts-staging?region=us-west-1&prefix=searchstax/solr/
#### PROD: 
https://s3.console.aws.amazon.com/s3/buckets/searchstax-repo-f3g03kdjf?region=us-east-1&prefix=searchstax/solr/&showversions=false

https://s3.console.aws.amazon.com/s3/buckets/searchstax-repo-f3g03kdjf-frankfurt?region=eu-central-1&prefix=searchstax/solr/&showversions=false

1. The jar needs to be uploaded to all the 4 buckets listed above.
2. Generate checksum for the jar file using below command. Replace the version accordingly below
  a. `sha1sum guano-<version>.jar >> guano-<version>.jar.sha1`
3. Upload both the following files to s3,
  a. guano-<version>.jar
  b. guano-<version>.jar.sha1

## Use this jar
Update all the searchstax/deploy/automation_settings_*.py files and replace the `GUANO=guano-<version>.jar` variable as per the version needed.

## Note on Existing/old Deployments
If there are existing/old deployments that are using the old guano jar version, then they need to be manually updated to the latest version as required.
