---
title: 메모리 및 동시성 제한
description: Azure Synapse Analytics에서 다양한 성능 수준과 리소스 클래스에 할당된 메모리 및 동시성 제한을 살펴봅니다.
services: synapse-analytics
author: ronortloff
manager: craigg
ms.service: synapse-analytics
ms.topic: conceptual
ms.subservice: sql-dw
ms.date: 02/04/2020
ms.author: rortloff
ms.reviewer: jrasnick
ms.custom: azure-synapse
ms.openlocfilehash: 5b72694f93ed5b712a0f684887df5b69a7b35c72
ms.sourcegitcommit: bf1340bb706cf31bb002128e272b8322f37d53dd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/03/2020
ms.locfileid: "89441683"
---
# <a name="memory-and-concurrency-limits-for-azure-synapse-analytics"></a>Azure Synapse Analytics에 대한 메모리 및 동시성 제한

Azure Synapse Analytics에서 다양한 성능 수준과 리소스 클래스에 할당된 메모리 및 동시성 제한을 살펴봅니다.  

## <a name="data-warehouse-capacity-settings"></a>데이터 웨어하우스 용량 제한

다음 표에서는 다양한 성능 수준의 데이터 웨어하우스에 대한 최대 용량을 보여줍니다. 성능 수준을 변경하려면 [컴퓨팅 조정 - 포털](quickstart-scale-compute-portal.md)을 참조하세요.

### <a name="service-levels"></a>서비스 수준

서비스 수준은 DW100c에서 DW30000c까지입니다.

| 성능 수준 | 컴퓨팅 노드 | 컴퓨팅 노드당 배포 | 데이터 웨어하우스당 메모리 크기(GB) |
|:-----------------:|:-------------:|:------------------------------:|:------------------------------:|
| DW100c            | 1             | 60                             |    60                          |
| DW200c            | 1             | 60                             |   120                          |
| DW300c            | 1             | 60                             |   180                          |
| DW400c            | 1             | 60                             |   240                          |
| DW500c            | 1             | 60                             |   300                          |
| DW1000c           | 2             | 30                             |   600                          |
| DW1500c           | 3             | 20                             |   900                          |
| DW2000c           | 4             | 15                             |  1200                          |
| DW2500c           | 5             | 12                             |  1500                          |
| DW3000c           | 6             | 10                             |  1800                          |
| DW5000c           | 10            | 6                              |  3000                          |
| DW6000c           | 12            | 5                              |  3600                          |
| DW7500c           | 15            | 4                              |  4500                          |
| DW10000c          | 20            | 3                              |  6000                          |
| DW15000c          | 30            | 2                              |  9000                          |
| DW30000c          | 60            | 1                              | 18000                          |

최대 서비스 수준은 DW30000c이며, 60개 컴퓨팅 노드 및 컴퓨팅 노드당 하나의 배포를 갖추고 있습니다. 예를 들어 DW30000c에서 600TB 데이터 웨어하우스는 컴퓨팅 노드당 약 10TB를 처리합니다.

## <a name="concurrency-maximums-for-workload-groups"></a>작업 그룹의 동시성 최댓값

[작업 그룹](sql-data-warehouse-workload-isolation.md)이 도입되면서 동시성 슬롯의 개념은 더 이상 적용되지 않습니다.  요청당 리소스는 백분율 단위로 할당되고 작업 그룹 정의에 지정됩니다.  그러나 동시성 슬롯을 제거하더라도 서비스 수준에 따라 쿼리당 필요한 최소한의 리소스가 있습니다.  아래 표에는 서비스 수준에 걸쳐 쿼리당 필요한 최소 리소스 양과 달성할 수 있는 관련 동시성이 정의되어 있습니다.

|서비스 수준|최대 동시 쿼리 수|REQUEST_MIN_RESOURCE_GRANT_PERCENT에 대해 지원되는 최소 %|
|---|---|---|
|DW100c|4|25%|
|DW200c|8|12.5%|
|DW300c|12|8%|
|DW400c|16|6.25%|
|DW500c|20|5%|
|DW1000c|32|3%|
|DW1500c|32|3%|
|DW2000c|48|2%|
|DW2500c|48|2%|
|DW3000c|64|1.5%|
|DW5000c|64|1.5%|
|DW6000c|128|0.75%|
|DW7500c|128|0.75%|
|DW10000c|128|0.75%|
|DW15000c|128|0.75%|
|DW30000c|128|0.75%|
||||

## <a name="concurrency-maximums-for-resource-classes"></a>리소스 클래스의 동시성 최댓값

각 쿼리에 효율적으로 실행할 수 있을 만큼 충분한 리소스가 있는지 확인하기 위해 Synapse SQL은 각 쿼리에 동시성 슬롯을 할당하여 리소스 사용률을 추적합니다. 시스템은 중요도 및 동시성 슬롯을 기반으로 쿼리를 큐에 넣습니다. 쿼리는 충분한 동시성 슬롯을 사용할 수 있을 때까지 큐에서 대기합니다. [중요도](sql-data-warehouse-workload-importance.md) 및 동시성 슬롯은 CPU 우선 순위를 결정합니다. 자세한 내용은 [워크로드 분석](analyze-your-workload.md)을 참조하세요.

**정적 리소스 클래스**

다음 표에는 각 [정적 리소스 클래스](resource-classes-for-workload-management.md)에 대한 최대 동시 쿼리 수 및 동시성 슬롯 수가 나와 있습니다.  

