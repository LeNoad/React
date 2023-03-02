# maven-deploy-plugin

>Maven Deploy Plugin은 deploy phase에서 동작하는 플러그인으로 remote repository에 artifact를 올리는 기능을 수행한다.

### 제대로 동작하기 위해서는 다음 정보가 필요하다
- repository에 대한 정보 (location, URL, 전송방법(FTP, SCP, SFTP...etc)) 그리고 인증이 필요한 계정정보
- artifacts에 대한 정보 - group, artifact, version, packaging, classifier
- a deployer: a method to actually perform the deployment.<br/>
(This can be implemented as a wagon transport use a system specific method)


# Goals
## 두 개의 goals를 갖고 있다.
1. >deploy:deploy is used to automatically install the artifact, its pom and the attached artifacts produced by a particular project. Most if not all of the information related to the deployment is stored in the project's pom.
2. >deploy:deploy-file is used to install a single artifact along with its pom. In that case the artifact information can be taken from an optionally specified pomFile, but can be completed/overriden using the command line.

# Usage
## deploy:deploy
deploy:deploy Mojo 를 활성화하려면 `<distributionManagement>` 가 POM 파일에 포함되고 `<repository/>` 정보에 remote 정보가 있어야 한다. release 와 snapshot repository 를 분리해서 사용한다면 `<snapshotRepository/>` 를 별도로 기술할수 있다. 마지막으로 project website 를 deploy 하려면 `<site/>` 항목을 기술해야 한다.

POM 파일에 repository 접근 계정을 기록하면 보안문제가 있을 수 있으므로 repository 정보만 기술하고 해당 id 의 계정 정보는 settings.xml 에 기술할 수 있다.

>pom.xml
```xml
[...]
  <distributionManagement>   
    <repository>
      <id>internal.repo</id>
      <name>MyCo Internal Repository</name>
      <url>Host to Company Repository</url>
    </repository>
    <snapshotRepository>
      <uniqueVersion>true</uniqueVersion>
      <id>snapshot.repo</id>
      <name>Project Snapshots</name>
      <url>Host to Snapshot Repository</url>
    </snapshotRepository>
  </distributionManagement>
[...]
```

>settings.xml
```xml
[...]
    <server>
      <!-- id 가 pom.xml 에 기술된 것과 일치해야 한다. -->
      <id>internal.repo</id>
      <username>maven</username>
      <password>foobar</password>
    </server>
[...]
```

plain text password를 넣기 부담스럽다면 maven repository 계정 정보 암호화를 하는방법이 존재한다. 참고해서 암호화된 password를 적용한다. 설정이 완료되었으면 deploy 를 실행해서 정상 설정 여부를 확인한다.

```code
mvn deploy -DrepositoryId=internal.repo
```

## deploy:deploy-file
원격 저장소에 아티팩트를 디플로이한다. 
```code
mvn deploy:deploy-file -Durl=file://C:\m2-repo \
                       -DrepositoryId=some.id \
                       -Dfile=your-artifact-1.0.jar \
                       [-DpomFile=your-pom.xml] \
                       [-DgroupId=org.some.group] \
                       [-DartifactId=your-artifact] \
                       [-Dversion=1.0] \
                       [-Dpackaging=jar] \
                       [-Dclassifier=test] \
                       [-DgeneratePom=true] \
                       [-DgeneratePom.description="My Project Description"] \
                       [-DrepositoryLayout=legacy] \
                       [-DuniqueVersion=false]
```

