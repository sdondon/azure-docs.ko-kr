---
ms.service: data-factory
ms.topic: include
ms.date: 11/09/2018
author: linda33wj
ms.author: jingwang
ms.openlocfilehash: c0fcdf1cf69c55f63288138bc7377a78295cb2be
ms.sourcegitcommit: 3543d3b4f6c6f496d22ea5f97d8cd2700ac9a481
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86544693"
---
## <a name="review-deployed-resources"></a>배포된 리소스 검토

파이프라인은 자동으로 adftutorial Blob 컨테이너에서 출력 폴더를 만듭니다. 그런 다음 입력 폴더에서 출력 폴더로 emp.txt 파일을 복사합니다. 

1. Azure Portal의 **adftutorial** 컨테이너 페이지에서 **새로 고침**을 선택하여 출력 폴더를 확인합니다. 
    
    ![새로 고침](media/data-factory-quickstart-verify-output-cleanup/output-refresh.png)

2. 폴더 목록에서 **출력**을 선택합니다. 

3. **emp.txt**가 출력 폴더에 복사되었는지 확인합니다. 

    ![새로 고침](media/data-factory-quickstart-verify-output-cleanup/output-file.png)

## <a name="clean-up-resources"></a>리소스 정리

빠른 시작에서 만든 리소스는 두 가지 방법으로 정리할 수 있습니다. 리소스 그룹의 모든 리소스를 포함하고 있는 [Azure 리소스 그룹](../articles/azure-resource-manager/management/overview.md)을 삭제할 수 있습니다. 다른 리소스를 그대로 유지하려면 이 자습서에서 만든 데이터 팩터리만 삭제합니다.

리소스 그룹을 삭제하면 그 안에 포함된 데이터 팩터리를 포함한 모든 리소스가 삭제됩니다. 다음 명령을 실행하여 전체 리소스 그룹을 삭제합니다. 

```powershell
Remove-AzResourceGroup -ResourceGroupName $resourcegroupname
```

> [!Note]
> 리소스 그룹 삭제하는 데 약간의 시간이 걸릴 수 있습니다. 프로세스에 대해 조금 기다려 주십시오

전체 리소스 그룹이 아니라 데이터 팩터리만 삭제하려면 다음 명령을 실행 합니다. 

```powershell
Remove-AzDataFactoryV2 -Name $dataFactoryName -ResourceGroupName $resourceGroupName
```