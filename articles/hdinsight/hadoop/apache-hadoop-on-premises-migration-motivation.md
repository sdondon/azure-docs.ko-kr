---
title: '이점: 온-프레미스 Apache Hadoop을 Azure HDInsight로 마이그레이션'
description: 온-프레미스 Hadoop 클러스터를 Azure HDInsight로 마이그레이션하도록 유도하는 동기 부여 및 혜택에 대해 알아봅니다.
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: ashishth
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: how-to
ms.date: 11/15/2019
ms.openlocfilehash: 1de9fc480c753b2497a1ea4e3438583b3582bc96
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87072786"
---
# <a name="migrate-on-premises-apache-hadoop-clusters-to-azure-hdinsight---motivation-and-benefits"></a>온-프레미스 Apache Hadoop 클러스터를 Azure HDInsight로 마이그레이션 - 동기 부여 및 혜택

이 문서는 온-프레미스 Apache Hadoop 에코 시스템 배포를 Azure HDInsight로 마이그레이션하는 모범 사례에 대한 시리즈의 첫 번째 문서입니다. 이 문서 시리즈는 Azure HDInsight에서 Apache Hadoop 솔루션을 설계, 배포 및 마이그레이션하는 책임을 맡고 있는 사람들을 위해 작성되었습니다. 이 문서가 도움이 될만한 역할로는 클라우드 설계자, Hadoop 관리자 및 DevOps 엔지니어가 포함됩니다. 소프트웨어 개발자, 데이터 엔지니어 및 데이터 과학자 또한 여러 종류의 클러스터가 클라우드에서 작동하는 방식에 대한 설명을 읽어보면 도움이 될 것입니다.

## <a name="why-to-migrate-to-azure-hdinsight"></a>Azure HDInsight로 마이그레이션하는 이유

Azure HDInsight는 Hadoop 구성 요소의 클라우드 배포입니다. Azure HDInsight는 대량 데이터를 쉽고 빠르며 비용 효율적으로 처리할 수 있도록 합니다. HDInsight는 다음과 같은 가장 인기 있는 오픈 소스 프레임워크를 포함하고 있습니다.

- Apache Hadoop
- Apache Spark
- Apache Hive with LLAP
- Apache Kafka
- Apache Storm
- Apache HBase
- R

## <a name="azure-hdinsight-advantages-over-on-premises-hadoop"></a>온-프레미스 Hadoop에 비해 Azure HDInsight의 이점

- **저렴한 비용** - [주문형 클러스터를 만들고](../hdinsight-hadoop-create-linux-clusters-adf.md) 사용한 만큼만 지불하여 비용을 줄일 수 있습니다. 컴퓨팅과 스토리지가 분리되어 클러스터 크기에 관계없이 데이터 볼륨이 유지되므로 유연성이 우수합니다.

- **클러스터 만들기 자동화** - 클러스터 만들기를 자동화하려면 최소한의 설치 및 구성이 필요합니다. 주문형 클러스터에 자동화를 사용할 수 있습니다.

- **관리 하드웨어 및 구성** - HDInsight 클러스터를 사용하면 물리적 하드웨어 또는 인프라에 대해 걱정할 필요가 없습니다. 클러스터 구성만 지정하면 Azure가 알아서 설정합니다.

- **쉽게 확장 가능** - HDInsight를 사용하면 워크로드를  [확장](../hdinsight-administer-use-portal-linux.md) 또는 축소할 수 있습니다. Azure는 데이터 처리 작업을 중단하지 않고 데이터 재배포 및 워크로드 리밸런싱을 처리합니다.

