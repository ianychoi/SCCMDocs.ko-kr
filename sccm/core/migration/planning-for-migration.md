---
title: "마이그레이션 계획 | System Center Configuration Manager"
description: "System Center Configuration Manager 대상 계층 구조로 데이터를 마이그레이션하기 전에 사이트 및 계층에 알아봅니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a80c7af58f88f76afd00771778411a4842a204c8


---
# <a name="planning-for-migration-to-system-center-configuration-manager"></a>System Center Configuration Manager로 마이그레이션 계획

*적용 대상: System Center Configuration Manager(현재 분기)*

System Center Configuration Manager 대상 계층 구조로 데이터를 마이그레이션하기 전에 Configuration Manager의 사이트 및 계층 구조를 알고 있어야 합니다. 사이트 및 계층에 대한 자세한 내용은 [System Center Configuration Manager의 기본 사항](../../core/understand/fundamentals.md)을 참조하세요.  

 먼저 대상 계층으로 사용할 System Center Configuration Manager 계층을 설치해야 지원되는 원본 계층에서 데이터를 마이그레이션할 수 있습니다.  

 대상 계층을 설치한 후 데이터 마이그레이션을 시작하기에 앞서 대상 계층에서 사용할 관리 기능을 구성합니다.  

 그 밖에 원본 계층과 대상 계층 간에 겹치는 부분도 계획해야 할 수 있습니다. 한 예로, 원본 계층이 대상 계층과 같은 네트워크 위치나 경계를 사용하도록 구성한 다음 대상 계층에 새 클라이언트를 설치하고 자동 사이트 할당을 사용하는 경우가 있습니다. 이 시나리오에서는 새로 설치한 Configuration Manager 클라이언트가 둘 중 한 계층에서 가입할 사이트를 선택할 수 있으므로 클라이언트가 원본 계층에 잘못 할당할 수 있습니다. 따라서 자동 사이트 할당을 사용하는 대신 해당 계층의 특정 사이트에 대상 계층의 새 클라이언트를 할당하도록 계획합니다.  

 사이트 할당에 대한 자세한 내용은 [서로 다른 버전의 System Center Configuration Manager 간 상호 운용성](../../core/plan-design/hierarchy/interoperability-between-different-versions.md) 항목의 [클라이언트 사이트 할당 고려 사항](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) 섹션을 참조하세요.  

## <a name="planning-topics"></a>계획 항목  
 다음 항목을 사용하여 지원되는 원본 계층을 System Center Configuration Manager 대상 계층으로 마이그레이션하는 방법을 계획할 수 있습니다.  

-   [System Center Configuration Manager에서 마이그레이션을 수행하기 위한 필수 조건](../../core/migration/prerequisites-for-migration.md)  

-   [System Center Configuration Manager의 마이그레이션 계획에 대한 관리자 검사 목록](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [System Center Configuration Manager로 데이터를 마이그레이션할지 여부 결정](../../core/migration/determine-whether-to-migrate-data.md)  

-   [System Center Configuration Manager에서 원본 계층 전략 계획](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [System Center Configuration Manager의 마이그레이션 계획에 대한 관리자 검사 목록](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [System Center Configuration Manager에서 클라이언트 마이그레이션 전략 계획](../../core/migration/planning-a-client-migration-strategy.md)  

-   [System Center Configuration Manager에서 콘텐츠 배포 마이그레이션 전략 계획](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Configuration Manager 개체를 System Center Configuration Manager로 마이그레이션하도록 계획](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [System Center Configuration Manager에서 마이그레이션 작업 모니터링 계획](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [System Center Configuration Manager에서 마이그레이션 완료 계획](../../core/migration/planning-to-complete-migration.md)  



<!--HONumber=Nov16_HO1-->

