---
title: Azure IoT 솔루션에 연결된 IoT 플러그 앤 플레이 미리 보기 디바이스와 상호 작용(Python) | Microsoft Docs
description: Python을 사용하여 Azure IoT 솔루션에 연결된 IoT 플러그 앤 플레이 미리 보기 디바이스에 연결하고 상호 작용합니다.
author: elhorton
ms.author: elhorton
ms.date: 7/13/2020
ms.topic: quickstart
ms.service: iot-pnp
services: iot-pnp
ms.custom: mvc
ms.openlocfilehash: e3f00bb601cce17721c5247941588be1c2de788d
ms.sourcegitcommit: 46f8457ccb224eb000799ec81ed5b3ea93a6f06f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87352734"
---
# <a name="quickstart-interact-with-an-iot-plug-and-play-preview-device-thats-connected-to-your-solution-python"></a>빠른 시작: 솔루션에 연결된 IoT 플러그 앤 플레이 미리 보기 디바이스와 상호 작용(Python)

[!INCLUDE [iot-pnp-quickstarts-service-selector.md](../../includes/iot-pnp-quickstarts-service-selector.md)]

IoT 플러그 앤 플레이 미리 보기를 사용하면 기본 디바이스 구현에 대한 지식이 없어도 디바이스 모델과 상호 작용할 수 있으므로 IoT가 간소화됩니다. 이 빠른 시작에서는 Python을 사용하여 솔루션에 연결된 IoT 플러그 앤 플레이 디바이스에 연결하고 제어하는 방법을 보여줍니다.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="prerequisites"></a>필수 구성 요소

