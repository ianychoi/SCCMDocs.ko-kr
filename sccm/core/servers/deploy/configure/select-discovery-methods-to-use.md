---
title: "검색 방법 선택 | System Center Configuration Manager"
description: "사용할 방법 및 해당 방법을 실행할 사이트에 대한 고려 사항을 검토합니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 7fa86796a9acd5e6baedd12f005bec58181f081b

---
# <a name="select-discovery-methods-to-use-for-system-center-configuration-manager"></a>System Center Configuration Manager에 사용할 검색 방법 선택

*적용 대상: System Center Configuration Manager(현재 분기)*

System Center Configuration Manager에 검색을 성공적 및 효율적으로 사용하려면 사용할 방법과 해당 방법을 실행할 사이트를 고려해야 합니다.  

 검색에서는 대량의 네트워크 트래픽이 발생할 수 있으며 검색에서 생성된 DDR(검색 데이터 기록)의 처리 시 상당한 CPU 리소스가 사용되므로 원하는 결과를 얻는 데 필요한 검색 방법만 사용해야 합니다. 한두 가지 검색 방법을 사용하고 제어된 방식으로 추가 방법을 사용하도록 설정하여 환경의 검색 수준을 확장할 수 있습니다. 이 항목의 정보는 올바른 결정을 내리는 데 도움이 될 수 있습니다.  

 다양한 검색 방법에 대한 자세한 내용은 [System Center Configuration Manager에 대한 검색 방법 정보](../../../../core/servers/deploy/configure/about-discovery-methods.md)를 참조하세요.  

## <a name="select-methods-to-discover-different-things"></a>각 항목을 검색할 방법 선택  
 잠재적인 Configuration Manager 클라이언트 컴퓨터 또는 사용자 리소스를 검색하려면 적절한 검색 방법을 사용하도록 설정해야 합니다. 여러 가지 검색 방법을 함께 사용하여 다양한 리소스를 찾고 이러한 리소스에 대한 추가 정보를 검색할 수 있습니다. 사용하는 검색 방법에 따라 검색되는 리소스 유형과 검색 프로세스에서 사용되는 Configuration Manager 서비스와 에이전트가 결정됩니다. 또한 검색할 수 있는 리소스에 대한 정보 유형도 결정됩니다.  

 **컴퓨터 검색**   
컴퓨터를 검색하려는 경우 Active Directory 시스템 검색 또는 네트워크 검색을 사용할 수 있습니다.  

 예를 들어 클라이언트 강제 설치를 사용하기 전에 Configuration Manager 클라이언트를 설치할 수 있는 리소스를 검색하려는 경우 Active Directory 시스템 검색을 실행할 수 있습니다. 또한 네트워크 검색을 실행하고 네트워크 검색 옵션을 사용하여 리소스의 운영 체제(이후에 클라이언트 강제 설치를 사용하는 데 필요)를 검색할 수 있습니다. 그러나 Active Directory 시스템 검색을 사용하면 리소스뿐만 아니라 기본적인 정보도 검색되고 Active Directory Domain Services에서 리소스에 대한 확장 정보를 검색할 수 있습니다. 이 정보는 클라이언트 설정 또는 콘텐츠 배포 할당을 위해 사용할 복잡한 쿼리와 컬렉션을 작성하는 데 유용할 수 있습니다. 한편 네트워크 검색은 다른 검색 방법으로는 얻을 수 없는 네트워크 토폴로지 관련 정보를 제공합니다. 그러나 네트워크 검색으로는 Active Directory 환경에 대한 정보를 얻을 수 없습니다.  

 또한 하트비트 검색만 사용하여 클라이언트 강제 설치 이외의 방법으로 설치한 클라이언트를 검색할 수도 있습니다. 그러나 다른 검색 방법과 달리 하트비트 검색은 활성 Configuration Manager 클라이언트가 없는 컴퓨터를 검색할 수 없으며 제한된 정보를 반환합니다. 하트비트 검색은 기존 데이터베이스 레코드의 기반이 되는 것이 아니라 이러한 레코드를 유지하기 위한 목적으로 사용됩니다. 하트비트 검색을 통해 제출된 정보는 복잡한 쿼리 또는 컬렉션을 작성하는 데 충분하지 않을 수 있습니다.  

 Active Directory 그룹 검색을 사용하여 지정된 그룹의 멤버 자격을 검색하는 경우 제한된 시스템 또는 컴퓨터 정보를 검색할 수 있습니다. 이는 컴퓨터의 전체 검색을 대체하지 않지만 기본적인 정보를 제공할 수 있습니다. 이러한 기본적인 정보는 클라이언트 강제 설치를 위해 부족합니다.  

 **사용자 검색**   
