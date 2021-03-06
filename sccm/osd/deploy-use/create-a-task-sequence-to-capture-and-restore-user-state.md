---
title: "사용자 환경을 캡처 및 복원하는 작업 순서 만들기"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager 작업 순서를 사용하여 운영 체제 배포 시나리오에서 사용자 상태 데이터를 캡처 및 복원할 수 있습니다."
ms.custom: na
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
caps.latest.revision: "7"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 3fb30240c7d926657e01a4b9e03cef38fd2ee128
ms.sourcegitcommit: 08f9854fb6c6d21e1e923b13e38a64d0bc2bc9a4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-system-center-configuration-manager"></a>System Center Configuration Manager에서 사용자 상태를 캡처 및 복원하는 작업 순서 만들기

*적용 대상: System Center Configuration Manager(현재 분기)*

System Center Configuration Manager 작업 순서를 사용하여 현재 운영 체제의 사용자 상태를 보존하려는 운영 체제 배포 시나리오에서 사용자 상태 데이터를 캡처 및 복원할 수 있습니다. 만드는 작업 순서 유형에 따라, 캡처 및 복원 단계가 작업 순서의 일부로 자동으로 추가될 수도 있습니다. 다른 시나리오에서는 캡처 및 복원 단계를 작업 순서에 수동으로 추가해야 할 수 있습니다. 이 항목에서는 사용자 상태 데이터를 캡처 및 복원하기 위해 기존 작업 순서에 추가해야 하는 단계를 제공합니다.  

##  <a name="BKMK_CaptureRestoreUserState"></a> 사용자 상태 데이터를 캡처 및 복원하는 방법  
 사용자 상태를 캡처하고 복원하려면 작업 순서에 다음 단계를 추가해야 합니다.  

-   **상태 저장소 요청**: 이 단계는 상태 마이그레이션 지점에 사용자 상태를 저장하는 경우에만 필요합니다.  

-   **사용자 상태 캡처**: 이 단계는 사용자 상태 데이터를 캡처하여 상태 마이그레이션 지점에 저장하거나 링크를 사용하여 로컬로 저장합니다.  

-   **사용자 상태 복원**: 이 단계는 대상 컴퓨터에서 사용자 상태 데이터를 복원합니다. 사용자 상태 마이그레이션 지점 또는 대상 컴퓨터에서 데이터를 검색할 수 있습니다.  

-   **상태 저장소 해제**: 이 단계는 상태 마이그레이션 지점에 사용자 상태를 저장하는 경우에만 필요합니다. 이 단계는 상태 마이그레이션 지점에서 이 데이터를 제거합니다.  

 사용자 상태를 캡처하고 복원하는 데 필요한 작업 순서 단계를 추가하려면 다음 단계를 따르십시오. 작업 순서를 만드는 방법에 대한 자세한 내용은 [작업 순서를 관리하여 작업 자동화](manage-task-sequences-to-automate-tasks.md)를 참조하세요.  

#### <a name="to-add-task-sequence-steps-to-capture-the-user-state"></a>사용자 상태를 캡처하는 작업 순서 단계를 추가하려면  

1.  **작업 순서** 목록에서 작업 순서를 선택한 후 **편집**을 클릭합니다.  

