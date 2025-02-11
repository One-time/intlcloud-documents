본 문서는 주로 GooseFS 빠른 배포, 디버깅 관련 가이드를 제공합니다. 로컬 기기에 GooseFS를 배포하고 COS(Cloud Object Storage)를 원격 스토리지로 만드는 가이드를 제공하며, 구체적인 순서는 다음과 같습니다.


## 전제 조건

GooseFS 사용 전 아래 작업을 준비해야 합니다.

1. COS 서비스에서 버킷을 생성해 원격 스토리지로 만듭니다. 작업 가이드에 대한 자세한 내용은 [콘솔 시작하기](https://intl.cloud.tencent.com/document/product/436/32955)를 참고하십시오.
2. [Java 8 또는 이후 버전](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html)을 설치합니다.
3. SSH를 통한 LocalHost 연결과 원격 로그인이 가능하도록 [SSH](https://www.ssh.com/ssh/)를 설치합니다.

## GooseFS 다운로드 및 구성

1. 공식 홈페이지 라이브러리에서 GooseFS 설치 패키지를 로컬에 다운로드 합니다. 다운로드 링크: [goosefs-1.1.0-bin.tar.gz](https://cos-data-lake-release-1253960454.cos.ap-guangzhou.myqcloud.com/goosefs/1.1.0/release/goosefs-1.1.0-bin.tar.gz).
2. 아래 명령어를 실행하여 설치 패키지의 압축을 해제합니다.
```shell
tar -zxvf goosefs-1.1.0-bin.tar.gz
cd goosefs-1.1.0
```
 압축 해제 후 gooseFS의 홈 디렉터리인 goosefs-1.1.0이 생성됩니다. 아래 문장에서는 해당 디렉터리의 절대 경로를 `${GOOSEFS_HOME}`으로 대신합니다.
3. `${GOOSEFS_HOME}/conf`의 디렉터리에 `conf/goosefs-site.properties`의 구성 파일을 생성하여 내장된 설정 템플릿을 사용할 수 있습니다.
```shell
$ cp conf/goosefs-site.properties.template conf/goosefs-site.properties
```
4. 구성 파일 `conf/goosefs-site.properties`에서 goosefs.master.hostname을 `localhost`로 설정합니다.
```shell
$ echo"goosefs.master.hostname=localhost">> conf/goosefs-site.properties
```

## GooseFS 활성화

1. GooseFS 활성화 전에 GooseFS가 로컬 환경에서 정확히 실행될 수 있도록 시스템 환경 검사를 진행합니다.
```shell
$ goosefs validateEnv local
```
2. GooseFS 활성화 전 아래 명령어를 실행하여 GooseFS를 포맷합니다. 해당 명령어는 GooseFS의 로그와 `worker` 스토리지 디렉터리의 내용을 삭제합니다.
```shell
$ goosefs format
```
3. 아래 명령어를 실행하여 GooseFS를 활성화할 수 있으며, GooseFS가 Master와 Worker를 각각 하나씩 실행하도록 시스템이 기본 설정 되어있습니다.
```shell
$ ./bin/goosefs-start.sh local SudoMount
```
 해당 명령어 실행을 완료한 후 http://localhost:9201과 http://localhost:9204에 액세스하여 Master와 Worker의 실행 상태를 각각 확인할 수 있습니다.

## GooseFS를 통해 COS(COSN) 혹은 Tencent Cloud HDFS (CHDFS)를 마운트합니다.

GooseFS가 COS(COSN）혹은 Tencent Cloud HDFS(CHDFS)를 GooseFS의 루트 경로에 마운트 해야하는 경우, 우선 `conf/core-site.xml` 구성에서 COSN 혹은 CHDFS의 필수 구성 항목을 지정해야 하고, 이는 `fs.cosn.impl`, `fs.AbstractFileSystem.cosn.impl`, `fs.cosn.userinfo.secretId`, `fs.cosn.userinfo.secretKey` 등을 포함하며 이에 국한되지 않습니다. 예시:

```xml

<!-- COSN related configurations -->
<property>
  <name>fs.cosn.impl</name>
  <value>org.apache.hadoop.fs.CosFileSystem</value>
</property>



<property>
   <name>fs.AbstractFileSystem.cosn.impl</name>
   <value>com.qcloud.cos.goosefs.CosN</value>
</property>



<property>
    <name>fs.cosn.userinfo.secretId</name>
    <value></value>
</property>



<property>
    <name>fs.cosn.userinfo.secretKey</name>
    <value></value>
</property>



<property>
    <name>fs.cosn.bucket.region</name>
    <value></value>
</property>



<!-- CHDFS related configurations -->
<property>
   <name>fs.AbstractFileSystem.ofs.impl</name>
   <value>com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter</value>
</property>



<property>
   <name>fs.ofs.impl</name>
   <value>com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter</value>
</property>



<property>
   <name>fs.ofs.tmp.cache.dir</name>
   <value>/data/chdfs_tmp_cache</value>
</property>



<!--appId-->      
<property>
   <name>fs.ofs.user.appid</name>
   <value>1250000000</value>
</property>

```

>?
>- COSN의 완전한 구성은 [Hadoop 툴](https://intl.cloud.tencent.com/document/product/436/6884)을 참고하십시오.
>- CHDFS의 완전한 구성은 CHDFS 마운트 를 참고하십시오.

다음으로 Namespace 생성을 통해 COS 혹은 CHDFS를 마운트 하는 방법과 절차를 소개합니다.

1. 네임스페이스 Namespace 하나를 생성하여 COS를 마운트합니다.

```shell
$ goosefs ns create myNamespace cosn://bucketName-1250000000/3TB \
--secret fs.cosn.userinfo.secretId=AKXXXXXXXXXXX \
--secret fs.cosn.userinfo.secretKey=XXXXXXXXXXXX \
--attribute fs.cosn.bucket.region=ap-xxx \
```

>! 
> - COSN을 마운트한 namespace를 생성할 경우 반드시 `- -secret` 매개변수를 사용하여 액세스 키를 지정해야 하며, `--attribute`를 사용하여  Hadoop-COS (COSN)의 모든 필수 매개변수를 지정해야 합니다. 구체적인 필수 매개변수는 [Hadoop 툴](https://intl.cloud.tencent.com/document/product/436/6884)을 참고하십시오.
> - Namespace 생성 시 읽기/쓰기 정책 (rPolicy/wPolicy)을 지정하지 않았을 경우 구성 파일 중에 지정한 read/write type 혹은 기본값 (CACHE/CACHE_THROUGH)을 사용합니다.
>
동일한 방법으로 네임스페이스 namespace 하나를 생성하여 Tencent Cloud HDFS 마운트에 사용할 수 있습니다.
```shell
goosefs ns create MyNamespaceCHDFS ofs://xxxxx-xxxx.chdfs.ap-guangzhou.myqcloud.com/3TB \
--attribute fs.ofs.user.appid=1250000000
--attribute fs.ofs.tmp.cache.dir=/tmp/chdfs
```
2. 생성 완료 후 `list` 명령어를 통해 클러스터에 생성된 모든 namespace를 나열할 수 있습니다.

```shell
$ goosefs ns list
namespace	      mountPoint	       ufsPath                     	 creationTime                wPolicy      	rPolicy	     TTL	   ttlAction
myNamespace    /myNamespace   cosn://bucketName-125xxxxxx/3TB  03-11-2021 11:43:06:239      CACHE_THROUGH   CACHE        -1      DELETE
myNamespaceCHDFS /myNamespaceCHDFS ofs://xxxxx-xxxx.chdfs.ap-guangzhou.myqcloud.com/3TB 03-11-2021 11:45:12:336 CACHE_THROUGH   CACHE  -1  DELETE
```

3. 아래 명령어를 실행하여 namespace의 세부 정보를 지정합니다.

```shell
$ goosefs ns stat myNamespace

NamespaceStatus{name=myNamespace, path=/myNamespace, ttlTime=-1, ttlAction=DELETE, ufsPath=cosn://bucketName-125xxxxxx/3TB, creationTimeMs=1615434186076, lastModificationTimeMs=1615436308143, lastAccessTimeMs=1615436308143, persistenceState=PERSISTED, mountPoint=true, mountId=4948824396519771065, acl=user::rwx,group::rwx,other::rwx, defaultAcl=, owner=user1, group=user1, mode=511, writePolicy=CACHE_THROUGH, readPolicy=CACHE}
```

메타데이터에서 기록한 정보는 아래 내용이 포함됩니다.

| 번호 | 매개변수                   | 설명 |
| ---- | ---------------------- | ----- |
| 1    | name                   | namespace 이름 |
| 2    | path                   | GooseFS에서 namespace의 경로 |
| 3    | ttlTime                | namespace 디렉터리와 파일의 ttl 주기 |
| 4    | ttlAction              | namespace 디렉터리와 파일의 ttl 처리 작업에는 FREE와 DELETE 두 가지 처리 작업이 있습니다. 기본값: FREE |
| 5    | ufsPath                | ufs에서 namespace의 마운트 경로 |
| 6    | creationTimeMs         | namespace 생성 시간, 단위: 밀리초 |
| 7    | lastModificationTimeMs | namespace 디렉터리와 파일의 최종 수정 시간, 단위: 밀리초 |
| 8    | persistenceState       | namespace의 지속 상태 |
| 9    | mountPoint             | namespace의 마운트 포인트가 하나인지에 대한 여부, 값은 항상 true |
| 10   | mountId                | namespace 마운트 포인트 ID |
| 11   | acl                    | namespace의 액세스 제어 리스트 |
| 12   | defaultAcl             | namespace의 기본 액세스 제어 리스트 |
| 13   | owner                  | namespace의 owner |
| 14   | group                  | namespace의 owner가 소속된 group |
| 15   | mode                   | namespace의 POSIX 권한 |
| 16   | writePolicy            | namespace의 쓰기 정책 |
| 17   | readPolicy             | namespace의 읽기 정책 |


## GooseFS를 통한 Table의 데이터 프리패치

1. GooseFS는 Hive Table의 데이터를  GooseFS에 프리패치할 수 있습니다. 프리패치 전에 관련 DB를 GooseFS에 연결해야 하며, 관련 명령어는 아래와 같습니다.

```shell
$ goosefs table attachdb --db test_db hive thrift://
172.16.16.22:7004 test_for_demo
```

>! 명령어의 thrift는 실제 Hive Metastore 주소를 입력해야 합니다.
>
2. DB 추가 후 ls 명령어를 통해 현재 연결 중인 DB와 Table 정보를 확인할 수 있습니다.

```shell
$ goosefs table ls test_db web_page

OWNER: hadoop
DBNAME.TABLENAME: testdb.web_page (
   wp_web_page_sk bigint,
   wp_web_page_id string,
   wp_rec_start_date string,
   wp_rec_end_date string,
   wp_creation_date_sk bigint,
   wp_access_date_sk bigint,
   wp_autogen_flag string,
   wp_customer_sk bigint,
   wp_url string,
   wp_type string,
   wp_char_count int,
   wp_link_count int,
   wp_image_count int,
   wp_max_ad_count int,
)
PARTITIONED BY (
)
LOCATION (
   gfs://172.16.16.22:9200/myNamespace/3000/web_page
)
PARTITION LIST (
   {
   partitionName: web_page
   location: gfs://172.16.16.22:9200/myNamespace/3000/web_page
   }
)
```

3. load 명령어를 통해 Table의 데이터를 프리패치합니다.

```shell
$ goosefs table load test_db web_page
Asynchronous job submitted successfully, jobId: 1615966078836
```

 Table의 데이터 프리패치는 비동기화 작업이므로 작업 ID 하나를 반환합니다. goosefs job stat &lt;Job Id> 명령어를 통해 프리패치 작업의 진행률을 확인할 수 있습니다. "COMPLETED" 상태가 되면 전체 프리패치 과정이 완료되었음을 의미합니다.

## GooseFS를 사용하여 파일 업로드와 다운로드 작업 실행

1. GooseFS는 대부분의 파일 시스템 작업 명령어를 지원하며, 다음 명령어를 통해 현재 지원하는 명령어 리스트를 확인할 수 있습니다.

```shell
$ goosefs fs
```

2. `ls` 명령어를 통해 GooseFS의 파일을 나열할 수 있습니다. 다음 예시에서 루트 디렉터리의 모든 파일을 나열하는 방법을 확인할 수 있습니다.

```shell
$ goosefs fs ls /
```

3. `copyFromLocal` 명령어를 통해 데이터를 로컬에서 GooseFS로 복사할 수 있습니다.

```shell
$ goosefs fs copyFromLocal LICENSE /LICENSE
Copied LICENSE to /LICENSE
$ goosefs fs ls /LICENSE
-rw-r--r--  hadoop         supergroup               20798       NOT_PERSISTED 03-26-2021 16:49:37:215   0% /LICENSE
```

4. `cat` 명령어를 통해 파일 내용을 확인할 수 있습니다.

```shell
$ goosefs fs cat /LICENSE                                                                         
Apache License
Version 2.0, January 2004
http://www.apache.org/licenses/
TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION
...
```

5. GooseFS는 로컬 디스크를 하부 파일 시스템으로 사용하는 것으로 기본 설정되어 있으며, 기본 파일 시스템 경로는 `./underFSStorage`입니다. `persist` 명령어를 통해 파일을 로컬 파일 시스템에 영속 저장할 수 있습니다.

```shell
$ goosefs fs persist /LICENSE
persisted file /LICENSE with size 26847
```

## GooseFS를 사용하여 신속하게 파일 업로드/다운로드

1. CFS 상태를 검사하여 파일이 캐시 되었는지 확인합니다. 파일 상태가 `PERSISTED`인 경우 파일이 메모리에 저장된 것을 의미하며, 파일 상태가 `NOT_PERSISTED`인 경우 파일이 메모리에 없음을 의미합니다.

```shell
$ goosefs fs ls /data/cos/sample_tweets_150m.csv
-r-x------ staff  staff 157046046 NOT_PERSISTED 01-09-2018 16:35:01:002   0% /data/cos/sample_tweets_150m.csv
```
2. 파일에 단어 'tencent'가 몇 개 있는지 통계를 낸 후 작업 소요 시간을 계산합니다.

```shell
$ time goosefs fs cat /data/s3/sample_tweets_150m.csv | grep-c kitten
889
real	0m22.857s
user	0m7.557s
sys	0m1.181s
```

3. 해당 데이터를 메모리에 캐시하여 조회 속도를 효과적으로 향상 시킬 수 있습니다. 자세한 예시는 아래와 같습니다.

```shell
$ goosefs fs ls /data/cos/sample_tweets_150m.csv
-r-x------ staff  staff 157046046 
ED 01-09-2018 16:35:01:002   0% /data/cos/sample_tweets_150m.csv
$ time goosefs fs cat /data/s3/sample_tweets_150m.csv | grep-c kitten
889
real	0m1.917s
user	0m2.306s
sys	    0m0.243s
```

 시스템 프로세스 딜레이가 1.181s에서 0.243s로 감소되어 10배 향상된 것을 알 수 있습니다.

## GooseFS 비활성화

아래 명령어를 통해 GooseFS를 비활성화할 수 있습니다.

```shell
$ ./bin/goosefs-stop.sh local
```
