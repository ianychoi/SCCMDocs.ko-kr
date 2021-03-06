---
title: "Intune을 사용하여 관리되는 Windows 8.1 및 Windows 10 장치에 대한 구성 항목 만들기"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager Windows 10 구성 항목을 사용하여 Windows 10 컴퓨터에 대한 설정을 관리할 수 있습니다."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 23e1e4dc-623a-4521-ad04-ae9482927097
caps.latest.revision: 
caps.handback.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 7f5a50ae6ea05af7e864cf94df3063d70bd737b4
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-create-configuration-items-for-windows-81-and-windows-10-devices-managed-without-the-system-center-configuration-manager-client"></a>System Center Configuration Manager 클라이언트 없이 관리되는 Windows 8.1 및 Windows 10 장치에 대한 구성 항목을 만드는 방법

  
 System Center Configuration Manager **Windows 8.1 및 Windows 10** 구성 항목을 사용하여 Configuration Manager에서 온-프레미스로 관리되거나 Microsoft Intune에 등록된 Windows 8.1 및 Windows 10 장치에 대한 설정을 관리할 수 있습니다.  
  
### <a name="to-create-a-windows-81-and-windows-10-configuration-item"></a>Windows 8.1 및 Windows 10 구성 항목을 만들려면  
  
1.  Configuration Manager 콘솔에서 **자산 및 준수**을 클릭합니다.  
  
2.  **자산 및 준수** 작업 영역에서 **준수 설정**을 확장하고 **구성 항목**을 클릭합니다.  
  
3.  **홈** 탭의 **만들기** 그룹에서 **구성 항목 만들기**를 클릭합니다.  
  
4.  **구성 항목 만들기 마법사** 의 **일반**페이지에서 구성 항목에 대한 이름 및 선택적 설명을 지정합니다.  
  
5.  **만들려는 구성 항목의 유형 지정**에서 **Windows 8.1 및 Windows 10**을 선택합니다.  
  
6.  Configuration Manager 콘솔에서 구성 항목을 검색하고 필터링하기 위해 범주를 만들고 할당하려면 **범주**를 클릭합니다.  
  
7.  마법사의 **지원되는 플랫폼** 페이지에서 구성 항목을 평가하는 특정 Windows 플랫폼을 선택합니다.  
  