사용자에 대한 정보를 검색하려는 경우 Active Directory 사용자 검색을 사용할 수 있습니다. Active Directory 시스템 검색과 마찬가지로, 이 방법은 Active Directory에서 사용자를 검색하며 확장된 Active Directory 정보와 더불어 기본적인 정보를 제공합니다. 이 정보를 사용하여 컴퓨터에 대해 하듯이 복잡한 쿼리 및 컬렉션을 작성할 수 있습니다.  

 **그룹 정보 검색**   
그룹과 그룹 멤버 자격에 대한 정보를 검색하려는 경우 Active Directory 그룹 검색을 사용합니다. 이 검색 방법을 통해 보안 그룹에 대한 리소스 레코드가 만들어집니다.  

 이 방법을 사용하여 특정 Active Directory 그룹을 검색함으로써 그룹의 구성원과 그룹에 중첩된 그룹을 확인할 수 있습니다. 또한 이 방법을 사용하여 그룹의 Active Directory 위치를 검색하고 Active Directory Domain Services에서 해당 위치의 각 자식 컨테이너를 회귀적으로 검색할 수 있습니다.  

 또한 이 검색 방법으로 배포 그룹의 멤버 자격을 검색할 수 있습니다. 이 방법을 사용하면 사용자와 컴퓨터 모두의 그룹 관계를 확인할 수 있습니다.  

 그룹을 검색할 때 구성원에 대한 제한된 정보를 검색할 수도 있습니다. 이는 Active Directory 시스템 또는 사용자 검색을 대체하지 않으며 일반적으로 복잡한 쿼리 및 컬렉션을 작성하거나 클라이언트 강제 설치의 기반으로 활용하기에 부족합니다.  

 **인프라 검색**   
네트워크 인프라 검색, Active Directory 포리스트 검색 및 네트워크 검색에 사용할 수 있는 두 가지 방법이 있습니다.  

 Active Directory 포리스트 검색을 사용하여 Active Directory 포리스트를 검색함으로써 서브넷에 대한 정보와 Active Directory 사이트 구성을 확인할 수 있습니다. 그런 다음 이러한 구성을 경계 위치로 Configuration Manager에 자동으로 입력할 수 있습니다.  

 네트워크 토폴로지를 검색하려는 경우 네트워크 검색을 사용합니다. 다른 검색 방법은 Active Directory Domain Services와 관련된 정보를 반환하고 클라이언트의 현재 네트워크 위치를 식별할 수 있는 반면, 네트워크의 서브넷과 라우터 토폴로지를 기반으로 인프라 정보를 제공하지는 않습니다.  

