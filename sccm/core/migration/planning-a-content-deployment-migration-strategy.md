---
title: "콘텐츠 마이그레이션"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager 대상 계층 구조로 데이터를 마이그레이션하는 동안 배포 지점을 사용하여 콘텐츠를 관리합니다."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 66f7759c-6272-4116-aad7-0d05db1d46cd
caps.latest.revision: "8"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 7332ff4bf0ad10bd18e42485fb548eee70deaf04
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/04/2018
---
# <a name="plan-a-content-deployment-migration-strategy-in-system-center-configuration-manager"></a>System Center Configuration Manager에서 콘텐츠 배포 마이그레이션 전략 계획

*적용 대상: System Center Configuration Manager(현재 분기)*

System Center Configuration Manager 대상 계층으로 데이터를 마이그레이션하는 동안 원본 및 대상 계층의 Configuration Manager 클라이언트는 원본 계층에 배포된 콘텐츠에 대한 액세스 권한을 유지 관리할 수 있습니다. 그뿐만 아니라, 마이그레이션을 사용하여 원본 계층의 배포 지점을 대상 계층의 배포 지점이 되도록 업그레이드하거나 재할당할 수 있습니다. 배포 지점을 공유하고 업그레이드하거나 재할당하는 경우 이 전략을 사용하면 마이그레이션하는 클라이언트를 위해 대상 계층의 새 서버에 콘텐츠를 재배포할 필요가 없습니다.  

대상 계층에서 콘텐츠를 다시 만들고 배포할 수 있지만 다음 옵션을 사용하여 이 콘텐츠를 관리할 수도 있습니다.  

-   원본 계층의 배포 지점을 대상 계층의 클라이언트와 공유합니다.  

-   원본 계층의 독립 실행형 Configuration Manager 2007 배포 지점 또는 Configuration Manager 2007 보조 사이트를 대상 계층의 배포 지점이 되도록 업그레이드합니다.  

-   System Center Configuration Manager 원본 계층의 배포 지점을 대상 계층의 사이트로 다시 할당합니다.  

마이그레이션 중에 콘텐츠 배포를 계획하려면 다음 섹션을 참조하십시오.  