8.  마법사의 **장치 설정** 페이지에서 구성하려는 설정 그룹을 선택합니다. 자세한 내용은 이 항목의 [Windows 8.1 및 Windows 10 구성 항목 설정 참조](#BKMK_Setref) 섹션을 참조하고 **다음**을 클릭합니다.  
  
    > [!TIP]  
    >  원하는 설정이 나열되지 않은 경우 **기본 설정 그룹에 없는 추가 설정 구성 확인란**을 선택합니다.  
  
9. 각 설정 페이지에서 필요한 설정과 장치에서 준수되지 않는 경우 수정 여부(지원되는 경우)를 구성합니다.  
  
10. 각 설정 그룹에 대해 구성 항목이 비규격인 것으로 확인되는 경우 보고될 심각성을 구성할 수도 있습니다.  
  
    -   **없음** - 이 준수 규칙에 실패한 장치가 Configuration Manager 보고서에 오류 심각도를 보고하지 않습니다.  
  
    -   **정보** - 이 준수 규칙에 실패한 장치가 Configuration Manager 보고서에 **정보** 오류 심각도를 보고합니다.  
  
    -   **경고** - 이 준수 규칙에 실패한 장치가 Configuration Manager 보고서에 **경고** 오류 심각도를 보고합니다.  
  
    -   **위험** - 이 준수 규칙에 실패한 장치가 Configuration Manager 보고서에 **위험** 오류 심각도를 보고합니다.  
  
    -   **위험(이벤트 포함)** - 이 준수 규칙에 실패한 장치가 Configuration Manager 보고서에 **위험** 오류 심각도를 보고합니다. 또한 이 심각도 수준은 응용 프로그램 이벤트 로그에 Windows 이벤트로 기록됩니다.  
  
11. 마법사의 **플랫폼 적용 여부 가능성** 페이지에서 이전에 선택한 지원되는 플랫폼과 호환되지 않는 설정을 검토합니다. 뒤로 돌아가서 이러한 설정을 제거하거나 계속할 수 있습니다.  
  
    > [!TIP]  
    >  지원되지 않는 설정은 준수 여부에 대해 평가되지 않습니다.  
  
12. 마법사를 완료합니다.  
  
 **자산 및 준수** 작업 영역의 **구성 항목** 노드에서 새 구성 항목을 볼 수 있습니다.  
  
##  <a name="windows-81-and-windows-10-configuration-item-settings-reference"></a>Windows 8.1 및 Windows 10 구성 항목 설정 참조  
  
### <a name="password"></a>암호  
 다음 설정은 Windows 10 이상을 실행하는 장치에만 적용됩니다.  
  
|설정|세부 정보|  
|-------------|-------------|  
|**장치에 암호 설정 필요**|지원되는 장치에는 암호가 필요합니다.|  
|**최소 암호 길이(문자 수)**|암호의 최소 길이입니다.|  
|**다음 기간 후 암호 만료(일)**|암호를 변경해야 할 때까지의 기간(일)입니다.|  
|**저장한 암호 수**|이전에 사용한 암호의 재사용을 제한합니다.|  
|**다음 로그온 실패 횟수 후 장치 초기화**|이 횟수만큼 로그인에 실패하면 장치를 초기화합니다.|  
|**다음 유휴 시간 후 장치 잠그기**|장치가 잠기기 전까지 유휴 상태(사용자 입력이 없음)로 있을 수 있는 시간을 지정합니다.|  
|**암호 복잡도**|'1234' 등의 PIN을 지정할 수 있는지 아니면 강력한 암호를 입력해야 하는지를 선택합니다.|  
|**암호 품질**|필요한 암호 복잡도 수준과 생체 인식 장치 사용 가능 여부를 선택합니다.|  
|**Exchange Server에 암호 복구 PIN 전송**|-|
|**장치 암호화**|대상 장치에서 암호화를 사용하도록 설정합니다.|  
  
###  <a name="device"></a>장치  
  
|설정 이름|세부 정보|  
|------------------|-------------|  
|**화면 캡처**|장치 디스플레이의 스크린샷을 찍을 수 있습니다.<br /><br /> (Windows 10만 해당)|  
|**진단 데이터 전송**|앱 로그 파일을 전송할 수 있습니다.<br /><br /> (Windows 8.1에만 해당)|  
|**진단 데이터 제출(Windows 10)**|앱 로그 파일을 전송할 수 있습니다.<br /><br /> (Windows 10만 해당)|  
|**지리적 위치**|장치에서 위치 서비스 정보를 사용할 수 있습니다.<br /><br /> (Windows 10만 해당)|  
|**복사 및 붙여넣기**|복사 및 붙여넣기를 사용하여 앱 간에 데이터를 전송합니다.<br /><br /> (Windows 10만 해당)|
|**초기화**|최종 사용자가 장치를 초기 설정으로 다시 설정할 수 있습니다.<br /><br /> (Windows 10만 해당)|  
|**Bluetooth**|장치 Bluetooth 기능을 사용할 수 있습니다.|  
|**Bluetooth 검색 가능 모드**|다른 Bluetooth 장치에서 장치를 검색할 수 있습니다.<br /><br /> (Windows 10만 해당)|  
|**Bluetooth 광고**|Bluetooth 광고를 사용할 수 있습니다.<br /><br /> (Windows 10만 해당)|  
|**음성 녹음**|장치의 녹음 기능을 사용할 수 있습니다.<br /><br /> (Windows 10만 해당)|
|**Cortana**|Cortana 음성 지원을 사용할 수 있습니다.<br /><br /> (Windows 10만 해당)|
|**알림 센터 알림**|Windows 10에서 알림 창을 사용하거나 사용하지 않도록 설정합니다. <br /><br /> (Windows 10만 해당)|
|**지역 설정 수정(데스크톱만 해당)**|최종 사용자가 장치에서 지역 설정을 변경할 수 없도록 합니다.|
|**전원 및 절전 모드 설정 수정(데스크톱만 해당)**|최종 사용자가 장치에서 전원 및 절전 모드 설정을 변경할 수 없도록 합니다.|
|**언어 설정 수정(데스크톱만 해당)**|사용자가 장치에서 언어 설정을 변경할 수 없도록 합니다.|
|**시스템 시간 수정**|최종 사용자가 장치 날짜 및 시간을 변경할 수 없도록 합니다.|
|**장치 이름 수정**|최종 사용자가 장치 이름을 변경할 수 없도록 합니다.|
  
### <a name="email-management"></a>전자 메일 관리  
 다음 설정은 Windows 8.1 및 Windows 10을 실행하는 장치에 적용됩니다.  
  
|설정|세부 정보|  
|-------------|-------------|  
|**POP 및 IMAP 전자 메일**|POP 및 IMAP 표준을 사용하는 전자 메일 계정에 연결할 수 있습니다.|  
|**최대 전자 메일 보존 시간**|전자 메일을 서버에서 삭제할 때까지 보존할 시간입니다.|  
|**허용된 메시지 형식**|사용자 전자 메일에서 HTML 형식을 사용할 수 있는지 아니면 일반 텍스트만 사용할 수 있는지를 지정합니다.|  
|**일반 텍스트 전자 메일의 최대 크기(자동 다운로드된 경우)**|자동 다운로드 시 일반 텍스트 전자 메일의 최대 크기를 제어합니다.|  
|**HTML 전자 메일의 최대 크기(자동 다운로드된 경우)**|자동 다운로드 시 HTML 전자 메일의 최대 크기를 제어합니다.|  
|**첨부 파일의 최대 크기(자동 다운로드된 경우)**|자동으로 다운로드되는 전자 메일의 최대 크기를 구성합니다.|  
|**일정 동기화**|장치에 대한 일정을 동기화할 수 있습니다.|  
|**사용자 지정 전자 메일 계정**|장치에서 Microsoft 이외의 계정을 사용할 수 있습니다.|  
|**Windows 메일 앱에서 Microsoft 계정을 옵션으로 설정**|Windows Mail에서 Microsoft 계정에 대한 요구 사항을 제거하려면 이 옵션을 구성합니다.|  
  
### <a name="store"></a>스토어  
 다음 설정은 Windows 10 이상을 실행하는 장치에만 적용됩니다.  
  
|설정|세부 정보|  
|-------------|-------------|  
|**앱 스토어**|장치에서 앱 스토어에 액세스할 수 있습니다.|  
|**앱 스토어에 액세스하려면 암호 입력**|앱 스토어에 액세스하려는 사용자는 암호를 입력해야 합니다.|  
|**앱에서 바로 구매**|사용자가 앱에서 바로 구매를 진행할 수 있습니다.|
|**스토어에서 앱 자동 업데이트**|Windows 스토어에서 설치된 앱이 자동으로 업데이트되도록 합니다.|
|**개인 저장소만 사용**|최종 사용자가 개인 스토어에서만 앱을 다운로드하도록 허용하려면 이 옵션을 사용하도록 설정합니다.|
|**스토어에서 시작된 앱 시작**|장치에 미리 설치되었거나 Windows 스토어에서 다운로드한 모든 앱을 사용하지 않도록 설정하는 데 사용합니다.|
  
### <a name="browser"></a>브라우저  
 다음 설정은 Windows 8.1 및 Windows 10을 실행하는 장치에 적용됩니다.  
  
|설정|세부 정보|  
|-------------|-------------|  
|**웹 브라우저 허용**|장치에서 웹 브라우저를 사용할 수 있습니다.|  
|**자동 채우기**|사용자가 브라우저에서 자동 완성 설정을 변경할 수 있습니다.|  
|**액티브 스크립팅**|브라우저에서 ActiveX 스크립트와 같은 스크립트를 실행할 수 있습니다.|  
|**플러그 인**|사용자가 Internet Explorer에 플러그 인을 추가할 수 있습니다.|  
|**팝업 차단**|브라우저 팝업 차단을 사용하거나 사용하지 않도록 설정합니다.|  
|**쿠키**|장치에 쿠키를 저장할 수 있습니다.|  
|**사기 경고**|사기성일 수 있는 웹 사이트 경고를 사용하거나 사용하지 않도록 설정합니다.|  
  
###  <a name="internet-explorer"></a>Internet Explorer  
 다음 설정은 Windows 8.1 및 Windows 10을 실행하는 장치에 적용됩니다.  
  
|설정 이름|세부 정보|  
|------------------|-------------|  
|**항상 추적 방지 헤더 보내기**|검색 정보가 타사 사이트로 전송되지 않도록 차단합니다.|  
|**인트라넷 보안 영역**|인트라넷 보안 영역에 보안 수준을 할당합니다.|  
|**인터넷 영역의 보안 수준**|인터넷 영역에 대한 보안 수준을 구성합니다.|  
|**인트라넷 영역의 보안 수준**|인트라넷 영역에 대한 보안 수준을 구성합니다.|  
|**신뢰할 수 있는 사이트 영역의 보안 수준**|신뢰할 수 있는 사이트 영역에 대한 보안 수준을 구성합니다.|  
|**제한된 사이트 영역의 보안 수준**|제한된 사이트 영역에 대한 보안 수준을 구성합니다.|  
|**인트라넷 영역의 네임스페이스**|인트라넷 영역에서 추가하거나 제거할 웹 사이트를 구성합니다.|  
|**한 단어를 입력하면 인트라넷 사이트로 이동**|앞에 HTTP를 추가하지 않고 유효한 사이트 이름을 입력하는 경우 Internet Explorer에서 인트라넷 사이트로 자동 이동하도록 허용하는 설정을 사용하거나 사용하지 않도록 설정합니다.|  
|**엔터프라이즈 모드 메뉴 옵션**|사용자가 Internet Explorer **도구** 메뉴에서 엔터프라이즈 모드를 활성화 및 비활성화할 수 있습니다.|  
|**보고서 위치 로깅(URL)**|엔터프라이즈 모드가 활성화된 경우 방문한 웹 사이트를 기록할 URL을 지정합니다.|  
|**엔터프라이즈 모드 사이트 목록 위치(URL)**|엔터프라이즈 모드가 활성화된 경우 이 모드를 사용할 웹 사이트 목록의 위치를 지정합니다.|  
  
###  <a name="cloud"></a>클라우드  
 다음 설정은 Windows 8.1 및 Windows 10을 실행하는 장치에 적용됩니다.  
  
|설정 이름|세부 정보|Windows 8.1|Windows 10|  
|------------------|-------------|-----------------|----------------|  
|**설정 동기화**|장치 간에 설정을 동기화할 수 있습니다.|예|예|  
|**자격 증명 동기화**|장치 간에 자격 증명을 동기화할 수 있습니다.|예|예|  
|**Microsoft 계정**|장치에서 Microsoft 계정을 사용할 수 있습니다.|예|예|  
|**유료 네트워크에서 설정 동기화**|인터넷 연결이 유료일 때 설정을 동기화할 수 있습니다.|예|예|  
  
###  <a name="security"></a>보안  
  
|설정 이름|세부 정보|  
|------------------|-------------|  
|**서명되지 않은 파일 설치**|서명되지 않은 파일을 로드할 수 있습니다.<br /><br /> (Windows 10만 해당)|  
|**서명되지 않은 응용 프로그램**|서명되지 않은 앱을 로드할 수 있습니다.<br /><br /> (Windows 10만 해당)|  
|**SMS 및 MMS 메시징**|장치에서 SMS 및 MMS 메시징을 사용할 수 있습니다.<br /><br /> (Windows 10만 해당)|  
|**이동식 저장소**|장치에서 SD 카드와 같은 이동식 저장소를 사용할 수 있습니다.<br /><br /> (Windows 10만 해당)|  
|**카메라**|장치 카메라를 사용할 수 있습니다.<br /><br /> (Windows 10만 해당)|  
|**NFC(근거리 통신)**|장치에서 NFC를 사용하여 통신할 수 있습니다.<br /><br /> (Windows 10만 해당)|  
|**AntiTheft 모드**|Windows 10 AntiTheft 모드 사용 여부를 제어합니다.<br /><br /> (Windows 10만 해당)|  
|**USB 연결 허용**|장치가 USB 연결을 통해 이 장치에 연결할 수 있습니다.<br /><br /> (Windows 10만 해당)|
|**프로필 파일**|Windows RT 장치에 대해 VPN 프로필을 프로비전합니다.<br /><br /> Windows 8.1만 해당)|  
|**프로필 이름**|Windows RT 장치에 대해 VPN 프로필을 프로비전합니다.<br /><br /> Windows 8.1만 해당)|  
|**모든 사용자용 프로필**|Windows RT 장치에 대해 VPN 프로필을 프로비전합니다.<br /><br /> Windows 8.1만 해당)|  
  
