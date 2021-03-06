---
title: "응용 프로그램 관리에 대한 보안 및 개인 정보"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager에서 응용 프로그램 관리에 대한 보안 및 개인 정보 모범 사례입니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
caps.latest.revision: "8"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 7ca91443af58fc342380b819ca53e42b75556090
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2017
---
# <a name="security-and-privacy-for-application-management-in-system-center-configuration-manager"></a>System Center Configuration Manager에서 응용 프로그램 관리에 대한 보안 및 개인 정보

*적용 대상: System Center Configuration Manager(현재 분기)*


##  <a name="security-best-practices-for-application-management"></a>응용 프로그램 관리의 보안 모범 사례  

|보안 모범 사례|추가 정보|  
|----------------------------|----------------------|  
|응용 프로그램 카탈로그 지점이 HTTPS 연결을 사용하도록 구성하고 사용자에게 악성 웹 사이트의 위험성에 대해 알려 줍니다.|응용 프로그램 카탈로그 웹 사이트 지점과 응용 프로그램 카탈로그 웹 서비스 지점이 HTTPS 연결을 수락하도록 구성합니다. 이렇게 하면 사용자에 대해 서버가 인증되고 전송되는 데이터를 보거나 변조할 수 없게 됩니다. 사용자에게 신뢰할 수 있는 웹 사이트에만 연결하도록 주지시켜 소셜 엔지니어링 공격을 방지합니다.<br /><br /> HTTPS를 사용하지 않을 때는 응용 프로그램 카탈로그에 조직 이름을 확인 증명으로 표시하는 브랜딩 구성 옵션을 사용하지 마세요.|  
|역할 구분을 사용하고, 응용 프로그램 카탈로그 웹 사이트 지점과 응용 프로그램 카탈로그 서비스 지점을 별도의 서버에 설치합니다.|응용 프로그램 카탈로그 웹 사이트 지점이 손상될 경우 응용 프로그램 카탈로그 웹 서비스 지점과는 다른 별도의 서버에 웹 사이트 지점을 설치합니다. 이렇게 하면 Configuration Manager 클라이언트와 Configuration Manager 인프라를 보호할 수 있습니다. 응용 프로그램 카탈로그 웹 사이트 지점이 인터넷에서 클라이언트 연결을 수락하는 경우 서버가 공격에 취약해지므로 이것이 특히 중요합니다.|  
|사용자가 응용 프로그램 카탈로그 사용을 마칠 때 브라우저를 닫도록 일러 줍니다.|응용 프로그램 카탈로그를 위해 사용하던 브라우저 창에서 외부 웹 사이트를 탐색할 경우 브라우저에서 인트라넷의 신뢰할 수 있는 사이트에 적합한 보안 설정을 계속 사용합니다.|  
|사용자에게 기본 장치를 식별할 수 있도록 허용하는 대신 사용자 장치 선호도를 수동으로 지정합니다. 사용량 기준 구성은 사용하도록 설정하지 마세요.|사용자나 장치에서 수집되는 정보를 신뢰할 수 있는 정보로 간주해서는 안 됩니다. 신뢰할 수 있는 관리자가 지정하지 않은 사용자 장치 선호도를 사용하여 소프트웨어를 배포할 경우 해당 소프트웨어를 받을 권한이 없는 사용자에게 컴퓨터에 소프트웨어가 설치될 수 있습니다.|  
|콘텐츠를 배포 지점에서 실행하지 않고 배포 지점에서 다운로드하도록 배포를 구성합니다.|콘텐츠를 배포 지점에서 다운로드하여 로컬로 실행하도록 배포를 구성하면 Configuration Manager 클라이언트가 콘텐츠를 다운로드한 후에 패키지 해시를 확인합니다. 클라이언트는 해당 해시가 정책에 있는 해시와 일치하지 않을 경우 패키지를 삭제합니다. 반면 배포 지점에서 직접 콘텐츠를 실행하도록 배포를 구성할 경우 Configuration Manager 클라이언트가 패키지 해시를 확인하지 않으므로 Configuration Manager 클라이언트가 변조된 소프트웨어를 설치할 가능성이 있습니다.<br /><br /> 배포 지점에서 직접 배포를 실행해야 할 경우 배포 지점에서 패키지에 대한 NTFS 최소 권한을 사용하고 IPsec(인터넷 프로토콜 보안)을 통해 클라이언트와 배포 지점 간, 그리고 배포 지점과 사이트 서버 간의 채널을 보호합니다.|  
|**관리 권한으로 실행** 옵션이 필요한 경우 사용자가 프로그램과 상호 작용할 수 없도록 합니다.|프로그램을 구성할 때 **사용자가 이 프로그램을 사용하도록 허용** 옵션을 설정하면 사용자가 사용자 인터페이스에서 요청되는 프롬프트에 응답할 수 있습니다. 이와 함께 프로그램이 **관리 권한으로 실행**으로도 구성된 경우 해당 프로그램이 실행되는 컴퓨터에 침입한 공격자가 사용자 인터페이스를 사용하여 클라이언트 컴퓨터에서 권한을 승격시킬 수 있게 됩니다.<br /><br /> 관리 자격 증명이 필요한 소프트웨어 배포의 경우에는 설치용 Windows Installer 및 사용자별 상승된 권한을 사용하는 프로그램을 사용하세요. 설치 프로그램은 관리 자격 증명이 없는 사용자의 컨텍스트에서 실행해야 합니다. Windows Installer의 사용자별 상승된 권한을 사용하면 관리자 자격 증명을 요구하는 응용 프로그램을 가장 안전하게 배포할 수 있습니다.|  
|**설치 권한** 클라이언트 설정을 사용하여 사용자가 소프트웨어를 대화형으로 설치할 수 있는지 여부를 제한합니다.|**컴퓨터 에이전트** 클라이언트 장치 **설치 권한** 설정을 구성하여 응용 프로그램 카탈로그 또는 소프트웨어 센터를 사용해 소프트웨어를 설치할 수 있는 사용자 유형을 제한합니다. 예를 들어 **설치 권한** 을 **관리자만**으로 설정하여 사용자 지정 클라이언트 설정을 만듭니다. 그런 다음, 이 클라이언트 설정을 서버 컬렉션에 적용하여 관리 권한이 없는 사용자가 해당 컴퓨터에 소프트웨어를 설치하지 못하도록 합니다.|  
|모바일 장치의 경우 서명된 응용 프로그램만 배포합니다.|모바일 장치 응용 프로그램은 해당 모바일 장치가 신뢰하는 CA(인증 기관)에서 코드에 서명한 경우에만 배포합니다. 예를 들면 다음과 같습니다.<br /><br /><ul><li>VeriSign과 같은 잘 알려진 CA에서 서명한 공급업체의 응용 프로그램</li><li>내부 CA를 사용하여 Configuration Manager와 별개로 서명한 내부 응용 프로그램</li><li>응용 프로그램 유형을 만들 때 Configuration Manager를 사용하여 서명했고 서명 인증서를 사용하는 내부 응용 프로그램</li></ul>|  
|Configuration Manager에서 **응용 프로그램 만들기 마법사**를 사용하여 모바일 장치 응용 프로그램에 서명한 경우 서명 인증서 파일 위치와 통신 채널을 보호해야 합니다.|권한 상승과 메시지 가로채기(man-in-the-middle) 공격을 방지하려면 서명 인증서 파일을 보안 폴더에 저장하고 다음 컴퓨터 간에 IPsec 또는 SMB(서버 메시지 블록)를 사용합니다.<br /><br /><ul><li>Configuration Manager 콘솔을 실행하는 컴퓨터</li><li>인증서 서명 파일이 저장된 컴퓨터</li><li>응용 프로그램 원본 파일이 저장된 컴퓨터</li></ul> 또는 **응용 프로그램 만들기 마법사**를 실행하기 전에 Configuration Manager와 별개로 응용 프로그램에 서명합니다.|  
|참조 컴퓨터를 보호하도록 액세스 제어 구현|관리자가 참조 컴퓨터를 찾아 배포 유형에 검색 방법을 구성하는 경우 해당 컴퓨터가 손상되지 않았는지 확인해야 합니다.|  
|응용 프로그램 관리와 관련된 다음과 같은 역할 기반 보안 역할이 부여된 관리자를 제한하고 모니터링합니다.<br /><br /><ul><li>**응용 프로그램 관리자**</li><li>**응용 프로그램 작성자**</li><li> **응용 프로그램 배포 관리자**</li></ul>|역할 기반 관리를 구성하는 경우에도 응용 프로그램을 만들고 배포하는 관리자는 생각보다 많은 권한을 가질 수 있습니다. 예를 들어 응용 프로그램을 만들거나 수정하는 관리자는 해당 보안 범위에 없는 종속된 응용 프로그램을 선택할 수 있습니다.|  
|Microsoft App-V(Application Virtualization) 가상 환경을 구성하는 경우 가상 환경에서 동일한 신뢰 수준을 갖는 응용 프로그램을 선택합니다.|App-V 가상 환경의 응용 프로그램은 클립보드와 같은 리소스를 공유할 수 있기 때문에 선택한 응용 프로그램들이 동일한 신뢰 수준을 갖도록 가상 환경을 구성해야 합니다.<br /><br /> 자세한 내용은 [App-V 가상 환경 만들기](../../apps/deploy-use/create-app-v-virtual-environments.md)를 참조하세요.|  
|Mac 컴퓨터용 응용 프로그램을 배포하는 경우 원본 파일이 신뢰할 수 있는 원본으로 만들어졌는지 확인해야 합니다.|CMAppUtil 도구는 원본 패키지 서명의 유효성을 검사하지 않으므로 신뢰할 수 있는 원본에서 만들어졌는지 확인해야 합니다. CMAppUtil 도구는 파일이 변조되었는지 여부를 검색할 수 없습니다.|  
|Mac 컴퓨터용 응용 프로그램을 배포하는 경우 **.cmmac** 파일 위치와 이 파일을 Configuration Manager로 가져올 때 사용하는 통신 채널을 보호합니다.|CMAppUtil 도구가 생성하며 Configuration Manager로 가져오는 **.cmmac** 파일은 서명되지 않으며 유효성도 검사되지 않습니다. 이 파일의 변조를 방지하려면 보안 폴더에 해당 파일을 저장하고 다음 컴퓨터 간에 IPsec 또는 SMB를 사용합니다.<br /><br /><ul><li>Configuration Manager 콘솔을 실행하는 컴퓨터</li><li>**.cmmac** 파일을 저장하는 컴퓨터</li></ul>.|  
|웹 응용 프로그램 배포 유형을 구성하는 경우 연결을 보호하기 위해 HTTP가 아닌 HTTPS를 사용해야 합니다.|HTTPS 링크가 아니라 HTTP 링크를 사용하여 웹 응용 프로그램을 배포하면 장치가 Rogue 서버로 리디렉션될 수 있고 장치와 서버 간에 전송되는 데이터가 변조될 수 있습니다.|  

