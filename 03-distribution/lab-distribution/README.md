# DISTRIBUTION LAB  - Create a build, a release bundle and distribute it to an edge node.

## Prerequisites
A working training lab setup



First go into the maven project folder
```
cd ./example/maven-example
```
### STEP 1 : Configure the JFrog Platform Environment
- Run
  ```
  jf c use devnext
  ```
### STEP 2 : Configure the  Maven Config
- Run
  ```
  jf mvnc --server-id-resolve swampup --server-id-deploy swampup --repo-resolve-releases payment-maven-dev-virtual --repo-resolve-snapshots payment-maven-dev-virtual --repo-deploy-releases payment-maven-dev-virtual --repo-deploy-snapshots payment-maven-dev-virtual
  ```

### STEP 3 : Build Maven Project
- Run 
  ```
  jf mvn clean install -f pom.xml --build-name payment-maven --build-number 2.0.0
  ```

### STEP 4 : Collect environment variables.
- Run 
  ```
  jf rt build-collect-env payment-maven 2.0.0
  ```
### STEP 5 : Collect VCS details from git and add them to a build.
- Run 
  ```
  jf rt build-add-git payment-maven 2.0.0
  ```
### STEP 6 : Publish build info.
- Run 
  ```
  jf rt build-publish payment-maven 2.0.0
  ```
### STEP 7 : Promote build in Artifactory.
- Run 
  ```
  jf rt build-promote payment-maven 2.0.0 payment-maven-qa-local --status='QA candidate' --comment='webservice is now QA candidate and hand over for regression test' --copy=true --props="maintainer=SolEng;stage=qa"
  ```
### STEP 8 : Set properties
- STEP 8 : Run 
  ```
   jf rt sp "payment-maven-qa-local/org/jfrog/test/" "unit.test=pass;"
  ```

### STEP 9 : CREATE RELEASE BUNDLE
- Go back to the root folder of the lab `cd ../..`
- Run 
  ```
  jf ds rbc --spec=rb-spec.json rb_devnext 1.0.0 --desc="release candidate"
  ```

### STEP 10 : SIGN RELEASE BUNDLE
- Run 
  ```
  jf ds rbs rb_devnext 1.0.0
  ```

### STEP 11 : DISTRIBUTE RELEASE BUNDLE
You need to update ``dist-rules.json`` so it will distribute to our own edge.
Example `dsod23loe107` => Go to `Administration > Platform management > Registered JPDs` to find the name to use.

- Run 
  ```
  jf ds rbd --dist-rules=dist-rules.json rb_devnext 1.0.0
  ```