###  <a name="peak-synchronization"></a>사용량이 가장 많을 때의 동기화  
 다음 설정은 Windows 10 이상을 실행하는 장치에만 적용됩니다.  
  
|설정 이름|세부 정보|  
|------------------|-------------|  
|**최대 사용량 시간 지정**|모바일 장치 동기화의 최대 사용량 시간을 구성합니다.|  
|**사용량이 가장 많을 때의 동기화 빈도**|구성한 사용량이 많은 시간 동안 동기화가 발생하는 빈도를 구성합니다.|  
|**사용량이 적을 때의 동기화 빈도**|구성한 사용량이 많은 시간 외에 동기화가 발생하는 빈도를 구성합니다.|  
  
###  <a name="roaming"></a>로밍  
  
|설정 이름|세부 정보|  
|------------------|-------------|  
|**로밍 시 장치 관리**|장치를 로밍 중일 때 Configuration Manager에서 장치를 관리할 수 있습니다.<br /><br /> (Windows 10만 해당)|  
|**로밍 시 소프트웨어 다운로드**|로밍 시 앱 및 소프트웨어를 다운로드할 수 있습니다.<br /><br /> (Windows 10만 해당)|  
|**로밍 시 전자 메일 다운로드**|로밍 시 전자 메일을 다운로드할 수 있습니다.<br /><br /> (Windows 10만 해당)|  
|**데이터 로밍**|데이터 액세스 시 네트워크 간 로밍이 가능합니다.| 
|**셀룰러에서 VPN**|셀룰러 네트워크에 연결된 동안 장치가 VPN 연결에 액세스할 수 있습니다.<br /><br /> (Windows 10만 해당)|
|**셀룰러에서 VPN 로밍**|셀룰러 네트워크에서 로밍하는 동안 장치가 VPN 연결에 액세스할 수 있습니다.<br /><br /> (Windows 10만 해당)| 
  