##  <a name="security-issues-for-application-management"></a>응용 프로그램 관리의 보안 문제  

-   낮은 권한을 가진 사용자가 클라이언트 컴퓨터에 있는 클라이언트 캐시에서 파일을 복사할 수 있습니다.  

     사용자는 클라이언트 캐시를 읽을 수 있지만 캐시에 쓸 수는 없습니다. 사용자에게 읽기 권한이 있으면 컴퓨터 간에 응용 프로그램 설치 파일을 복사할 수 있습니다.  

-   낮은 권한을 가진 사용자가 클라이언트 컴퓨터의 소프트웨어 배포를 기록하는 파일을 변경할 수 있습니다.  

     응용 프로그램 기록 정보는 보호되지 않으므로 사용자는 응용 프로그램 설치 여부를 보고하는 파일을 변경할 수 있습니다.  

-   APP-V 패키지는 서명되지 않습니다.  

     Configuration Manager의 App-V 패키지는 콘텐츠가 신뢰할 수 있는 원본에서 온 것이고 전송 중에 변경되지 않았음을 확인할 수 있는 서명을 지원하지 않습니다. 이 보안 문제를 완화하는 방법은 없습니다. 보안 모범 사례를 따라 신뢰할 수 있는 원본과 보안 위치에서 콘텐츠를 다운로드해야 합니다.  

