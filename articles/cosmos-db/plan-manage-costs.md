---
title: Azure Cosmos DB에 대 한 비용 계획 및 관리
description: Azure Portal에서 비용 분석을 사용 하 여 Azure Cosmos DB에 대 한 비용을 계획 하 고 관리 하는 방법을 알아봅니다.
author: SnehaGunda
ms.author: sngun
ms.custom: subject-cost-optimization
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 08/19/2020
ms.openlocfilehash: 7f0a8fcb841399eb910f5f043cc75ddad037ee30
ms.sourcegitcommit: d661149f8db075800242bef070ea30f82448981e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88606869"
---
# <a name="plan-and-manage-costs-for-azure-cosmos-db"></a>Azure Cosmos DB에 대 한 비용 계획 및 관리

이 문서에서는 Azure Cosmos DB에 대 한 비용을 계획 하 고 관리 하는 방법을 설명 합니다.

- 리소스를 만들기 전에 비용을 예측 합니다.
- 리소스 사용을 시작 하는 예상 비용 검토
- 비용 관리 기능을 사용 하 여 예산 및 모니터링 비용 설정
- 예상 비용을 검토 하 고 지출 추세를 식별 하 여 작업할 수 있는 영역을 표시 합니다.

Azure Cosmos DB에 대 한 비용은 Azure 청구서의 월별 비용 중 일부일 뿐입니다. 다른 Azure 서비스를 사용 하는 경우 타사 서비스를 포함 하 여 Azure 구독에 사용 되는 모든 Azure 서비스 및 리소스에 대 한 요금이 청구 됩니다. 이 문서에서는 Azure Cosmos DB에 대 한 비용을 계획 하 고 관리 하는 방법을 설명 합니다. Azure Cosmos DB에 대 한 비용 관리에 익숙해 졌으 면 구독에 사용 되는 모든 Azure 서비스에 대 한 비용을 관리 하는 비슷한 방법을 적용할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

비용 분석은 다양한 종류의 Azure 계정 유형을 지원합니다. 지원되는 계정 유형의 전체 목록을 보려면 [Cost Management 데이터 이해](../cost-management-billing/costs/understand-cost-mgt-data.md)를 참조하세요. 비용 데이터를 보려면 적어도 Azure 계정에 대한 읽기 권한이 필요합니다. Azure Cost Management 데이터에 액세스하는 방법에 대한 정보는 [데이터에 대한 액세스 할당](../cost-management-billing/costs/assign-access-acm-data.md)을 참조하세요.

## <a name="provisioned-throughput-or-serverless"></a>프로 비전 된 처리량 또는 서버 리스

Azure Cosmos DB는 [프로 비전 된 처리량](set-throughput.md) 및 [서버](serverless.md)를 사용 하지 않는 두 가지 유형의 용량 모드를 지원 합니다. Azure Cosmos DB 사용에 대 한 요금이 청구 되는 방식은 이러한 두 모드 사이에서 매우 다양 하므로 워크 로드에 가장 적합 한 것을 선택 하는 것이 중요 합니다. 이 선택을 수행 하는 방법에 대 한 지침과 권장 사항은 [프로 비전 된 처리량과 서버 리스 서버 간 선택 방법](throughput-serverless.md) 문서를 참조 하세요.

## <a name="estimating-provisioned-throughput-costs-with-capacity-calculator"></a>용량 계산기를 사용 하 여 프로 비전 된 처리량 비용 예측

