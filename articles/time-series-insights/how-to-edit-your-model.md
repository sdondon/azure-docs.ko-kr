---
title: Gen2 환경의 데이터 모델링-Azure Time Series Insights | Microsoft Docs
description: Azure Time Series Insights Gen2의 데이터 모델링에 대해 알아봅니다.
author: deepakpalled
ms.author: dpalled
manager: diviso
ms.workload: big-data
ms.service: time-series-insights
services: time-series-insights
ms.topic: conceptual
ms.date: 06/30/2020
ms.custom: seodec18
ms.openlocfilehash: ac5322b93fc5f804292cfbff2c2e7eeb79b5989f
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87098427"
---
# <a name="data-modeling-in-azure-time-series-insights-gen2"></a>Azure Time Series Insights Gen2의 데이터 모델링

이 문서에서는 Azure Time Series Insights Gen2에서 시계열 모델을 사용 하는 방법을 설명 합니다. 몇 가지 일반적인 데이터 시나리오를 자세히 설명합니다.

> [!TIP]
> * [시계열 모델](concepts-model-overview.md)에 대해 자세히 알아보세요.
> * [Azure Time Series Insights Gen2 explorer](./time-series-insights-update-explorer.md)탐색에 대해 자세히 알아보세요.

## <a name="instances"></a>인스턴스

Azure Time Series Insights 탐색기는 브라우저 내에서 인스턴스 **만들기**, **읽기**, **업데이트**및 **삭제** 작업을 지원 합니다. 

시작 하려면 Azure Time Series Insights 탐색기 **분석** 보기에서 **모델** 뷰를 선택 합니다.

### <a name="create-a-single-instance"></a>단일 인스턴스 만들기

