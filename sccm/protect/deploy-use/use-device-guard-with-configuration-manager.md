---
title: "Windows Device Guard 관리 방법"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager를 사용하여 Windows Device Guard를 관리하는 방법을 알아봅니다."
ms.custom: na
ms.date: 10/20/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
caps.latest.revision: 
caps.handback.revision: 
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 8d84d0d65db7668baa7be9bbf0ad1df869b37919
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="device-guard-management-with-configuration-manager"></a>Configuration Manager로 Device Guard 관리

*적용 대상: System Center Configuration Manager(현재 분기)*

## <a name="introduction"></a>소개
Device Guard는 맬웨어와 기타 신뢰할 수 없는 소프트웨어로부터 PC를 보호하도록 설계된 Windows 10 기능 그룹입니다. 사용자가 알고 있는 승인된 코드만 실행할 수 있도록 하여 악의적인 코드가 실행되지 못하게 합니다.

Device Guard는 소프트웨어 및 하드웨어 기반 보안 기능을 모두 포함합니다. 구성 가능한 코드 무결성은 PC에서 실행할 수 있는 명시적인 소프트웨어 목록을 적용하는 소프트웨어 기반 보안 계층입니다. 자체적으로 구성 가능한 코드 무결성에는 하드웨어 또는 펌웨어 필수 구성 요소가 없습니다. Configuration Manager와 함께 배포된 Windows Defender 응용 프로그램 제어 정책을 사용하면 이 문서에서 설명하는 최소 Windows 버전 및 SKU 요구 사항을 충족하는 대상 컬렉션의 PC에서 구성 가능한 코드 무결성 정책을 사용할 수 있습니다. 선택적으로 Configuration Manager를 통해 배포된 코드 무결성 정책의 하이퍼바이저 기반 보호는 가능한 하드웨어의 그룹 정책을 통해 사용할 수 있습니다.

Device Guard에 대한 자세한 내용은 [Device Guard 배포 가이드](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)를 참조하세요.

## <a name="using-device-guard-with-configuration-manager"></a>Configuration Manager에서 Device Guard 사용

Configuration Manager를 사용하여 Device Guard가 컬렉션의 PC에서 실행되는 모드를 구성할 수 있는 Windows Defender 응용 프로그램 제어 정책을 배포할 수 있습니다. 

다음 모드 중 하나를 구성할 수 있습니다.

1.  **적용 사용** - 신뢰할 수 있는 실행 파일만 실행할 수 있습니다.
2.  **감사 전용** - 모든 실행 파일을 실행할 수 있지만, 실행되는 신뢰할 수 없는 실행 파일을 로컬 클라이언트 이벤트 로그에 로깅합니다.

>[!TIP]
>이 버전의 Configuration Manager에서 Device Guard는 시험판 기능입니다. 이 기능을 사용하도록 설정하려면 [System Center Configuration Manager의 시험판 기능](/sccm/core/servers/manage/pre-release-features)을 참조하세요.

## <a name="what-can-run-when-you-deploy-a-windows-defender-application-control-policy"></a>Windows Defender 응용 프로그램 제어 정책을 배포할 때 실행할 수 있는 항목

Windows Device Guard를 사용하면 사용자가 관리하는 PC에서 실행할 수 있는 사항을 철저하게 제어할 수 있습니다. 이 기능은 원하지 않는 소프트웨어가 실행되지 못하게 하는 것이 중요한 높은 수준의 보안이 요구되는 부서의 PC에 특히 유용할 수 있습니다.

정책을 배포할 때 일반적으로 다음과 같은 실행 파일을 실행할 수 있습니다.

- Windows 운영 체제 구성 요소
- Windows Hardware Quality Labs 시그니처가 있는 하드웨어 개발자 센터 드라이버
- Windows 스토어 앱
- Configuration Manager 클라이언트 
- Windows Defender 응용 프로그램 제어 정책이 처리된 후 PC에서 설치한 Configuration Manager를 통해 배포되는 모든 소프트웨어 
- Windows 구성 요소 업데이트 소스:
    - Windows Update
    - Windows Update for Business
    - Windows Server Update Services
    - Configuration Manager