###  <a name="encryption"></a>암호화  
  
|설정 이름|세부 정보|  
|------------------|-------------|  
|**메모리 카드 암호화**|장치에 사용되는 모든 메모리 카드를 암호화해야 합니다.<br /><br /> (Windows 10만 해당)|  
|**장치에 파일 암호화**|장치의 파일을 암호화해야 합니다.|  
|**전자 메일 서명 필요**|메일을 전송하기 전에 서명해야 합니다.|  
|**서명 알고리즘**|서명된 메일의 서명 알고리즘을 선택합니다.|  
|**전자 메일 암호화 필요**|메일을 전송하기 전에 암호화해야 합니다.|  
|**암호화 알고리즘**|메일을 암호화하기 위한 알고리즘을 선택합니다.|  
  
###  <a name="wireless-communications"></a>무선 통신  
 다음 설정은 Windows 10 이상을 실행하는 장치에만 적용됩니다.  
  
|설정 이름|세부 정보|  
|------------------|-------------|  
|**무선 네트워크 연결**|장치 Wi-Fi 기능을 사용하거나 사용하지 않도록 설정합니다.|  
|**Wi-Fi 테더링**|사용자가 장치를 모바일 핫스팟으로 사용할 수 있습니다.|  
|**가능한 경우 Wi-Fi로 데이터 오프로드**|가능한 경우 장치에서 Wi-Fi 연결을 사용하려면이 옵션을 구성합니다.|  
|**Wi-Fi 핫스팟 보고**|-|  
|**Wi-Fi 수동 구성**|-|  
  
