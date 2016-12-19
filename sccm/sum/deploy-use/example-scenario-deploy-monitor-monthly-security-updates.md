---

title: "보안 소프트웨어 업데이트를 배포하고 모니터링하는 예제 시나리오 | Configuration Manager"
description: "Configuration Manager에서 소프트웨어 업데이트를 사용하는 방법에 대한 이 예제 시나리오를 사용하여 Microsoft 월별 릴리스에 대한 보안 소프트웨어 업데이트를 배포하고 모니터링합니다."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.technology:
- configmgr-sum
ms.service: 
ms.assetid: c32f757a-02da-43f2-b055-5cfd097d8c43
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: cd03ddda0a39704a5715f7ed8d620daaefb57653



---
# <a name="example-scenario-for-using-system-center-configuration-manager-to-deploy-and-monitor-the-security-software-updates-released-monthly-by-microsoft"></a>System Center Configuration Manager를 사용하여 Microsoft에서 매월 릴리스하는 보안 소프트웨어 업데이트를 배포하고 모니터링하는 예제 시나리오

*적용 대상: System Center Configuration Manager(현재 분기)*

이 항목에서는 System Center Configuration Manager의 소프트웨어 업데이트를 사용하여 Microsoft에서 매월 릴리스하는 보안 소프트웨어 업데이트를 배포 및 모니터링하는 방법을 보여 주는 예제 시나리오를 제공합니다.  

 이 시나리오에서 John은 Woodgrove 은행의 Configuration Manager 관리자입니다. 이한일은 다음 조건과 요구 사항에 따라 소프트웨어 업데이트 배포 전략을 만들어야 합니다.  

-   활성 소프트웨어 업데이트 배포는 Microsoft에서 매월 두 번째 화요일에 보안 소프트웨어 업데이트를 릴리스하고 나서 1주 후에 실행됩니다. Microsoft의 그러한 일정을 보통 화요일 패치라고 합니다.  

-   소프트웨어 업데이트가 배포 지점에 다운로드되어 준비됩니다. 그런 다음 배포를 클라이언트 하위 집합에 대해 테스트한 후 소프트웨어 업데이트를 현재의 프로덕션 환경에서 전체적으로 배포합니다.  

-   이한일은 매월 또는 매년 소프트웨어 업데이트의 호환성을 모니터링할 수 있어야 합니다.  

 이 시나리오에서는 소프트웨어 업데이트 지점 인프라가 이미 구현되어 있는 것으로 가정합니다. 다음 정보를 사용하여 Configuration Manager에서 소프트웨어 업데이트를 계획하고 구성합니다.  

|프로세스|참조|  
|-------------|---------------|  
|소프트웨어 업데이트에 대한 핵심 개념을 검토합니다.|[소프트웨어 업데이트 소개](../understand/software-updates-introduction.md)|  
|소프트웨어 업데이트를 계획합니다. 이 정보를 활용하여 용량 고려 사항을 계획하고 소프트웨어 업데이트 지점 인프라, 소프트웨어 업데이트 지점 설치, 동기화 설정, 소프트웨어 업데이트에 대한 클라이언트 설정 등을 확인할 수 있습니다.|[소프트웨어 업데이트 계획](../plan-design/plan-for-software-updates.md)|  
|소프트웨어 업데이트를 구성합니다. 이 정보를 활용하여 계층에서 소프트웨어 업데이트 지점을 설치 및 구성하고 소프트웨어 업데이트를 구성 및 동기화할 수 있습니다.<br /><br /> 이 시나리오에서 John은 Microsoft의 최신 보안 소프트웨어 업데이트를 검색할 수 있도록 소프트웨어 업데이트 동기화 일정을 매월 두 번째 수요일에 실행하도록 구성합니다.|[소프트웨어 업데이트 동기화](../get-started/synchronize-software-updates.md)|  

 이 항목의 다음 섹션에서는 조직 내에서 Configuration Manager 보안 소프트웨어 업데이트를 배포하고 모니터링할 수 있도록 지원하는 단계 예제를 제공합니다.

##  <a name="a-namebkmkstep1a-step-1-create-a-software-update-group-for-yearly-compliance"></a><a name="BKMK_Step1"></a> 1단계: 연간 준수에 대한 소프트웨어 업데이트 그룹 만들기  
 John은 2016년에 릴리스한 모든 보안 소프트웨어 업데이트에 대한 준수를 모니터링하는 데 사용하기 위해 소프트웨어 업데이트 그룹을 만듭니다. 이를 위해 다음 표에 나온 단계를 수행합니다.  

