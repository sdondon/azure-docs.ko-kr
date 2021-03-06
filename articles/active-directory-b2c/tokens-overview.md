---
title: 토큰 개요 - Azure Active Directory B2C
description: Azure Active Directory B2C에서 사용되는 토큰에 대해 알아봅니다.
services: active-directory-b2c
author: msmimart
manager: celestedg
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 08/31/2020
ms.author: mimart
ms.subservice: B2C
ms.openlocfilehash: 19b65554801a22954499219e43ed021a7cc8c121
ms.sourcegitcommit: bcda98171d6e81795e723e525f81e6235f044e52
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89258438"
---
# <a name="overview-of-tokens-in-azure-active-directory-b2c"></a>Azure Active Directory B2C의 토큰 개요

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Azure AD B2C(Azure Active Directory B2C)는 각 [인증 흐름](application-types.md)을 처리할 때 여러 형식의 보안 토큰을 내보냅니다. 이 문서에서는 각 토큰 유형의 형식, 보안 특성 및 내용을 설명합니다.

## <a name="token-types"></a>토큰 형식

Azure AD B2C는 인증에 토큰을 사용하고 리소스에 안전하게 액세스하는 [OAuth 2.0 및 OpenID Connect 프로토콜](protocols-overview.md)을 지원합니다. Azure AD B2C에 사용되는 모든 토큰은 전달자에 대한 정보 어설션과 토큰의 주체를 포함하는 [JWT(JSON 웹 토큰)](https://self-issued.info/docs/draft-ietf-oauth-json-web-token.html)입니다.

Azure AD B2C와 통신하는 데 사용되는 토큰은 다음과 같습니다.

- *ID 토큰* - 애플리케이션에서 사용자를 식별하는 데 사용할 수 있는 클레임을 포함한 JWT입니다. 이 토큰은 동일한 애플리케이션 또는 서비스의 두 구성 요소 간의 통신에 대한 HTTP 요청에 안전하게 전송됩니다. 필요에 따라 ID 토큰에서 클레임을 사용할 수 있습니다. 일반적으로 계정 정보를 표시하거나 애플리케이션에서 액세스 제어를 결정할 수 있도록 하는 데 사용됩니다. ID 토큰은 서명되어 있지만, 암호화되지는 않습니다. 애플리케이션 또는 API에서 ID 토큰을 받으면 서명의 유효성을 검사하여 토큰이 인증되었음을 증명해야 합니다. 애플리케이션 또는 API도 토큰에서 일부 클레임의 유효성을 검사하여 유효하다는 것을 입증해야 합니다. 애플리케이션에서 유효성을 검사하는 클레임은 시나리오 요구 사항에 따라 다를 수 있지만, 애플리케이션은 모든 시나리오에서 몇 가지 일반적인 클레임 유효성 검사를 수행해야 합니다.
- *액세스 토큰* - API에 부여된 권한을 식별하는 데 사용할 수 있는 클레임을 포함한 JWT입니다. 액세스 토큰은 서명되어 있지만, 암호화되지는 않습니다. 액세스 토큰은 API 및 리소스 서버에 대한 액세스를 제공하는 데 사용됩니다.  API에서 액세스 토큰을 받으면 서명의 유효성을 검사하여 토큰이 인증되었음을 증명해야 합니다. API는 또한 토큰에서 일부 클레임의 유효성을 검사하여 유효하다는 것을 입증해야 합니다. 애플리케이션에서 유효성을 검사하는 클레임은 시나리오 요구 사항에 따라 다를 수 있지만, 애플리케이션은 모든 시나리오에서 몇 가지 일반적인 클레임 유효성 검사를 수행해야 합니다.
- *새로 고침 토큰* - 새로 고침 토큰은 OAuth 2.0 흐름에서 새 ID 토큰 및 액세스 토큰을 획득하는 데 사용됩니다. 이를 통해 애플리케이션은 해당 사용자와의 상호 작용을 요구하지 않으면서 사용자 대신 리소스에 장기적으로 액세스할 수 있습니다. 새로 고침 토큰은 애플리케이션에 불투명합니다. Azure AD B2C에서 발급되며 Azure AD B2C에서만 검사 및 해석될 수 있습니다. 또한 수명이 길지만, 새로 고침 토큰이 특정 기간 동안 지속될 것으로 예상하여 애플리케이션을 작성해서는 안 됩니다. 다양한 이유로 언제든지 새로 고침 토큰이 무효화될 수 있기 때문입니다. 애플리케이션에서 새로 고침 토큰이 유효한지 확인하는 유일한 방법은 Azure AD B2C에 대한 토큰 요청을 수행하여 교환을 시도해 보는 것입니다. 새로 고침 토큰을 새 토큰으로 교환할 때 토큰 응답에 새로운 새로 고침 토큰을 받게 됩니다. 새 새로 고침 토큰을 저장합니다. 이전에 요청에 사용된 새로 고침 토큰을 바꿉니다. 이렇게 하면 새로 고침 토큰이 최대한 오랫동안 유효한 상태로 유지되도록 할 수 있습니다.

## <a name="endpoints"></a>엔드포인트

[등록된 애플리케이션](tutorial-register-applications.md)은 토큰을 수신하고 해당 엔드포인트에 요청을 보내 Azure AD B2C와 통신합니다.

- `https://<tenant-name>.b2clogin.com/<tenant-name>.onmicrosoft.com/<policy-name>/oauth2/v2.0/authorize`
- `https://<tenant-name>.b2clogin.com/<tenant-name>.onmicrosoft.com/<policy-name>/oauth2/v2.0/token`

애플리케이션이 Azure AD B2C에서 수신하는 보안 토큰은 `/authorize` 또는 `/token` 엔드포인트에서 가져올 수 있습니다. `/authorize` 엔드포인트에서 ID 토큰을 획득하는 경우 JavaScript 기반 웹 애플리케이션에 로그인하는 사용자가 자주 사용하는 [암시적 흐름](implicit-flow-single-page-application.md)을 사용하도록 합니다. `/token` 엔드포인트에서 ID 토큰을 획득하는 경우 브라우저에서 숨겨진 토큰을 유지하는 [인증 코드 흐름](openid-connect.md#get-a-token)을 사용하도록 합니다.

## <a name="claims"></a>클레임

Azure AD B2C를 사용하는 경우 토큰의 내용에 대해 정교하게 세분화된 조정을 해야 합니다. [사용자 흐름](user-flow-overview.md) 및 [사용자 지정 정책](custom-policy-overview.md)을 구성하여 애플리케이션에 필요한 클레임에서 사용자 데이터의 특정 세트를 전송할 수 있습니다. 이러한 클레임은 **displayName** 및 **emailAddress**와 같은 표준 속성을 포함할 수 있습니다. 애플리케이션에서 이러한 클레임을 사용하여 사용자 및 요청을 안전하게 인증할 수 있습니다.

ID 토큰에 있는 클레임은 특정 순서로 반환되지 않습니다. 또한 언제든지 새 클레임을 ID 토큰에 도입할 수 있습니다. 새 클레임이 도입되므로 애플리케이션을 중단하지 말아야 합니다. 클레임에 [사용자 지정 특성](user-flow-custom-attributes.md)을 포함할 수도 있습니다.

다음 표에는 Azure AD B2C에서 발급한 ID 토큰 및 액세스 토큰에서 예측할 수 있는 클레임이 나열되어 있습니다.

| 속성 | 클레임 | 예제 값 | Description |
| ---- | ----- | ------------- | ----------- |
| 사용자 | `aud` | `90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6` | 토큰의 의도한 수신자를 식별합니다. Azure AD B2C의 경우 대상은 애플리케이션 ID입니다. 애플리케이션은 이 값의 유효성을 검사하고 일치하지 않을 경우 토큰을 거부해야 합니다. 대상은 리소스와 동의어입니다. |
| 발급자 | `iss` |`https://<tenant-name>.b2clogin.com/775527ff-9a37-4307-8b3d-cc311f58d925/v2.0/` | 토큰을 생성하고 반환하는 STS(보안 토큰 서비스)를 식별합니다. 또한 사용자가 인증한 디렉터리도 식별합니다. 애플리케이션은 발급자 클레임의 유효성을 검사하여 토큰이 적절한 엔드포인트에서 제공된 것인지 확인해야 합니다. |
| 발급 시간 | `iat` | `1438535543` | epoch 시간으로 표시된, 토큰이 발급된 시간입니다. |
| 만료 시간 | `exp` | `1438539443` | epoch 시간으로 표시된, 토큰이 무효화되는 시간입니다. 애플리케이션은 이 클레임을 사용하여 토큰 수명의 유효성을 확인해야 합니다. |
| 이전이 아님 | `nbf` | `1438535543` | epoch 시간으로 표시된, 토큰이 유효화되는 시간입니다. 일반적으로 토큰이 발급된 시간과 같습니다. 애플리케이션은 이 클레임을 사용하여 토큰 수명의 유효성을 확인해야 합니다. |
| 버전 | `ver` | `1.0` | Azure AD B2C에서 정의된 ID 토큰의 버전입니다. |
| 코드 해시 | `c_hash` | `SGCPtt01wxwfgnYZy2VJtQ` | 코드 해시는 OAuth 2.0 인증 코드와 함께 토큰이 발급된 경우에만 ID 토큰에 포함됩니다. 코드 해시는 인증 코드의 신뢰성이 유효한지 검사하는 데 사용할 수 있습니다. 이 유효성 검사를 수행하는 방법에 대한 자세한 내용은 [OpenID Connect 사양](https://openid.net/specs/openid-connect-core-1_0.html)을 참조하세요.  |
| 액세스 토큰 해시 | `at_hash` | `SGCPtt01wxwfgnYZy2VJtQ` | 액세스 토큰 해시는 OAuth 2.0 액세스 토큰과 함께 토큰이 발급된 경우에만 ID 토큰에 포함됩니다. 액세스 토큰 해시는 액세스 토큰의 신뢰성이 유효한지 검사하는 데 사용할 수 있습니다. 이 유효성 검사를 수행하는 방법에 대한 자세한 내용은 [OpenID Connect 사양](https://openid.net/specs/openid-connect-core-1_0.html)을 참조하세요.  |
| nonce | `nonce` | `12345` | nonce는 토큰 재생 공격을 완화하는 데 사용된 전략입니다. 애플리케이션은 `nonce` 쿼리 매개 변수를 사용하여 권한 부여 요청에 nonce를 지정할 수 있습니다. 요청에 제공한 값은 수정되지 않고 ID 토큰의 `nonce` 클레임에만 내보내집니다. 이 클레임을 통해 애플리케이션은 요청에 지정된 값에 대해 값의 유효성을 확인할 수 있습니다. 애플리케이션은 ID 토큰 유효성 검사 프로세스 중에 이 유효성 검사를 수행해야 합니다. |
| 제목 | `sub` | `884408e1-2918-4cz0-b12d-3aa027d7563b` | 애플리케이션의 사용자와 같이 토큰에서 정보를 어설션하는 주체입니다. 이 값은 변경할 수 없으며 재할당 또는 재사용할 수 없습니다. 예를 들어 리소스 액세스에 토큰을 사용할 때 이 값을 사용하면 안전하게 인증 검사를 수행할 수 있습니다. 기본적으로 주체 클레임은 디렉터리에 있는 사용자의 개체 ID로 채워집니다. |
| 인증 컨텍스트 클래스 참조 | `acr` | 해당 없음 | 이전 정책에서만 사용됩니다. |
| 보안 프레임워크 정책 | `tfp` | `b2c_1_signupsignin1` | ID 토큰을 회득하는 데 사용된 정책의 이름입니다. |
| 인증 시간 | `auth_time` | `1438535543` | 사용자가 자격 증명을 마지막으로 입력한 시간이며 epoch 시간으로 표시됩니다. 이러한 인증은 새로운 로그인, SSO(Single Sign-On) 세션 또는 다른 로그인 유형 간에 차이가 없습니다. `auth_time`은 애플리케이션(또는 사용자)이 Azure AD B2C에 대한 인증 시도를 마지막으로 시작한 시간입니다. 인증에 사용되는 메서드는 차별화되지 않습니다. |
| 범위 | `scp` | `Read`| 액세스 토큰에 대한 리소스에 부여된 권한입니다. 여러 부여된 권한은 공백으로 구분됩니다. |
| 권한 있는 주체 | `azp` | `975251ed-e4f5-4efd-abcb-5f1a8f566ab7` | 요청을 시작한 클라이언트 애플리케이션의 **애플리케이션 ID**입니다. |

## <a name="configuration"></a>구성

다음 속성은 Azure AD B2C에서 내보낸 [보안 토큰의 수명을 관리](configure-tokens.md)하는 데 사용됩니다.

- **액세스 및 ID 토큰 수명(분)** - OAuth 2.0 전달자 토큰의 수명은 보호된 리소스에 대한 액세스를 얻는 데 사용됩니다. 기본값은 60분입니다. 최솟값(포함)은 5분입니다. 최댓값(포함)은 1440분입니다.

- **새로 고침 토큰 수명(일)** - 새로 고침 토큰을 새 액세스 또는 ID 토큰을 획득하는 데 사용할 수 있기까지의 최대 기간입니다. 또한 기간에는 애플리케이션에 `offline_access` 범위가 부여된 경우 새로운 새로 고침 토큰을 가져오는 작업도 포함됩니다. 기본값은 14일입니다. 최솟값(포함)은 1일입니다. 최댓값(포함)은 90일입니다.

- **새로 고침 토큰 슬라이딩 윈도우 수명(일)** - 이 기간이 경과한 후 사용자는 애플리케이션에서 가져온 가장 최근의 새로 고침 토큰의 유효 기간과 관계 없이 강제로 다시 인증합니다. 스위치가 **제한된**으로 설정된 경우 제공될 수 있습니다. **새로 고침 토큰 수명(일)** 값보다 크거나 같아야 합니다. 스위치가 **제한 없는**으로 설정된 경우 특정 값을 제공할 수 없습니다. 기본값은 90일입니다. 최솟값(포함)은 1일입니다. 최댓값(포함)은 365일입니다.

다음 사용 사례는 이러한 속성을 사용하여 사용하도록 설정됩니다.

- 애플리케이션에서 지속적으로 활성 상태인 한 사용자가 모바일 애플리케이션에 무기한으로 로그인 상태를 유지하도록 허용합니다. 로그인 사용자 흐름에서 **새로 고침 토큰 슬라이딩 창 수명(일)** 을 **제한 없는**으로 설정할 수 있습니다.
- 적절한 액세스 토큰 수명을 설정하여 업계의 보안 및 규정 준수 요구 사항을 충족합니다.

이러한 설정을 암호 재설정 사용자 흐름에는 사용할 수 없습니다.

## <a name="compatibility"></a>호환성

다음 속성은 [토큰 호환성을 관리](configure-tokens.md)하는 데 사용됩니다.

- **발급자(iss) 클레임** - 이 속성은 토큰을 발급한 Azure AD B2C 테넌트를 식별합니다. 기본값은 `https://<domain>/{B2C tenant GUID}/v2.0/`입니다. `https://<domain>/tfp/{B2C tenant GUID}/{Policy ID}/v2.0/`의 값에는 Azure AD B2C 테넌트 및 토큰 요청에 사용된 사용자 흐름에 대한 ID가 포함됩니다. [OpenID Connect 검색 1.0 사양](https://openid.net/specs/openid-connect-discovery-1_0.html)과 호환되기 위해 애플리케이션이나 라이브러리에 Azure AD B2C가 필요한 경우 이 값을 사용합니다.

- **주체(sub) 클레임** - 이 속성은 토큰에서 정보를 어설션하는 엔터티를 식별합니다. 기본값은 **ObjectID**이며, 토큰의 `sub` 클레임을 사용자의 개체 ID로 채웁니다. **지원되지 않음**의 값은 이전 버전과 호환성을 위해서만 제공됩니다. 가능하면 바로 **ObjectID**로 전환하는 것이 좋습니다.

- **정책 ID를 나타내는 클레임** - 이 속성은 토큰 요청에 사용된 정책 ID가 채워지는 클레임 유형을 식별합니다. 기본값은 `tfp`입니다. `acr`의 값은 이전 버전과 호환성을 위해서만 제공됩니다.

## <a name="pass-through"></a>통과

사용자가 과정을 시작하면 Azure AD B2C는 ID 공급자로부터 액세스 토큰을 받습니다. Azure AD B2C는 이 토큰을 사용하여 해당 사용자에 대한 정보를 검색합니다. 사용자는 Azure AD B2C에서 등록한 애플리케이션으로 토큰이 통과되도록 [사용자 흐름에서 클레임을 활성화](idp-pass-through-user-flow.md)하거나 [사용자 지정 정책에서 클레임을 정의](idp-pass-through-custom.md)합니다. 토큰을 클레임으로 전달 하는 기능을 활용 하려면 응용 프로그램에서 [권장 사용자 흐름](user-flow-versions.md) 을 사용 해야 합니다.

Azure AD B2C는 현재 Facebook 및 Google을 비롯한 OAuth 2.0 ID 공급자의 액세스 토큰 통과만 지원합니다. 다른 모든 ID 공급자에 대한 클레임은 빈 상태로 반환됩니다.

## <a name="validation"></a>유효성 검사

토큰의 유효성을 검사하려면 애플리케이션이 해당 토큰의 서명과 클레임을 모두 확인해야 합니다. 기본 설정 언어에 따라 JWT의 유효성 검사에 다양한 오픈 소스 라이브러리를 사용할 수 있습니다. 고유한 유효성 검사 논리를 구현하는 대신 이러한 옵션을 탐색하는 것이 좋습니다.

### <a name="validate-signature"></a>서명의 유효성 검사

JWT에는 *헤더*, *본문* 및 *서명*이라는 3개의 세그먼트가 포함됩니다. 서명 세그먼트는 애플리케이션에서 신뢰할 수 있도록 토큰의 신뢰성이 유효한지 검사하는 데 사용할 수 있습니다. Azure AD B2C 토큰은 RSA 256 등의 업계 표준 비대칭 암호화 알고리즘을 사용하여 서명됩니다.

토큰의 헤더에는 토큰 서명에 사용된 키 및 암호화 방법에 대한 정보가 들어 있습니다.

```
{
        "typ": "JWT",
        "alg": "RS256",
        "kid": "GvnPApfWMdLRi8PDmisFn7bprKg"
}
```

**alg** 클레임의 값은 토큰을 서명하는 데 사용된 알고리즘을 나타냅니다. **kid** 클레임의 값은 토큰을 서명하는 데 사용된 공개 키를 나타냅니다. Azure AD B2C는 특정 시점에서 공개-프라이빗 키 쌍의 세트 중 하나를 사용하여 토큰에 서명할 수 있습니다. Azure AD B2C는 가능한 키 세트를 주기적으로 회전합니다. 이러한 키 변경을 자동으로 처리하도록 애플리케이션을 작성해야 합니다. Azure AD B2C에서 사용된 공개 키에 대한 업데이트를 확인하기 위한 적절한 빈도는 24시간입니다. 예기치 않은 키 변경을 처리 하려면 예기치 않은 **kid** 값을 수신 하는 경우 공개 키를 다시 검색 하도록 응용 프로그램을 작성 해야 합니다.

Azure AD B2C에는 OpenID Connect 메타데이터 엔드포인트가 있습니다. 애플리케이션은 이 엔드포인트를 사용하여 런타임 시 Azure AD B2C에 대한 정보를 요청할 수 있습니다. 이 정보에는 엔드포인트, 토큰 콘텐츠 및 토큰 서명 키가 포함됩니다. Azure AD B2C 테넌트에는 각 정책에 대한 JSON 메타데이터 문서가 포함되어 있습니다. 메타데이터 문서는 몇 가지 유용한 정보를 포함하는 JSON 개체입니다. 메타데이터에는 토큰 서명에 사용되는 공개 키 세트의 위치를 제공하는 **jwks_uri**가 포함됩니다. 해당 위치는 여기에 제공되어 있지만 메타데이터 문서를 사용하고 **jwks_uri**를 구문 분석하여 위치를 동적으로 가져오는 것이 가장 좋습니다.

```
https://contoso.b2clogin.com/contoso.onmicrosoft.com/b2c_1_signupsignin1/discovery/v2.0/keys
```
이 URL에 있는 JSON 문서에는 특정 시점에서 사용 중인 공개 키 정보가 모두 포함되어 있습니다. 앱은 JWT 헤더에 `kid` 클레임을 사용하여 특정 토큰 서명에 사용된 JSON 문서의 공개 키를 선택할 수 있습니다. 그런 다음 올바른 공개 키와 표시된 알고리즘을 사용하여 서명 유효성 검사를 수행할 수 있습니다.

`contoso.onmicrosoft.com` 테넌트의 `B2C_1_signupsignin1` 정책에 대한 메타데이터 문서는 다음에서 확인할 수 있습니다.

```
https://contoso.b2clogin.com/contoso.onmicrosoft.com/b2c_1_signupsignin1/v2.0/.well-known/openid-configuration
```

토큰을 서명하는 데 어떤 정책을 사용할지(그리고 메타데이터를 요청하기 위해 이동하는 위치) 결정하기 위한 두 가지 옵션이 있습니다. 먼저 정책 이름은 토큰의 `acr` 클레임에 포함됩니다. base-64로 본문을 디코딩하고 결과 JSON 문자열을 역직렬화하여 JWT의 본문에서 클레임을 구문 분석할 수 있습니다. `acr` 클레임은 토큰을 발급하는 데 사용된 정책의 이름입니다. 다른 옵션은 요청을 발급할 때 `state` 매개 변수의 값에 정책을 인코딩한 다음, 이를 디코딩하여 어떤 정책을 사용할지 결정하는 것입니다. 두 방법 중 하나는 유효합니다.

서명 유효성 검사를 수행하는 방법에 대한 설명은 이 문서의 범위를 벗어납니다. 많은 오픈 소스 라이브러리가 토큰의 유효성을 검사하는 데 유용할 수 있습니다.

### <a name="validate-claims"></a>클레임의 유효성 검사

애플리케이션 또는 API가 ID 토큰을 받은 경우 ID 토큰의 클레임에 대해서도 몇 가지 검사를 수행해야 합니다. 다음 클레임을 확인해야 합니다.

- **audience** - ID 토큰이 애플리케이션에 제공된 것이 맞는지 확인합니다.
- **not before** 및 **expiration time** - ID 토큰이 만료되지 않았는지 확인합니다.
- **issuer** - Azure AD B2C에서 애플리케이션에 토큰을 발급했는지 확인합니다.
- **nonce** - 토큰 재생 공격 완화를 위한 전략입니다.

애플리케이션에서 수행해야 하는 유효성 검사의 전체 목록은 [OpenID Connect 사양](https://openid.net)을 참조하세요.

## <a name="next-steps"></a>다음 단계

[액세스 토큰을 사용하는 방법](access-tokens.md)에 대해 자세히 알아보세요.