>[!IMPORTANT]
>이러한 항목에 설치에 사용하는 방식(앞서 언급된 업데이트 메커니즘 또는 인터넷)과 상관없이 인터넷 또는 타사 소프트웨어 업데이트에서 자동으로 업데이트되는 Windows에 기본으로 제공되지 *않는* 소프트웨어는 포함되지 않습니다. Configuration Manager 클라이언트를 통해 배포된 소프트웨어 변경 사항만 실행할 수 있습니다.

## <a name="before-you-start"></a>시작하기 전에

Windows Defender 응용 프로그램 제어 정책을 구성하거나 배포하기 전에 다음 정보를 참조하세요.

- Device Guard 관리는 Configuration Manager의 시험판 기능이므로 변경될 수 있습니다.
- Configuration Manager에서 Device Guard를 사용하려면 관리하는 PC에서 Windows 10 Enterprise 버전 1703 이상이 실행 중이어야 합니다.
- 클라이언트 PC에서 정책을 처리하고 나면 Configuration Manager가 해당 클라이언트에서 관리된 설치 프로그램으로 구성되며, 정책을 처리한 후 SCCM을 통해 배포된 소프트웨어는 자동으로 신뢰됩니다. Windows Defender 응용 프로그램 제어 정책 프로세스가 처리되기 전에 관리되는 구성으로 설치된 소프트웨어는 자동으로 신뢰되지 않습니다.
- Windows Defender 응용 프로그램 제어 정책을 성공적으로 처리하려면 클라이언트 PC가 도메인 컨트롤러에 연결되어 있어야 합니다.
- 배포 중에 구성할 수 있는 Windows Defender 응용 프로그램 제어 정책의 준수는 기본적으로 매일 평가하도록 예약됩니다. 정책 처리 시 문제가 발생하면 규정 준수 평가 일정을 더 짧게 구성하면 좋을 수 있습니다(예: 1시간마다). 이 일정은 장애 발생 시 클라이언트에서 Windows Defender 응용 프로그램 제어 정책을 다시 처리하는 빈도를 나타냅니다.
- 선택한 적용 모드와 관계 없이 Windows Defender 응용 프로그램 제어 정책을 배포할 때는 클라이언트 PC에서 .hta 확장명을 사용하는 HTML 응용 프로그램을 실행할 수 없습니다.

## <a name="how-to-create-a-windows-defender-application-control-policy"></a>Windows Defender 응용 프로그램 제어 정책을 만드는 방법
1.  Configuration Manager 콘솔에서 **자산 및 준수**를 클릭합니다.
2.  **자산 및 준수** 작업 영역에서 **엔드포인트 보호**를 펼친 다음 **Windows Defender 응용 프로그램 제어 정책**을 클릭합니다.
3.  **홈** 탭의 **만들기** 그룹에서 **Windows Defender 응용 프로그램 제어 정책 만들기**를 클릭합니다.
4.  **Windows Defender 응용 프로그램 제어 정책 만들기 마법사**의 **일반** 페이지에서 다음 설정을 지정합니다.
    - **이름** - 이 Windows Defender 응용 프로그램 제어 정책에 대한 고유한 이름을 입력합니다. 
    - **설명** - 필요에 따라 Configuration Manager 콘솔에서 이 정책을 식별하는 데 도움이 되는 설명을 입력합니다.
    - **적용 모드** - 클라이언트 PC에서 다음과 같은 Device Guard 적용 방법 중 하나를 선택합니다.
        - **적용 사용** - 신뢰할 수 있는 실행 파일만 실행할 수 있습니다.
        - **감사 전용** - 모든 실행 파일을 실행할 수 있지만, 실행되는 신뢰할 수 없는 실행 파일을 로컬 클라이언트 이벤트 로그에 로깅합니다.
