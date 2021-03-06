---
author: rothja
ms.service: azure-resource-manager
ms.topic: include
ms.date: 2/14/2020
ms.author: rohink
ms.openlocfilehash: 0f7187300ec96ce417866c4fb8fa02783c1da63a
ms.sourcegitcommit: 3543d3b4f6c6f496d22ea5f97d8cd2700ac9a481
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86515885"
---
**공용 DNS 영역**

| 리소스 | 제한 |
| --- | --- |
| 구독 당 공용 DNS 영역 |250 <sup>1</sup> |
| 공용 DNS 영역별 레코드 집합 |1만 <sup>1</sup> |
| 공용 DNS 영역에 있는 레코드 집합 당 레코드 |20 |
| 단일 Azure 리소스에 대 한 별칭 레코드 수 |20|

<sup>1</sup> 이러한 제한을 늘려야 하는 경우 Azure 지원에 문의하세요.

**사설 DNS 영역**

| 리소스 | 제한 |
| --- | --- |
| 구독 당 사설 DNS 영역 |1000|
| 개인 DNS 영역별 레코드 집합 |25000|
| 개인 DNS 영역에 대 한 레코드 집합 당 레코드 |20|
| 개인 DNS 영역별 Virtual Network 링크 |1000|
| 자동 등록을 사용 하는 개인 DNS 영역 당 가상 네트워크 링크 |100|
| 자동 등록을 사용 하도록 설정한 상태에서 가상 네트워크가 연결 될 수 있는 개인 DNS 영역 수 |1|
| 가상 네트워크가 연결 될 수 있는 개인 DNS 영역 수 |1000|
| 가상 머신이 Azure DNS 해결 프로그램으로 보낼 수 있는 초당 DNS 쿼리 수입니다 (초당). |500 <sup>1</sup> |
| 가상 컴퓨터당 최대 DNS 쿼리 수 (응답 보류 중) |200 <sup>1</sup> |

<sup>1</sup> 이러한 제한은 가상 네트워크 수준이 아닌 모든 개별 가상 컴퓨터에 적용 됩니다. 이러한 제한을 초과 하는 DNS 쿼리는 삭제 됩니다.