#### <a name="to-configure-a-wireless-network-connection"></a>무선 네트워크 연결을 구성하려면  
  
1.  **모바일 장치의 무선 통신 설정 구성** 페이지에서 **추가**를 클릭합니다.  
  
2.  **무선 네트워크 연결** 대화 상자에서 모바일 장치에 프로비전할 무선 연결에 대해 다음 정보를 지정합니다.  
  
|설정|추가 정보|  
|-------------|----------------------|  
|**네트워크 이름(SSID)**|Wi-Fi 네트워크의 이름을 입력합니다.|  
|**네트워크 연결**|**인터넷** 또는 **작업**을 선택합니다.|  
|**인증**|무선 연결에 대한 인증 방법을 다음 중에서 선택합니다.<br /><br /> - **개방형**<br /><br /> - **공유**<br /><br /> - **WPA**<br /><br /> - **WPA-PSK**<br /><br /> - **WPA2**<br /><br /> - **WPA2-PSK**|  
|**데이터 암호화**|이 연결에 사용되는 암호화 방법을 선택합니다. 선택한 **인증** 방법에 따라 다른 값을 선택할 수 있습니다.<br /><br /> - **사용 안 함**<br /><br /> - **WEP**<br /><br /> - **TKIP**<br /><br /> - **AES**|  
|**키 인덱스**|**데이터 암호화** 설정, **WEP** 에 사용할 키 인덱스를 **1** ~ **4**사이에서 선택합니다.|  
|**이 네트워크를 인터넷에 연결**|무선 연결의 모바일 장치가 인터넷에 연결할 수 있도록 하는 프록시 설정을 제공하려면 이 옵션을 선택합니다.|  
|**프록시 서버 설정**|필요에 따라 **HTTP** , **WAP** 및 **소켓**에 대해 **서버** 및 **포트**설정을 지정합니다.|  
|**802.1X 네트워크 액세스 사용**|EAP 방식을 지정하여 연결을 보호하려면 이 옵션을 선택합니다.|  
|**EAP 방식**|사용할 EAP 방식을 다음 중에서 선택합니다.<br /><br /> - **PEAP**<br> - **스마트 카드 또는 인증서**|  
  
  
  
### <a name="certificates"></a>인증서  
 모바일 장치에 설치할 인증서를 가져올 수 있습니다.  
  
 인증서를 가져오려면 **가져오기**를 클릭하고 다음 값을 지정합니다.  
  
-   **인증서 파일** – 찾아보기를 클릭하고 가져오려는 인증서 파일(확장명 **.cer** )을 선택합니다.  
  
-   **대상 저장소** – 모바일 장치에서 가져온 인증서를 추가할 하나 이상의 대상 저장소를 다음 중에서 선택합니다.  
  
    -   **루트**  
  
    -   **CA**  
  
    -   **일반**  
  
    -   **권한 있음**  
  
    -   **SPC**  
  
    -   **피어**  
  
-   **역할** – 대상 저장소로 **SPC** (소프트웨어 게시자 인증서)를 선택하는 경우 인증서와 연결할 역할을 다음 중에서 선택합니다.  
  
    -   **통신사**  
  
    -   **관리자**  
  
    -   **인증된 사용자**  
  
    -   **IT 관리자**  
  
    -   **인증되지 않은 사용자**  
  
    -   **신뢰할 수 있는 프로비전 서버**  
  
### <a name="system-security"></a>시스템 보안  
  
|설정|세부 정보|  
|-------------|-------------|  
|**사용자 계정 컨트롤**|장치에서 Windows 사용자 계정 컨트롤을 사용하거나 사용하지 않도록 설정합니다.|  
|**네트워크 방화벽**|Windows 방화벽을 사용하거나 사용하지 않도록 설정합니다.<br /><br /> (Windows 8.1에만 해당)|  
|**업데이트(Windows 8.1 및 이전 버전)**|컴퓨터에 Windows 소프트웨어 업데이트를 다운로드할 방법을 선택합니다. 예를 들어 업데이트는 자동으로 다운로드하되 사용자가 업데이트 설치 여부를 선택하도록 지정할 수 있습니다.|  
|**업데이트 최소 분류**|Windows 컴퓨터에 다운로드되는 업데이트의 최소 분류를 **없음**, **중요**또는 **권장**중에서 선택합니다.|  
|**업데이트(Windows 10)**|컴퓨터에 Windows 소프트웨어 업데이트를 다운로드할 방법을 선택합니다. 예를 들어 업데이트는 자동으로 다운로드하되 사용자가 업데이트 설치 여부를 선택하도록 지정할 수 있습니다.<br /><br /> (Windows 10만 해당)|  
|**설치 날짜**|업데이트를 설치할 날짜를 선택합니다.<br /><br /> (Windows 10만 해당)|  
|**설치 시간**|업데이트를 설치할 시간을 선택합니다.<br /><br /> (Windows 10만 해당)|  
|**SmartScreen**|Windows SmartScreen을 사용하거나 사용하지 않도록 설정합니다.|  
|**바이러스 방지**|바이러스 백신 소프트웨어가 장치에 설치되도록 하려면 선택합니다.|  
|**바이러스 방지 서명이 최신임**|바이러스 백신 서명 파일이 최신 상태가 되도록 하려면 선택합니다.|  
|**시험판 기능**|Microsoft에서 장치에 시험판 설정 및 기능을 배포할 수 있습니다.<br /><br /> (Windows 10만 해당)|  
|**루트 인증서 수동 설치**|(Windows 10만 해당)| 
|**수동 등록 취소 허용**|사용자가 MDM 솔루션을 통해 자신을 관리에서 등록 취소할 수 있습니다.| 
  
