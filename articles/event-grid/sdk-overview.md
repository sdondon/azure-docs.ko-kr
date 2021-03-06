---
title: Azure Event Grid SDK
description: Azure Event Grid에 대한 SDK를 설명합니다. 이러한 SDK는 관리, 게시 및 소비를 제공합니다.
ms.topic: reference
ms.date: 07/07/2019
ms.openlocfilehash: 2b21d8bf2c393b096e9046765e6cfadc76baffbf
ms.sourcegitcommit: d7008edadc9993df960817ad4c5521efa69ffa9f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86119109"
---
# <a name="event-grid-sdks-for-management-and-publishing"></a>관리 및 게시에 대한 Event Grid SDK

Event Grid는 사용자가 프로그래밍 방식으로 리소스를 관리하고 이벤트를 게시할 수 있는 SDK를 제공합니다.

## <a name="management-sdks"></a>관리 SDK

관리 SDK를 사용하면 Event Grid 토픽 및 구독을 만들고, 업데이트하고, 삭제할 수 있습니다. 현재는 다음 SDK를 사용할 수 있습니다.

* [.NET](https://www.nuget.org/packages/Microsoft.Azure.Management.EventGrid)
* [Go](https://github.com/Azure/azure-sdk-for-go)
* [Java](https://search.maven.org/#search%7Cga%7C1%7Cazure-mgmt-eventgrid)
* [노드](https://www.npmjs.com/package/azure-arm-eventgrid)
* [Python](https://pypi.python.org/pypi/azure-mgmt-eventgrid)
* [Ruby](https://rubygems.org/gems/azure_mgmt_event_grid)

## <a name="data-plane-sdks"></a>데이터 평면 SDK

데이터 평면 SDK를 사용하면 인증, 이벤트 형성, 지정된 엔드포인트에 비동기 게시를 처리하여 토픽에 이벤트를 게시할 수 있습니다. 또한 첫 번째 파티 이벤트를 사용할 수 있습니다. 현재는 다음 SDK를 사용할 수 있습니다.

* [.NET](https://www.nuget.org/packages/Microsoft.Azure.EventGrid)
* [Go](https://github.com/Azure/azure-sdk-for-go)
* [Java](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventgrid)
* [노드](https://www.npmjs.com/package/azure-eventgrid)
* [Python](https://pypi.python.org/pypi/azure-eventgrid)
* [Ruby](https://rubygems.org/gems/azure_event_grid)

## <a name="next-steps"></a>다음 단계

* 예제 애플리케이션은 [Event Grid 코드 샘플](https://azure.microsoft.com/resources/samples/?sort=0&service=event-grid)을 참조하세요.
* Event Grid에 대한 소개는 [Event Grid란?](overview.md)을 참조하세요.
* Azure CLI의 Event Grid 명령은 [Azure CLI](/cli/azure/eventgrid)를 참조하세요.
* PowerShell의 Event Grid 명령은 [PowerShell](/powershell/module/az.eventgrid)를 참조하세요.