-   게시된 App-V 응용 프로그램을 컴퓨터의 모든 사용자가 설치할 수 있습니다.  

     App-V 응용 프로그램이 컴퓨터에 게시되면 해당 컴퓨터에 로그인하는 모든 사용자가 이 응용 프로그램을 설치할 수 있습니다. 즉, 응용 프로그램이 게시된 후에 응용 프로그램을 설치할 수 있는 사용자를 제한할 수 없습니다.  

-   회사 포털에 대한 설치 권한을 제한할 수 없습니다.  

     설치 권한을 제한(예: 장치의 기본 사용자나 로컬 관리자로만 제한)하도록 클라이언트 설정을 구성할 수 있지만 회사 포털에는 이 설정이 적용되지 않습니다. 이 설정을 사용하면 사용자가 설치가 허용되지 않은 앱을 설치할 수 있어 권한 상승이 발생할 수 있습니다.  

##  <a name="BKMK_CertificatesSilverlight5"></a> 응용 프로그램 카탈로그에 필요한 높은 권한 모드 및 Microsoft Silverlight 5용 인증서  
 Configuration Manager 클라이언트에는 Microsoft Silverlight 5가 필요하며, 사용자가 응용 프로그램 카탈로그에서 소프트웨어를 설치하려면 Microsoft Silverlight 5를 높은 권한 모드로 실행해야 합니다. 기본적으로 Silverlight 응용 프로그램은 사용자 데이터에 액세스할 수 없도록 부분 신뢰 모드로 실행됩니다. Configuration Manager는 Microsoft Silverlight 5가 클라이언트에 아직 설치되어 있지 않으면 자동으로 설치합니다. 기본적으로 Configuration Manager는 컴퓨터 에이전트의 **Silverlight 응용 프로그램의 높은 권한 모드 실행을 허용합니다.** 클라이언트 설정을 **예**로 설정합니다. 이 설정을 사용하면 서명되고 신뢰할 수 있는 Silverlight 응용 프로그램에서 높은 권한 모드를 요청할 수 있게 됩니다.  

 응용 프로그램 카탈로그 웹 사이트 지점 사이트 시스템 역할을 설치하면 클라이언트에서 각 Configuration Manager 클라이언트 컴퓨터의 신뢰할 수 있는 게시자 컴퓨터 인증서 저장소에 Microsoft 서명 인증서를 설치합니다. 이 인증서를 사용하면 이 인증서로 서명된 Silverlight 응용 프로그램을 높은 권한 모드로 실행할 수 있습니다. 응용 프로그램 카탈로그의 소프트웨어를 설치하려는 컴퓨터에서는 이 모드를 사용해야 합니다. Configuration Manager에서는 이 서명 인증서를 자동으로 관리합니다. 서비스 연속성을 위해 이 Microsoft 서명 인증서를 수동으로 삭제하거나 이동하지 마십시오.  