2.  상태 마이그레이션 지점을 사용하여 사용자 상태를 저장하는 경우 작업 순서에 **상태 저장소 요청** 단계를 추가합니다. **작업 순서 편집기** 대화 상자에서 **추가**를 클릭하고 **사용자 상태**를 가리킨 다음 **상태 저장소 요청**을 클릭합니다. **상태 저장소 요청** 단계에 대한 다음 속성 및 옵션을 지정하고 **적용**을 클릭합니다.  

     **속성** 탭에서 다음 옵션을 지정합니다.  

    -   단계의 이름과 설명을 입력합니다.  

    -   **컴퓨터에서 상태 캡처**를 클릭합니다.  

    -   **다시 시도 횟수** 상자에 오류가 발생할 경우 작업 순서가 사용자 상태 데이터를 캡처하려고 시도하는 횟수를 지정합니다.  

    -   **다시 시도 지연 시간(초)** 상자에 작업 순서가 데이터를 캡처하기 위해 다시 시도하기까지 기다리는 시간(초)을 지정합니다.  

    -   Configuration Manager [네트워크 액세스 계정](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA)을 사용하여 상태 데이터에 연결할지 여부를 지정하려면 **컴퓨터 계정에서 상태 저장소에 연결하지 못하는 경우 네트워크 액세스 계정 사용** 확인란을 선택합니다.  

     **옵션** 탭에서 다음 옵션을 지정합니다.  

    -   이 단계가 실패하는 경우라도 작업 순서의 다음 단계로 계속 진행하려면 **오류 발생 시 계속** 확인란을 선택합니다.  

    -   오류가 발생하는 경우 작업 순서를 계속 진행하기 위해 충족되어야 할 조건을 지정합니다.  