|프로세스|참조|  
|-------------|---------------|  
|Configuration Manager 콘솔의 **모든 소프트웨어 업데이트** 노드에서, 다음 기준을 충족하여 2015년에 릴리스되거나 수정된 보안 소프트웨어 업데이트만 표시하는 기준을 추가합니다.<br /><br /><ul><li>**기준**: 릴리스 또는 수정 날짜</li><li>**조건**: 특정 날짜보다 크거나 같음<br />**값**: 1/1/2015</li><li>**조건**: 업데이트 분류<br />**값**: 보안 업데이트</li><li>**기준**: 만료됨 <br />**값**: 아니요</li></ul>|추가 정보 없음|
|이한일은 모든 필터링된 소프트웨어 업데이트를 새 소프트웨어 업데이트 그룹에 다음 요구 사항과 함께 추가합니다.<br /><br /><ul><li>**이름**: 준수 그룹 - Microsoft 보안 업데이트 2015</li><li>**설명**: 소프트웨어 업데이트|[업데이트 그룹에 소프트웨어 업데이트 추가](add-software-updates-to-an-update-group.md)|  

##  <a name="a-namebkmkstep2a-step-2-create-an-automatic-deployment-rule-for-the-current-month"></a><a name="BKMK_Step2"></a> 2단계: 이번 달에 대한 자동 배포 규칙 만들기  
 이한일은 Microsoft에서 이번 달에 릴리스한 보안 소프트웨어 업데이트에 대해 자동 배포 규칙을 만듭니다. 이를 위해 다음 표에 나온 단계를 수행합니다.  

|프로세스|참조|  
|-------------|---------------|  
|다음 요구 사항을 갖는 자동 배포 규칙을 만듭니다.<br /><br /><ol><li>**일반** 탭에서 다음 내용을 구성합니다.<br /> <ul><li>이름으로 **Monthly Security Updates**를 지정합니다.</li><li>제한된 클라이언트가 포함된 테스트 컬렉션을 선택합니다.</li><li>**새 소프트웨어 업데이트 그룹 만들기**를 선택합니다.</li><li>**이 규칙을 실행한 후 배포 사용**이 선택되지 않았는지 확인합니다.</li></ul></li><li>**배포 설정** 탭에서 기본 설정을 선택합니다.</li><li>**소프트웨어 업데이트** 페이지에서 다음 속성 필터와 검색 조건을 구성합니다.<br /><ul><li>릴리스 또는 수정 날짜 **지난 1개월**</li><li>업데이트 분류 **보안 업데이트**</li></ul></li><li>**평가** 페이지에서 매**월** **두 번째 목요일**의 일정으로 규칙을 실행하도록 설정합니다. 또한 John은 동기화 일정을 매**월** **두 번째 수요일**에 실행하도록 설정했는지 확인합니다.</li><li>배포 일정, 사용자 환경, 경고, 다운로드 설정 페이지에서 기본 설정을 사용합니다.</li><li>**배포 패키지** 페이지에서 새 배포 패키지를 지정합니다.</li><li>다운로드 위치 및 언어 선택 페이지에서 기본 설정을 사용합니다.</li></ol>|[소프트웨어 업데이트 자동 배포](automatically-deploy-software-updates.md)|  

##  <a name="a-namebkmkstep3a-step-3-verify-that-software-updates-are-ready-to-deploy"></a><a name="BKMK_Step3"></a> 3단계: 소프트웨어 업데이트 배포 준비 확인  
 이한일은 매월 두 번째 목요일에 소프트웨어 업데이트의 배포가 준비되었는지 확인합니다. 다음 작업을 수행합니다.  

