---
title: "Mac 컴퓨터 응용 프로그램 만들기"
titleSuffix: Configuration Manager
description: "Mac 컴퓨터용 응용 프로그램을 만들고 배포할 때 고려해야 할 사항을 확인합니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab1aecdd-d943-44f5-b0a9-e8fe7439e5d6
caps.latest.revision: "9"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 912632c672c49deefc946e089dad6a82454c4b67
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2017
---
# <a name="create-mac-computer-applications-with-system-center-configuration-manager"></a>System Center Configuration Manager에서 Mac 컴퓨터 응용 프로그램 만들기

*적용 대상: System Center Configuration Manager(현재 분기)*

Mac 컴퓨터용 응용 프로그램을 만들고 배포할 때는 다음 사항을 고려하세요.  

> [!IMPORTANT]  
>  Configuration Manager 클라이언트가 설치된 Mac 컴퓨터에 응용 프로그램을 배포하는 방법에 대한 자세한 내용은 이 항목의 절차를 참조하세요. Microsoft Intune에 등록된 Mac 컴퓨터는 응용 프로그램 배포를 지원하지 않습니다.  

## <a name="general-considerations"></a>일반적인 고려 사항  
 System Center Configuration Manager를 사용하여 Configuration Manager Mac 클라이언트를 실행하는 Mac 컴퓨터에 응용 프로그램을 배포할 수 있습니다. Mac 컴퓨터에 소프트웨어를 배포하는 단계는 Windows 컴퓨터에 소프트웨어를 배포하는 단계와 비슷합니다. 그러나 Configuration Manager로 관리되는 Mac 컴퓨터용 응용 프로그램을 만들고 배포하기 전에 다음을 고려해야 합니다.  

-   Mac 컴퓨터에 Mac 응용 프로그램 패키지를 배포하려면 먼저 Mac 컴퓨터에서 **CMAppUtil** 도구를 사용하여 이러한 응용 프로그램을 Configuration Manager에서 읽을 수 있는 형식으로 변환해야 합니다.  

-   Configuration Manager에서는 Mac 응용 프로그램을 사용자에게 배포할 수 없습니다. 대신, 장치에만 배포할 수 있습니다. 마찬가지로, Mac 응용 프로그램 배포의 경우 Configuration Manager에서는 **소프트웨어 배포 마법사**의 **배포 설정** 페이지에서 **사용자의 기본 장치에 소프트웨어 미리 배포** 옵션을 지원하지 않습니다.  

-   Mac 응용 프로그램은 시뮬레이션된 배포를 지원합니다.  

-   **사용 가능**용도를 가진 Mac 컴퓨터에는 응용 프로그램을 배포할 수 없습니다.  

-   Mac 컴퓨터의 경우 소프트웨어를 배포할 때 절전 모드 해제 패킷 보내기 옵션이 지원되지 않습니다.  

-   Mac 컴퓨터에서는 응용 프로그램 콘텐츠를 다운로드하는 데 BITS(Background Intelligent Transfer Service)를 지원하지 않습니다. 응용 프로그램 다운로드가 실패할 경우 처음부터 다시 시작됩니다.  

-   Configuration Manager에서는 Mac 컴퓨터용 배포 유형을 만들 때 글로벌 조건을 지원하지 않습니다.  

## <a name="steps-to-create-and-deploy-an-application"></a>응용 프로그램을 만들어 배포하는 단계  
 다음 표에는 Mac 컴퓨터를 만들고 배포하기 위한 단계, 세부 정보 및 정보가 나와 있습니다.  

