---
title: 일반적인 명명 된 엔터티
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.topic: include
ms.date: 05/13/2020
ms.author: aahi
ms.openlocfilehash: 32e80c50ff6f543679852cbd7e5ce9bda92d01e1
ms.sourcegitcommit: f0b206a6c6d51af096a4dc6887553d3de908abf3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2020
ms.locfileid: "84140940"
---
끝점에 요청을 보낼 때 다음 엔터티 범주가 반환 됩니다 `/entities/recognition/general` .

| Category   | 하위 범주 | 설명                          | 시작 모델 버전                                                    | 참고 |
|------------|-------------|--------------------------------------|-------------------------------------------------------------|--------------------------------------|
| Person     | 해당 없음         | 사람의 이름입니다.  | `2019-10-01`  | NER v 2.1에서 반환 됩니다. |
| PersonType | 해당 없음         | 사용자가 보유 한 작업 유형 또는 역할 | `2020-02-01` | |
|위치    | 해당 없음         | 자연 스러운 랜드마크, 구조, 지리적 기능 및 지정 학적 엔터티     |  `2019-10-01` | NER v 2.1에서 반환 됩니다. |
|위치     | 지정 학적 엔터티 (GPE)        | 도시, 국가/지역, 주.      | `2020-02-01` | |
|위치     | Structural                       | 구조체를 만들었습니다. | `2020-04-01` | |
|위치     | 지리적       | 강, 대양 및 deserts와 같은 지리적 및 자연 기능. |  `2020-04-01` | |
|조직  | 해당 없음 | 회사, 정치적 그룹, 음악 밴드, 스포츠 클럽, 정부 기관, 공공 단체.  | `2019-10-01` | Nationalities 및 religions는이 엔터티 형식에 포함 되지 않습니다. NER v 2.1에서 반환 됩니다. |
|조직 | 의료 | 의료 회사 및 그룹. | `2020-04-01` |  |
|조직 | 재고 교환 | 재고 교환 그룹. | `2020-04-01` | |
| 조직 | 스포츠 | 스포츠 관련 조직. | `2020-04-01` |  |
| 이벤트  | 해당 없음 | 기록, 소셜 및 자연스럽 게 발생 하는 이벤트입니다. | `2020-02-01` |  |
| 이벤트  | Culture | 문화권 이벤트 및 휴일. | `2020-04-01` | |
| 이벤트  | Natural | 자연스럽 게 발생 하는 이벤트입니다. | `2020-04-01` |  |
| 이벤트  | 스포츠 | 스포츠 이벤트.  | `2020-04-01` | |
| 제품 | 해당 없음 | 다양 한 범주의 물리적 개체 | `2020-02-01` | |
| 제품 | 제품 컴퓨팅 | 제품을 계산 합니다. |  `2020-02-01 ` | |
| 기술 | 해당 없음 | 기능, 기술 또는 전문 지식. | `2020-02-01` |  |
| 주소 | 해당 없음 | 전체 우편 주소  | `2020-04-01` |  |
| PhoneNumber | 해당 없음 | 전화 번호 (미국과 EU 전화 번호만 해당). | `2019-10-01` | NER v 2.1에서 반환 됩니다. |
| 메일 | 해당 없음 | 전자 메일 주소. | `2019-10-01` | NER v 2.1에서 반환 됩니다. |
| URL | 해당 없음 | 웹 사이트에 대 한 Url입니다. | `2019-10-01` | NER v 2.1에서 반환 됩니다.  |
| IP | 해당 없음 | 네트워크 IP 주소. | `2019-10-01` | NER v 2.1에서 반환 됩니다. |
| DateTime | 해당 없음 | 날짜 및 시간입니다. | `2019-10-01` | NER v 2.1에서 반환 됩니다. | 
| DateTime | 날짜 | 일정 날짜 | `2019-10-01` | NER v 2.1에서 반환 됩니다. |
| DateTime | 시간 | 하루 중 시간 | `2019-10-01` | NER v 2.1에서 반환 됩니다. |
| DateTime | DateRange | 날짜 범위. | `2019-10-01` | NER v 2.1에서 반환 됩니다. |
| DateTime | TimeRange | 시간 범위. | `2019-10-01` | NER v 2.1에서 반환 됩니다. |
| DateTime | 기간 | 기간 | `2019-10-01` | NER v 2.1에서 반환 됩니다. |
| DateTime | 설정 | 반복 횟수를 설정 합니다. |  `2019-10-01` | NER v 2.1에서 반환 됩니다. |
| 수량 | 해당 없음 | 숫자 및 숫자 수량. | `2019-10-01` | NER v 2.1에서 반환 됩니다.  |
| 수량 | 숫자 | 숫자 | `2019-10-01` | NER v 2.1에서 반환 됩니다. |
| 수량 | 백분율 | 백분율.| `2019-10-01` | NER v 2.1에서 반환 됩니다. |
| 수량 | Ordinal | 서 수 번호입니다. | `2019-10-01` | NER v 2.1에서 반환 됩니다. |
| 수량 | Age | 에이징을. | `2019-10-01` |  NER v 2.1에서 반환 됩니다. |
| 수량 | 통화 | 환산. | `2019-10-01` | NER v 2.1에서 반환 됩니다. |
| 수량 | 차원 | 차원과 측정. | `2019-10-01` | NER v 2.1에서 반환 됩니다. |
| 수량 | 온도 | 낮게. | `2019-10-01` | NER v 2.1에서 반환 됩니다. |