5.  필요에 따라 PC의 특정 파일 또는 폴더에 대한 신뢰를 추가하려면 **Windows Defender 응용 프로그램 제어 정책 만들기 마법사**의 **포함** 탭에서 **추가**를 클릭합니다. 
6.  **신뢰할 수 있는 파일 또는 폴더 추가** 대화 상자에서 신뢰하려는 파일 또는 폴더에 대한 정보를 지정합니다. 로컬 파일 또는 폴더 경로를 지정하거나 연결할 수 잇는 권한이 있는 원격 장치에 연결한 후 해당 장치의 파일 또는 폴더 경로를 지정할 수 있습니다.
Windows Defender 응용 프로그램 제어 정책에서 폴더의 특정 파일에 대한 신뢰를 추가하면 다음을 수행할 수 있습니다.
    - 관리되는 설치 관리자 동작 문제 해결
    - Configuration Manager로 배포할 수 없는 LOB(기간 업무) 앱 신뢰
    - 운영 체제 배포 이미지에 포함된 앱 신뢰 
7.  **다음**을 클릭한 다음 마법사를 완료합니다.

>[!IMPORTANT]
>Configuration Manager 클라이언트의 버전 1706 이상을 실행하는 클라이언트 PC에서만 신뢰할 수 있는 파일 또는 폴더를 포함하도록 지원됩니다. 모든 포함 규칙이 Windows Defender 응용 프로그램 제어 정책에 포함되어 있고 정책이 Configuration Manager 클라이언트에서 이전 버전을 실행하는 클라이언트 PC에 배포되는 경우 정책이 적용되지 않습니다. 이전 클라이언트를 업그레이드하여 이 문제를 해결합니다. 포함 규칙을 포함하지 않는 정책은 여전히 이전 버전의 Configuration Manager 클라이언트에 적용될 수 있습니다.

## <a name="how-to-deploy-a-windows-defender-application-control-policy"></a>Windows Defender 응용 프로그램 제어 정책을 배포하는 방법
1.  Configuration Manager 콘솔에서 **자산 및 준수**를 클릭합니다.
2.  **자산 및 준수** 작업 영역에서 **엔드포인트 보호**를 펼친 다음 **Windows Defender 응용 프로그램 제어 정책**을 클릭합니다.
3.  정책 목록에서 배포하려는 정책을 선택하고 **홈** 탭의 **배포** 그룹에서 **배포**를 클릭합니다.
4.  **Windows Defender 응용 프로그램 제어 정책 배포** 대화 상자에서 정책을 배포하려는 컬렉션을 선택합니다. 그런 다음 클라이언트에서 정책을 평가하는 일정을 구성합니다. 마지막으로 클라이언트에는 구성된 모든 유지 관리 기간 외에도 정책을 평가할 수 있는지 여부를 선택합니다.
5.  작업을 마쳤으면 **확인**을 클릭하여 정책을 배포합니다. 

### <a name="restarting-the-device-after-deploying-the-policy"></a>정책을 배포한 후 장치 다시 시작

클라이언트 PC에서 정책이 처리된 후에는 **컴퓨터 다시 시작**의 **클라이언트 설정**에 따라 해당 클라이언트가 다시 시작하도록 예약됩니다. 정책을 적용하기 위해 다시 시작해야 하는 것은 아니지만 기본값입니다. 다시 시작하기를 끄려면 다음 단계를 수행하세요.

1. **Windows Defender 응용 프로그램 정책 만들기** 마법사를 엽니다.
2. **일반** 페이지에서 **모든 프로세스에 대해 이 정책을 적용할 수 있도록 장치 다시 시작 적용** 확인란을 취소합니다.
3. **다음**을 계속 클릭하여 마법사를 종료합니다.



## <a name="how-to-monitor-a-windows-defender-application-control-policy"></a>Windows Defender 응용 프로그램 제어 정책을 모니터링하는 방법

모든 PC에 올바르게 적용되었는지 확인하기 위해 [준수 설정 모니터링](/sccm/compliance/deploy-use/monitor-compliance-settings) 문서의 정보를 사용하여 배포된 정책이 모든 PC에 올바르게 적용되었는지 모니터링할 수 있습니다.

Windows Defender 응용 프로그램 제어 정책의 처리를 모니터링하려면 클라이언트 PC에서 다음 로그 파일을 사용합니다.

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