|단계|세부 정보|  
|----------|-------------|  
|**1단계**: Configuration Manager에서 사용할 수 있도록 Mac 응용 프로그램 준비|Mac 소프트웨어 패키지에서 Configuration Manager 응용 프로그램을 만들려면 먼저 Mac 컴퓨터에서 **CMAppUtil** 도구를 사용하여 Mac 소프트웨어를 Configuration Manager**.cmmac** 파일로 변환해야 합니다.|  
|**2단계**: Mac 소프트웨어가 포함된 Configuration Manager 응용 프로그램 만들기|**응용 프로그램 만들기 마법사**를 사용하여 Mac 소프트웨어용 응용 프로그램을 만듭니다.|  
|**3단계**: Mac 응용 프로그램에 대한 배포 유형 만들기|이 단계는 응용 프로그램에서 이 정보를 자동으로 가져오지 않은 경우에만 필요합니다.|  
|**4단계**: Mac 응용 프로그램 배포|**소프트웨어 배포 마법사**를 사용하여 Mac 컴퓨터에 응용 프로그램을 배포합니다.|  
|**5단계**: Mac 응용 프로그램 배포 모니터링|Mac 컴퓨터에 대한 응용 프로그램 배포의 성공 여부를 모니터링합니다.|  

## <a name="supplemental-procedures-to-create-and-deploy-applications-for-mac-computers"></a>Mac 컴퓨터용 응용 프로그램을 만들어 배포하기 위한 보충 절차  
 Configuration Manager로 관리되는 Mac 컴퓨터용 응용 프로그램을 만들어 배포하려면 다음 절차를 따르세요.  

###  <a name="step-1-prepare-mac-applications-for-configuration-manager"></a>1단계: Configuration Manager에서 사용할 수 있도록 Mac 응용 프로그램 준비  
 Configuration Manager 응용 프로그램을 만들고 Mac 컴퓨터에 배포하는 프로세스는 Windows 컴퓨터용 배포 프로세스와 비슷합니다. 그러나 Mac 배포 유형이 포함된 Configuration Manager 응용 프로그램을 만들기 전에 **CMAppUtil** 도구를 사용하여 응용 프로그램을 준비해야 합니다. 이 도구는 Mac 클라이언트 설치 파일과 함께 다운로드됩니다. **CMAppUtil** 도구는 다음 Mac 패키지의 검색 데이터를 포함하여 응용 프로그램에 대한 정보를 수집할 수 있습니다.  

-   Apple 디스크 이미지(.dmg)  

-   메타 패키지 파일(.mpkg)  

-   Mac OS X 설치 관리자 패키지(.pkg)  

-   Mac OS X 응용 프로그램(.app)  

응용 프로그램 정보를 수집한 후에 **CMAppUtil** 에서는 확장명이 **.cmmac**인 파일을 만듭니다. 이 파일은 Mac 소프트웨어용 설치 파일과 응용 프로그램이 이미 설치되었는지 여부를 평가하는 데 사용할 수 있는 검색 방법에 대한 정보를 포함합니다. **CMAppUtil** 은 여러 Mac 응용 프로그램이 포함된 **.dmg** 파일을 처리하여 각 응용 프로그램에 대해 서로 다른 배포 유형을 만들 수도 있습니다.  

1.  Mac 컴퓨터에서, Microsoft 다운로드 센터에서 다운로드한 **macclient.dmg** 파일의 콘텐츠를 추출한 폴더에 Mac 소프트웨어 설치 패키지를 복사합니다.  

2.  같은 Mac 컴퓨터에서, 터미널 윈도우를 열고 **macclient.dmg** 파일의 콘텐츠를 추출한 폴더로 이동합니다.  