-   [원본 계층 구조와 대상 계층 구조 간에 배포 지점 공유](#About_Shared_DPs_in_Migration)  

-   [Configuration Manager 2007 공유 배포 지점 업그레이드 계획](#Planning_to_Upgrade_DPs)  

    -   [배포 지점 업그레이드 프로세스](#BKIMK_UpgradeProcess)  

    -   [Configuration Manager 2007 보조 사이트 업그레이드 계획](#BKMK_UpgradeSS)  

-   [System Center Configuration Manager 배포 지점 재할당 계획](#BKMK_ReassignDistPoint)  

    -   [배포 지점 재할당 프로세스](#BKMK_ReassignProcess)  

-   [콘텐츠 마이그레이션 시 콘텐츠 소유권](#About_Migrating_Content)  

##  <a name="About_Shared_DPs_in_Migration"></a> 원본 계층 구조와 대상 계층 구조 간에 배포 지점 공유  
마이그레이션 중에 원본 계층의 배포 지점을 대상 계층과 공유할 수 있습니다. 공유된 배포 지점을 사용하면 원본 계층에서 마이그레이션한 콘텐츠를 대상 계층의 클라이언트에서 바로 사용할 수 있도록 만들 수 있으므로, 해당 콘텐츠를 다시 만든 다음 대상 계층의 새 배포 지점에 배포할 필요가 없습니다. 대상 계층의 클라이언트가 공유된 배포 지점에 배포되는 콘텐츠를 요청하면 공유 배포 지점을 유효한 콘텐츠 위치로 클라이언트에 제공할 수 있습니다.  

 원본 계층에서 마이그레이션하는 작업이 활성 상태로 유지되는 동안 대상 계층에서 클라이언트의 유효한 콘텐츠 위치로 사용될 뿐 아니라, 배포 지점을 업그레이드하거나 대상 계층에 재할당할 수 있습니다. Configuration Manager 2007 공유 배포 지점을 업그레이드하고 System Center 2012 Configuration Manager 공유 배포 지점을 재할당할 수 있습니다. 공유 배포 지점을 업그레이드하거나 재할당하면 배포 지점이 원본 계층에서 제거되고 대상 계층의 배포 지점이 됩니다. 공유 대상 계층을 업그레이드하거나 재할당하면 원본 계층에서 마이그레이션을 완료한 후에 대상 계층의 배포 지점을 계속 사용할 수 있습니다. 공유 배포 지점을 업그레이드하는 방법에 대한 자세한 내용은 [Configuration Manager 2007 공유 배포 지점 업그레이드 계획](#Planning_to_Upgrade_DPs)을 참조하세요. 공유 배포 지점을 재할당하는 방법에 대한 자세한 내용은 [System Center Configuration Manager 배포 지점 재할당 계획](#BKMK_ReassignDistPoint)을 참조하세요.  

 원본 계층의 원본 사이트에서 배포 지점을 공유하도록 선택할 수 있습니다. 원본 사이트의 배포 지점을 공유하면 각 기본 사이트 및 해당 기본 사이트의 조건에 맞는 각 배포 지점에서 자식 보조 사이트가 공유됩니다. 공유 배포 지점이 되는 조건을 갖추려면 배포 지점을 호스트하는 사이트 시스템 서버를 FQDN(정규화된 도메인 이름)으로 설정해야 합니다. NetBIOS 이름으로 설정된 배포 지점은 무시됩니다.  

> [!TIP]  
>  Configuration Manager 2007에서는 사이트 시스템 서버의 FQDN을 설정할 필요가 없습니다.  

공유 배포 지점을 계획하려면 다음 정보를 참조하십시오.  

-   공유할 배포 지점이 공유 배포 지점의 필수 구성 요소를 충족해야 합니다. 이러한 필수 구성 요소에 대한 자세한 내용은 [System Center Configuration Manager에서 마이그레이션을 수행하기 위한 필수 조건](../../core/migration/prerequisites-for-migration.md)의 [마이그레이션을 위한 필수 구성](../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations)을 참조하세요.  

-   공유 배포 지점 작업은 원본 사이트 및 모든 직계 자식 보조 사이트에서 조건에 맞는 모든 배포 지점을 공유하는 사이트 전체 설정입니다. 배포 지점 공유를 사용하는 경우 공유할 개별 배포 지점을 선택할 수 없습니다.  

-   대상 계층의 클라이언트는 원본 계층에서 공유된 배포 지점에 배포된 패키지의 콘텐츠 위치 정보를 받을 수 있습니다. Configuration Manager 2007 원본 계층에 있는 배포 지점의 경우 이러한 콘텐츠 위치로는 분기 배포 지점, 서버 공유의 배포 지점 및 표준 배포 지점이 있습니다.  

    > [!WARNING]  
    >  원본 계층을 변경하면 원래의 원본 계층에 있던 공유 배포 지점을 더 이상 사용할 수 없고 대상 계층의 클라이언트에 콘텐츠 위치로 제공할 수 없습니다. 원래의 원본 계층을 사용하도록 마이그레이션을 다시 구성하면 이전 공유 배포 지점이 유효한 콘텐츠 위치 서버로 복원됩니다.  

-   공유 배포 지점에 호스트된 패키지를 마이그레이션하는 경우 원본 계층과 대상 계층의 패키지 버전이 같게 유지되어야 합니다. 원본 계층과 대상 계층의 패키지 버전이 다르면 대상 계층의 클라이언트가 공유 배포 지점에서 해당 콘텐츠를 받을 수 없습니다. 그러므로 원본 계층의 패키지를 업데이트할 경우 패키지 데이터를 다시 마이그레이션해야 대상 계층의 클라이언트가 공유 배포 지점에서 콘텐츠를 받을 수 있습니다.  

    > [!NOTE]  
    >  공유 배포 지점에 호스트된 패키지의 세부 정보를 보면 다음 데이터 수집 주기가 끝날 때까지 원본 사이트 **공유 배포 지점** 탭에 **호스트된 마이그레이션 패키지**로 표시되는 패키지 수가 업데이트되지 않습니다.  

-   대상 계층에 연결되는 Configuration Manager 콘솔의 **관리** 작업 영역의 **원본 계층** 노드에서 공유 배포 지점과 해당 속성을 확인할 수 있습니다.  

-   Configuration Manager 2007 원본 계층에서 공유 배포 지점을 사용하여 Microsoft Application Virtualization(App-V)의 패키지를 호스트할 수 없습니다. App-V 패키지를 마이그레이션하고 대상 계층의 클라이언트가 사용할 수 있도록 변환해야 합니다. 그러나 System Center 2012 Configuration Manager 또는 System Center Configuration Manager 원본 계층에서 공유 배포 지점을 사용하면 App-V 패키지를 대상 계층의 클라이언트용으로 호스트할 수 있습니다.  

-   Configuration Manager 2007 원본 계층에서 보호된 배포 지점을 공유하면 대상 계층에서 해당 배포 지점의 보호되는 네트워크 위치를 포함하는 경계 그룹이 만들어집니다. 대상 계층에서는 이 경계 그룹을 변경할 수 없습니다. 그러나 Configuration Manager 2007 원본 계층의 배포 지점에 대한 보호되는 경계 정보를 변경하면 다음 데이터 수집 주기가 끝난 후에 해당 변경 사항이 대상 계층에 반영됩니다.  

    > [!NOTE]  
    >  System Center 2012 Configuration Manager 및 System Center Configuration Manager 사이트에서는 보호된 배포 지점이 아니라 기본 배포 지점이라는 개념을 사용합니다. Configuration Manager 2007 원본 사이트에서 공유된 배포 지점에만 이 조건이 적용됩니다.  

원본 사이트에서 배포 지점을 공유하기 전에는 공유 가능한 배포 지점이 Configuration Manager 콘솔에 표시되지 않습니다. 배포 지점을 공유하면 성공적으로 공유된 배포 지점만 나열됩니다.  

배포 지점을 공유한 후에는 원본 계층에서 공유 배포 지점의 구성을 변경할 수 있습니다. 배포 지점의 구성 변경 사항은 다음 데이터 수집 주기가 끝난 후 대상 계층에 반영됩니다. 공유 조건에 맞게 업데이트된 배포 지점은 자동으로 공유되지만 더 이상 조건에 맞지 않는 배포 지점은 배포 지점 공유가 중단됩니다. 예를 들어 인트라넷 FQDN으로 설정되지 않아 처음에 대상 계층과 공유되지 않은 배포 지점이 있을 수 있습니다. 이 배포 지점의 FQDN을 설정한 후에 다음 데이터 수집 주기에서 이 구성을 확인하면 이 배포 지점이 대상 계층과 공유됩니다.  

##  <a name="Planning_to_Upgrade_DPs"></a> Configuration Manager 2007 공유 배포 지점 업그레이드 계획  
Configuration Manager 2007 원본 계층에서 마이그레이션할 때 공유 배포 지점을 업그레이드하여 System Center Configuration Manager 배포 지점으로 만들 수 있습니다. 기본 사이트와 보조 사이트에서 배포 지점을 업그레이드할 수 있습니다. 업그레이드 프로세스는 Configuration Manager 2007 계층에서 배포 지점을 제거하고 대상 계층에서 이 배포 지점을 사이트 시스템 서버로 만듭니다. 이 프로세스는 배포 지점에 있는 기존 콘텐츠를 배포 지점 컴퓨터의 새 위치로도 복사합니다. 그러면 업그레이드 프로세스에서 콘텐츠의 사본을 수정하여 대상 계층에서 콘텐츠 배포와 함께 사용할 단일 인스턴스 저장소를 만듭니다. 그러므로 배포 지점을 업그레이드할 때, 마이그레이션되어 Configuration Manager 2007 배포 지점에 호스트된 콘텐츠를 재배포할 필요가 없습니다.  

Configuration Manager에서 콘텐츠를 단일 인스턴스 저장소로 변환하고 나면 Configuration Manager는 배포 지점 컴퓨터에서 원래 원본 콘텐츠를 삭제하여 디스크 공간을 확보합니다. Configuration Manager에서는 원래 원본 콘텐츠 위치를 사용하지 않습니다.  

공유할 수 있는 모든 Configuration Manager 2007 배포 지점을 System Center Configuration Manager로 업그레이드할 수 있는 것은 아닙니다. 업그레이드가 가능하려면 Configuration Manager 2007 배포 지점이 업그레이드 조건을 충족해야 합니다. 이러한 조건에는 배포 지점이 설치된 사이트 시스템 서버 및 설치된 Configuration Manager 2007 배포 지점 유형이 있습니다. 예를 들어 기본 사이트의 사이트 서버 컴퓨터에 설치된 배포 지점 유형은 업그레이드할 수 없지만 보조 사이트의 사이트 서버 컴퓨터에 설치된 표준 배포 지점은 업그레이드할 수 있습니다.  

> [!NOTE]  
>  대상 계층의 배포 지점에 대해 지원되는 운영 체제 버전을 실행하는 컴퓨터에 있는 Configuration Manager 2007 공유 배포 지점만 업그레이드할 수 있습니다. 예를 들어 Windows Vista를 실행하는 컴퓨터에 있는 Configuration Manager 2007 배포 지점을 공유할 수는 있지만 System Center Configuration Manager에서 이 운영 체제를 배포 지점으로 사용할 수 없으므로 이 공유 배포 지점을 업그레이드할 수는 없습니다.  

다음 표에는 업그레이드할 수 있는 Configuration Manager 2007 배포 지점의 각 유형별로 지원되는 위치가 나열되어 있습니다.  

|배포 지점의 유형|사이트 서버가 아닌 사이트 시스템 컴퓨터의 배포 지점|사이트 서버가 아닌 사이트 시스템 컴퓨터의 배포 지점 및 다른 사이트 시스템 역할을 호스팅하는 배포 지점|보조 사이트 서버의 배포 지점|  
|--------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------|  
|표준 배포 지점|예|아니요|예|  
|서버 공유의 배포 지점<sup>1</sup>|예|아니요|아니요|  
|분기 배포 지점|예|아니요|아니요|  

 <sup>1</sup> System Center Configuration Manager에서는 사이트 시스템의 서버 공유를 지원하지 않지만 서버 공유에 있는 Configuration Manager 2007 배포 지점의 업그레이드는 지원합니다. 서버 공유에 있는 Configuration Manager 2007 배포 지점을 업그레이드하면 이 배포 지점 유형이 자동으로 서버로 변환되며 단일 인스턴스 콘텐츠 저장소를 저장할 배포 지점 컴퓨터의 드라이브를 선택해야 합니다.  

> [!WARNING]  
>  분기 배포 지점을 업그레이드하기 전에 Configuration Manager 2007 클라이언트 소프트웨어를 제거합니다. Configuration Manager 2007 클라이언트 소프트웨어가 설치된 분기 배포 지점을 업그레이드하면 이전에 컴퓨터에 배포했던 콘텐츠가 컴퓨터에서 제거되고 배포 지점이 업그레이드되지는 않습니다.  

Configuration Manager 콘솔의 **원본 계층** 노드에서 업그레이드할 수 있는 배포 지점을 확인하려면 원본 사이트를 선택한 후 **공유 배포 지점** 탭을 선택합니다. 업그레이드 가능한 배포 지점은 **업그레이드 가능** 열에 **예** 로 표시됩니다.  

Configuration Manager 2007 보조 사이트 서버에 설치된 배포 지점을 업그레이드할 경우 보조 사이트가 원본 계층에서 제거됩니다. 이 시나리오의 명칭은 보조 사이트 업그레이드이지만 배포 지점 사이트 시스템 역할에만 적용됩니다. 따라서 보조 사이트는 업그레이드되지 않고 그 대신 제거됩니다. 이에 따라 보조 사이트 서버였던 컴퓨터에는 대상 계층의 배포 지점이 남게 됩니다. 보조 사이트에서 배포 지점을 업그레이드하려고 계획하는 경우 이 항목에서 [Configuration Manager 2007 보조 사이트 업그레이드 계획](#BKMK_UpgradeSS)을 참조하세요.  

###  <a name="BKIMK_UpgradeProcess"></a> 배포 지점 업그레이드 프로세스  
Configuration Manager 콘솔을 사용하여 대상 계층 구조와 공유하는 Configuration Manager 2007 배포 지점을 업그레이드할 수 있습니다. 공유 배포 지점을 업그레이드할 경우 해당 배포 지점이 Configuration Manager 2007 사이트에서 제거됩니다. 그런 다음, 대상 계층에서 지정한 기본 또는 보조 사이트에 연결된 배포 지점으로 설치됩니다. 업그레이드 프로세스는 배포 지점에 저장되는 마이그레이션된 콘텐츠의 복사본을 만든 다음 이 복사본을 단일 인스턴스 콘텐츠 저장소로 변환합니다. Configuration Manager는 패키지를 단일 인스턴스 콘텐츠 저장소로 변환할 때 패키지에 **배포 지점에서 프로그램 실행**으로 설정된 하나 이상의 보급 알림이 포함되지 않으면 배포 지점 컴퓨터의 SMSPKG 공유에서 이 패키지를 삭제합니다.  

배포 지점을 업그레이드하기 위해 Configuration Manager는 원본 사이트의 SMS 공급자에서 데이터를 수집하도록 설정된 **원본 사이트 액세스 계정**을 사용합니다. 이 계정으로 원본 사이트에서 데이터를 수집하려면 사이트 개체에 대한 **읽기** 권한만 있으면 되지만, 업그레이드하는 동안 Configuration Manager 2007 사이트에서 배포 지점을 제거하려면 **사이트** 클래스에 대한 **삭제** 및 **수정** 권한도 있어야 합니다.  

> [!NOTE]  
>  Configuration Manager는 한 번에 하나의 배포 지점에서만 콘텐츠를 단일 인스턴스 저장소로 변환할 수 있습니다. 다중 배포 지점 업그레이드를 설정할 경우 배포 지점은 업그레이드를 위해 대기하며 한 번에 하나씩 처리됩니다.  

공유 배포 지점을 업그레이드하기 전에 먼저 배포 지점에 배포된 모든 콘텐츠를 마이그레이션해야 합니다. 배포 지점을 업그레이드하기 전에 마이그레이션하지 않은 콘텐츠는 업그레이드 후 대상 계층에서 사용할 수 없습니다. 배포 지점을 업그레이드하면 마이그레이션된 패키지의 콘텐츠는 대상 계층의 단일 인스턴스 저장소와 호환되는 형식으로 변환됩니다.  

Configuration Manager 콘솔을 통해 배포 지점을 업그레이드하려면 Configuration Manager 2007 사이트 시스템 서버가 다음 조건을 충족해야 합니다.  

-   배포 지점 구성 및 위치를 업그레이드할 수 있어야 합니다.  

-   배포 지점 컴퓨터에는 콘텐츠를 Configuration Manager 2007 콘텐츠 저장소 형식에서 단일 인스턴스 저장소 형식으로 변환하는 데 충분한 디스크 공간이 있어야 합니다. 이 변환 작업에는 배포 지점에 저장된 가장 큰 패키지의 크기와 동일한 사용 가능한 디스크 공간이 필요합니다.  

-   배포 지점 컴퓨터는 대상 계층에서 배포 지점으로 지원되는 운영 체제 버전을 실행해야 합니다.  

    > [!NOTE]  
    >  Configuration Manager는 배포 지점이 업그레이드에 적합한지 확인할 때 배포 지점 컴퓨터에 설치된 운영 체제 버전의 유효성은 검사하지 않습니다.  

배포 지점을 업그레이드하려면 **관리** 작업 영역에서 **마이그레이션**및 **원본 계층** 노드를 차례로 확장한 다음 업그레이드할 배포 지점이 포함된 사이트를 선택합니다. 그런 다음 세부 정보 창의 **공유 배포 지점** 탭에서 업그레이드할 배포 지점을 선택합니다.  

**재할당 가능** 열에서 상태를 확인하면 배포 지점의 업그레이드가 준비되었는지 확인할 수 있습니다.  그런 다음 Configuration Manager 콘솔 리본에서 **배포 지점** 탭의 **배포 지점** 그룹에 있는 **재할당**을 선택합니다. 곧 시작되는 마법사를 사용하여 배포 지점의 업그레이드를 완료할 수 있습니다.  

공유 배포 지점을 업그레이드할 때 대상 계층에서 선택한 기본 사이트나 보조 사이트에 배포 지점을 할당해야 합니다. 배포 지점이 업그레이드되면 이 배포 지점을 다른 배포 지점처럼 대상 계층 내의 배포 지점으로 관리할 수 있습니다.  

Configuration Manager 콘솔에서 **관리** 작업 영역의 **마이그레이션** 노드 아래에 있는 **배포 지점 마이그레이션** 노드를 선택하면 배포 지점 업그레이드의 진행률을 모니터링할 수 있습니다. 또한 대상 계층의 중앙 관리 사이트 서버에 있는 **Migmctrl.log** 또는 대상 계층에서 업그레이드된 배포 지점을 관리하는 사이트 서버에 있는 **distmgr.log** 를 통해 관련 정보를 확인할 수 있습니다.  

> [!NOTE]  
>  배포 지점을 대상 계층으로 업그레이드하면 배포 지점 사이트 시스템 역할이 Configuration Manager 2007 원본 사이트에서 제거됩니다. 하지만 배포 지점으로 보낸 패키지는 Configuration Manager 2007 계층 구조에서 업데이트되지 않습니다. 배포 지점에 보낸 패키지는 Configuration Manager 2007 콘솔에서 사이트 시스템 컴퓨터를 **알 수 없음**의 **유형**을 갖는 배포 지점으로 계속 표시합니다. 이후 Configuration Manager 2007의 패키지에서 업데이트가 실행될 경우 사이트에서 알 수 없는 사이트 시스템에서 이 패키지를 업데이트하려고 시도할 때 배포 관리자가 해당 사이트에 대한 distmgr.log를 통해 오류를 보고합니다.  

공유 배포 지점을 업그레이드하지 않기로 결정한 경우 대상 계층의 배포 지점을 이전 Configuration Manager 2007 배포 지점에 계속 설치할 수 있습니다. 새 배포 지점을 설치하려면 먼저 배포 지점 컴퓨터에서 모든 Configuration Manager 2007 사이트 시스템 역할을 제거해야 합니다. 여기에는 해당 컴퓨터가 사이트 서버 컴퓨터인 경우 Configuration Manager 2007 사이트도 포함됩니다. Configuration Manager 2007 배포 지점을 제거할 때 배포 지점에 배포된 콘텐츠는 컴퓨터에서 삭제되지 않습니다.  

###  <a name="BKMK_UpgradeSS"></a> Configuration Manager 2007 보조 사이트 업그레이드 계획  
 Configuration Manager 2007 보조 사이트 서버에서 호스트되는 공유 배포 지점을 마이그레이션을 통해 업그레이드할 경우 Configuration Manager에서는 배포 지점 사이트 시스템 역할을 대상 계층의 배포 지점으로 업그레이드합니다. 또한 원본 계층에서 보조 사이트도 제거합니다. 따라서 보조 사이트 없이 System Center Configuration Manager 배포 지점이 만들어집니다.  

 사이트 서버 컴퓨터에 있는 배포 지점의 업그레이드가 가능하려면 Configuration Manager로 해당 컴퓨터에 있는 각 사이트 시스템 역할과 보조 사이트를 제거할 수 있어야 합니다. 일반적으로 Configuration Manager 2007 서버 공유의 공유 배포 지점은 업그레이드가 가능합니다. 그러나 서버 공유가 보조 사이트 서버에 있는 경우 보조 사이트와 이 컴퓨터의 공유 배포 지점은 업그레이드할 수 없습니다. 이는 프로세스에서 보조 사이트를 제거하려고 할 때 서버 공유는 추가 사이트 시스템 개체로 처리되고 프로세스에서 이 개체를 제거할 수 없기 때문입니다. 이 시나리오에서는 보조 사이트 서버에서 표준 배포 지점을 사용하도록 설정한 다음 콘텐츠를 이 표준 배포 지점에 재배포하면 됩니다. 이 프로세스에서는 네트워크 대역폭을 사용하지 않습니다. 또한 작업이 완료되면 서버 공유에서 배포 지점을 제거하고 서버 공유를 제거한 다음, 배포 지점과 보조 사이트를 업그레이드할 수 있습니다.  

 공유 배포 지점을 업그레이드하려면 먼저 Configuration Manager 2007의 배포 지점 구성을 검토하여 Configuration Manager 2007에서 계속 사용하려는 보조 사이트의 배포 지점을 업그레이드하지 않도록 해야 합니다. 보조 사이트 서버에 있는 공유 배포 지점을 업그레이드하면 Configuration Manager 2007 계층 구조에서 사이트 시스템 서버가 제거되어 해당 계층 구조에서 더 이상 사용할 수 없기 때문에 이 방법을 사용하는 것이 좋습니다. 보조 사이트가 제거되면 해당 보조 사이트의 나머지 배포 지점이 분리됩니다. 이는 해당 배포 지점이 Configuration Manager 2007에서 관리되지 않게 되고 더 이상 공유되지 않거나 업그레이드할 수 없음을 의미합니다.  

> [!WARNING]  
>  Configuration Manager 콘솔에서 공유 배포 지점을 볼 때 공유 배포 지점이 원격 사이트 시스템 서버 또는 보조 사이트 서버에 있는지는 표시되지 않습니다.  

 원격 네트워크 위치에 주로 이 위치에 대한 콘텐츠 배포를 제어하는 데 사용되는 보조 사이트가 있는 경우 공유 배포 지점이 있는 이 보조 사이트를 업그레이드하는 것이 좋습니다. System Center Configuration Manager 배포 지점에 콘텐츠를 배포할 경우 대역폭 제어를 설정할 수 있으므로 보조 사이트를 배포 지점으로 업그레이드하고 대역폭 제어용으로 배포 지점을 설정하고 대상 계층의 해당 네트워크 위치에 보조 사이트가 설치되지 않도록 할 수 있는 경우가 많습니다.  

 보조 사이트 서버의 공유 배포 지점을 업그레이드하는 프로세스는 다른 공유 배포 지점 업그레이드와 동일합니다. 콘텐츠는 대상 계층에서 사용 중인 단일 인스턴스 저장소로 복사된 후 변환됩니다. 그러나 보조 사이트 서버에 있는 공유 배포 지점을 업그레이드할 때도 업그레이드 프로세스에서 관리 지점(있는 경우)을 제거한 다음 보조 사이트를 서버에서 제거합니다. 따라서 보조 사이트는 Configuration Manager 2007 계층 구조에서 제거됩니다. 보조 사이트를 제거할 때 Configuration Manager는 원본 사이트에서 데이터를 수집하도록 설정된 계정을 사용합니다.  

 업그레이드 중에 Configuration Manager 2007 보조 사이트가 제거될 때부터 대상 계층에서 배포 지점 설치가 시작될 때까지는 지연 시간이 발생합니다. 이 지연 시간은 데이터 수집 주기에 따라 결정되며 최대 시간은 4시간입니다. 지연 시간은 새 배포 지점 설치가 시작될 때까지 보조 사이트가 제거될 수 있는 시간을 제공합니다.  

 공유 배포 지점을 업그레이드하는 방법에 대한 자세한 내용은 [Configuration Manager 2007 공유 배포 지점 업그레이드 계획](#Planning_to_Upgrade_DPs)을 참조하세요.  

##  <a name="BKMK_ReassignDistPoint"></a> System Center Configuration Manager 배포 지점 재할당 계획  
 지원되는 System Center 2012 Configuration Manager 버전에서 같은 버전의 계층으로 마이그레이션할 경우 원본 계층의 공유 배포 지점을 대상 계층 내의 사이트에 재할당할 수 있습니다. 이것은 Configuration Manager 2007 배포 지점을 업그레이드하여 대상 계층의 배포 지점으로 만드는 개념과 비슷합니다. 기본 사이트와 보조 사이트에서 배포 지점을 재할당할 수 있습니다. 배포 지점을 재할당하면 원본 계층에서 배포 지점이 제거되고 컴퓨터 및 해당 배포 지점이 사용자가 대상 계층에서 선택한 사이트의 사이트 시스템 서버가 됩니다.  

 배포 지점을 재할당할 경우에는 원본 사이트 배포 지점에서 호스트했던 마이그레이션된 콘텐츠는 재배포할 필요가 없습니다. 또한 배포 지점을 재할당할 때는 Configuration Manager 2007 배포 지점의 업그레이드와 달리 배포 지점 컴퓨터에 추가 디스크 공간이 필요하지 않습니다. System Center 2012 Configuration Manager부터 배포 지점에서 콘텐츠에 대해 단일 인스턴스 저장소 형식을 사용합니다. 계층 구조 간에 배포 지점을 재할당할 때 배포 지점 컴퓨터의 콘텐츠를 변환할 필요가 없습니다.  

 System Center 2012 Configuration Manager 배포 지점을 재할당할 수 있도록 하려면 다음 기준을 충족해야 합니다.  

-   공유 배포 지점은 사이트 서버가 아닌 다른 컴퓨터에 설치되어 있어야 합니다.  

-   공유 배포 지점은 추가 사이트 시스템 역할과 함께 배치할 수 없습니다.  

Configuration Manager 콘솔의 **원본 계층** 노드에서 재할당할 수 있는 배포 지점을 확인하려면 원본 사이트를 선택한 다음 **공유 배포 지점** 탭을 선택합니다. 재할당 가능한 배포 지점의 경우 **재할당 가능 열**에 **예**가 표시됩니다. System Center 2012 R2 Configuration Manager 이전 버전에서 이 열 이름은 **업그레이드 가능**이었습니다.  

###  <a name="BKMK_ReassignProcess"></a> 배포 지점 재할당 프로세스  
 Configuration Manager 콘솔을 사용하여 활성 원본 계층에서 공유 배포 지점을 재할당할 수 있습니다. 공유 배포 지점을 재할당할 경우 해당 배포 지점은 원본 사이트에서 제거된 다음 대상 계층에 지정한 기본 또는 보조 사이트에 연결되는 배포 지점으로 설치됩니다.  

 배포 지점을 재할당하기 위해 대상 계층에서는 원본 사이트의 SMS 공급자에서 데이터를 수집하도록 설정된 원본 사이트 액세스 계정을 사용합니다. 필요한 권한과 추가 필수 조건에 대한 자세한 내용은 [System Center Configuration Manager에서 마이그레이션을 수행하기 위한 필수 조건](../../core/migration/prerequisites-for-migration.md)을 참조하세요.  

## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>동시에 여러 공유 배포 지점 마이그레이션
버전 1610부터 **배포 지점 재할당**을 사용하여 Configuration Manager 프로세스에서 동시에 최대 50개의 공유 배포 지점을 병렬로 재할당하도록 할 수 있습니다. 여기에는 다음을 실행하는 지원되는 원본 사이트의 공유 배포 지점이 포함됩니다.  
- Configuration Manager 2007
- System Center 2012 Configuration Manager
- System Center 2012 R2 Configuration Manager
- System Center Configuration Manager(현재 분기)

배포 지점을 다시 할당하는 경우 각 배포 지점이 업그레이드되거나 다시 할당될 자격이 있어야 합니다. 관련된 작업 및 프로세스의 이름(업그레이드 또는 재할당)은 원본 사이트에서 실행하는 Configuration Manager 버전에 따라 달라집니다. 그러나 두 작업의 최종 결과는 동일합니다. 배포 지점이 해당 콘텐츠가 구현된 현재 분기 사이트 중 하나에 할당됩니다.

버전 1610 이전에는 Configuration Manager에서 한 번에 하나의 배포 지점만 처리할 수 있었습니다. 이제 다음과 같은 주의 사항은 있지만 배포 지점을 원하는 개수만큼 재할당할 수 있습니다.  
- 재할당할 배포 지점을 다중 선택할 수는 없지만 둘 이상을 큐에 넣으면 Configuration Manager에서 다음 배포 지점을 시작하기 전에 배포 지점이 완료되기를 기다리는 대신 병렬로 처리합니다.  
- 기본적으로 최대 50개의 배포 지점이 동시에 병렬로 처리됩니다. 첫 번째 배포 지점의 재할당이 완료되면 Configuration Manager에서 51번째 배포 지점의 처리를 시작합니다.  
- Configuration Manager SDK를 사용하는 경우 **SharedDPImportThreadLimit**를 변경하여 Configuration Manager에서 병렬로 처리할 수 있는 재할당된 배포 지점 수를 조정할 수 있습니다.


##  <a name="About_Migrating_Content"></a> 콘텐츠 마이그레이션 시 콘텐츠 소유권 할당  
 배포할 콘텐츠를 마이그레이션하는 경우 콘텐츠 개체를 대상 계층 내 사이트에 할당해야 합니다. 그러면 이 사이트는 대상 계층에서 해당 콘텐츠의 소유자가 됩니다. 대상 계층의 최상위 사이트는 콘텐츠의 메타데이터를 마이그레이션하는 사이트지만 네트워크를 통해 콘텐츠의 원래 원본 파일을 사용하는 사이트는 할당된 사이트입니다.  

 콘텐츠를 마이그레이션할 때 사용되는 네트워크 대역폭을 최소화하려면 네트워크에서 원본 계층의 콘텐츠 위치에 가까운 대상 계층의 사이트로 콘텐츠 소유권을 이전하는 것이 좋습니다. 대상 계층의 콘텐츠에 대한 정보는 전체에서 공유되므로 모든 사이트에서 사용할 수 있습니다.  

 콘텐츠 관련 정보는 데이터베이스 복제를 통해 모든 사이트에 공유되지만 기본 사이트에 할당한 후 다른 기본 사이트의 배포 지점에 배포한 콘텐츠는 파일 기반 복제를 통해 전송됩니다. 이 전송은 중앙 관리 사이트를 경유한 다음 다른 기본 사이트로 라우팅됩니다. 사이트를 콘텐츠 소유자로 할당하는 경우 마이그레이션 전이나 도중에 여러 기본 사이트에 배포할 패키지를 중앙에서 관리하면 대역폭이 낮은 네트워크를 통한 데이터 전송을 줄일 수 있습니다.