차단 또는 감사되는 특정 소프트웨어를 확인하려면 다음 로컬 클라이언트 이벤트 로그를 참조하세요.

1.  실행 파일을 차단하고 감사하려면 **응용 프로그램 및 서비스 로그** > **Microsoft** > **Windows** > **코드 무결성** > **운영**을 사용합니다.
2.  Windows Installer 및 스크립트 파일을 차단하고 감사하려면 **응용 프로그램 및 서비스 로그** > **Microsoft** > **Windows** > **AppLocker** > **MSI 및 스크립트**를 사용합니다.

## <a name="automatically-let-software-run-if-it-is-trusted-by-intelligent-security-graph"></a>Intelligent Security Graph에서 신뢰할 수 있는 경우 소프트웨어 자동 실행

Microsoft ISG(Intelligent Security Graph)에서 결정하는 대로 잠긴 장치에서 좋은 평판이 있는 소프트웨어를 실행하게 할 수 있습니다. ISG에는 [Windows Defender SmartScreen](https://docs.microsoft.com/windows/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) 및 기타 Microsoft 서비스가 포함되어 있습니다. 신뢰할 수 있는 소프트웨어가 되도록 하려면 장치에서 Windows Defender SmartScreen을 실행해야 합니다.

1. **Windows Defender 응용 프로그램 정책 만들기** 마법사를 엽니다.
2. **포함** 페이지에서 **Intelligent Security Graph에서 신뢰하는 소프트웨어 권한 부여** 확인란을 선택합니다.
3. [신뢰할 수 있는 파일 또는 폴더] 상자에서 신뢰할 수 있게 하려는 파일과 폴더를 추가합니다.
4. **다음**을 계속 클릭하여 마법사를 종료합니다.



## <a name="security-and-privacy-information-for-device-guard"></a>Device Guard의 보안 및 개인 정보

- 이 시험판 버전의 경우 프로덕션 환경에서 Windows Defender 응용 프로그램 제어 정책을 **감사만** 적용 모드로 배포하지 마세요. 이 모드는 랩 설정에서만 기능을 테스트하는 데 도움이 됩니다.
- **감사 전용** 또는 **적용 사용** 모드에서 정책을 배포했으며 정책을 적용하기 위해 다시 시작하지 않은 장치는 신뢰할 수 없는 소프트웨어 설치에 취약합니다.
이 경우 장치를 다시 시작하거나 **적용 사용** 모드에서 정책을 받아도 소프트웨어가 계속 실행될 수 있습니다.
- Windows Defender 응용 프로그램 제어 정책이 유효한지 확인하려면 랩 환경에서 장치를 준비합니다. 그런 다음 **적용 사용** 정책을 배포하고 마지막으로 최종 사용자에게 장치를 제공하기 전에 장치를 다시 시작합니다.
- **적용 사용**으로 정책을 배포한 후, 나중에 **감사 전용**으로 동일한 장치에 정책을 배포하지 마세요. 이 구성을 사용하면 신뢰할 수 없는 소프트웨어가 실행될 수 있습니다.
- Configuration Manager를 사용하여 Windows Defender 응용 프로그램 제어 정책을 통해 클라이언트 PC에서 구성 가능한 코드 무결성을 사용하도록 설정하는 경우, 이 정책은 로컬 관리자 권한이 있는 사용자가 Windows Defender 응용 프로그램 제어 정책을 우회하거나 그렇지 않고 신뢰할 수 없는 소프트웨어를 실행하는 것을 차단하지 않습니다. 
- 로컬 관리자 권한이 있는 사용자가 구성 가능한 코드 무결성을 사용 안함으로 설정하지 못하게 하는 유일한 방법은 서명된 이진 파일을 배포하는 것입니다. 이 배포 방법은 그룹 정책을 통해 가능하지만 현재 Configuration Manager에서는 지원되지 않습니다.
- 클라이언트 PC에서 Configuration Manager를 관리된 설치 프로그램으로 설정하면 AppLocker 정책을 사용합니다. AppLocker는 관리된 설치 프로그램을 식별하는 데만 사용하고 모든 적용은 구성 가능한 코드 무결성을 통해 수행됩니다. 