3.  **Tools** 폴더로 이동하여 다음 명령줄 명령을 입력합니다.  

     **./CMAppUtil** *<속성\>*  

     예를 들어 사용자 데스크톱 폴더에 저장된 **MySoftware.dmg**라는 Apple 디스크 이미지 파일의 콘텐츠를 같은 폴더에서 **cmmac** 파일로 변환하려고 할 수 있습니다. 또한 디스크 이미지 파일에 있는 모든 응용 프로그램에 대해 **cmmac** 파일을 만들려고 할 수 있습니다. 이렇게 하려면 다음 명령줄을 사용합니다.  

     **./CMApputil –c /Users/** *<사용자 이름\>* **/Desktop/MySoftware.dmg -o /Users/** *<사용자 이름\>* **/Desktop -a**  

    > [!NOTE]  
    >  응용 프로그램 이름의 길이는 128자 이하여야 합니다.  

     **CMAppUtil**에 대한 옵션을 구성하려면 다음 표에 나온 명령줄 속성을 사용하세요.  

    |속성|추가 정보|  
    |--------------|----------------------|  
    |**-h**|사용 가능한 명령줄 속성을 표시합니다.|  
    |**-r**|제공된 **detection.xml** 파일의 **.cmmac** 을 **stdout**에 출력합니다. 이 출력에는 검색 매개 변수와 **CMAppUtil** 파일을 만드는 데 사용된 **.cmmac** 의 버전이 포함됩니다.|  
    |**-c**|변환할 원본 파일을 지정합니다.|  
    |**-o**|–c 속성과 함께 사용되어 출력 경로를 지정합니다.|  
    |**-a**|–c 속성과 함께 사용되어 디스크 이미지 파일에 있는 모든 응용 프로그램과 패키지에 대해 .cmmac 파일을 자동으로 만듭니다.|  
    |**-s**|검색 매개 변수가 없는 경우 **detection.xml** 만들기를 건너뛰고 **.cmmac** 파일 없이 **detection.xml** 파일을 강제로 만듭니다.|  
    |**-v**|진단 정보와 함께 **CMAppUtil** 도구에서 더욱 자세한 출력을 표시합니다.|  

4.  지정한 출력 폴더에 **.cmmac** 파일이 만들어졌는지 확인합니다.  

###  <a name="create-a-configuration-manager-application-that-contains-the-mac-software"></a>Mac 소프트웨어가 포함된 Configuration Manager 응용 프로그램 만들기  

Configuration Manager로 관리되는 Mac 컴퓨터용 응용 프로그램을 만들려면 다음 절차를 따르세요.  

1.  Configuration Manager 콘솔에서 **소프트웨어 라이브러리** > **응용 프로그램 관리** > **응용 프로그램**을 선택합니다.  

3.  **홈** 탭의 **만들기** 그룹에서 **응용 프로그램 만들기**를 선택합니다.  

4.  **응용 프로그램 만들기 마법사** 의 **일반**페이지에서 **설치 파일에서 이 응용 프로그램에 대한 정보 자동 검색**을 선택합니다.  

    > [!NOTE]  
    >  응용 프로그램에 대한 정보를 직접 지정하려면 **응용 프로그램 정보 수동 지정**을 선택합니다. 수동으로 정보를 지정하는 방법에 대한 자세한 내용은 [System Center Configuration Manager에서 응용 프로그램을 만드는 방법](../../apps/deploy-use/create-applications.md)을 참조하세요.  

5.  **유형** 드롭다운 목록에서 **Mac OS X**를 선택합니다.  

6.  **위치** 필드에서 응용 프로그램 정보를 검색할 Mac 응용 프로그램 설치 파일(**.cmmac** 파일)에 대한 UNC 경로를 *\\\\<서버\>\\<공유\>\\<파일 이름\>* 형식으로 지정합니다. 또는 **찾아보기**를 선택하여 설치 파일 위치를 찾아서 지정합니다.  

    > [!NOTE]  
    >  응용 프로그램이 포함된 UNC 경로에 대한 액세스 권한이 있어야 합니다.  

7.  **다음**을 선택합니다.  

8.  **응용 프로그램 만들기 마법사**의 **정보 가져오기** 페이지에서 가져온 정보를 검토합니다. 필요한 경우 **이전**을 선택하여 뒤로 돌아가서 오류를 수정할 수 있습니다. 계속 진행하려면 **다음**을 선택합니다.  