- **글로벌 가용성** -HDInsight는 다른 빅 데이터 분석 제품 보다 더 많은 [지역](https://azure.microsoft.com/regions/services/) 에서 사용할 수 있습니다. Azure HDInsight는 주요 통치 지역에서 엔터프라이즈 요구 사항을 충족할 수 있도록 Azure Government, 중국 및 독일에서도 사용할 수 있습니다.

- **보안 및 규정 준수** - HDInsight를 사용하면  [Azure Virtual Network](../hdinsight-plan-virtual-network-deployment.md),  [암호화](../hdinsight-hadoop-create-linux-clusters-with-secure-transfer-storage.md) 및  [Azure Active Directory](../domain-joined/hdinsight-security-overview.md)와 통합을 통해 엔터프라이즈 데이터 자산을 보호할 수 있습니다. 또한 HDInsight는 가장 널리 사용되는 산업 및 정부  [규격 표준](https://azure.microsoft.com/overview/trusted-cloud)을 충족합니다.

- **간소화 된 버전 관리** -Azure HDInsight는 Hadoop 에코 시스템 구성 요소의 버전을 관리 하 고 최신 상태로 유지 합니다. 소프트웨어 업데이트는 일반적으로 온-프레미스 배포를 위한 복잡한 프로세스입니다.

- **구성 요소 간의 종속성이 적은 특정 워크 로드에 대해 최적화 된 작은 클러스터** -일반적인 온-프레미스 Hadoop 설치 프로그램은 다양 한 용도로 사용 되는 단일 클러스터를 사용 합니다. Azure HDInsight를 사용하면 워크로드 관련 클러스터를 만들 수 있습니다. 특정 워크로드에 대한 클러스터를 만들면 복잡성이 점점 증가하는 단일 클러스터를 유지할 필요가 없습니다.

- **생산성** - 원하는 개발 환경에서 다양한 Hadoop 및 Spark용 도구를 사용할 수 있습니다.

- **사용자 지정 도구 또는 타사 애플리케이션을 통해 확장성 제공** - HDInsight 클러스터는 설치된 구성 요소를 통해 확장 가능하며 Azure 마켓플레이스에서 [원클릭](https://azure.microsoft.com/services/hdinsight/partner-ecosystem/) 배포를 사용하여 다른 빅 데이터 솔루션과 통합할 수도 있습니다.

- **간편한 관리, 관리 및 모니터링** -Azure HDInsight는 [Azure Monitor 로그](../hdinsight-hadoop-oms-log-analytics-tutorial.md)와 통합   하 여 모든 클러스터를 모니터링할 수 있는 단일 인터페이스를 제공 합니다.

- **다른 Azure 서비스와 통합** - HDInsight는 다음과 같은 인기 Azure 서비스와 쉽게 통합할 수 있습니다.

    - ADF(Azure Data Factory)
    - Azure Blob Storage
    - Azure Data Lake Storage Gen2
    - Azure Cosmos DB
    - Azure SQL Database
    - Azure Analysis Services

- **자동 복구 프로세스 및 구성 요소** - HDInsight는 자체 모니터링 인프라를 사용하여 지속적으로 인프라 및 오픈 소스 구성 요소를 확인합니다. 또한 오픈 소스 구성 요소 및 노드를 사용할 수 없는 경우처럼 중요한 오류를 자동으로 복구합니다. OSS 구성 요소에 장애가 발생하면 Ambari에서 경고가 트리거됩니다.

자세한 내용은 [Azure HDInsight 및 Apache Hadoop 기술 스택이란?](../hadoop/apache-hadoop-introduction.md) 문서를 참조하세요.

## <a name="migration-planning-process"></a>마이그레이션 계획 프로세스

온-프레미스 Hadoop 클러스터를 Azure HDInsight로 마이그레이션하는 계획을 세울 때에는 다음 단계를 따르는 것이 좋습니다.

1. 현재 온-프레미스 배포 및 토폴로지를 이해합니다.
2. 현재 프로젝트 범위, 타임라인 및 팀 전문 분야를 이해합니다.
3. Azure 요구 사항을 이해합니다.
4. 모범 사례를 기반으로 세부 계획을 작성합니다.

## <a name="gathering-details-to-prepare-for-a-migration"></a>마이그레이션을 준비하기 위한 세부 정보 수집

이 섹션에서는 다음에 대한 중요한 정보를 수집하는 데 도움이 되는 템플릿 설문지를 제공합니다.

- 온-프레미스 배포
- 프로젝트 세부 정보
- Azure 요구 사항

### <a name="on-premises-deployment-questionnaire"></a>온-프레미스 배포 질문

| **질문** | **예제** | **답변** |
|---|---|---|
|**토픽**: **환경**|||
|클러스터 배포 버전|HDP 2.6.5, CDH 5.7|
|빅 데이터 에코시스템 구성 요소|HDFS, Yarn, Hive, LLAP, Impala, Kudu, HBase, Spark, MapReduce, Kafka, Zookeeper, Solr, Sqoop, Oozie, Ranger, Atlas, Falcon, Zeppelin, R|
|클러스터 유형|Hadoop, Spark, Confluent Kafka, Storm, Solr|
|클러스터 수|4|
|마스터 노드 수|2|
|작업자 노드 수|100|
|에 지 노드 수| 5|
|총 디스크 공간|100TB|
|마스터 노드 구성|m/y, cpu, 디스크 등|
|데이터 노드 구성|m/y, cpu, 디스크 등|
|에지 노드 구성|m/y, cpu, 디스크 등|
|HDFS 암호화를 사용합니까?|예|
|고가용성|HDFS HA, Metastore HA|
|재해 복구/백업|백업 클러스터 지원 여부|  
|클러스터에 종속된 시스템|SQL Server, Teradata, Power BI, MongoDB|
|타사 통합|Tableau, GridGain, Qubole, Informatica, Splunk|
|**토픽**: **보안**|||
|경계 보안|방화벽|
|클러스터 인증 및 권한 부여|Active Directory, Ambari, Cloudera Manager, 인증 없음|
|HDFS 액세스 제어|  수동, ssh 사용자|
|Hive 인증 및 권한 부여|Sentry, LDAP, AD with Kerberos, Ranger|
|감사|Ambari, Cloudera Navigator, Ranger|
|모니터링|Graphite, collectd, statsd, Telegraf, InfluxDB|
|경고|Kapacitor, Prometheus, Datadog|
|데이터 보존 기간| 3년, 5년|
|클러스터 관리자|단일 관리자, 다중 관리자|

### <a name="project-details-questionnaire"></a>프로젝트 세부 정보 설문지

|**질문**|**예제**|**답변**|
|---|---|---|
|**토픽**: **워크로드 및 빈도**|||
|MapReduce 작업|10개 작업 -- 하루 2회||
|Hive 작업|100개 작업 -- 1시간마다||
|Spark 일괄 작업|50개 작업 -- 15분마다||
|Spark Streaming 작업|5개 작업 -- 3분마다||
|Structured Streaming 작업|5개 작업 -- 1분마다||
|ML 모델 학습 작업|2개 작업 -- 주당 1회||
|프로그래밍 언어|Python, Scala, Java||
|스크립팅|셸, Python||
|**토픽**: **데이터**|||
|데이터 원본|플랫 파일, Json, Kafka, RDBMS||
|데이터 오케스트레이션|Oozie 워크플로, Airflow||
|메모리 내 조회|Apache Ignite, Redis||
|데이터 대상|HDFS, RDBMS, Kafka, MPP ||
|**토픽**: **메타데이터**|||
|Hive DB 형식|Mysql, Postgres||
|Hive metastore 수|2||
|Hive 테이블 수|100||
|레인저 정책 수|20||
|Oozie 워크플로 수|100||
|**토픽**: **규모**|||
|복제를 비롯한 데이터 볼륨|100TB||
|일일 수집 볼륨|50GB||
|데이터 증가 속도|연 10%||
|클러스터 노드 증가 속도|연 5%
|**토픽**: **클러스터 사용률**|||
|평균 CPU 사용률(%)|60%||
|평균 메모리 사용률(%)|75%||
|디스크 공간 사용률|75%||
|평균 네트워크 사용률(%)|25%
|**토픽**: **직원**|||
|관리자 수|2||
|개발자 수|10||
|최종 사용자 수|100||
|기술|Hadoop, Spark||
|마이그레이션 작업에 사용할 수 있는 리소스의 수|2||
|**토픽**: **제한 사항**|||
|현재 제한 사항|대기 시간이 높음||
|현재 과제|동시성 문제||

### <a name="azure-requirements-questionnaire"></a>Azure 요구 사항 설문지

|**질문**|**예제**|**답변**|
|---|---|---|
|**토픽**: **인프라** |||
| 기본 지역|미국 동부||
|VNet이 기본 설정입니까?|예||
|HA/DR이 필요합니까?|예||
|다른 클라우드 서비스와의 통합 여부|ADF, CosmosDB||
|**토픽**: **데이터 이동**  |||
|초기 로드 기본 설정|DistCp, Data box, ADF, WANDisco||
|데이터 전송 델타|DistCp, AzCopy||
|지속적인 증분 데이터 전송|DistCp, Sqoop||
|**토픽**: **모니터링 및 경고** |||
|Azure와 타사의 모니터링 및 경고 사용 비교|Azure 모니터링 및 경고 사용||
|**토픽**: **보인 기본 설정** |||
|보호되는 프라이빗 데이터 파이프라인인가요?|예||
|도메인 가입 클러스터(ESP)입니까?|     예||
|온-프레미스 AD가 클라우드와 동기화됩니까?|     예||
|동기화 할 AD 사용자의 수|          100||
|암호를 클라우드와 동기화해도 괜찮습니까?|    예||
|클라우드 전용 사용자입니까?|                 예||
|MFA가 필요합니까?|                       아니요|| 
|데이터 권한 부여 요구 사항이 있습니까?|  예||
|역할 기반 액세스 제어를 사용합니까?|        예||
|감사가 필요합니까?|                  예||
|저장 데이터 암호화를 사용합니까?|          예||
|전송 중 데이터 암호화를 사용합니까?|       예||
|**토픽**: **재설계 기본 설정** |||
|단일 클러스터 vs 특정 클러스터 형식|특정 클러스터 형식||
|공동 배치된 스토리지 Vs 원격 스토리지|원격 스토리지||
|데이터로 더 작은 클러스터 크기는 원격으로 저장되나요?|더 작은 클러스터 크기||
|하나의 큰 클러스터 대신 작은 클러스터 여러 개를 사용합니까?|작은 클러스터 여러 개 사용||
|원격 metastore를 사용합니까?|예||
|서로 다른 클러스터 간에 metastore를 공유합니까?|예||
|워크로드를 분해합니까?|Hive 작업을 Spark 작업으로 대체||
|데이터 오케스트레이션에 ADF를 사용합니까?|아니요||

## <a name="next-steps"></a>다음 단계

이 시리즈의 다음 문서를 읽어보세요.

- [온-프레미스에서 Azure HDInsight Hadoop으로 마이그레이션하는 아키텍처 모범 사례](apache-hadoop-on-premises-migration-best-practices-architecture.md)