###  <a name="windows-server-work-folders"></a>Windows 서버 작업 폴더  
 다음 설정은 Windows 8.1 및 Windows 10을 실행하는 장치에 적용됩니다.  
  
|설정 이름|세부 정보|  
|------------------|-------------|  
|**작업 폴더 URL**|사용자가 장치에서 연결할 수 있는 Windows Server 작업 폴더의 위치를 구성합니다.|  
  
### <a name="allowed-and-blocked-apps-windows-phone-only"></a>허용 및 차단된 앱(Windows Phone만 해당)  
 회사의 규격 또는 비규격 Intune 관리앱 목록을 지정할 수 있습니다. Windows Phone에서 이러한 앱의 설치를 허용하거나 차단할 수 있습니다.  
  
 같은 구성 항목에서 호환 앱과 비호환 앱을 모두 지정할 수는 없습니다.  
  
#### <a name="to-specify-apps-that-are-allowed-or-blocked"></a>허용하거나 차단할 앱을 지정하려면  
  
**허용된 앱 및 차단된 앱 목록** 페이지에서 다음 정보를 지정합니다.  
  
|설정|추가 정보|  
    |-------------|----------------------|  
    |**차단되는 앱 목록**|사용자가 설치할 수 없는 앱 목록을 지정하려면 이 옵션을 선택합니다.|  
    |**허용되는 앱 목록**|사용자가 설치할 수 있는 앱 목록을 지정하려면 이 옵션을 선택합니다. 다른 모든 앱이 설치에서 차단됩니다.|  
    |**추가**|앱을 선택한 목록에 추가합니다. 원하는 이름, 앱 게시자(선택 사항) 및 앱 스토어의 앱 URL을 지정합니다.<br /><br /> URL을 지정하려면 Windows 스토어에서 사용할 앱을 검색합니다.<br /><br /> 앱 페이지를 열고 클립보드에 URL을 복사합니다. 이제 이 URL을 허용되는 앱 또는 차단되는 앱 목록에서 URL로 사용할 수 있습니다.<br /><br /> **예:** 스토어에서 **Skype** 앱을 검색합니다. 사용하는 URL이 **http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51**이 됩니다.|  
    |**편집**|선택한 앱의 이름, 게시자 및 URL을 편집할 수 있습니다.|  
    |**제거**|목록에서 선택한 앱을 삭제합니다.|  
    |**가져오기**|지정한 앱 목록을 쉼표로 구분된 값 파일로 가져옵니다. 파일의 형식, 응용 프로그램 이름, 게시자, 앱 URL을 사용합니다.|  
  
### <a name="windows-10-team"></a>Windows 10 팀  
 다음 설정은 Windows 10 Team을 실행하는 장치에만 적용됩니다.  
  
|설정 이름|세부 정보|  
|------------------|-------------|  
|**센서로 방에서 사람이 감지되면 화면이 자동으로 켜지도록 허용**|센서가 방에서 사람을 감지하면 장치가 자동으로 켜지도록 합니다.|  
|**무선 프로젝션용 PIN 필요**|장치의 무선 프로젝션 기능을 사용하려면 PIN을 입력해야 하는지 여부를 지정합니다.|  
|**유지 관리 기간**|장치를 업데이트할 수 있는 기간을 구성합니다. 시작 시간 및 지속 기간(1-5시간)을 구성할 수 있습니다.|
|**Azure Operational Insights**|Microsoft Operations Manager 제품군에 포함되어 있는 Azure Operational Insights는 Windows 10 Team 장치에서 로그 파일 데이터를 수집, 저장 및 분석합니다.<br>Azure Operational insights에 연결하려면 작업 영역 ID 및 작업 영역 키를 지정해야 합니다.| 
|**Miracast 무선 프로젝션**|Windows 10 Team 장치에서 Miracast 지원 장치를 프로젝션에 사용할 수 있도록 하려면 이 옵션을 사용합니다.<br>이 옵션을 사용하도록 설정하는 경우 **Miracast 채널 선택**에서 콘텐츠 프로젝션에 사용할 Miracast 채널을 선택합니다.|
|**시작 화면에 표시되는 모임 정보**|이 옵션을 사용하도록 설정하는 경우 **시작** 화면의 **모임** 타일에 표시할 정보를 선택할 수 있습니다. 다음과 같습니다.<br><br>- **이끌이 및 시간만 표시**<br>- **이끌이, 시간 및 제목 표시(비공개 모임의 경우 제목이 숨겨짐)**|
|**잠금 화면 배경 이미지 URL**|지정한 URL에서 Windows 10 Team 장치의 **시작** 화면에 사용자 지정 배경을 표시하려면 이 설정을 사용합니다.<br>이미지는 PNG 형식이어야 하며 URL은 **https://**로 시작되어야 합니다.| 
  