9. **응용 프로그램 만들기 마법사**의 **일반 정보** 페이지에서 응용 프로그램에 대한 정보(예: 응용 프로그램 이름, 설명, 버전, Configuration Manager 콘솔에서 응용 프로그램을 참조하는 데 도움이 되는 선택적 참조)를 지정합니다.  

    > [!NOTE]  
    >  일부 응용 프로그램 정보는 응용 프로그램 설치 파일에서 이전에 가져온 경우 이 페이지에 이미 있을 수 있습니다.  

10. **다음**을 선택하고 **요약** 페이지에서 응용 프로그램 정보를 검토한 다음 **응용 프로그램 만들기 마법사**를 완료합니다.  

11. Configuration Manager 콘솔의 **응용 프로그램** 노드에 새 응용 프로그램이 표시됩니다.  

###  <a name="step-3-create-a-deployment-type-for-the-mac-application"></a>단계: Mac 응용 프로그램에 대한 배포 유형 만들기  
 Configuration Manager로 관리되는 Mac 컴퓨터에 대한 배포 유형을 만들려면 다음 절차를 따르세요.  

> [!NOTE]  
>  **응용 프로그램 만들기 마법사**에서 응용 프로그램에 대한 정보를 자동으로 가져온 경우 해당 응용 프로그램에 대한 배포 유형이 이미 만들어져 있을 수 있습니다.  

1.  Configuration Manager 콘솔에서 **소프트웨어 라이브러리** > **응용 프로그램 관리** > **응용 프로그램**을 선택합니다.  

3.  응용 프로그램을 선택합니다. 그런 다음 **홈** 탭의 **응용 프로그램** 그룹에서 **배포 유형 만들기**를 선택하여 이 응용 프로그램에 대한 새 배포 유형을 만듭니다.  

    > [!NOTE]  
    >  또한 **응용 프로그램 만들기 마법사**와 *<응용 프로그램 이름\>***속성** 대화 상자의 **배포 유형** 탭에서 **배포 유형 만들기 마법사**를 시작할 수도 있습니다.  

4.  **배포 유형 만들기 마법사**의 **일반** 페이지에 있는 **유형** 드롭다운 목록에서 **Mac OS X**을 선택합니다.  

5.  **위치** 필드에서 응용 프로그램 설치 파일(**.cmmac** 파일)에 대한 UNC 경로를 \\\\<서버\>\\<공유\>\\<파일 이름\> 형식으로 지정합니다. 또는 **찾아보기**를 선택하여 설치 파일 위치를 찾아서 지정합니다.  

    > [!NOTE]  
    >  응용 프로그램이 포함된 UNC 경로에 대한 액세스 권한이 있어야 합니다.  

6.  **다음**을 선택합니다.  

7.  **배포 유형 만들기 마법사** 의 **정보 가져오기**페이지에서 가져온 정보를 검토합니다. 필요한 경우 **이전**을 선택하여 뒤로 돌아가서 오류를 수정할 수 있습니다. 계속 진행하려면 **다음**을 선택합니다.  

8.  **배포 유형 만들기 마법사** 의 **일반 정보**페이지에서 응용 프로그램 이름, 설명, 배포 유형이 제공되는 언어와 같은 응용 프로그램에 대한 정보를 지정합니다.  

    > [!NOTE]  
    >  일부 배포 유형 정보는 응용 프로그램 설치 파일에서 이전에 가져온 경우 이 페이지에 이미 있을 수 있습니다.  

9. **다음**을 선택합니다.  

10. **배포 유형 만들기 마법사**의 **요구 사항** 페이지에서, Mac 컴퓨터에 배포 유형을 설치하기 전에 충족해야 하는 조건을 지정할 수 있습니다.  

11. **추가**를 선택하여 **요구 사항 만들기** 대화 상자를 열고 새 요구 사항을 추가합니다.  

    > [!NOTE]  
    >  또한 *<배포 유형 이름\>* **속성** 대화 상자의 **요구 사항** 탭에서 새 요구 사항을 추가할 수도 있습니다.  