이 빠른 시작을 완료하려면 개발 머신에 Python 3.7이 필요합니다. [python.org](https://www.python.org/)에서 여러 플랫폼에 권장되는 최신 버전을 다운로드할 수 있습니다. 다음 명령을 사용하여 현재 Python 버전을 확인할 수 있습니다.  

```cmd/sh
python --version
```

다음 명령을 실행하여 [Python 서비스 SDK 미리 보기 패키지](https://pypi.org/project/azure-iot-hub/2.2.1rc0/)를 설치합니다.

```cmd/sh
pip3 install azure-iot-hub==2.2.1rc0
```

[!INCLUDE [iot-pnp-prepare-iot-hub.md](../../includes/iot-pnp-prepare-iot-hub.md)]

다음 명령을 실행하여 허브에 대한 IoT 허브 연결 문자열을 가져옵니다. 이 연결 문자열을 기록해 두십시오. 이 빠른 시작의 뒷부분에서 사용하게 됩니다.

```azurecli-interactive
az iot hub show-connection-string --hub-name <YourIoTHubName> --output table
```

다음 명령을 실행하여 허브에 추가한 디바이스에 대한 디바이스 연결 문자열을 가져옵니다. 이 연결 문자열을 기록해 두십시오. 이 빠른 시작의 뒷부분에서 사용하게 됩니다.

```azurecli-interactive
az iot hub device-identity show-connection-string --hub-name <YourIoTHubName> --device-id <YourDeviceID> --output
```

## <a name="run-the-sample-device"></a>샘플 디바이스 실행

이 빠른 시작에서는 Python으로 작성한 샘플 자동 온도 조절 디바이스를 IoT 플러그 앤 플레이 디바이스로 사용합니다. 샘플 디바이스를 실행하려면 다음을 수행합니다.

1. 원하는 폴더에서 터미널 창을 엽니다. 다음 명령을 실행하여 [Azure IoT Python SDK](https://github.com/Azure/azure-iot-sdk-python) GitHub 리포지토리를 다음 위치에 복제합니다.

    ```cmd/sh
    git clone https://github.com/Azure/azure-iot-sdk-python
    ```

1. 이 터미널 창은 이제 **디바이스** 터미널로 사용됩니다. 복제된 리포지토리의 폴더로 이동하여 */azure-iot-sdk-python/azure-iot-device/samples/pnp* 폴더로 이동합니다.

1. 다음과 같이 _디바이스 연결 문자열_을 구성합니다.

    ```cmd/sh
    set IOTHUB_DEVICE_CONNECTION_STRING=<YourDeviceConnectionString>
    ```

1. 다음 명령을 사용하여 샘플 자동 온도 조절 디바이스를 실행합니다.

    ```cmd/sh
    python pnp_thermostat.py
    ```

1. 디바이스에서 일부 정보를 보냈으며 현재 온라인 상태임을 보고했다는 메시지가 표시됩니다. 이 메시지는 디바이스가 허브로 원격 분석 데이터를 보내기 시작했으며, 이제 명령 및 속성 업데이트를 받을 준비가 되었음을 나타냅니다. 이 터미널을 닫지 마세요. 서비스 샘플이 작동하는지 확인하는 데 필요합니다.

## <a name="run-the-sample-solution"></a>샘플 솔루션 실행

이 빠른 시작에서는 Python에서 샘플 IoT 솔루션을 사용하여 방금 설정한 샘플 디바이스와 상호 작용합니다.

1. **서비스** 터미널로 사용할 또 다른 터미널 창을 엽니다. 서비스 SDK는 미리 보기 상태이므로 [Python SDK 미리 보기 분기](https://github.com/Azure/azure-iot-sdk-python/tree/pnp-preview-refresh)에서 샘플을 복제해야 합니다.

    ```cmd/sh
    git clone https://github.com/Azure/azure-iot-sdk-python -b pnp-preview-refresh
    ```

1. 복제된 리포지토리 분기의 폴더로 이동하여 */azure-iot-sdk-python/azure-iot-hub/samples* 폴더로 이동합니다.

1. 디바이스 ID 및 IoT Hub 연결 문자열의 환경 변수를 구성합니다.

    ```cmd/sh
    set IOTHUB_CONNECTION_STRING=<YourIOTHubConnectionString>
    set IOTHUB_DEVICE_ID=<Your device ID>
    ```

1. 샘플 폴더에는 `pnp` 접두사가 있는 샘플 파일이 4개 있습니다. 이 샘플은 각 API를 사용하여 IoT 플러그 앤 플레이 디바이스와 상호 작용하는 방법을 보여줍니다.

### <a name="get-digital-twin"></a>디지털 쌍 가져오기

**서비스** 터미널에서 다음 명령을 사용하여 이 샘플을 실행합니다.

```cmd/sh
python pnp_get_digital_twin_sample.py
```

출력은 디바이스의 디지털 쌍을 표시하고 해당하는 모델 ID를 출력합니다.

```cmd/sh
{'$dtId': 'mySimpleThermostat', '$metadata': {'$model': 'dtmi:com:example:Thermostat;1'}}
Model Id: dtmi:com:example:Thermostat;1
```

다음 코드 조각은 *pnp_get_digital_twin_sample.py*의 샘플 코드를 보여줍니다.

```python
    # Get digital twin and retrieve the modelId from it
    digital_twin = iothub_digital_twin_manager.get_digital_twin(device_id)
    if digital_twin:
        print(digital_twin)
        print("Model Id: " + digital_twin["$metadata"]["$model"])
    else:
        print("No digital_twin found")
```

### <a name="update-a-digital-twin"></a>디지털 쌍 업데이트

이 샘플은 *patch*를 사용하여 디바이스의 디지털 쌍을 통해 속성을 업데이트하는 방법을 보여줍니다. *pnp_update_digital_twin_sample.py*의 다음 코드 조각은 패치를 구성하는 방법을 보여줍니다.

```python
# If you already have a component thermostat1:
# patch = [{"op": "replace", "path": "/thermostat1/targetTemperature", "value": 42}]
patch = [{"op": "add", "path": "/targetTemperature", "value": 42}]
iothub_digital_twin_manager.update_digital_twin(device_id, patch)
print("Patch has been succesfully applied")
```

**서비스** 터미널에서 다음 명령을 사용하여 이 샘플을 실행합니다.

```cmd/sh
python pnp_update_digital_twin_sample.py
```

다음과 같은 출력이 표시되는 **디바이스** 터미널에서 업데이트가 적용되었는지 확인할 수 있습니다.

```cmd/sh
the data in the desired properties patch was: {'targetTemperature': 42, '$version': 2}
previous values
42
```

**서비스** 터미널에 패치 적용에 성공한 것이 확인됩니다.

```cmd/sh
Patch has been successfully applied
```

### <a name="invoke-a-command"></a>명령 호출

명령을 호출하려면 *pnp_invoke_command_sample.py* 샘플을 실행합니다. 이 샘플은 간단한 자동 온도 조절 디바이스에서 명령을 호출하는 방법을 보여줍니다. 이 샘플을 실행하기 전에 **서비스** 터미널에서 `IOTHUB_COMMAND_NAME` 및 `IOTHUB_COMMAND_PAYLOAD` 환경 변수를 설정합니다.

```cmd/sh
set IOTHUB_COMMAND_NAME="getMaxMinReport" # this is the relevant command for the thermostat sample
set IOTHUB_COMMAND_PAYLOAD="hello world" # this payload doesn't matter for this sample
```

**서비스** 터미널에서 다음 명령을 사용하여 샘플을 실행합니다.
  
```cmd/sh
python pnp_invoke_command_sample.py
```

**서비스** 터미널에 디바이스의 확인 메시지가 표시됩니다.

```cmd/sh
{"tempReport": {"avgTemp": 34.5, "endTime": "13/07/2020 16:03:38", "maxTemp": 49, "minTemp": 11, "startTime": "13/07/2020 16:02:18"}}
```

**디바이스** 터미널에, 디바이스가 명령을 수신한 것이 보입니다.

```cmd/sh
Command request received with payload
hello world
Will return the max, min and average temperature from the specified time hello to the current time
Done generating
{"tempReport": {"avgTemp": 34.2, "endTime": "09/07/2020 09:58:11", "maxTemp": 49, "minTemp": 10, "startTime": "09/07/2020 09:56:51"}}
Sent message
```

[!INCLUDE [iot-pnp-clean-resources.md](../../includes/iot-pnp-clean-resources.md)]

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서는 IoT 플러그 앤 플레이 디바이스를 IoT 솔루션에 연결하는 방법을 알아보았습니다. IoT 플러그 앤 플레이 디바이스 모델에 대한 자세한 내용은 다음을 참조하세요.

> [!div class="nextstepaction"]
> [IoT 플러그 앤 플레이 미리 보기 모델링 개발자 가이드](concepts-developer-guide.md)