| 서비스 수준 | 최대 동시 쿼리 수 | 사용 가능한 동시성 슬롯 수 | staticrc10에서 사용되는 슬롯 | staticrc20에서 사용되는 슬롯 | staticrc30에서 사용되는 슬롯 | staticrc40에서 사용되는 슬롯 | staticrc50에서 사용되는 슬롯 | staticrc60에서 사용되는 슬롯 | staticrc70에서 사용되는 슬롯 | staticrc80에서 사용되는 슬롯 |
|:-------------:|:--------------------------:|:---------------------------:|:---------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|
| DW100c        |  4                         |    4                        | 1         | 2          | 4          | 4          | 4         |  4         |  4         |  4         |
| DW200c        |  8                         |    8                        | 1         | 2          | 4          | 8          |  8         |  8         |  8         |  8        |
| DW300c        | 12                         |   12                        | 1         | 2          | 4          | 8          |  8         |  8         |  8         |   8        |
| DW400c        | 16                         |   16                        | 1         | 2          | 4          | 8          | 16         | 16         | 16         |  16        |
| DW500c        | 20                         |   20                        | 1         | 2          | 4          | 8          | 16         | 16         | 16         |  16        |
| DW1000c       | 32                         |   40                        | 1         | 2          | 4          | 8          | 16         | 32         | 32         |  32        |
| DW1500c       | 32                         |   60                        | 1         | 2          | 4          | 8          | 16         | 32         | 32         |  32        |
| DW2000c       | 48                         |   80                        | 1         | 2          | 4          | 8          | 16         | 32         | 64         |  64        |
| DW2500c       | 48                         |  100                        | 1         | 2          | 4          | 8          | 16         | 32         | 64         |  64        |
| DW3000c       | 64                         |  120                        | 1         | 2          | 4          | 8          | 16         | 32         | 64         |  64        |
| DW5000c       | 64                         |  200                        | 1         | 2          | 4          | 8          | 16         | 32         | 64         | 128        |
| DW6000c       | 128                        |  240                        | 1         | 2          | 4          | 8          | 16         | 32         | 64         | 128        |
| DW7500c       | 128                        |  300                        | 1         | 2          | 4          | 8          | 16         | 32         | 64         | 128        |
| DW10000c      | 128                        |  400                        | 1         | 2          | 4          | 8          | 16         | 32         | 64         | 128        |
| DW15000c      | 128                        |  600                        | 1         | 2          | 4          | 8          | 16         | 32         | 64         | 128        |
| DW30000c      | 128                        | 1200                        | 1         | 2          | 4          | 8          | 16         | 32         | 64         | 128        |

**동적 리소스 클래스**

다음 표에는 각 [동적 리소스 클래스](resource-classes-for-workload-management.md)에 대한 최대 동시 쿼리 수 및 동시성 슬롯 수가 나와 있습니다. 동적 리소스 클래스는 모든 서비스 수준에 걸쳐 small, medium, large, xlarge 리소스 클래스에 각각 3, 10, 22, 70%의 메모리 백분율 할당을 사용합니다.

| 서비스 수준 | 최대 동시 쿼리 수 | 사용 가능한 동시성 슬롯 수 | smallrc에서 사용되는 슬롯 | mediumrc에서 사용되는 슬롯 | largerc에서 사용되는 슬롯 | xlargerc에서 사용되는 슬롯 |
|:-------------:|:--------------------------:|:---------------------------:|:---------------------:|:----------------------:|:---------------------:|:----------------------:|
| DW100c        |  4                         |    4                        | 1                     |  1                     |  1                    |   2                    |
| DW200c        |  8                         |    8                        | 1                     |  1                     |  1                    |   5                    |
| DW300c        | 12                         |   12                        | 1                     |  1                     |  2                    |   8                    |
| DW400c        | 16                         |   16                        | 1                     |  1                     |  3                    |  11                    |
| DW500c        | 20                         |   20                        | 1                     |  2                     |  4                    |  14                    |
| DW1000c       | 32                         |   40                        | 1                     |  4                     |  8                    |  28                    |
| DW1500c       | 32                         |   60                        | 1                     |  6                     |  13                   |  42                    |
| DW2000c       | 32                         |   80                        | 2                     |  8                     |  17                   |  56                    |
| DW2500c       | 32                         |  100                        | 3                     | 10                     |  22                   |  70                    |
| DW3000c       | 32                         |  120                        | 3                     | 12                     |  26                   |  84                    |
| DW5000c       | 32                         |  200                        | 6                     | 20                     |  44                   | 140                    |
| DW6000c       | 32                         |  240                        | 7                     | 24                     |  52                   | 168                    |
| DW7500c       | 32                         |  300                        | 9                     | 30                     |  66                   | 210                    |
| DW10000c      | 32                         |  400                        | 12                    | 40                     |  88                   | 280                    |
| DW15000c      | 32                         |  600                        | 18                    | 60                     | 132                   | 420                    |
| DW30000c      | 32                         | 1200                        | 36                    | 120                    | 264                   | 840                    |

쿼리 실행을 시작할 수 있는 동시성 슬롯이 충분하지 않은 경우 쿼리는 중요도에 따라 큐에 대기되고 실행됩니다.  중요도가 동일한 경우 쿼리는 선입 선출 방식으로 실행됩니다.  쿼리가 완료 되 고 쿼리 및 슬롯의 수가 한도 미만으로 떨어지면 Azure Synapse Analytics는 대기 중인 쿼리를 해제 합니다.

## <a name="next-steps"></a>다음 단계

리소스 클래스를 활용하여 워크로드를 추가로 최적화하는 방법에 대한 자세한 내용은 다음 문서를 검토하세요.

* [워크로드 관리를 위한 리소스 클래스](resource-classes-for-workload-management.md)
* [워크로드 분석](analyze-your-workload.md)
