---
title: 데이터 암호화-Azure Portal-Azure Database for PostgreSQL-단일 서버
description: Azure Portal를 사용 하 여 Azure Database for PostgreSQL 단일 서버에 대 한 데이터 암호화를 설정 하 고 관리 하는 방법을 알아봅니다.
author: kummanish
ms.author: manishku
ms.service: postgresql
ms.topic: how-to
ms.date: 01/13/2020
ms.custom: devx-track-azurecli
ms.openlocfilehash: 0db0a705d97743bb199550bc74ade8e270c7472c
ms.sourcegitcommit: 53acd9895a4a395efa6d7cd41d7f78e392b9cfbe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90907482"
---
# <a name="data-encryption-for-azure-database-for-postgresql-single-server-by-using-the-azure-portal"></a>Azure Portal를 사용 하 여 Azure Database for PostgreSQL 단일 서버에 대 한 데이터 암호화

Azure Portal를 사용 하 여 Azure Database for PostgreSQL 단일 서버에 대 한 데이터 암호화를 설정 하 고 관리 하는 방법을 알아봅니다.

## <a name="prerequisites-for-azure-cli"></a>Azure CLI에 대 한 필수 구성 요소

* Azure 구독 및 해당 구독에 대한 관리자 권한이 있어야 합니다.
* Azure Key Vault에서 고객이 관리 하는 키에 사용할 주요 자격 증명 모음 및 키를 만듭니다.
* 키 자격 증명 모음에는 고객이 관리 하는 키로 사용할 수 있는 다음과 같은 속성이 있어야 합니다.
  * [일시 삭제](../key-vault/general/soft-delete-overview.md)

    ```azurecli-interactive
    az resource update --id $(az keyvault show --name \ <key_vault_name> -test -o tsv | awk '{print $1}') --set \ properties.enableSoftDelete=true
    ```

  * [보호 된 데이터 삭제](../key-vault/general/soft-delete-overview.md#purge-protection)

    ```azurecli-interactive
    az keyvault update --name <key_vault_name> --resource-group <resource_group_name>  --enable-purge-protection true
    ```

* 키에는 고객 관리 키로 사용할 다음 특성이 있어야 합니다.
  * 만료 날짜 없음
  * 사용 안 함 없음
  * Get, wrap 키 및 래핑 해제 키 작업을 수행할 수 있습니다.

## <a name="set-the-right-permissions-for-key-operations"></a>키 작업에 대 한 올바른 사용 권한 설정

1. Key Vault에서 액세스 정책 **Access policies**  >  **추가 액세스 정책**을 선택 합니다.

   :::image type="content" source="media/concepts-data-access-and-security-data-encryption/show-access-policy-overview.png" alt-text="액세스 정책을 사용 하는 Key Vault의 스크린샷 강조 표시 된 액세스 정책 추가":::

2. **키 사용 권한**을 선택 하 고 **가져오기**, **래핑**, **래핑**해제 및 PostgreSQL 서버의 이름인 **보안 주체**를 선택 합니다. 기존 보안 주체 목록에서 서버 보안 주체를 찾을 수 없는 경우 등록 해야 합니다. 처음으로 데이터 암호화를 설정 하려고 할 때 서버 보안 주체를 등록 하 라는 메시지가 표시 되 고 실패 합니다.  

   :::image type="content" source="media/concepts-data-access-and-security-data-encryption/access-policy-wrap-unwrap.png" alt-text="액세스 정책 개요":::

3. **저장**을 선택합니다.

## <a name="set-data-encryption-for-azure-database-for-postgresql-single-server"></a>단일 서버 Azure Database for PostgreSQL에 대 한 데이터 암호화 설정

1. Azure Database for PostgreSQL에서 **데이터 암호화** 를 선택 하 여 고객 관리 키를 설정 합니다.

   :::image type="content" source="media/concepts-data-access-and-security-data-encryption/data-encryption-overview.png" alt-text="데이터 암호화가 강조 표시 된 Azure Database for PostgreSQL의 스크린샷":::

2. 키 자격 증명 모음 및 키 쌍을 선택 하거나 키 식별자를 입력할 수 있습니다.

   :::image type="content" source="media/concepts-data-access-and-security-data-encryption/setting-data-encryption.png" alt-text="데이터 암호화 옵션이 강조 표시 된 Azure Database for PostgreSQL의 스크린샷":::

3. **저장**을 선택합니다.

4. 임시 파일을 포함 하 여 모든 파일이 완전히 암호화 되었는지 확인 하려면 서버를 다시 시작 합니다.

## <a name="using-data-encryption-for-restore-or-replica-servers"></a>복원 또는 복제 서버에 데이터 암호화 사용

Key Vault에 저장된 고객 관리형 키를 사용하여 Azure Database for PostgreSQL Single 서버를 암호화한 후에는 새로 만든 서버 복사본도 암호화됩니다. 로컬 또는 지역 복원 작업을 통해 또는 복제본 (로컬/지역 간) 작업을 통해이 새 복사본을 만들 수 있습니다. 따라서 암호화 된 PostgreSQL 서버의 경우 다음 단계를 사용 하 여 암호화 된 복원 된 서버를 만들 수 있습니다.

1. 서버에서 **개요**  >  **복원**을 선택 합니다.

   :::image type="content" source="media/concepts-data-access-and-security-data-encryption/show-restore.png" alt-text="개요 및 복원이 강조 표시 된 Azure Database for PostgreSQL의 스크린샷":::

   또는 복제를 사용 하는 서버의 경우 **설정** 머리글 아래에서 **복제**를 선택 합니다.

   :::image type="content" source="media/concepts-data-access-and-security-data-encryption/postgresql-replica.png" alt-text="복제가 강조 표시 된 Azure Database for PostgreSQL의 스크린샷":::

2. 복원 작업이 완료 되 면 새로 만든 서버가 기본 서버 키로 암호화 됩니다. 그러나 서버에서 기능 및 옵션을 사용할 수 없으며 서버에 액세스할 수 없습니다. 그러면 새 서버의 id에 키 자격 증명 모음에 대 한 액세스 권한이 아직 제공 되지 않았기 때문에 데이터 조작을 방지할 수 있습니다.

   :::image type="content" source="media/concepts-data-access-and-security-data-encryption/show-restore-data-encryption.png" alt-text="액세스할 수 없음 상태가 강조 표시 된 Azure Database for PostgreSQL의 스크린샷":::

3. 서버에 액세스할 수 있도록 하려면 복원 된 서버에서 키의 유효성을 다시 검사 합니다. **데이터 암호화**  >  **유효성 검사 키**를 선택 합니다.

   > [!NOTE]
   > 새 서버의 서비스 주체에 게 키 자격 증명 모음에 대 한 액세스 권한이 있어야 하기 때문에 첫 번째 유효성 재검사 시도는 실패 합니다. 서비스 주체를 생성 하려면 오류를 표시 하 고 서비스 주체를 생성 하는 **키 다시 유효성**검사를 선택 합니다. 이후에는이 문서 앞부분의 [이러한 단계](#set-the-right-permissions-for-key-operations) 를 참조 하세요.

   :::image type="content" source="media/concepts-data-access-and-security-data-encryption/show-revalidate-data-encryption.png" alt-text="유효성 재검사 단계가 강조 표시 된 Azure Database for PostgreSQL의 스크린샷":::

   키 자격 증명 모음에 새 서버에 대 한 액세스 권한을 부여 해야 합니다.

4. 서비스 주체를 등록 한 후 키의 유효성을 다시 검사 하 고 서버에서 정상적인 기능을 다시 시작 합니다.

   :::image type="content" source="media/concepts-data-access-and-security-data-encryption/restore-successful.png" alt-text="복원 된 기능을 보여 주는 Azure Database for PostgreSQL의 스크린샷":::

## <a name="next-steps"></a>다음 단계

 데이터 암호화에 대 한 자세한 내용은 [고객 관리 키를 사용 하 여 단일 서버 데이터 암호화 Azure Database for PostgreSQL](concepts-data-encryption-postgresql.md)를 참조 하세요.