프로 비전 된 처리량 모드에서 Azure Cosmos DB를 사용 하려는 경우 Azure Cosmos 계정에 리소스를 만들기 전에 [Azure Cosmos DB 용량 계산기](https://cosmos.azure.com/capacitycalculator/) 를 사용 하 여 비용을 예측 합니다. 용량 계산기는 워크 로드에 필요한 처리량 및 비용의 추정치를 얻는 데 사용 됩니다. 적절 한 크기의 프로 비전 된 처리량을 사용 하 여 Azure Cosmos 데이터베이스 및 컨테이너를 구성 하거나 작업에 대 한 [요청 단위 (r u/초)](request-units.md)를 구성 하는 것은 비용과 성능을 최적화 하는 데 필요 합니다. API 형식, 지역 수, 항목 크기, 초당 읽기/쓰기 요청, 예상 비용을 얻기 위해 저장 된 총 데이터 등의 세부 정보를 입력 해야 합니다. 용량 계산기에 대해 자세히 알아보려면 [예상](estimate-ru-with-capacity-planner.md) 문서를 참조 하세요.

다음 스크린샷은 용량 계산기를 사용 하 여 처리량 및 비용 예측을 보여 줍니다.

:::image type="content" source="./media/plan-manage-costs/capacity-calculator-cost-estimate.png" alt-text="Azure Cosmos DB 용량 계산기의 예상 비용":::

## <a name="estimating-serverless-costs"></a>서버 리스 비용 예측

서버를 사용 하지 않는 모드로 Azure Cosmos DB를 사용 하려면 월 기준으로 사용할 수 있는 [요청 단위](request-units.md) 및 GB의 저장소 수를 예상 해야 합니다. 한 달에 발생 하는 데이터베이스 작업의 수를 평가 하 여 필요한 요청 단위 양을 예측 하 고 해당 하는 시간을 해당 하는 작업 비용에 곱할 수 있습니다. 다음 표에서는 일반적인 데이터베이스 작업에 대 한 예상 비용을 보여 줍니다.

| 작업(Operation) | 예상 비용 | 메모 |
| --- | --- | --- |
| 항목 만들기 | 5RU | 5 개 미만의 속성을 인덱싱하는 1kb 항목에 대 한 평균 비용 |
| 항목 업데이트 | 10RU | 5 개 미만의 속성을 인덱싱하는 1kb 항목에 대 한 평균 비용 |
| 해당 ID 및 파티션 키로 개별 항목 읽기 (지점 읽기) | 1RU | 1kb 항목에 대 한 평균 비용 |
| 항목 삭제 | 5RU | |
| 쿼리 실행 | 10RU | [인덱싱을](index-overview.md) 최대한 활용 하 고 100 결과를 반환 하는 쿼리의 평균 비용 |

> [!IMPORTANT] 
> 위의 표에서 메모를 확인 합니다. 작업의 실제 비용을 보다 정확 하 게 예측 하기 위해 [Azure Cosmos 에뮬레이터](local-emulator.md) 를 사용 하 여 [작업의 정확한 작업 비용을 측정할](find-request-unit-charge.md)수 있습니다. Azure Cosmos Emulator는 서버 리스 서버를 지원 하지 않지만 데이터베이스 작업에 대 한 표준 작업 요금을 보고 하 고이 예측에 사용할 수 있습니다.

한 달 동안 소비할 가능성이 높은 요청 단위 및 GB 저장소의 총 수를 계산한 후에는 **([요청 단위 수]/100만 * $0.25) + ([GB의 저장소] * $0.25)** 와 같은 수식이 예상 비용을 반환 합니다.

> [!NOTE]
> 앞의 예제에 표시 된 비용은 데모용 으로만 사용 됩니다. 최신 가격 정보는 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/) 를 참조 하세요.

## <a name="review-estimated-costs-from-the-azure-portal"></a>Azure Portal에서 예상 비용을 검토 합니다.

Azure Portal에서 Azure Cosmos DB 리소스를 사용 하기 시작 하면 예상 비용을 볼 수 있습니다. 다음 단계를 사용 하 여 예상 비용을 검토 합니다.

1. Azure Portal에 로그인 하 여 Azure Cosmos 계정으로 이동 합니다.
1. **개요** 섹션으로 이동 합니다.
1. 아래쪽의 **비용** 차트를 확인 합니다. 이 차트는 구성 가능한 기간 동안의 현재 비용을 예상 하 여 보여 줍니다.
1. 그래프 컨테이너와 같은 새 컨테이너를 만듭니다.
1. 400 r u/초와 같은 워크 로드에 필요한 처리량을 입력 합니다. 처리량 값을 입력 한 후에는 다음 스크린샷에 표시 된 가격 책정을 확인할 수 있습니다.

   :::image type="content" source="./media/plan-manage-costs/cost-estimate-portal.png" alt-text="예상 비용 Azure Portal":::

## <a name="use-budgets-and-cost-alerts"></a>예산 및 비용 경고 사용

