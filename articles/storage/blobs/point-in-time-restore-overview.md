---
title: 블록 blob에 대 한 지정 시간 복원
titleSuffix: Azure Storage
description: 블록 blob에 대 한 지정 시간 복원은 지정 된 시간에 저장소 계정을 이전 상태로 복원할 수 있도록 하 여 실수로 인 한 삭제 또는 손상 으로부터 보호 합니다.
services: storage
author: tamram
ms.service: storage
ms.topic: conceptual
ms.date: 09/18/2020
ms.author: tamram
ms.subservice: blobs
ms.custom: references_regions, devx-track-azurecli, devx-track-azurepowershell
ms.openlocfilehash: 7fbebf21b79d2a533de0a872dfe6a10bc8f8e7e5
ms.sourcegitcommit: bdd5c76457b0f0504f4f679a316b959dcfabf1ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90987038"
---
# <a name="point-in-time-restore-for-block-blobs"></a>블록 blob에 대 한 지정 시간 복원

지정 시간 복원은 블록 blob 데이터를 이전 상태로 복원할 수 있도록 하 여 실수로 인 한 삭제 또는 손상 으로부터 보호 합니다. 특정 시점 복원은 사용자 또는 응용 프로그램이 실수로 데이터를 삭제 하거나 응용 프로그램 오류로 인해 데이터가 손상 되는 경우에 유용 합니다. 또한 지정 시간 복원은 추가 테스트를 실행 하기 전에 데이터 집합을 알려진 상태로 되돌려야 하는 테스트 시나리오를 가능 하 게 합니다.

특정 시점 복원은 범용 v2 저장소 계정에 대해서만 지원 됩니다. 핫 및 쿨 액세스 계층의 데이터만 지정 시간 복원을 사용 하 여 복원할 수 있습니다.

저장소 계정에 대 한 지정 시간 복원을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [블록 blob 데이터에 지정 시간 복원 수행](point-in-time-restore-manage.md)을 참조 하세요.

## <a name="how-point-in-time-restore-works"></a>특정 시점 복원 작동 방법

지정 시간 복원을 사용 하도록 설정 하려면 저장소 계정에 대 한 관리 정책을 만들고 보존 기간을 지정 합니다. 보존 기간 동안 현재 상태에서 이전 시점의 상태로 블록 blob을 복원할 수 있습니다.

지정 시간 복원을 시작 하려면 [Blob 범위 복원](/rest/api/storagerp/storageaccounts/restoreblobranges) 작업을 호출 하 고 UTC 시간으로 복원 지점을 지정 합니다. 복원할 컨테이너 및 blob 이름의 사전순 범위를 지정 하거나, 범위를 생략 하 여 저장소 계정의 모든 컨테이너를 복원할 수 있습니다. 복원 작업당 최대 10 개의 사전순 범위가 지원 됩니다.

Azure Storage는 UTC 시간 및 현재 순간에 지정 된 요청 된 복원 지점 사이에 지정 된 blob에 대 한 모든 변경 내용을 분석 합니다. 복원 작업은 원자성 이므로 모든 변경 내용을 복원 하는 데 완전히 성공 하거나 실패 합니다. 복원할 수 없는 blob이 있는 경우 작업이 실패 하 고 영향을 받는 컨테이너 다시 시작에 대 한 읽기 및 쓰기 작업이 실패 합니다.

한 번에 하나의 복원 작업만 저장소 계정에서 실행할 수 있습니다. 복원 작업은 진행 중인 동안에는 취소할 수 없지만 첫 번째 작업을 실행 취소 하기 위해 두 번째 복원 작업을 수행할 수 있습니다.

**Blob 범위 복원** 작업은 작업을 고유 하 게 식별 하는 복원 ID를 반환 합니다. 지정 시간 복원 상태를 확인 하려면 **Blob 범위 복원** 작업에서 반환 된 복원 ID를 사용 하 여 **복원 상태 가져오기** 작업을 호출 합니다.

복원 작업에 대 한 다음 제한 사항에 유의 하세요.