##  <a name="a-namebkmkshareda-discovery-data-is-shared-between-sites"></a><a name="bkmk_shared"></a> 검색 데이터가 사이트 간에 공유됨  
 Configuration Manager가 검색 데이터를 데이터베이스에 추가하면 이 데이터가 금방 계층 구조의 모든 사이트에서 공유됩니다. 일반적으로 계층 구조의 여러 사이트에서 같은 정보를 검색하는 것에는 아무 유익이 없으므로 사용하는 각 검색 방법의 여러 인스턴스를 여러 사이트에서 실행하기보다는 단일 인스턴스를 하나의 사이트에서 실행하도록 구성하는 것이 좋습니다.  

 그러나 일부 환경에서는 동일한 검색 방법이 여러 사이트에서 별도의 구성과 일정으로 실행되도록 할당하는 것이 유용할 수 있습니다. 이는 검색 방법을 실행하는 구성이 단일 사이트에 고유하기 때문입니다. 그런 다음 한 사이트에서 검색을 실행한 후 그 결과를 다른 사이트와 공유하거나, 각각 로컬 리소스에 대해 검색을 실행하고 WAN을 통해 다른 위치에서 정보를 검색하지 않는 동일한 방법을 두 사이트에서 사용할 수 있습니다.  예를 들어 각 사이트에서 WAN을 통해 모든 네트워크 위치에 대한 검색을 실행하는 대신 로컬 네트워크를 검색하도록 지정하는 네트워크 검색을 사용할 때 유용한 경우가 많습니다. 동일한 검색 방법의 여러 인스턴스가 각기 다른 사이트에서 실행되도록 구성하는 경우 각 사이트의 구성을 신중하게 계획하여 둘 이상의 사이트가 네트워크 또는 Active Directory에서 동일한 리소스를 검색하지 않도록 합니다. 여러 사이트에서 같은 위치와 리소스를 검색하면 네트워크 대역폭이 추가로 사용될 뿐만 아니라 아무 가치가 없는데도 사이트 서버에서 처리해야 하는 중복된 리소스 DDR(검색 데이터 기록)이 만들어집니다.  

 다음 표에는 각 검색 방법을 구성할 수 있는 사이트가 정리되어 있습니다.  

|검색 방법|지원되는 위치|  
|----------------------|-------------------------|  
|Active Directory 포리스트 검색|중앙 관리 사이트<br /><br /> 기본 사이트|  
|Active Directory 그룹 검색|기본 사이트|  
|Active Directory 시스템 검색|기본 사이트|  
|Active Directory 사용자 검색|기본 사이트|  
|하트비트 검색<sup>1</sup>|기본 사이트|  
|네트워크 검색|기본 사이트<br /><br /> 보조 사이트|  

 <sup>1</sup> 보조 사이트에서는 하트비트 검색을 구성할 수 없지만 클라이언트에서 하트비트 DDR을 받을 수 있습니다.  

 보조 사이트에서 네트워크 검색을 실행하거나 하트비트 검색 DDR을 받으면 파일 기반 복제를 통해 부모 기본 사이트로 DDR을 전송합니다. 그 이유는 기본 사이트와 중앙 관리 사이트만 DDR을 처리할 수 있기 때문입니다. DDR이 처리되는 방법에 대한 자세한 내용은 [검색 데이터 기록 정보](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs)를 참조하세요.  

## <a name="considerations-for-different-discovery-methods"></a>다양한 검색 방법에 대한 고려 사항  
 각 사이트 서버와 네트워크 환경은 서로 다르기 때문에 초기 검색 구성을 제한하고 각 사이트 서버를 긴밀하게 모니터링하여 생성된 검색 데이터를 처리할 수 있는지 확인합니다.  

-   시스템, 사용자 또는 그룹에 대한 Active Directory 검색 방법을 사용하는 경우:  

    -   도메인 컨트롤러에 대한 빠른 네트워크 연결을 갖는 사이트에서 검색을 실행합니다.  

    -   검색이 최신 정보에 액세스할 수 있도록 Active Directory 복제 토폴로지를 고려합니다.  

    -   검색 구성의 범위를 고려하고 검색해야 할 Active Directory 위치와 그룹으로 검색을 제한합니다.  

-   네트워크 검색을 사용하는 경우:  

    -   제한된 초기 구성을 사용하여 네트워크 토폴로지를 파악합니다.  

    -   네트워크 토폴로지를 파악한 후에는 보다 완전하게 검색할 네트워크 영역에 중요한 특정 사이트에서 네트워크 검색이 실행되도록 구성합니다.  

-   하트비트 검색은 특정 사이트에서 실행되지 않기 때문에 전반적인 계획에서 검색을 실행할 위치를 고려하지 않아도 됩니다.  

-   각 사이트 서버와 네트워크 환경은 서로 다르기 때문에 초기 검색 구성을 제한하고 각 사이트 서버를 긴밀하게 모니터링하여 생성된 검색 데이터를 처리할 수 있는지 확인합니다.  