### <a name="windows-information-protection"></a>Windows Information Protection  

기업에서 직원 소유 장치가 증가됨에 따라 메일, 소셜 미디어, 공용 클라우드 등의 앱 및 서비스를 통해 실수에 의한 데이터 유출의 위험도 증가하며, 이러한 상황은 기업에서 제어할 수 없습니다. 예를 들면 직원이 자신의 개인 메일 계정에서 최신 엔지니어링 그림을 보내거나 제품 정보를 복사하여 트윗에 붙여넣거나 진행 중인 판매 보고서를 해당 공용 클라우드 저장소에 저장하는 경우가 있습니다.

WIP(Windows Information Protection)를 사용하면 직원 환경을 방해하지 않고 잠재적인 데이터 유출로부터 기업을 보호할 수 있습니다. 또한 WIP를 통해 사용자 환경 또는 다른 앱을 변경하지 않고도 엔터프라이즈 소유 장치와 직원이 직장으로 가져온 개인 장치에서 실수에 의한 데이터 유출로부터 기업을 보호할 수 있습니다.

 Configuration Manager WIP 구성 항목 설정은 EDP, 엔터프라이즈 네트워크 위치, 보호 수준 및 암호화 설정으로 보호되는 앱 목록을 관리합니다.

Configuration Manager로 엔터프라이즈 데이터 보호를 구성하는 방법에 대한 자세한 내용은 [WIP(Windows Information Protection)를 사용하여 엔터프라이즈 데이터 보호](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)를 참조하세요.


### <a name="microsoft-edge"></a>Microsoft Edge  
다음 설정은 Windows 10 이상을 실행하는 장치에 적용됩니다.  
  