- [Put 블록 또는](/rest/api/storageservices/put-block) [URL에서 put 블록](/rest/api/storageservices/put-block-from-url)을 통해 업로드 되었지만 [put 블록 목록을](/rest/api/storageservices/put-block-list)통해 커밋되지 않은 블록은 blob의 일부가 아니므로 복원 작업의 일부로 복원 되지 않습니다.
- 활성 임대가 있는 blob은 복원할 수 없습니다. 활성 임대가 있는 blob이 복원할 blob의 범위에 포함 되는 경우 복원 작업은 원자적으로 실패 합니다.
- 스냅숏은 복원 작업의 일부로 생성 되거나 삭제 되지 않습니다. 기본 blob만 이전 상태로 복원 됩니다.
- Blob이 현재 순간과 복원 지점 사이에서 핫 및 쿨 계층 사이를 이동 하면 blob이 이전 계층으로 복원 됩니다. 그러나 보관 계층으로 이동한 blob은 복원 되지 않습니다.

> [!IMPORTANT]
> 복원 작업을 수행 하는 경우 Azure Storage은 작업 기간 동안 복원 되는 범위의 blob에 대 한 데이터 작업을 차단 합니다. 읽기, 쓰기 및 삭제 작업은 기본 위치에서 차단 됩니다. 이러한 이유로 복원 작업이 진행 되는 동안 Azure Portal의 컨테이너 나열 등의 작업이 예상 대로 수행 되지 않을 수 있습니다.
>
> 저장소 계정이 지리적으로 복제 되는 경우 보조 위치에서 읽기 작업은 복원 작업 중에 진행할 수 있습니다.

> [!CAUTION]
> 지정 시간 복원은 블록 Blob에 대한 작업만 복원하도록 지원합니다. 컨테이너에 대한 작업은 복원할 수 없습니다. 컨테이너 [삭제](/rest/api/storageservices/delete-container) 작업을 호출 하 여 저장소 계정에서 컨테이너를 삭제 하는 경우 해당 컨테이너는 복원 작업을 통해 복원할 수 없습니다. 컨테이너를 삭제 하는 대신, 개별 blob을 복원 하는 것이 좋습니다.

### <a name="prerequisites-for-point-in-time-restore"></a>지정 시간 복원에 대 한 필수 조건

지정 시간 복원을 사용 하려면 지정 시간 복원을 사용 하도록 설정 하기 전에 다음과 같은 Azure Storage 기능을 사용 하도록 설정 해야 합니다.

- [일시 삭제](soft-delete-overview.md)
- [변경 피드](storage-blob-change-feed.md)
- [Blob 버전 관리](versioning-overview.md)

### <a name="retention-period-for-point-in-time-restore"></a>지정 시간 복원에 대 한 보존 기간

저장소 계정에 대 한 특정 시점 복원을 사용 하도록 설정 하는 경우 보존 기간을 지정 합니다. 저장소 계정의 블록 blob은 보존 기간 동안 복원 될 수 있습니다.

지정 시간 복원을 사용 하도록 설정 하면 보존 기간이 시작 됩니다. 보존 기간이 시작 되기 전에는 blob을 상태로 복원할 수 없습니다. 예를 들어 1 년 5 월 1 일에 30 일 동안 지정 시간 복원을 사용 하도록 설정한 경우 5 월 15 일까 지 최대 15 일까 지 복원할 수 있습니다. 6 월 1 일에는 1 일에서 30 일 사이에 데이터를 복원할 수 있습니다.

지정 시간 복원에 대 한 보존 기간은 일시 삭제에 지정 된 보존 기간 보다 하루 이상 적어야 합니다. 예를 들어 일시 삭제 보존 기간이 7 일로 설정 된 경우 지정 시간 복원 보존 기간은 1 ~ 6 일이 될 수 있습니다.

### <a name="permissions-for-point-in-time-restore"></a>지정 시간 복원에 대 한 사용 권한

복원 작업을 시작 하려면 클라이언트에 저장소 계정의 모든 컨테이너에 대 한 쓰기 권한이 있어야 합니다. Azure Active Directory (Azure AD)를 사용 하 여 복원 작업에 권한을 부여 하는 권한을 부여 하려면 저장소 계정, 리소스 그룹 또는 구독 수준에서 보안 주체에 **저장소 계정 참가자** 역할을 할당 합니다.