12. **범주** 드롭다운 목록에서 이 요구 사항을 장치에 대한 것으로 선택합니다.  

13. Mac 컴퓨터가 설치 요구 사항을 충족하는지 평가하는 데 사용할 조건을 **조건** 드롭다운 목록에서 선택합니다. 이 목록의 콘텐츠는 선택한 범주에 따라 달라집니다.  

14. 사용자 또는 장치가 설치 요구 사항을 충족하는지 평가하기 위해 선택된 조건을 지정된 값과 비교하는 데 사용할 연산자를 **연산자** 드롭다운 목록에서 선택합니다. 사용할 수 있는 연산자는 선택한 조건에 따라 달라집니다.  

15. 사용자 또는 장치가 설치 요구 사항을 충족하는지 평가하기 위해 선택한 조건 및 연산자와 함께 사용할 값을 **값** 필드에서 지정합니다. 사용할 수 있는 값은 선택한 조건과 연산자에 따라 달라집니다.

16. **확인**을 선택하여 요구 사항 규칙을 저장하고 **요구 사항 만들기** 대화 상자를 끝냅니다.  

17. **배포 유형 만들기 마법사**의 **요구 사항** 페이지에서 **다음**을 선택합니다.  

18. **배포 유형 만들기 마법사** 의 **요약**페이지에서 마법사가 수행하는 작업을 검토합니다.  필요한 경우 **이전**을 선택하여 뒤로 돌아가서 배포 유형 설정을 변경할 수 있습니다. **다음**을 선택하여 배포 유형을 만듭니다.  

19. **진행률** 페이지가 완료된 후에 수행된 작업을 검토하고 **닫기**를 선택하여 **배포 유형 만들기 마법사**를 완료합니다.  

20. **응용 프로그램 만들기 마법사**에서 이 마법사를 시작한 경우 마법사의 **배포 유형** 페이지로 돌아갑니다.  

###  <a name="deploy-the-mac-application"></a>Mac 응용 프로그램 배포  
 Mac 컴퓨터에 응용 프로그램을 배포하는 단계는 Windows 컴퓨터에 응용 프로그램을 배포하는 단계와 거의 동일하지만, 다음과 같은 차이점이 있습니다.  

-   사용자에게는 응용 프로그램을 배포할 수 없습니다.  

-   **사용 가능** 용도를 갖는 배포는 지원되지 않습니다.  

-   **소프트웨어 배포 마법사**의 **배포 설정** 페이지에서 **사용자의 기본 장치에 소프트웨어 미리 배포** 옵션이 지원되지 않습니다.  

-   Mac 컴퓨터에서는 소프트웨어 센터를 지원하지 않으므로 **소프트웨어 배포 마법사**의 **사용자 환경** 페이지에 있는 **사용자 알림** 설정이 무시됩니다.  

-   Mac 컴퓨터의 경우 소프트웨어를 배포할 때 절전 모드 해제 패킷 보내기 옵션이 지원되지 않습니다.  

> [!NOTE]  
>  Mac 컴퓨터만 포함하는 컬렉션을 만들 수 있습니다. 이렇게 하려면 쿼리 규칙을 사용하는 컬렉션을 만들고 [쿼리를 만드는 방법](../../core/servers/manage/create-queries.md) 항목의 예제 WQL 쿼리를 사용합니다.  

 자세한 내용은 [응용 프로그램 배포](../../apps/deploy-use/deploy-applications.md)를 참조하세요.  

###  <a name="step-5-monitor-the-deployment-of-the-mac-application"></a>5단계: Mac 응용 프로그램 배포 모니터링  
 Windows 컴퓨터에 대한 응용 프로그램 배포를 모니터링하는 것과 동일한 프로세스를 사용하여 Mac 컴퓨터에 대한 응용 프로그램 배포를 모니터링할 수 있습니다.  

 자세한 내용은 [응용 프로그램 모니터링](/sccm/apps/deploy-use/monitor-applications-from-the-console)을 참조하세요.  