3.  작업 순서에 **사용자 상태 캡처** 단계를 추가합니다. **작업 순서 편집기** 대화 상자에서 **추가**를 클릭하고 **사용자 상태**를 가리킨 다음 **사용자 상태 캡처**를 클릭합니다. **사용자 상태 캡처** 단계에 대한 다음 속성 및 옵션을 지정하고 **확인**을 클릭합니다.  

    > [!IMPORTANT]  
    >  작업 순서에 이 단계를 추가하는 경우 **OSDStateStorePath** 작업 순서 변수도 설정하여 사용자 상태 데이터가 저장되는 위치를 지정합니다. 사용자 상태를 로컬로 저장하는 경우 루트 폴더를 지정하지 마십시오. 이 경우 작업 순서가 실패할 수 있습니다. 사용자 데이터를 로컬로 저장하는 경우 항상 폴더 또는 하위 폴더를 사용합니다. 이 변수에 대한 자세한 내용은 [사용자 상태 캡처 작업 순서 동작 변수](../understand/task-sequence-action-variables.md#BKMK_CaptureUserState)를 참조하세요.  

     **속성** 탭에서 다음 옵션을 지정합니다.  

    -   단계의 이름과 설명을 입력합니다.  

    -   사용자 상태 데이터를 캡처하는 데 사용되는 USMT 원본 파일이 포함된 패키지를 지정합니다.  

    -   캡처할 사용자 프로필을 지정합니다.  

        -   모든 사용자 프로필을 캡처하려면 **표준 옵션을 사용하여 모든 사용자 프로필 캡처** 를 클릭합니다.  

        -   캡처할 사용자 프로필을 개별적으로 지정하려면 **사용자 프로필 캡처 방식을 사용자 지정** 을 클릭합니다. 사용자 프로필 정보를 포함하는 구성 파일(miguser.xml, migsys.xml 또는 migapp.xml)을 선택합니다. 여기서는 config.xml 구성 파일을 사용할 수 없지만 OSDMigrageAdditionalCaptureOptions 및 OSDMigrateAdditionalRestoreOptions 변수를 사용하여 USMT 명령줄에 수동으로 추가할 수 있습니다.

    -   오류가 발생하는 경우 로그 파일에 기록할 정보 수준을 지정하려면 **자세한 정보 로깅 사용** 을 선택합니다.  

    -   **EFS(파일 시스템 암호화)를 사용하는 파일 건너뛰기**를 선택합니다.  

    -   **파일 시스템 액세스를 사용하여 복사** 를 선택하고 다음 설정을 지정합니다.  

        -   **일부 파일을 캡처할 수 없는 경우 계속**: 이 설정을 사용하면 일부 파일을 캡처할 수 없는 경우라도 작업 순서 단계에서 마이그레이션 프로세스를 계속 진행할 수 있습니다. 이 옵션을 사용하지 않도록 설정했는데 파일을 캡처할 수 없는 경우 작업 순서 단계는 실패합니다. 기본적으로 이 옵션은 사용하도록 설정됩니다.  

        -   **파일을 복사하지 않고 링크를 사용하여 로컬로 캡처**: 이 설정을 사용하면 USMT 4.0에서 사용할 수 있는 하드 링크 마이그레이션 기능을 사용할 수 있습니다. USMT 4.0 이전의 USMT 버전을 사용하는 경우 이 설정은 무시됩니다.  

        -   **오프라인 모드로 캡처(Windows PE만 해당)**:이 설정을 사용하면 기존 운영 체제로 부팅하지 않고 Windows PE에서 사용 상태를 캡처할 수 있습니다. USMT 4.0 이전의 USMT 버전을 사용하는 경우 이 설정은 무시됩니다.  

    -   **VSS(Volume Copy Shadow) 서비스를 사용하여 캡처**를 선택합니다. USMT 4.0 이전의 USMT 버전을 사용하는 경우 이 설정은 무시됩니다.  

     **옵션** 탭에서 다음 옵션을 지정합니다.  

    -   이 단계가 실패하는 경우라도 작업 순서의 다음 단계로 계속 진행하려면 **오류 발생 시 계속** 확인란을 선택합니다.  

    -   오류가 발생하는 경우 작업 순서를 계속 진행하기 위해 충족되어야 할 조건을 지정합니다.  

4.  상태 마이그레이션 지점을 사용하여 사용자 상태를 저장하는 경우 [상태 저장소 해제](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) 단계를 작업 순서에 추가합니다. **작업 순서 편집기** 대화 상자에서 **추가**를 클릭하고 **사용자 상태**를 가리킨 후 **상태 저장소 해제**를 클릭합니다. **상태 저장소 해제** 단계에 대한 다음 속성과 옵션을 지정한 후 **확인**을 클릭합니다.  

    > [!IMPORTANT]  
    >  **상태 저장소 해제** 단계 이전에 실행되는 작업 순서 작업은 **상태 저장소 해제** 단계가 시작되기 전에 모두 성공적으로 수행되어야 합니다.  

     **속성** 탭에서 단계에 대한 이름 및 설명을 입력합니다.  

     **옵션** 탭에서 다음 옵션을 지정합니다.  

    -   이 단계가 실패하는 경우라도 작업 순서의 다음 단계로 계속 진행하려면 **오류 발생 시 계속** 확인란을 선택합니다.  

    -   오류가 발생하는 경우 작업 순서를 계속 진행하기 위해 충족되어야 할 조건을 지정합니다.  

 대상 컴퓨터에서 사용자 상태를 캡처할 수 있도록 이 작업 순서를 배포합니다. 작업 순서를 배포하는 방법에 대한 자세한 내용은 [작업 순서 배포](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)를 참조하세요.  

#### <a name="to-add-task-sequence-steps-to-restore-the-user-state"></a>사용자 상태를 복원하는 작업 순서 단계를 추가하려면  

1.  **작업 순서** 목록에서 작업 순서를 선택한 후 **편집**을 클릭합니다.  

2.  [사용자 상태 복원](../understand/task-sequence-steps.md#BKMK_RestoreUserState) 단계를 작업 순서에 추가합니다. **작업 순서 편집기** 대화 상자에서 **추가**를 클릭하고 **사용자 상태**를 가리킨 후 **사용자 상태 복원**을 클릭합니다. 이 단계에서 상태 마이그레이션 지점에 연결됩니다. **사용자 상태 복원** 단계에 대한 다음 속성과 옵션을 지정한 후 **확인**을 클릭합니다.  

     **속성** 탭에서 다음 속성을 지정합니다.  

    -   단계의 이름과 설명을 입력합니다.  

    -   사용자 상태 데이터를 복원할 수 있도록 USMT를 포함하는 패키지를 지정합니다.  

    -   복원할 사용자 프로필을 지정합니다.  

        -   모든 사용자 프로필을 복원하려면 **캡처된 모든 사용자 프로필을 표준 옵션으로 복원** 을 클릭합니다.  

        -   개별 사용자 프로필을 복원하려면 **사용자 프로필 복원 사용자 지정**을 클릭합니다. 사용자 프로필 정보를 포함하는 구성 파일(miguser.xml, migsys.xml 또는 migapp.xml)을 선택합니다. 여기서는 config.xml 구성 파일을 사용할 수 없지만 OSDMigrageAdditionalCaptureOptions 및 OSDMigrateAdditionalRestoreOptions 변수를 사용하여 USMT 명령줄에 수동으로 추가할 수 있습니다.

    -   복원한 프로필에 새 암호를 제공하려면 **로컬 컴퓨터 사용자 프로필 복원** 을 선택합니다. 로컬 프로필에 대한 암호를 마이그레이션할 수 없습니다.  

        > [!NOTE]  
        >  로컬 사용자 계정이 있는 경우 [사용자 상태 캡처](../understand/task-sequence-steps.md#BKMK_CaptureUserState) 단계를 사용하고 **캡처된 모든 사용자 프로필을 표준 옵션으로 복원**을 선택하면 [사용자 상태 복원](../understand/task-sequence-steps.md#BKMK_RestoreUserState) 단계의 **로컬 컴퓨터 사용자 프로필 복원** 설정을 선택해야 합니다. 그렇지 않으면 작업 순서가 실패합니다.  

    -   파일을 복원할 수 없는 경우라도 **사용자 상태 복원** 단계를 계속 진행하려면 **일부 파일을 복원할 수 없는 경우 계속** 을 선택합니다.  

         로컬 링크를 사용하여 사용자 상태를 저장한 경우 복원이 성공하지 못하면 관리자가 데이터를 저장하기 위해 만든 하드 링크를 직접 삭제하거나 작업 순서가 자동으로 USMTUtils 도구를 실행할 수 있습니다. USMTUtils를 사용하여 하드 링크를 삭제하는 경우 USMTUtils를 실행한 후 [컴퓨터 다시 시작](../understand/task-sequence-steps.md#BKMK_RestartComputer) 단계를 추가해야 합니다.  

    -   오류가 발생하는 경우 로그 파일에 기록할 정보 수준을 지정하려면 **자세한 정보 로깅 사용** 을 선택합니다.  

     **옵션** 탭에서 다음 옵션을 지정합니다.  

    -   이 단계가 실패하는 경우라도 작업 순서의 다음 단계로 계속 진행하려면 **오류 발생 시 계속** 확인란을 선택합니다.  

    -   오류가 발생하는 경우 작업 순서를 계속 진행하기 위해 충족되어야 할 조건을 지정합니다.  

3.  상태 마이그레이션 지점을 사용하여 사용자 상태를 저장하는 경우 [상태 저장소 해제](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) 단계를 작업 순서에 추가합니다. **작업 순서 편집기** 대화 상자에서 **추가**를 클릭하고 **사용자 상태**를 가리킨 후 **상태 저장소 해제**를 클릭합니다. **상태 저장소 해제** 단계에 대한 다음 속성과 옵션을 지정한 후 **확인**을 클릭합니다.  

    > [!IMPORTANT]  
    >  **상태 저장소 해제** 단계 이전에 실행되는 작업 순서 작업은 **상태 저장소 해제** 단계가 시작되기 전에 모두 성공적으로 수행되어야 합니다.  

     **속성** 탭에서 단계에 대한 이름 및 설명을 입력합니다.  

     **옵션** 탭에서 다음 옵션을 지정합니다.  

    -   이 단계가 실패하는 경우라도 작업 순서의 다음 단계로 계속 진행하려면 **오류 발생 시 계속** 확인란을 선택합니다.  

    -   오류가 발생하는 경우 작업 순서를 계속 진행하기 위해 충족되어야 할 조건을 지정합니다.  

 대상 컴퓨터에서 사용자 상태를 복원할 수 있도록 이 작업 순서를 배포합니다. 작업 순서를 배포하는 방법에 대한 자세한 내용은 [작업 순서 배포](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)를 참조하세요.  

## <a name="next-steps"></a>다음 단계
[작업 순서 배포 모니터링](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)
