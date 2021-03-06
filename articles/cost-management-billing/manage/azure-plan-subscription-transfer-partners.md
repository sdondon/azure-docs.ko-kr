---
title: 한 파트너에서 다른 파트너로 Azure 구독 전송(미리 보기)
description: 이 문서는 Azure 구독의 청구 소유권을 이전하기 전후에 알아두어야 할 사항을 이해하는 데 도움이 됩니다.
author: bandersmsft
ms.reviewer: mcville
ms.service: cost-management-billing
ms.topic: conceptual
ms.date: 09/07/2020
ms.author: banders
ms.openlocfilehash: 246128ec3d26e4bf3f2a5a8f0660aab7d9daca3d
ms.sourcegitcommit: c52e50ea04dfb8d4da0e18735477b80cafccc2cf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89554205"
---
# <a name="transfer-azure-subscriptions-from-one-partner-to-another-preview"></a>한 파트너에서 다른 파트너로 Azure 구독 전송(미리 보기)

이 문서는 Azure 구독의 청구 소유권을 이전하기 전후에 알아두어야 할 사항을 이해하는 데 도움이 됩니다. Microsoft 파트너 간에 Azure 계획에 따른 Azure 구독 이전을 시작하려면 파트너에게 문의해야 합니다. 파트너가 시작하는 방법에 대한 지침을 보냅니다. 이전 프로세스가 완료되면 구독의 청구 소유권이 변경됩니다.

## <a name="user-access"></a>사용자 액세스

Azure RBAC(역할 기반 액세스 제어)를 사용하여 할당된 기존 사용자, 그룹 또는 서비스 주체에 대한 액세스는 전환 중에 영향을 받지 않습니다. [Azure RBAC](../../role-based-access-control/overview.md)는 Azure 리소스에 액세스할 수 있는 사용자, 해당 리소스로 수행할 수 있는 작업 및 액세스 권한이 있는 영역을 관리하는 데 도움을 줍니다. 새 파트너에게는 구독 이전을 통해 리소스에 대한 RBAC 액세스 권한이 부여되지 않습니다. 이전 파트너는 RBAC 액세스를 유지합니다.

따라서 이전 파트너에 대한 Azure RBAC 액세스를 제거하고 새 파트너에 대한 액세스 권한을 추가하는 것이 중요합니다. 새 파트너 액세스 권한을 부여하는 방법에 대한 자세한 내용은 [Azure RBAC(Azure 역할 기반 액세스 제어)란?](../../role-based-access-control/overview.md)을 참조하세요. 이전 파트너의 RBAC 액세스를 제거하는 방법에 대한 자세한 내용은 [역할 할당 제거](../../role-based-access-control/role-assignments-portal.md#remove-a-role-assignment)를 참조하세요.

또한 새 파트너는 구독에 대한 [AOBO(Admin on Behalf Of)](https://channel9.msdn.com/Series/cspdev/Module-11-Admin-On-Behalf-Of-AOBO) 액세스 권한을 자동으로 가져오지 못합니다. 사용자를 대신해 Azure 구독을 관리하려면 파트너에게 AOBO가 필요합니다. 새 파트너 AOBO 액세스 권한을 부여하는 방법에 대한 자세한 내용은 [Azure 구독 계정의 청구 소유권을 다른 계정으로 이전](billing-subscription-transfer.md)을 참조하세요.

## <a name="stop-a-transfer"></a>이전 중지

이전 요청이 제출되었다는 확인 메시지를 받은 후 **이전을 계속하지 않으려는 경우** 다음 옵션 중 하나를 사용할 수 있습니다.

- 현재 파트너가 요청을 아직 수락하지 않은 경우 새 파트너에게 시작된 이전 요청을 취소하도록 요청할 수 있습니다(상태가 보류 중일 때).
- 현재 파트너에게 이전 요청을 받을 때 어떠한 조치도 취하지 않도록 요청합니다. 현재 파트너의 동의 없이는 이전을 계속할 수 없습니다. 요청이 만료됩니다.
- 새 파트너와의 _재판매인 관계를 제거_할 수 있습니다. 이 작업을 수행하면 구독이 이동하는 기능이 제거됩니다. 요청을 효과적으로 취소합니다.

[Microsoft 법률](https://www.microsoft.com/legal/) 웹 사이트의 옵션 중 하나를 사용하여 도움을 요청하거나, 위법 행위 또는 의심스러운 활동을 보고할 수 있습니다. 문제를 보고하는 옵션은 규정 준수 및 윤리에 따릅니다.

## <a name="next-steps"></a>다음 단계

- 새 파트너 RBAC 액세스 권한을 부여하려면 [Azure RBAC(Azure 역할 기반 액세스 제어)란?](../../role-based-access-control/overview.md)을 참조하세요.
- 새 파트너 AOBO 액세스 권한을 부여하려면 [Azure 구독 계정의 청구 소유권을 다른 계정으로 이전](billing-subscription-transfer.md)을 참조하세요.