|설정 이름|세부 정보|  
|------------------|-------------| 
|Microsoft Edge|장치에서 Edge 웹 브라우저를 사용할 수 있습니다.| 
|**주소 표시줄에 검색 제안 허용**|검색 구문을 입력하면 검색 엔진에서 사이트를 제안할 수 있습니다.|  
|**Internet Explorer로 인트라넷 트래픽 보내기 허용**||  
|**Do Not Track 허용**|Do Not Track은 사이트 방문을 추적하지 말 것을 웹 사이트에 알립니다.|  
|**SmartScreen 사용**|SmartScreen을 사용하여 사용자가 다운로드한 파일에 악성 코드가 포함되지 않았는지를 확인합니다.|  
|**팝업 허용**|브라우저 팝업을 허용하거나 사용하지 않도록 설정합니다.|  
|**쿠키 허용**|쿠키를 허용하거나 사용하지 않도록 설정합니다.|  
|**자동 채우기 허용**|Microsoft Edge 브라우저의 자동 채우기 기능을 사용하도록 허용합니다.|  
|**암호 관리자 허용**|Microsoft Edge 브라우저의 암호 관리자 기능을 사용하도록 허용합니다.|  
|**엔터프라이즈 모드 사이트 목록 위치**|엔터프라이즈 모드에서 열 웹 사이트 목록을 찾을 위치를 지정합니다. 사용자는 이 목록을 편집할 수 없습니다.|
|**플래그에 대한 액세스 차단**|최종 사용자가 개발자 및 실험 설정이 포함된 Edge의 about:flags 페이지에 액세스하지 못하게 합니다.|
|**SmartScreen 프롬프트 재정의**|최종 사용자가 잠재적으로 악의적인 웹 사이트에 대한 SmartScreen 필터 경고를 무시할 수 있도록 합니다.|
|**파일에 대한 SmartScreen 프롬프트 재정의**|최종 사용자가 잠재적으로 악의적인 파일 다운로드에 대한 SmartScreen 필터 경고를 무시할 수 있도록 합니다.|
|**WebRTC 로컬 호스트 IP 주소**|웹 RTC 프로토콜을 사용하여 전화를 걸 때 사용자의 localhost IP 주소를 차단합니다.|
|**기본 검색 엔진**|사용할 기본 검색 엔진을 지정합니다. 최종 사용자는 언제든지 이 값을 변경할 수 있습니다.|
|**OpenSearch XML URL**|OpenSearch XML 파일을 사용하여 Microsoft Edge에 대한 검색 서비스를 만들 수 있습니다.<br>자세한 내용은 [OpenSearch](https://msdn.microsoft.com/library/windows/desktop/dd940337)를 참조하세요.|
|**홈페이지(데스크톱만 해당)**|Edge 브라우저에서 홈페이지로 사용할 사이트의 목록을 추가합니다(데스크톱에만 해당).|  


### <a name="windows-defender"></a>Windows Defender
다음 설정은 Windows 10 이상을 실행하는 장치에 적용됩니다.
 
|설정 이름|세부 정보|  
|------------------|-------------|  
|**실시간 모니터링 허용**|맬웨어, 스파이웨어 및 기타 원치 않는 소프트웨어에 대한 실시간 검사를 사용하도록 설정합니다.|
|**동작 모니터링 허용**|Defender가 장치에서 의심스러운 활동의 알려진 특정 패턴을 확인할 수 있습니다.|
|**네트워크 검사 시스템 사용**|NIS(네트워크 검사 시스템)에서는 Microsoft Endpoint Protection Center에서 제공하는 알려진 취약점 서명을 사용해 악의적인 트래픽을 검색하고 차단함으로써 네트워크 기반 익스플로잇으로부터 장치를 보호할 수 있습니다.|
|**모든 다운로드 검사**|Defender가 인터넷에서 다운로드하는 모든 파일을 검사하는지 여부를 제어합니다.|
|**스크립트 검사 허용**|Defender가 Internet Explorer에서 사용되는 스크립트를 검사할 수 있습니다.|
|**파일 및 프로그램 활동 모니터링**|Defender가 장치에서 파일 및 프로그램 활동을 모니터링할 수 있습니다.
|**해결된 맬웨어 추적 일수**|이전에 영향을 받은 장치를 수동으로 확인할 수 있도록 지정한 기간(일) 동안 Defender가 해결된 맬웨어를 계속 추적하도록 합니다. 기간(일)을 0으로 설정하면 맬웨어가 격리 폴더에 유지되며 자동으로 제거되지 않습니다.|
|**클라이언트 UI 액세스 허용**|Windows Defender 사용자 인터페이스를 사용자가 볼 수 없도록 숨길지 여부를 제어합니다.<br>이 설정을 변경하면 다음에 사용자 PC를 다시 시작할 때 설정이 적용됩니다.|
|**시스템 검사 예약**|선택한 날짜와 시간에 정기적으로 수행되는 전체 또는 빠른 시스템 검사를 예약할 수 있습니다.|
|**매일 빠른 검색 예약**|선택한 시간에 매일 수행되는 빠른 검사를 예약할 수 있습니다.
|**검사하는 동안 CPU 사용 제한**|검사에 사용할 수 있는 CPU의 양을 1에서 100 사이로 제한할 수 있습니다.|
|**보관 파일 검사**|Defender에서 .zip 또는 .cab 파일과 같은 보관된 파일을 검사할 수 있습니다.|
|**전자 메일 메시지 검사**|Defender에서 장치에 도착하는 전자 메일 메시지를 검사할 수 있습니다.|
|**이동식 드라이브 검사**|Defender에서 USB 스틱과 같은 이동식 드라이브를 검사할 수 있습니다.|
|**매핑된 드라이브 검사**|Defender가 매핑된 네트워크 드라이브의 파일을 검사할 수 있습니다.<br>드라이브의 파일이 읽기 전용인 경우 Defender는 해당 파일에서 발견된 맬웨어를 제거할 수 없습니다.|
|**네트워크 공유 폴더에서 열린 파일 검사**|Defender가 UNC 경로에서 액세스한 파일 등 공유 네트워크 드라이브의 파일을 검사할 수 있습니다.<br>드라이브의 파일이 읽기 전용인 경우 Defender는 해당 파일에서 발견된 맬웨어를 제거할 수 없습니다.|
|**서명 업데이트 간격**|Defender가 새 서명 파일을 확인하도록 할 간격을 지정합니다.
|**클라우드 보호 허용**|사용자가 관리하는 장치의 맬웨어 활동에 대한 정보를 Microsoft 활성 보호 서비스가 수신하도록 허용하거나 차단합니다. 이 정보는 향후 서비스를 개선하는 데 사용됩니다.|
|**사용자에게 샘플 제출 확인**|악의적 파일인지 여부를 확인하기 위해 추가로 분석해야 할 수도 있는 파일을 Microsoft에 자동으로 전송할지 여부를 제어합니다.|
|**사용자 동의 없이 설치된 응용 프로그램 검색**|Windows Defender에서 사용자 동의 없이 설치된 것으로 분류한 소프트웨어가 실행되지 않도록 등록된 Windows 데스크톱 장치를 보호합니다. 이러한 응용 프로그램이 실행되지 않도록 장치를 보호하거나, 감사 모드를 사용하여 응용 프로그램이 사용자 동의 없이 설치될 때 보고할 수 있습니다.|
|**파일 및 폴더 제외**|C:\Path 또는 %ProgramFiles%\Path\filename.exe와 같은 파일 및 폴더를 제외 목록에 하나 이상 추가합니다. 이러한 파일과 폴더는 실시간 또는 예약된 검색에 포함되지 않습니다.|
|**파일 확장명 제외**|jpg 또는 txt와 같은 파일 확장명을 제외 목록에 하나 이상 추가합니다. 이러한 확장명의 파일은 실시간 또는 예약된 검색에 포함되지 않습니다.|
|**프로세스 제외**|.exe, .com 또는 .scr 유형의 프로세스를 제외 목록에 하나 이상 추가합니다. 이러한 프로세스는 실시간 또는 예약된 검색에 포함되지 않습니다.|

  
## <a name="see-also"></a>참고 항목  
 [System Center Configuration Manager 클라이언트 없이 관리되는 장치에 대한 구성 항목](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)