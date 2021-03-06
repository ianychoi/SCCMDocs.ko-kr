---
title: "설치 다운로더"
titleSuffix: Configuration Manager
description: "사이트 설치 시 주요 설치 파일의 최신 버전을 사용하도록 하기 위한 이 독립 실행형 응용 프로그램에 대해 알아봅니다."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: dec591ac845b6c54421197099e56d7a4a86783ae
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2017
---
# <a name="setup-downloader-for-system-center-configuration-manager"></a>System Center Configuration Manager에 대한 설치 다운로더

*적용 대상: System Center Configuration Manager(현재 분기)*

설치 프로그램을 실행하여 System Center Configuration Manager 사이트를 설치하거나 업그레이드하기 전에 설치하려는 Configuration Manager 버전의 설치 다운로더 독립 실행형 응용 프로그램을 사용하여 업데이트된 설치 파일을 다운로드할 수 있습니다.  

업데이트된 설치 파일을 사용하면 사이트 설치 시 주요 설치 파일의 최신 버전을 사용하게 됩니다. 개요:   
-   설치 다운로더를 사용하여 설치를 시작하기 전에 파일을 다운로드할 때는 파일을 포함할 폴더를 지정합니다.  
-   설치 다운로더를 실행하는 데 사용하는 계정에는 다운로드 폴더에 대한 **모든 권한**이 있어야 합니다.  
-   설치 프로그램을 실행하여 사이트를 설치하거나 업그레이드할 때는 이전에 다운로드한 파일의 이 로컬 복사본을 사용하도록 지정할 수 있습니다. 이렇게 하면 사이트 설치 또는 업그레이드를 시작할 때 설치 프로그램이 Microsoft에 연결하지 않아도 됩니다.  
-   후속 사이트 설치 또는 업그레이드에도 설치 파일의 동일 로컬 복사본을 사용할 수 있습니다.  

설치 다운로더가 다운로드하는 파일 형식은 다음과 같습니다.  
-   필요한 필수 조건 재배포 가능 파일  
-   언어 팩  
-   설치 프로그램에 대한 최신 제품 업데이트  

설치 다운로더를 실행하는 다음 두 가지 옵션이 있습니다.
- 사용자 인터페이스를 사용하여 응용 프로그램 실행
- 명령줄 옵션을 보려면 명령 프롬프트에서 응용 프로그램을 실행합니다.


## <a name="run-setup-downloader-with-the-user-interface"></a>사용자 인터페이스를 사용하여 설치 다운로더 실행  

1.  인터넷에 액세스할 수 있는 컴퓨터에서 Windows 탐색기를 열고 **&lt;Configuration Manager 설치 미디어\>\SMSSETUP\BIN\X64**로 이동합니다.  

2.  설치 다운로더를 열려면 **Setupdl.exe**를 두 번 클릭합니다.   

3. 업데이트된 설치 파일을 호스트할 폴더의 경로를 지정한 다음 **다운로드**를 클릭합니다. 설치 다운로더가 현재 다운로드 폴더에 있는 파일을 확인하고, 누락된 파일이나 기존 파일보다 최신 파일만 다운로드합니다. 또한 다운로드한 언어에 대한 하위 폴더 및 기타 필요한 하위 폴더를 만듭니다.  

4.  다운로드 결과를 검토하려면 C 드라이브의 루트 디렉터리에 있는 **ConfigMgrSetup.log** 파일을 엽니다.  

## <a name="run-setup-downloader-from-a-command-prompt"></a>명령 프롬프트에서 설치 다운로더 실행  

1.  명령 프롬프트 창에서 **&lt;*Configuration Manager 설치 미디어*\>\SMSSETUP\BIN\X64**로 이동합니다.   

2.  설치 다운로더를 열려면 **Setupdl.exe**를 실행합니다.

    **Setupdl.exe**와 함께 다음 명령줄 옵션을 사용할 수 있습니다.   

    -   **/VERIFY**: 언어 파일이 포함된 다운로드 폴더에서 파일을 확인하려면 이 옵션을 사용합니다. 오래된 파일 목록을 보려면 C 드라이브의 루트 디렉터리에 있는 ConfigMgrSetup.log 파일을 검토합니다. 이 옵션을 사용하면 파일이 다운로드되지 않습니다.  

    -   **/VERIFYLANG**: 다운로드 폴더에서 언어 파일을 확인하려면 이 옵션을 사용합니다. 오래된 언어 파일 목록을 보려면 C 드라이브의 루트 디렉터리에 있는 ConfigMgrSetup.log 파일을 검토합니다.

    -   **/LANG**: 다운로드 폴더에 언어 파일만 다운로드하려면 이 옵션을 사용합니다.  

    -   **/NOUI**: 사용자 인터페이스를 표시하지 않고 설치 다운로더를 시작하려면 이 옵션을 사용합니다. 이 옵션을 사용하는 경우 명령 프롬프트에서 명령의 일부로 **다운로드 경로**를 지정해야 합니다.  

    -   **&lt;다운로드 경로\>**: 다운로드 폴더 경로를 지정하여 확인 또는 다운로드 프로세스를 자동으로 시작할 수 있습니다. **/NOUI** 옵션을 사용하는 경우 다운로드 경로를 지정해야 합니다. 다운로드 경로를 지정하지 않는 경우 설치 다운로더가 열릴 때 경로를 지정해야 합니다. 폴더가 없는 경우 설치 다운로더에서 폴더를 만듭니다.  

    예제 명령:

    -   **setupd &lt;다운로드 경로\>**  

        -   설치 다운로더가 시작되고 지정된 다운로드 폴더의 파일을 확인한 후 누락된 파일이나 기존 파일보다 최신 버전인 파일만 다운로드합니다.     

    -   **setupdl /VERIFY &lt;다운로드 경로\>**  

        -   설치 다운로더가 시작되고 지정된 다운로드 폴더의 파일을 확인합니다.  

    -   **setupdl /NOUI &lt;다운로드 경로\>**  

        -   설치 다운로더가 시작되고 지정된 다운로드 폴더의 파일을 확인한 후 누락된 파일이나 기존 파일보다 최신 버전인 파일만 다운로드합니다.  

    -   **setupdl /LANG  &lt;다운로드 경로\>**  

        -   설치 다운로더가 시작되고 지정된 다운로드 폴더의 언어 파일을 확인한 후 누락된 언어 파일이나 기존 파일보다 최신 언어 파일만 다운로드합니다.  

    -   **setupdl /VERIFY**  

        -   설치 다운로더가 시작되면 다운로드 폴더의 경로를 지정해야 합니다. **확인**을 클릭하면 설치 다운로드가 다운로드 폴더의 파일을 확인합니다.  

3.  다운로드 결과를 검토하려면 C 드라이브의 루트 디렉터리에 있는 **ConfigMgrSetup.log** 파일을 엽니다.