## <a name="limitations-and-known-issues"></a>제한 사항 및 알려진 문제

블록 blob에 대 한 지정 시간 복원에는 다음과 같은 제한 사항 및 알려진 문제가 있습니다.

- 표준 범용 v2 저장소 계정의 블록 blob만 지정 시간 복원 작업의 일부로 복원할 수 있습니다. 추가 blob, 페이지 blob 및 premium 블록 blob은 복원 되지 않습니다. 보존 기간 동안 컨테이너를 삭제 한 경우 해당 컨테이너는 지정 시간 복원 작업으로 복원 되지 않습니다. 컨테이너를 삭제 하지 못하도록 보호 하는 방법에 대 한 자세한 내용은 [컨테이너의 일시 삭제 (미리 보기)](soft-delete-container-overview.md)를 참조 하세요.
- 지정 시간 복원 작업에서 핫 또는 쿨 계층의 블록 blob만 복원할 수 있습니다. 보관 계층에서 블록 blob을 복원 하는 것은 지원 되지 않습니다. 예를 들어 핫 계층의 Blob을 2일 전에 보관 계층으로 이동하고 복원 작업이 3일 전 지점으로 복원하면 Blob이 핫 계층으로 복원되지 않습니다. 보관 된 blob을 복원 하려면 먼저 보관 계층 외부로 이동 합니다.
- 복원할 범위의 블록 blob에 활성 임대가 있는 경우 지정 시간 복원 작업이 실패 합니다. 복원 작업을 시작 하기 전에 활성 임대를 중단 합니다.
- Azure Data Lake Storage Gen2 플랫 및 계층적 네임 스페이스는 복원할 수 없습니다.

> [!IMPORTANT]
> 블록 blob을 2020 년 9 월 22 일 이전 지점으로 복원 하는 경우 지정 시간 복원에 대 한 미리 보기 제한이 적용 됩니다. 일반적으로 사용 가능한 지정 시간 복원 기능을 활용 하려면 2020 년 9 월 22 일 이상인 복원 지점을 선택 하는 것이 좋습니다.

## <a name="pricing-and-billing"></a>가격 책정 및 대금 청구

지정 시간 복원에 대 한 요금은 복원 작업을 수행 하기 위해 처리 된 데이터의 양에 따라 달라 집니다. 처리 되는 데이터의 양은 복원 지점 및 현재 순간 사이에 발생 한 변경 내용 수를 기반으로 합니다. 예를 들어 저장소 계정에서 blob 데이터를 차단 하기 위해 상대적으로 일정 하 게 변경 되는 것으로 간주 되는 복원 작업은 시간 1 일에 다시 복원 되는 복원 작업은 10 일이 지나면 복원 작업의 1/10입니다.

복원 작업의 비용을 예측 하려면 변경 피드 로그를 검토 하 여 복원 기간 동안 수정 된 데이터의 양을 예측 합니다. 예를 들어 변경 피드의 보존 기간이 30 일이 고 변경 피드의 크기가 10mb 인 경우 10 일 이전 지점으로 복원 하는 것은 해당 지역의 LRS 계정에 대해 나열 된 가격의 약 1/3입니다. 이전에 27 일의 시점으로 복원 하는 것은 나열 된 가격의 약 9-1/10입니다.

지정 시간 복원에 대 한 가격 책정에 대 한 자세한 내용은 [블록 blob 가격 책정](https://azure.microsoft.com/pricing/details/storage/blobs/)을 참조 하세요.

## <a name="next-steps"></a>다음 단계

- [블록 blob 데이터에 지정 시간 복원 수행](point-in-time-restore-manage.md)
- [Azure Blob Storage의 변경 피드 지원](storage-blob-change-feed.md)
- [Blob에 일시 삭제를 사용하도록 설정](soft-delete-enable.md)
- [Blob 버전 관리 설정 및 관리](versioning-enable.md)