> [!WARNING]  
>  **Silverlight 응용 프로그램의 높은 권한 모드 실행을 허용합니다.** 클라이언트 설정을 사용하도록 설정하는 경우 컴퓨터 저장소 또는 사용자 저장소의 신뢰할 수 있는 게시자 인증서 저장소에 있는 인증서로 서명된 모든 Silverlight 응용 프로그램을 높은 권한 모드에서 실행할 수 있습니다. 이 클라이언트 설정으로는 Configuration Manager 응용 프로그램 카탈로그 또는 컴퓨터 저장소의 신뢰할 수 있는 게시자 인증서 저장소에 대해서만 높은 권한 모드로 응용 프로그램을 실행할 수 없습니다. 맬웨어가 예를 들어 사용자 저장소의 신뢰할 수 있는 게시자 저장소에 Rogue 인증서를 추가할 경우 맬웨어가 자체 Silverlight 응용 프로그램을 사용하여 높은 권한 모드로 실행될 수 있습니다.  

 **Silverlight 응용 프로그램의 높은 권한 모드 실행을 허용합니다.** 클라이언트 설정을 **아니요**로 설정해도 Microsoft 서명 인증서가 클라이언트에서 삭제되지는 않습니다.  

 Silverlight의 신뢰할 수 있는 응용 프로그램에 대한 자세한 내용은 [신뢰할 수 있는 응용 프로그램](http://go.microsoft.com/fwlink/p/?LinkId=252842)을 참조하세요.  

##  <a name="privacy-information-for-application-management"></a>응용 프로그램 관리의 개인 정보 보호  
 응용 프로그램 관리를 사용하면 계층의 모든 클라이언트 컴퓨터 또는 클라이언트 모바일 장치에서 모든 응용 프로그램, 프로그램 또는 스크립트를 실행할 수 있습니다. Configuration Manager에서는 사용자가 실행하는 응용 프로그램, 프로그램 또는 스크립트의 유형이나 이러한 응용 프로그램, 프로그램 또는 스크립트에서 전송하는 정보의 유형을 제어하지 않습니다. 응용 프로그램 배포 과정에서 Configuration Manager는 클라이언트와 서버 간에 장치 및 로그인 계정을 식별하는 정보를 전송할 수 있습니다.  

 Configuration Manager에는 소프트웨어 배포 프로세스에 대한 상태 정보가 유지됩니다. 소프트웨어 배포 상태 정보는 클라이언트가 HTTPS를 사용하여 통신할 때를 제외하고 암호화되지 않습니다. 상태 정보는 데이터베이스에 암호화된 형식으로 저장되지 않습니다.  

 Configuration Manager 응용 프로그램 설치를 사용하여 클라이언트에 소프트웨어를 원격으로, 대화형으로 또는 자동으로 설치하는 경우 해당 소프트웨어의 소프트웨어 사용 조건이 적용될 수 있습니다. 이 소프트웨어 사용 시에는 System Center Configuration Manager의 소프트웨어 사용 조건과는 별도의 사용 조건이 적용됩니다. Configuration Manager를 사용하여 소프트웨어를 배포하기 전에는 항상 소프트웨어 사용 조건을 검토하고 동의해야 합니다.  

 응용 프로그램 배포는 기본적으로 이루어지지 않으며 여러 구성 단계가 필요합니다.  

 효율적인 소프트웨어 배포에 도움이 되는 두 가지 선택적인 기능으로 사용자 장치 선호도와 응용 프로그램 카탈로그가 있습니다.  

-   사용자 장치 선호도는 사용자를 장치에 매핑하여, Configuration Manager 관리자가 특정 사용자에게 소프트웨어를 배포하면 사용자가 가장 자주 사용하는 하나 이상의 컴퓨터에 자동으로 해당 소프트웨어가 설치됩니다.  

-   응용 프로그램 카탈로그는 사용자가 소프트웨어를 설치하도록 요청할 수 있는 웹 사이트입니다.  

 다음 섹션에서는 사용자 장치 선호도 및 응용 프로그램 카탈로그와 관련된 개인 정보 보호에 대해 설명합니다.  

 응용 프로그램 관리를 구성하기 전에 개인 정보 보호 요구 사항을 고려하십시오.  

##  <a name="user-device-affinity"></a>사용자 장치 선호도  
-  Configuration Manager는 클라이언트 및 관리 지점 사이트 시스템 간에 정보를 전송할 수 있습니다. 이 정보를 통해 컴퓨터와 로그인 계정 및 로그인 계정의 요약된 사용량을 식별할 수 있습니다.  
-  클라이언트가 HTTPS를 사용하여 통신해야 하도록 관리 지점을 구성하지 않는 한, 클라이언트 및 서버 간에 전송되는 정보는 암호화되지 않습니다.  
-  사용자를 장치에 매핑하는 데 사용하는 컴퓨터 및 로그인 계정 사용량 정보는 클라이언트 컴퓨터에 저장되고, 관리 지점으로 전송된 후 Configuration Manager 데이터베이스에 저장됩니다. 오래된 정보는 기본적으로 90일 이후에 데이터베이스에서 삭제됩니다. 삭제 동작은 **오래된 사용자 장치 선호도 데이터 삭제** 사이트 유지 관리 작업을 설정하여 구성할 수 있습니다.
-  Configuration Manager는 사용자 장치 선호도에 대한 상태 정보를 유지 관리합니다. HTTPS를 사용하여 통신하도록 관리 지점의 클라이언트를 구성하지 않는 한, 상태 정보는 전송 도중 암호화되지 않습니다. 데이터베이스에서는 상태 정보가 암호화된 형식으로 저장되지 않습니다.  
-  컴퓨터, 로그인 계정 사용량 정보 및 상태 정보가 Microsoft로 전송되지는 않습니다.  
-  사용자 및 장치 선호도를 설정하는 데 사용하는 컴퓨터 및 로그인 사용량 정보는 항상 사용하도록 설정되어 있습니다. 또한 사용자 및 관리자가 사용자 장치 선호도 정보를 제공할 수도 있습니다.  

##  <a name="application-catalog"></a>응용 프로그램 카탈로그  
-  Configuration Manager 관리자는 응용 프로그램 카탈로그를 통해 사용자가 실행할 수 있도록 응용 프로그램, 프로그램 또는 스크립트를 게시할 수 있습니다. Configuration Manager에서는 카탈로그에 게시되는 프로그램 또는 스크립트의 유형이나 이러한 프로그램 또는 스크립트에서 전송하는 정보의 유형을 제어하지 않습니다.    
-  Configuration Manager는 클라이언트 및 응용 프로그램 카탈로그 사이트 시스템 역할 간에 정보를 전송할 수 있습니다. 이 정보를 통해 컴퓨터 및 로그인 계정을 식별할 수 있습니다. HTTPS를 사용하여 클라이언트를 연결하도록 이러한 사이트 시스템 역할을 구성하지 않는 한, 클라이언트 및 서버 간에 전송되는 정보는 암호화되지 않습니다.  
-  응용 프로그램 승인 요청에 대한 정보는 Configuration Manager 데이터베이스에 저장됩니다. 취소 또는 거부된 요청과 해당 요청 기록 항목은 기본적으로 30일 후에 삭제됩니다. 삭제 동작은 **오래된 응용 프로그램 요청 데이터 삭제** 사이트 유지 관리 작업을 설정하여 구성할 수 있습니다. 상태가 승인됨 및 보류 중인 응용 프로그램 승인 요청은 삭제되지 않습니다.  
-  응용 프로그램 카탈로그에서 보내고 받는 모든 정보는 Microsoft로 전송되지 않습니다.  
-  응용 프로그램 카탈로그는 기본적으로 설치되지 않습니다. 이를 설치하려면 몇 가지 구성 단계가 필요합니다.  
