---
title: Azure Analysis Services 별칭 서버 이름 | Microsoft Docs
description: Azure Analysis Services 서버 이름 별칭을 만드는 방법에 대해 알아봅니다. 그러면 사용자는 서버 이름 대신 짧은 별칭 이름으로 서버에 연결할 수 있습니다.
author: minewiskan
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 06/16/2020
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 435649c5431ff14461245fee88cebe4a2c571663
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85361441"
---
# <a name="alias-server-names"></a>별칭 서버 이름

사용자는 서버 이름 별칭을 사용하여 서버 이름 대신 짧은 *별칭*을 가진 Azure Analysis Services 서버에 연결할 수 있습니다. 클라이언트 애플리케이션에서 연결할 때 **link://** protocol 프로토콜 형식을 사용하여 별칭을 엔드포인트로 지정합니다. 그러면 엔드포인트가 연결할 실제 서버 이름을 반환합니다.

별칭 서버 이름은 다음과 같은 경우에 유용합니다.

- 사용자에게 영향을 주지 않고 서버 간 모델을 마이그레이션하는 경우 
- 친숙한 서버 이름이 사용자가 기억하기 쉽습니다. 
- 다른 시간에 다른 서버에 사용자를 지정하는 경우 
- Azure Traffic Manager를 사용할 때와 같이 지리적으로 보다 가까이 있는 인스턴스에 다른 지역의 사용자를 지정하는 경우 

유효한 Azure Analysis Services 서버 이름을 반환하는 모든 HTTPS 엔드포인트는 별칭으로 사용할 수 있습니다. 엔드포인트는 포트 443을 통해 HTTPS를 지원해야 하며 URI에 포트를 지정하지 말아야 합니다.

![링크 형식을 사용하는 별칭](media/analysis-services-alias/aas-alias-browser.png)

클라이언트에서 연결할 때 **link://** 프로토콜 형식으로 별칭 서버 이름을 입력합니다. 예를 들어 Power BI Desktop에서:

![Power BI Desktop 연결](media/analysis-services-alias/aas-alias-connect-pbid.png)

## <a name="create-an-alias"></a>별칭 만들기

별칭 엔드포인트를 만들려면 유효한 Azure Analysis Services 서버 이름을 반환하는 메서드를 사용할 수 있습니다. 예를 들어 실제 서버 이름을 포함하는 Azure Blob Storage에서 파일을 참조하거나, ASP.NET Web Forms 애플리케이션을 만들고 게시합니다.

이 예제에서 ASP.NET Web Forms 애플리케이션은 Visual Studio에서 만들어집니다. 페이지 참조 및 사용자 정의 컨트롤은 default.aspx 페이지에서 제거 됩니다. Default.aspx의 내용은 단순히 다음 페이지 지시문입니다.

```
<%@ Page Title="Home Page" Language="C#" AutoEventWireup="true" CodeBehind="Default.aspx.cs" Inherits="FriendlyRedirect._Default" %>
```

Default.aspx.cs의 Page_Load 이벤트는 Response.Write() 메서드를 사용하여 Azure Analysis Services 서버 이름을 반환합니다.

```
protected void Page_Load(object sender, EventArgs e)
{
    this.Response.Write("asazure://<region>.asazure.windows.net/<servername>");
}
```

## <a name="see-also"></a>참고 항목

[클라이언트 라이브러리](https://docs.microsoft.com/analysis-services/client-libraries?view=azure-analysis-services-current)   
[Power BI Desktop에서 연결](analysis-services-connect-pbi.md)
