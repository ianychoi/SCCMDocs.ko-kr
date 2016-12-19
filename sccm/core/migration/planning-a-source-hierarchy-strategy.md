---
title: "원본 계층 전략 | System Center Configuration Manager"
description: "System Center Configuration Manager 마이그레이션 작업을 구성하기 전에 원본 계층을 구성하고 원본 사이트의 데이터를 수집합니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4800a800-66c8-4c35-aebe-e413a23790c1
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 11ab1dc90c3e26b159346693b8e85a182219daf4


---
# <a name="planning-a-source-hierarchy-strategy-in-system-center-configuration-manager"></a>System Center Configuration Manager에서 원본 계층 구조 전략 계획

*적용 대상: System Center Configuration Manager(현재 분기)*

System Center Configuration Manager 환경에서 마이그레이션 작업을 구성하려면 먼저 원본 계층을 구성하고 이 계층에 있는 하나 이상의 원본 사이트에서 데이터를 수집해야 합니다. 다음 섹션을 사용하여 원본 계층 및 원본 사이트를 구성하는 방법과 Configuration Manager를 통해 원본 계층의 원본 사이트에서 정보를 수집하는 방법에 대해 계획합니다.  

-   [원본 계층 구조](#BKMK_Source_Hierarchies)  

-   [원본 사이트](#BKMK_Source_Sites)  

-   [데이터 수집](#BKMK_Data_Gathering)  

##  <a name="a-namebkmksourcehierarchiesa-source-hierarchies"></a><a name="BKMK_Source_Hierarchies"></a> 원본 계층 구조  
원본 계층은 마이그레이션할 데이터가 포함된 Configuration Manager 계층입니다. 마이그레이션을 구성하고 원본 계층을 지정할 때 원본 계층의 최상위 사이트를 지정합니다. 이 사이트를 원본 사이트라고도 합니다. 원본 계층 구조에서 데이터를 마이그레이션할 수 있는 추가 사이트 또한 원본 사이트라고 합니다.  

-   Configuration Manager 2007 원본 계층에서 데이터를 마이그레이션하는 마이그레이션 작업을 구성할 경우 원본 계층의 특정 원본 사이트 하나 이상에서 데이터를 마이그레이션하도록 구성합니다.  

-   System Center 2012 Configuration Manager 이상 버전을 실행하는 원본 계층에서 데이터를 마이그레이션하는 마이그레이션 작업을 구성할 경우 최상위 사이트만 지정하면 됩니다.  

원본 계층 구조는 한 번에 하나만 구성할 수 있습니다.  

-   새 원본 계층을 구성하면 이 계층이 자동으로 현재 원본 계층이 되어 이전 원본 계층을 대체합니다.  

-   원본 계층을 구성할 때는 Configuration Manager에서 해당 원본 사이트의 SMS 공급자 및 사이트 데이터베이스에 연결하는 데 사용할 자격 증명과 원본 계층의 최상위 사이트를 지정해야 합니다.  

-   Configuration Manager에서는 이러한 자격 증명을 사용하여 데이터 수집을 실행해 원본 사이트의 배포 지점 및 개체에 대한 정보를 검색합니다.  

-   데이터 수집 프로세스의 일부로 원본 계층에서 자식 사이트를 확인합니다.  

-   원본 계층이 Configuration Manager 2007 계층이면 해당 추가 사이트를 원본 사이트로 구성하고 각 원본 사이트에 별도의 자격 증명을 사용할 수 있습니다.  

원본 계층 구조는 연속으로 여러 개 구성할 수 있지만 마이그레이션은 한 번에 하나의 원본 계층 구조에 대해서만 활성화됩니다.  

-   현재 원본 계층에서 마이그레이션을 완료하기 전에 추가 원본 계층을 구성할 경우 Configuration Manager는 현재 원본 계층에 대해 모든 활성 마이그레이션 작업을 취소하고 예약된 모든 마이그레이션 작업을 연기합니다.  

-   그러면 새로 구성한 원본 계층 구조가 현재 원본 계층 구조가 되고 원래 원본 계층 구조는 이제 비활성 상태가 됩니다.  

-   그 다음에는 새 원본 계층의 연결 자격 증명, 추가 원본 사이트 및 마이그레이션 작업을 구성할 수 있습니다.  

비활성 원본 계층을 복원할 경우 이전에 **마이그레이션 데이터 정리** 작업을 사용하지 않았다면 해당 원본 계층에 대해 이전에 구성된 마이그레이션 작업을 볼 수 있습니다. 그러나 이 계층에서 마이그레이션을 계속하려면 먼저 계층의 해당되는 원본 사이트에 연결할 자격 증명을 다시 구성한 후 완료되지 않은 마이그레이션 작업을 다시 예약해야 합니다.  

> [!CAUTION]  
>  두 개 이상의 원본 계층에서 데이터를 마이그레이션하려면 각 추가 원본 계층에 고유한 사이트 코드 집합이 있어야 합니다.  

원본 계층을 구성하는 방법에 대한 자세한 내용은 [System Center Configuration Manager로 마이그레이션할 원본 계층 및 원본 사이트 구성](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)을 참조하세요.  

##  <a name="a-namebkmksourcesitesa-source-sites"></a><a name="BKMK_Source_Sites"></a> 원본 사이트  
 원본 사이트는 마이그레이션할 데이터가 포함된 원본 계층 내 사이트입니다. 원본 계층의 최상위 사이트는 항상 첫 번째 원본 사이트가 됩니다. 마이그레이션하는 동안 새 원본 계층의 첫 번째 원본 사이트에서 데이터가 수집될 때 해당 계층의 추가 사이트에 대한 정보도 검색됩니다.  

 초기 원본 사이트에 대해 데이터 수집이 완료된 후 다음에 수행할 작업은 원본 계층의 제품 버전에 따라 달라집니다.  

### <a name="source-sites-that-run-configuration-manager-2007-sp2"></a>Configuration Manager 2007 SP2를 실행하는 원본 사이트  
 Configuration Manager 2007 SP2 계층의 초기 원본 사이트에서 데이터가 수집되면 마이그레이션 작업을 만들기 전에 추가 원본 사이트를 구성할 필요가 없습니다. 그러나 추가 사이트에서 데이터를 마이그레이션하려면 먼저 추가 사이트를 원본 사이트로 구성하고 System Center Configuration Manager를 통해 이 사이트에서 데이터를 수집해야 합니다.  

 추가 사이트에서 데이터를 수집하려면 각 사이트를 개별적으로 원본 사이트로 구성해야 합니다. 이렇게 하려면 각 원본 사이트의 SMS 공급자 및 사이트 데이터베이스에 연결하기 위해 System Center Configuration Manager에 대한 자격 증명을 지정해야 합니다. 원본 사이트에 대한 자격 증명을 구성하고 나면 사이트에 대해 데이터 수집 프로세스가 시작됩니다.  

 Configuration Manager 2007 SP2 원본 계층에서 추가 원본 사이트를 구성할 경우 위에서 아래 방향으로 원본 사이트를 구성해야 합니다. 따라서 최하위 계층 사이트는 마지막으로 구성해야 합니다. 언제든지 계층의 분기 안에 원본 사이트를 구성할 수 있지만 자식 사이트를 원본 사이트로 구성하려면 먼저 부모 사이트를 원본 사이트로 구성해야 합니다.  

> [!NOTE]  
>  Configuration Manager 2007 SP2 계층 구조의 경우 기본 사이트에서만 마이그레이션이 지원됩니다.  

### <a name="source-sites-that-run-system-center-2012-configuration-or-later"></a>System Center 2012 Configuration 이상을 실행하는 원본 사이트  
 System Center 2012 Configuration Manager 이상 계층의 초기 원본 사이트에서 데이터가 수집되면 해당 원본 계층에서 추가 원본 사이트를 구성할 필요가 없습니다. Configuration Manager 2007과는 달리 이러한 Configuration Manager 버전에서는 공유 데이터베이스를 사용하며 공유 데이터베이스를 통해 초기 원본 사이트에서 사용 가능한 모든 개체를 확인한 후 마이그레이션할 수 있기 때문입니다.  

 그러나 데이터를 수집할 액세스 계정을 구성할 경우 원본 계층의 여러 컴퓨터에 액세스할 수 있는 **원본 사이트 SMS 공급자 계정** 권한을 부여해야 할 수 있습니다. 원본 사이트가 각기 다른 컴퓨터에 있는 SMS 공급자의 여러 인스턴스를 지원하는 경우 이 권한이 필요할 수 있습니다. 데이터 수집이 시작되면 대상 계층의 최상위 사이트는 원본 계층의 최상위 사이트에 연결하여 사이트에 대한 SMS 공급자의 위치를 확인합니다. 이 경우 SMS 공급자의 첫 번째 인스턴스만 확인됩니다. 데이터 수집 프로세스에서 확인된 위치에 있는 SMS 공급자에 액세스할 수 없는 경우 프로세스는 실패하고 사이트에 대한 SMS 공급자의 인스턴스를 실행하는 추가 컴퓨터에 연결을 시도하지 않습니다.  

##  <a name="a-namebkmkdatagatheringa-data-gathering"></a><a name="BKMK_Data_Gathering"></a> 데이터 수집  
 Configuration Manager가 원본 사이트에서 데이터를 수집하기 시작하는 시점은 원본 계층을 지정하거나, 원본 계층의 각 추가 원본 사이트에 대해 자격 증명을 구성하거나, 원본 사이트에 대한 배포 지점을 공유한 직후입니다.  

 데이터 수집 프로세스는 단순 일정에 따라 자동으로 반복되어 원본 사이트 내 데이터의 변경 내용에 대해 동기화 상태를 유지합니다. 기본적으로 이 프로세스는 4시간마다 반복됩니다. 원본 사이트의 **속성** 을 편집하면 이 주기에 대한 일정을 수정할 수 있습니다. 초기 데이터 수집 프로세스는 Configuration Manager 데이터베이스의 모든 개체를 검토하므로 완료하는 데 다소 시간이 걸릴 수 있습니다. 이후의 데이터 수집 프로세스는 데이터의 변경 내용만 확인하므로 더 적은 시간이 소요됩니다.  

 대상 계층의 최상위 사이트는 데이터를 수집하기 위해 원본 사이트의 SMS 공급자와 사이트 데이터베이스에 연결한 후 개체 및 배포 지점의 목록을 검색합니다. 이 연결에서 원본 사이트 액세스 계정이 사용됩니다. 데이터 수집을 위한 필수 구성에 대한 자세한 내용은 [System Center Configuration Manager에서 마이그레이션을 수행하기 위한 필수 조건](../../core/migration/prerequisites-for-migration.md)을 참조하세요.  

 Configuration Manager 콘솔에서 **지금 데이터 수집** 및 **데이터 수집 중지** 작업을 사용하여 데이터 수집 프로세스를 시작하고 중지할 수 있습니다.  

 원본 사이트에 대해 **데이터 수집 중지** 옵션을 사용한 후에는 먼저 사이트에 대한 자격 증명을 다시 구성해야 사이트에서 다시 데이터를 수집할 수 있습니다. 원본 사이트를 다시 구성하기 전에 Configuration Manager는 해당 사이트에서 새 개체 또는 이전에 마이그레이션된 개체의 변경 내용을 확인할 수 없습니다.  

> [!NOTE]  
>  독립 실행형 기본 사이트를 중앙 관리 사이트가 있는 계층으로 확장하려면 먼저 모든 데이터 수집을 중지해야 합니다. 사이트 확장을 완료한 후 데이터 수집을 다시 구성할 수 있습니다.  

### <a name="gather-data-now"></a>콘솔에서  
 초기 데이터 수집 프로세스는 사이트에 대해 실행된 후 자동으로 반복되어 마지막 데이터 수집 주기 이후에 업데이트된 개체를 확인합니다. 또한 Configuration Manager 콘솔에서 **지금 데이터 수집** 작업을 사용하면 프로세스를 즉시 시작하고 다음 주기의 시작 시간을 다시 설정할 수 있습니다.  

 원본 사이트에 대해 데이터 수집 프로세스가 성공적으로 완료되면 원본 사이트의 배포 지점을 공유할 수 있고 사이트에서 데이터를 마이그레이션하는 마이그레이션 작업을 구성할 수 있습니다. 데이터 수집은 마이그레이션을 위한 반복 프로세스로서 사용자가 원본 계층을 변경하거나 **데이터 수집 중지** 작업을 사용하여 사이트에 대한 데이터 수집 프로세스를 종료할 때까지 계속 실행됩니다.  

### <a name="stop-gathering-data"></a>및  
 Configuration Manager에서 사이트에 새로 추가되거나 변경된 개체를 더 이상 확인하지 않으려면 **데이터 수집 중지** 작업을 사용하여 원본 사이트에 대한 데이터 수집 프로세스를 종료할 수 있습니다. 또한 이 경우 Configuration Manager는 대상 계층의 클라이언트에 원본의 공유 배포 지점을 제공하지 않게 됩니다. 이 공유 배포 지점은 마이그레이션된 콘텐츠에 대한 콘텐츠 위치입니다.  

 각 원본 사이트에서 데이터 수집을 중지하려면 맨 아래 계층 원본 사이트에서 **데이터 수집 중지** 작업을 실행한 다음 각 부모 사이트에서 이 프로세스를 반복해야 합니다. 원본 계층의 최상위 사이트는 데이터 수집을 중지하는 마지막 사이트가 되어야 합니다. 부모 사이트에서 이 작업을 수행하기 전에 각 자식 사이트에서 데이터 수집을 중지해야 합니다. 일반적으로 마이그레이션 프로세스를 완료할 준비가 된 경우에만 데이터 수집을 중지합니다.  

 원본 사이트에 대해 데이터 수집을 중지한 후에 사이트의 개체 및 컬렉션에 대해 이전에 수집된 정보는 새 마이그레이션 작업을 구성할 때 계속 사용할 수 있습니다. 그러나 새 개체나 새 컬렉션은 볼 수 없으며 기존 개체에 적용된 변경 내용도 볼 수 없습니다. 원본 사이트를 다시 구성하고 데이터 수집을 다시 시작하면 이전에 마이그레이션된 개체에 대한 정보 및 상태를 볼 수 있습니다.  



<!--HONumber=Nov16_HO1-->