[예산](../cost-management/tutorial-acm-create-budgets.md)을 만들면 비용을 관리하고 관련자에게 비정상 지출 및 과다 지출 위험을 자동으로 알리는 경고를 만들 수 있습니다. 경고는 예산 및 비용 임계값에 따른 지출을 기준으로 합니다. Azure 구독 및 리소스 그룹에 대 한 예산과 경고가 생성 되므로 전체 비용 모니터링 전략의 일부로 유용 합니다. 그러나 더 높은 수준에서 비용을 추적 하도록 설계 되었기 때문에 Azure Cosmos DB 비용과 같은 개별 Azure 서비스 비용을 관리 하는 기능이 제한 될 수 있습니다.

Azure 구독에 지출 한도가 있는 경우 Azure는 크레딧 금액을 초과 하 여 지출 하지 못하도록 합니다. Azure 리소스를 만들고 사용할 때 크레딧이 사용 됩니다. 신용 한도에 도달 하면 배포한 리소스는 해당 청구 기간의 나머지 기간 동안 사용 하지 않도록 설정 됩니다. 신용 한도를 변경할 수 없지만 제거할 수는 있습니다. 지출 한도에 대 한 자세한 내용은 [Azure 지출 한도](../billing/billing-spending-limit.md)를 참조 하세요.

## <a name="monitor-costs"></a>비용 모니터링

Azure Cosmos DB에서 리소스를 사용 하는 경우 비용이 발생 합니다. 리소스 사용 단위 비용은 시간 간격 (초, 분, 시간 및 일) 또는 요청 단위 사용에 따라 달라 집니다. Azure Cosmos DB를 시작 하는 즉시 비용이 발생 하며 Azure Portal의 [비용 분석](../cost-management/quick-acm-cost-analysis.md) 창에서이를 볼 수 있습니다.

비용 분석을 사용 하면 서로 다른 시간 간격에 대 한 그래프 및 테이블의 Azure Cosmos DB 비용을 볼 수 있습니다. 몇 가지 예로는 일, 현재, 이전 달 및 연도가 있습니다. 예산 및 예상 비용에 대 한 비용을 볼 수도 있습니다. 시간이 지남에 따라 더 긴 보기로 전환 하면 지출 추세를 파악 하 고 낭비를 발생 시킬 수 있는 위치를 확인할 수 있습니다. 예산을 만든 경우 해당 위치를 쉽게 확인할 수도 있습니다. 비용 분석에서 Azure Cosmos DB 비용을 보려면 다음을 수행 합니다.

1. [Azure Portal](https://portal.azure.com)에 로그인합니다.

1. **Cost Management + 청구** 창을 열고 메뉴에서 **비용 관리** 를 선택한 다음 **비용 분석**을 선택 합니다. 그런 다음 **범위** 드롭다운에서 특정 구독에 대 한 범위를 변경할 수 있습니다.

1. 기본적으로 모든 서비스에 대 한 비용은 첫 번째 도넛형 차트에 표시 됩니다. "Azure Cosmos DB" 이라는 레이블이 지정 된 차트에서 영역을 선택 합니다.

1. Azure Cosmos DB와 같은 단일 서비스에 대 한 비용을 좁히려면 **필터 추가** 를 선택 하 고 **서비스 이름**을 선택 합니다. 그런 다음 목록에서 **Azure Cosmos DB** 을 선택 합니다. Azure Cosmos DB에 대 한 비용을 보여 주는 예제는 다음과 같습니다.
 
   :::image type="content" source="./media/plan-manage-costs/cost-analysis-pane.png" alt-text="비용 분석 창으로 비용 모니터링":::

위의 예제에서는 2 월의 Azure Cosmos DB에 대 한 현재 비용을 볼 수 있습니다. 차트에는 위치 및 리소스 그룹별 Azure Cosmos DB 비용도 포함 됩니다.

## <a name="next-steps"></a>다음 단계

Azure Cosmos DB에서 가격 책정의 작동 방식에 대해 자세히 알아보려면 다음 문서를 참조 하세요.

* [Azure Cosmos DB의 가격 책정 모델](how-pricing-works.md)
* [Azure Cosmos DB의 프로비저닝된 처리량 비용 최적화](optimize-cost-throughput.md)
* [Azure Cosmos DB의 쿼리 비용 최적화](optimize-cost-queries.md)
* [Azure Cosmos DB의 스토리지 비용 최적화](optimize-cost-storage.md)