|프로세스|참조|  
|-------------|---------------|  
|소프트웨어 업데이트 동기화가 성공적으로 완료되었는지 확인합니다.|[소프트웨어 업데이트 동기화 상태](monitor-software-updates.md#BKMK_SUSyncStatus)|  

##  <a name="a-namebkmkstep4a-step-4-deploy-the-software-update-group"></a><a name="BKMK_Step4"></a> 4단계: 소프트웨어 업데이트 그룹 배포  
 이한일은 소프트웨어 업데이트의 배포가 준비된 것을 확인한 후 소프트웨어 업데이트를 배포합니다. 이를 위해 다음 표에 나온 단계를 수행합니다.  

|프로세스|참조|  
|-------------|---------------|  
|새 소프트웨어 업데이트 그룹에 대해 두 개의 테스트 배포를 만듭니다. 그런 다음 각 배포에 대해 다음 환경을 고려합니다.<br /><br /> **워크스테이션 테스트 배포**: 워크스테이션 테스트 배포에 대해 다음 사항을 고려합니다.<br /><br /><ul><li>배포를 확인하기 위해 워크스테이션 클라이언트의 하위 집합이 포함된 배포 컬렉션을 지정합니다.</li><li>현재 환경의 워크스테이션 클라이언트에 적합한 배포 설정을 구성합니다.</li></ul><br />**서버 테스트 배포**: 서버 테스트 배포에 대해 다음 사항을 고려합니다.<br /><br /><ul><li>배포를 확인하기 위해 서버 클라이언트의 하위 집합이 포함된 배포 컬렉션을 지정합니다.</li><li>현재 환경의 서버 클라이언트에 적합한 배포 설정을 구성합니다.</li></ul>|[소프트웨어 업데이트 배포](deploy-software-updates.md)|  
|테스트 배포가 성공적으로 배포된 것을 확인합니다.|[소프트웨어 업데이트 배포 상태](monitor-software-updates.md#BKMK_SUDeployStatus)|  
|프로덕션 워크스테이션 및 서버가 포함된 새 컬렉션을 사용하여 두 개의 배포를 업데이트합니다.|추가 정보 없음|  

##  <a name="a-namebkmkstep5a-step-5-monitor-compliance-for-deployed-software-updates"></a><a name="BKMK_Step5"></a> 5단계: 배포된 소프트웨어 업데이트에 대한 준수 모니터링  
 이한일은 소프트웨어 업데이트 배포의 호환성을 모니터링합니다. 이를 위해 다음 표에 나온 단계를 수행합니다.  

|프로세스|참조|  
|-------------|---------------|  
|John은 Configuration Manager 콘솔에서 소프트웨어 업데이트 배포 상태를 모니터링하고 콘솔에서 사용할 수 있는 소프트웨어 업데이트 배포 보고서를 확인합니다.|[System Center Configuration Manager에서 소프트웨어 업데이트 모니터링](../../sum/deploy-use/monitor-software-updates.md)|  

##  <a name="a-namebkmkstep6a-step-6-add-monthly-software-updates-to-the-yearly-update-group"></a><a name="BKMK_Step6"></a> 6단계: 연간 업데이트 그룹에 월간 소프트웨어 업데이트 추가  
 이한일은 연간 소프트웨어 업데이트 그룹에 월간 소프트웨어 업데이트 그룹의 소프트웨어 업데이트를 추가합니다. 이를 위해 다음 표에 나온 단계를 수행합니다.  

|프로세스|참조|  
|-------------|---------------|  
|월간 소프트웨어 업데이트 그룹에서 소프트웨어 업데이트를 선택하고 연간 호환성에 대해 만든 소프트웨어 업데이트 그룹에 이 소프트웨어 업데이트를 추가합니다. 또한 소프트웨어 업데이트 호환성을 추적하고 관리를 위한 다양한 보고서를 만듭니다.|[배포된 업데이트 그룹에 소프트웨어 업데이트 추가](add-software-updates-to-an-update-group.md)|  

이한일은 보안 소프트웨어 업데이트에 대한 월간 배포를 성공적으로 완료했습니다. 그는 계속적으로 소프트웨어 업데이트 호환성을 모니터링하고 보고함으로써 현재의 환경에 있는 클라이언트가 수용 가능한 호환성 수준을 유지하도록 합니다.  

##  <a name="a-namebkmkmonthlyprocessa-recurring-monthly-process-to-deploy-software-updates"></a><a name="BKMK_MonthlyProcess"></a> 소프트웨어 업데이트를 배포하는 월간 되풀이 프로세스  
 이한일은 소프트웨어 업데이트를 배포하고 나서 첫 달이 지난 후 3~6단계를 수행하여 Microsoft에서 릴리스한 월간 보안 소프트웨어 업데이트를 배포합니다.  



<!--HONumber=Nov16_HO1-->

