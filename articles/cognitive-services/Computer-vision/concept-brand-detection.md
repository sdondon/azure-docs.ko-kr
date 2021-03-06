---
title: 브랜드 검색 - Computer Vision
titleSuffix: Azure Cognitive Services
description: 이 문서에서는 특수 한 개체 검색 모드에 대해 설명 합니다. Computer Vision API를 사용 하 여 브랜드 및/또는 로고 검색
services: cognitive-services
author: PatrickFarley
manager: nitinme
ms.service: cognitive-services
ms.subservice: computer-vision
ms.topic: conceptual
ms.date: 08/08/2019
ms.author: pafarley
ms.openlocfilehash: 50e4fe1e2573c8566bbdf5697bb81b025a00935c
ms.sourcegitcommit: 58faa9fcbd62f3ac37ff0a65ab9357a01051a64f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/29/2020
ms.locfileid: "80131731"
---
# <a name="detect-popular-brands-in-images"></a>이미지에서 인기 있는 브랜드 검색

브랜드 검색은 수천 개의 글로벌 로고에 대한 데이터베이스를 사용하여 이미지 또는 비디오에서 상용 브랜드를 식별하는 [개체 검색](concept-object-detection.md)의 특수 모드입니다. 예를 들어 이 기능을 사용하여 소셜 미디어에서 가장 인기 있거나 미디어 제품 배치에서 가장 일반적인 브랜드를 검색할 수 있습니다.

Computer Vision 서비스는 지정된 이미지에 브랜드 로고가 있는지 여부를 검색합니다. 이 경우 브랜드 이름, 신뢰도 점수 및 로고 주변의 경계 상자 좌표를 반환합니다.

기본 제공 로고 데이터베이스는 가전제품, 의류 등의 인기 있는 브랜드를 포함하고 있습니다. 찾고 있는 브랜드가 Computer Vision 서비스에서 검색되지 않는 경우 [Custom Vision](https://docs.microsoft.com/azure/cognitive-services/Custom-Vision-Service/) 서비스를 사용하여 사용자 고유의 로고 검색기를 만들고 학습하는 것이 더 좋을 수 있습니다.

## <a name="brand-detection-example"></a>브랜드 검색 예제

다음 JSON 응답에서는 예제 이미지의 브랜드를 검색할 때 Computer Vision에서 반환하는 내용을 보여 줍니다.

![Microsoft 레이블과 로고가 있는 빨간색 셔츠](./Images/red-shirt-logo.jpg)

```json
"brands":[  
   {  
      "name":"Microsoft",
      "rectangle":{  
         "x":20,
         "y":97,
         "w":62,
         "h":52
      }
   }
]
```

브랜드 검색기는 경우에 따라 로고 이미지와 스타일이 적용된 브랜드 이름 모두를 별도의 두 로고로 선택합니다.

![Microsoft 레이블과 로고가 있는 회색 스웨터](./Images/gray-shirt-logo.jpg)

```json
"brands":[  
   {  
      "name":"Microsoft",
      "rectangle":{  
         "x":58,
         "y":106,
         "w":55,
         "h":46
      }
   },
   {  
      "name":"Microsoft",
      "rectangle":{  
         "x":58,
         "y":86,
         "w":202,
         "h":63
      }
   }
]
```

## <a name="use-the-api"></a>API 사용

브랜드 검색 기능은 [이미지 분석](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa) API의 일부 입니다. 이 API는 네이티브 SDK 또는 REST 호출을 통해 호출할 수 있습니다. `Brands` **Visualfeatures** 쿼리 매개 변수에를 포함 합니다. 그런 다음 전체 JSON 응답을 가져오는 경우 `"brands"` 섹션의 내용에 대 한 문자열을 구문 분석 하면 됩니다.

* [빠른 시작: Computer Vision .NET SDK](./quickstarts-sdk/client-library.md?pivots=programming-language-csharp)
* [빠른 시작: 이미지 분석 (REST API)](./quickstarts/csharp-analyze.md)
