### mvn 把本地的jar包 deploy到远程私服



```
 mvn deploy:deploy-file -DgroupId=com.jikabao -DartifactId=possdk -Dversion=0.7.0-SNAPSHOT -Dpackaging=jar -Dfile=/Users/jz/.m2/repository/com/jikabao/possdk/0.7.4-SNAPSHOT/possdk-0.7.4-SNAPSHOT.jar  -Durl=http://repo.hualala.com/nexus/content/repositories/snapshots/ -DrepositoryId=hualala-snapshots -DgeneratePom=true -DpomFile=/Users/jz/.m2/repository/com/jikabao/possdk/0.7.4-SNAPSHOT/possdk-0.7.4-SNAPSHOT.pom

```