##  <a name="a-namebkmkbesta-best-practices-for-discovery"></a><a name="bkmk_best"></a> 검색 모범 사례  
 **Active Directory 그룹 검색을 실행하기 전에 Active Directory 시스템 검색과 Active Directory 그룹 검색 실행:**  

 Active Directory 그룹 검색에서는 이전에 검색되지 않은 사용자 또는 컴퓨터가 그룹의 구성원으로 식별될 경우 해당 사용자 또는 컴퓨터에 대한 기본적인 정보를 검색합니다. Active Directory 그룹 검색은 이 유형의 검색을 위해 최적화되어 있지 않으므로 이 프로세스로 인해 Active Directory 그룹 검색의 실행 속도가 느려질 수 있습니다. 또한 Active Directory 그룹 검색은 검색되는 사용자와 컴퓨터에 대한 기본적인 정보만 식별하고 사용자 또는 컴퓨터에 대한 완전한 검색 레코드를 만들지 않습니다. Active Directory 시스템 검색과 Active Directory 사용자 검색을 실행하면 각 개체 유형에 대한 추가 Active Directory 특성을 사용할 수 있으므로 Active Directory 그룹 검색이 더 효율적으로 실행됩니다.  

 **Active Directory 그룹 검색을 실행하는 경우 Configuration Manager에서 사용할 그룹만 지정:**  

 Active Directory 그룹 검색의 리소스 사용을 제어하기 위해 Configuration Manager에서 사용하는 그룹만 지정합니다. 이는 Active Directory 그룹 검색이 검색되는 각 그룹에서 사용자, 컴퓨터 및 중첩된 그룹을 회귀적으로 검색하기 때문입니다. 중첩된 각 그룹의 검색으로 Active Directory 그룹 검색의 범위가 확장되어 성능이 저하될 수 있습니다. 또한 Active Directory 그룹 검색에 대한 델타 검색을 구성하는 경우 검색 방법이 각 그룹에서 변경 사항을 모니터링합니다. 이 검색 방법으로 불필요한 그룹을 검색해야 하므로 성능이 더욱 떨어집니다.  

 **전체 검색 사이의 간격을 더 길게 늘리고, 델타 검색을 더 자주 실행하도록 검색 방법 구성:**  

 델타 검색은 전체 검색 주기보다 더 적은 리소스를 사용하고 Active Directory에서 새로운 리소스 또는 수정된 리소스를 파악할 수 있으므로 델타 검색을 사용하면 전체 검색 주기의 빈도를 줄여 일주일에 한 번 이하만 실행할 수 있습니다. Active Directory 시스템 검색, Active Directory 사용자 검색 및 Active Directory 그룹 검색은 Active Directory 개체의 거의 모든 변경 사항을 파악하고 리소스에 대한 정확한 검색 데이터를 유지할 수 있습니다.  

 **네트워크 위치가 Active Directory 도메인 컨트롤러와 가장 가까운 기본 사이트에서 Active Directory 검색 방법 실행:**  

 Active Directory 검색의 성능을 높이려면 도메인 컨트롤러에 대한 고속 네트워크 연결을 갖는 기본 사이트에서 검색을 실행하는 것이 좋습니다. 여러 사이트에서 Active Directory 검색 방법을 실행하는 경우 중복을 피하여 각 검색 방법을 구성하는 것이 좋습니다. 이전 버전의 Configuration Manager와 달리 검색 데이터가 사이트 전체에서 공유됩니다. 따라서 같은 정보를 여러 사이트에서 검색할 필요가 없습니다. 자세한 내용은 [검색 데이터가 사이트 간에 공유됨](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared)을 참조하세요.  

 **검색 데이터로부터 경계를 자동으로 만들려는 경우 한 사이트에서만 Active Directory 포리스트 검색 실행:**  

 계층에 있는 둘 이상의 사이트에서 Active Directory 포리스트 검색을 실행하는 경우 한 사이트에서 자동으로 경계를 만드는 옵션만 사용하도록 설정하는 것이 좋습니다. 이는 Active Directory 포리스트 검색이 각 사이트에서 실행되어 경계를 만들므로 Configuration Manager에서 이러한 경계를 하나의 경계 개체로 병합할 수 없기 때문입니다. 여러 사이트에서 자동으로 경계를 만들도록 Active Directory 포리스트 검색을 구성하는 경우 Configuration Manager 콘솔에서 중복된 경계 개체가 표시될 수 있습니다.  



<!--HONumber=Nov16_HO1-->