1. 시계열 모델 선택기 패널로 이동 하 고 메뉴에서 **인스턴스** 를 선택 합니다. 선택한 Azure Time Series Insights 환경에 연결 된 모든 인스턴스가 표시 됩니다.

    [![인스턴스를 먼저 선택 하 여 단일 인스턴스를 만듭니다.](media/v2-update-how-to-tsm/how-to-tsm-instances-panel.png)](media/v2-update-how-to-tsm/how-to-tsm-instances-panel.png#lightbox)

1. **+추가**를 선택합니다.

    [![+ 추가 단추를 선택 하 여 인스턴스를 추가 합니다.](media/v2-update-how-to-tsm/how-to-tsm-add-instance.png)](media/v2-update-how-to-tsm/how-to-tsm-add-instance.png#lightbox)

1. 인스턴스 정보를 입력하고 형식 및 계층 구조 연결을 선택한 다음, **만들기**를 선택합니다.

### <a name="bulk-upload-one-or-more-instances"></a>하나 이상의 인스턴스 대량 업로드

> [!TIP]
> JSON에서 사용자의 데스크톱에 인스턴스를 저장할 수 있습니다. 다운로드 한 JSON 파일은 다음 단계를 통해 업로드할 수 있습니다.

1. **JSON 업로드**를 선택합니다.
1. 인스턴스 페이로드를 포함하는 파일을 선택합니다.

    [![JSON을 통해 인스턴스를 대량 업로드 합니다.](media/v2-update-how-to-tsm/how-to-tsm-bulk-upload-instances.png)](media/v2-update-how-to-tsm/how-to-tsm-bulk-upload-instances.png#lightbox)

1. **업로드**를 선택합니다.

### <a name="edit-a-single-instance"></a>단일 인스턴스 편집

1. 인스턴스를 선택 하 고 **편집** 또는 **연필 아이콘**을 선택 합니다. 
1. 필요에 따라 변경하고 **저장**을 선택합니다.

    [![단일 인스턴스를 편집 합니다.](media/v2-update-how-to-tsm/how-to-tsm-edit-instance.png)](media/v2-update-how-to-tsm/how-to-tsm-edit-instance.png#lightbox)

### <a name="delete-an-instance"></a>인스턴스 삭제

1. 인스턴스를 선택 하 고 **삭제** 또는 **저장 함 아이콘**을 선택 합니다.

   [![삭제를 선택 하 여 인스턴스를 삭제 합니다.](media/v2-update-how-to-tsm/how-to-tsm-delete-instance.png)](media/v2-update-how-to-tsm/how-to-tsm-delete-instance.png#lightbox)

1. **삭제**를 선택 하 여 삭제를 확인 합니다.

> [!NOTE]
> 인스턴스는 삭제할 필드 유효성 검사를 성공적으로 통과 해야 합니다.

## <a name="hierarchies"></a>계층 구조

Azure Time Series Insights 탐색기는 브라우저 내에서 계층 **만들기**, **읽기**, **업데이트**및 **삭제** 작업을 지원 합니다. 

시작 하려면 Azure Time Series Insights 탐색기 **분석** 보기에서 **모델** 뷰를 선택 합니다.

### <a name="create-a-single-hierarchy"></a>단일 계층 구조 만들기

1. 시계열 모델 선택기 패널로 이동 하 고 메뉴에서 **계층** 을 선택 합니다. 선택한 Azure Time Series Insights 환경과 연결 된 모든 계층이 표시 됩니다.

    [![창을 통해 계층을 만듭니다.](media/v2-update-how-to-tsm/how-to-tsm-hierarchy-panel.png)](media/v2-update-how-to-tsm/how-to-tsm-hierarchy-panel.png#lightbox)

1. **+추가**를 선택합니다.

    [![계층 + 추가 단추를 클릭 합니다.](media/v2-update-how-to-tsm/how-to-tsm-add-new-hierarchy.png)](media/v2-update-how-to-tsm/how-to-tsm-add-new-hierarchy.png#lightbox)

1. 오른쪽 창에서 **+ 수준 추가** 를 선택 합니다.

    [![계층에 수준을 추가 합니다.](media/v2-update-how-to-tsm/how-to-tsm-save-hierarchy-levels.png)](media/v2-update-how-to-tsm/how-to-tsm-save-hierarchy-levels.png#lightbox)

1. 계층 세부 정보를 입력 하 고 **저장**을 선택 합니다.

    [![계층 세부 정보를 지정 하십시오.](media/v2-update-how-to-tsm/how-to-tsm-add-hierarchy-level.png)](media/v2-update-how-to-tsm/how-to-tsm-add-hierarchy-level.png#lightbox)

### <a name="bulk-upload-one-or-more-hierarchies"></a>하나 이상의 계층 구조 대량 업로드

> [!TIP]
> JSON에서 데스크톱에 계층을 저장할 수 있습니다. 다운로드 한 JSON 파일은 다음 단계를 통해 업로드할 수 있습니다.

1. **JSON 업로드**를 선택합니다.
1. 계층 구조 페이로드를 포함하는 파일을 선택합니다.
1. **업로드**를 선택합니다.

    [![계층의 대량 업로드에 대 한 선택 항목입니다.](media/v2-update-how-to-tsm/how-to-tsm-bulk-upload-hierarchies.png)](media/v2-update-how-to-tsm/how-to-tsm-bulk-upload-hierarchies.png#lightbox)

### <a name="edit-a-single-hierarchy"></a>단일 계층 구조 편집

1. 계층을 선택 하 고 **편집** 또는 **연필 아이콘**을 선택 합니다.
1. 필요에 따라 변경하고 **저장**을 선택합니다.

    [![단일 계층 편집을 위한 선택 항목입니다.](media/v2-update-how-to-tsm/how-to-tsm-edit-hierarchy.png)](media/v2-update-how-to-tsm/how-to-tsm-edit-hierarchy.png#lightbox)

### <a name="delete-a-hierarchy"></a>계층 구조 삭제

1. 계층을 선택 하 고 **삭제** 또는 **폐기물 저장 아이콘**을 선택 합니다. 

    [![삭제 단추를 선택 하 여 계층을 삭제 합니다.](media/v2-update-how-to-tsm/how-to-tsm-delete-hierarchy.png)](media/v2-update-how-to-tsm/how-to-tsm-delete-hierarchy.png#lightbox)

1. **삭제**를 선택 하 여 삭제를 확인 합니다.

## <a name="types"></a>형식

Azure Time Series Insights 탐색기는 브라우저 내에서 형식 **만들기**, **읽기**, **업데이트**및 **삭제** 작업을 지원 합니다. 

시작 하려면 Azure Time Series Insights 탐색기 **분석** 보기에서 **모델** 뷰를 선택 합니다.

### <a name="create-a-single-type"></a>단일 형식 만들기

1. 시계열 모델 선택기 패널로 이동 하 고 메뉴에서 **형식** 을 선택 합니다. 선택한 Azure Time Series Insights 환경에 연결 된 모든 유형이 표시 됩니다.

    [![시계열 모델 유형 창](media/v2-update-how-to-tsm/how-to-tsm-type-panel.png)](media/v2-update-how-to-tsm/how-to-tsm-type-panel.png#lightbox)

1. **+ 추가** 를 선택 하 여 **새 형식 추가** 팝업 모달을 표시 합니다.
1. 형식에 대 한 속성 및 변수를 입력 합니다. 입력 한 후 **저장**을 선택 합니다. 

    [![유형을 추가 하는 구성 설정입니다.](media/v2-update-how-to-tsm/how-to-tsm-add-new-type.png)](media/v2-update-how-to-tsm/how-to-tsm-add-new-type.png#lightbox)

### <a name="bulk-upload-one-or-more-types"></a>하나 이상의 형식 대량 업로드

> [!TIP]
> JSON에서 사용자의 데스크톱에 형식을 저장할 수 있습니다. 다운로드 한 JSON 파일은 다음 단계를 통해 업로드할 수 있습니다.

1. **JSON 업로드**를 선택합니다.
1. 형식 페이로드를 포함하는 파일을 선택합니다.
1. **업로드**를 선택합니다.

    [![대량 형식 업로드 옵션입니다.](media/v2-update-how-to-tsm/how-to-tsm-bulk-upload-types-json.png)](media/v2-update-how-to-tsm/how-to-tsm-bulk-upload-types-json.png#lightbox)

### <a name="edit-a-single-type"></a>단일 형식 편집

1. 유형을 선택 하 고 **편집** 또는 **연필 아이콘**을 선택 합니다.
1. 필요에 따라 변경하고 **저장**을 선택합니다.

    [![창에서 형식을 편집 합니다.](media/v2-update-how-to-tsm/how-to-tsm-edit-type.png)](media/v2-update-how-to-tsm/how-to-tsm-edit-type.png#lightbox)

### <a name="delete-a-type"></a>형식 삭제

1. 유형을 선택 하 고 **삭제** 또는 **폐기물 저장 아이콘**을 선택 합니다.

   [![삭제를 선택 하 여 형식을 삭제 합니다.](media/v2-update-how-to-tsm/how-to-tsm-delete-type.png)](media/v2-update-how-to-tsm/how-to-tsm-delete-type.png#lightbox)

1. **삭제**를 선택 하 여 삭제를 확인 합니다.

## <a name="next-steps"></a>다음 단계

- 시계열 모델에 대 한 자세한 내용은 [데이터 모델링](./concepts-model-overview.md)을 참조 하세요.

- Gen2에 대 한 자세한 내용을 보려면 [Azure Time Series Insights Gen2 탐색기에서 데이터 시각화](./time-series-insights-update-explorer.md)를 참조 하세요.

- 지원 되는 JSON 셰이프에 대 한 자세한 내용은 [지원 되는 json 셰이프](./time-series-insights-send-events.md#supported-json-shapes)를 참조 하세요.
