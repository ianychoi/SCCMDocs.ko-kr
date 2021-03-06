---
title: "클라이언트 보안 및 개인 정보"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager에서 클라이언트에 대한 보안 및 개인 정보에 대해 알아봅니다."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
caps.latest.revision: "10"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: b28a461894bcd1cffd3c98bfce9fcfe22cc7a8f0
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2017
---
# <a name="security-and-privacy-for-clients-in-system-center-configuration-manager"></a>System Center Configuration Manager에서 클라이언트에 대한 보안 및 개인 정보

*적용 대상: System Center Configuration Manager(현재 분기)*

이 문서에는 System Center Configuration Manager에서 클라이언트에 대한 보안 및 개인 정보와 Exchange Server 커넥터에서 관리하는 모바일 장치에 대한 보안 및 개인 정보가 포함되어 있습니다.  

##  <a name="BKMK_Security_Cliients"></a> 클라이언트에 대한 보안 모범 사례  
 Configuration Manager에서 Configuration Manager 클라이언트를 실행하는 장치의 데이터를 허용하면 클라이언트가 사이트를 공격할 위험이 있습니다. 예를 들어 이러한 클라이언트는 잘못된 형식의 인벤토리를 보내거나 사이트 시스템의 오버로드를 시도할 수 있습니다. Configuration Manager 클라이언트는 신뢰할 수 있는 장치에만 배포하세요. 또한 다음 보안 모범 사례를 활용하면 허위 장치 또는 손상된 장치로부터 사이트를 보호하는 데 도움이 됩니다.  

 **IIS를 실행하는 사이트 시스템에 대한 클라이언트 통신에 PKI(공개 키 인프라) 인증서 사용:**  

-   사이트 속성으로 **사이트 시스템 설정** 을 **HTTPS만 사용**으로 구성합니다.  

-   **/UsePKICert** CCMSetup 속성을 사용하여 클라이언트를 설치합니다.  

-   CRL(인증서 해지 목록)을 사용하고 클라이언트 및 통신 서버에서 항상 액세스할 수 있도록 합니다.  

 이 인증서는 모바일 장치 클라이언트와 인터넷상의 클라이언트 컴퓨터 연결에 필요하며 배포 지점만 제외하고 인트라넷상의 모든 클라이언트 연결에 사용하는 것이 좋습니다.  

 PKI 인증서 요구 사항 및 PKI 인증서를 사용하여 Configuration Manager를 보호하는 방법에 대한 자세한 내용은 [System Center Configuration Manager를 위한 PKI 인증서 요구 사항](../../../../core/plan-design/network/pki-certificate-requirements.md)을 참조하세요.  

 **트러스트된 도메인의 클라이언트 컴퓨터 자동으로 승인, 다른 컴퓨터 수동으로 확인 및 승인**  

 계층에 대한 승인을 수동 방식이 되도록 구성할 수 있고 트러스트된 도메인의 컴퓨터에 대해 자동 방식으로, 또는 모든 컴퓨터에 대해 자동 방식으로 구성할 수 있습니다. 가장 안전한 승인 방법은 트러스트된 도메인의 구성원인 클라이언트는 자동으로 승인하고 나머지 모든 컴퓨터는 수동으로 확인 및 승인하는 것입니다. 신뢰할 수 없는 컴퓨터가 네트워크에 액세스하지 못하도록 방지하는 다른 액세스 제어 방법이 없는 경우 모든 클라이언트를 자동으로 승인하는 방식은 사용하지 않는 것이 좋습니다.  

 PKI 인증을 사용할 수 없을 때 승인을 통해 Configuration Manager에서 관리되는 것으로 신뢰하는 컴퓨터를 식별합니다.  

 컴퓨터를 수동으로 승인하는 방법에 대한 자세한 내용은 [장치 노드에서 클라이언트 관리](../../../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode)를 참조하세요.  

 **클라이언트가 Configuration Manager 계층 구조에 액세스하지 못하도록 막는 데 차단 방식에 의존하지 않음**  

 차단된 클라이언트는 Configuration Manager 인프라에서 거부되므로 사이트 시스템과 통신하여 정책을 다운로드하거나, 인벤토리 데이터를 업로드하거나, 상태 또는 상태 메시지를 보낼 수 없습니다. 그러나 사이트 시스템에서 HTTP 클라이언트 연결을 허용할 경우 Configuration Manager 계층 구조를 신뢰할 수 없는 컴퓨터로부터 보호하기 위해 차단에 의존하면 안 됩니다. 이 시나리오에서 차단된 클라이언트는 새로운 자체 서명된 인증서 및 하드웨어 ID를 사용하여 사이트에 다시 가입할 수 있습니다. 차단은 클라이언트에 운영 체제를 배포할 때 모든 사이트 시스템에서 HTTPS 클라이언트 연결을 허용할 경우 손실되거나 손상된 부팅 미디어를 차단하는 데 사용하도록 만들어졌습니다. PKI를 사용하고 PKI에서 CRL을 지원하는 경우 손상되었을 가능성이 있는 인증서에 대비한 1차 방어선에는 항상 인증서 해지를 배치하는 것이 좋습니다. Configuration Manager에서 클라이언트를 차단하면 계층 구조를 보호하기 위한 이차 방어 수단이 됩니다.  

 자세한 내용은 [Determine whether to block clients in System Center Configuration Manager](../../../../core/clients/deploy/plan/determine-whether-to-block-clients.md)(System Center Configuration Manager에서 클라이언트를 차단할지 여부 결정)를 참조하세요.  

 **특정 환경에 적합한 가장 안전한 클라이언트 설치 방법 사용:**  

-   도메인 컴퓨터의 경우 그룹 정책 클라이언트 설치 및 소프트웨어 업데이트 기반 클라이언트 설치 방법은 클라이언트 강제 설치보다 더 안전합니다.  

-   액세스 제어 및 변경 제어를 적용할 경우 이미징 및 수동 설치는 매우 안전한 방법이 될 수 있습니다.  

 모든 클라이언트 설치 방법 중 클라이언트 강제 설치는 로컬 관리 권한, Admin$ 공유 및 여러 방화벽 예외 등과 같은 자체의 여러 종속성으로 인해 보안 수준이 가장 낮습니다. 종속성이 있으면 공격 노출 영역은 그만큼 늘어납니다.  

 다른 클라이언트 설치 방법에 대한 자세한 내용은 [System Center Configuration Manager의 클라이언트 설치 방법](../../../../core/clients/deploy/plan/client-installation-methods.md)을 참조하세요.  

 또한 가능하면 Configuration Manager에서 보안 권한이 가장 적게 필요한 클라이언트 설치 방법을 선택하고 클라이언트 배포 이외의 용도로 사용될 수 있는 권한이 포함된 보안 역할을 할당받는 관리자의 수를 제한합니다. 예를 들어 자동 클라이언트 업그레이드에는 **전체 관리자** 보안 역할이 필요하며 이 보안 역할은 관리자에게 모든 보안 권한을 부여합니다.  

 각 클라이언트 설치 방법에 필요한 종속성 및 보안 권한에 대한 자세한 내용은 [컴퓨터 클라이언트에 대한 필수 조건](../../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers)의 "설치 방법 종속성"을 참조하세요.  

 **클라이언트 강제 설치 사용 시 클라이언트 강제 설치 계정을 보호하기 위한 추가 단계 수행**  

 이 계정은 Configuration Manager 클라이언트 소프트웨어를 설치할 각 컴퓨터의 로컬**Administrators** 그룹 구성원이어야 하지만, **Domain Admins** 그룹에는 클라이언트 강제 설치 계정을 추가하면 안 됩니다. 대신 글로벌 그룹을 만든 후 이 글로벌 그룹을 클라이언트 컴퓨터의 로컬 **관리자** 그룹에 추가합니다. 또한 클라이언트 강제 설치 계정을 로컬 **관리자** 그룹에 추가하는 제한 그룹 설정을 추가하기 위해 그룹 정책 개체를 만들 수도 있습니다.  

 추가 보안을 제공하기 위해 클라이언트 강제 설치 계정을 여러 개 만들고 각 계정에 제한된 수의 컴퓨터에 대한 관리 액세스 권한을 부여할 수 있습니다. 이 경우 한 계정의 보안이 손상되면 해당 계정이 액세스 권한을 갖는 클라이언트 컴퓨터의 보안만 손상됩니다.  

 **클라이언트 컴퓨터 이미징 전 인증서 제거**  

 이미징 기술을 사용하여 클라이언트를 배포하려는 경우 이미지를 캡처하기 전에 항상 PKI 인증서와 같이 클라이언트 인증 및 자체 서명된 인증서가 포함된 인증서를 제거하세요. 이러한 인증서를 제거하지 않으면 클라이언트는 서로를 가장할 수 있으므로 각 클라이언트의 데이터를 확인할 수 없게 됩니다.  

 Sysprep을 사용하여 컴퓨터 이미징을 준비하는 방법에 대한 자세한 내용은 해당 Windows 배포 설명서를 참조하세요.  

 **Configuration Manager 컴퓨터 클라이언트가 권한 있는 인증서 사본을 가져오는지 확인:**  

-   Configuration Manager의 신뢰할 수 있는 루트 키  

     Active Directory 스키마를 Configuration Manager에 대해 확장하지 않았고 클라이언트에서 관리 지점과 통신할 때 PKI 인증서를 사용하지 않는 경우 해당 클라이언트는 Configuration Manager 신뢰할 수 있는 루트 키에 의존하여 유효한 관리 지점을 인증합니다. 이 시나리오에서 클라이언트는 신뢰할 수 있는 루트 키를 사용하지 않고서는 해당 관리 지점이 계층에 대해 신뢰할 수 있는 관리 지점이라는 사실을 확인할 수 없습니다. 신뢰할 수 있는 루트 키가 없으면 노련한 공격자가 클라이언트를 허위 관리 지점으로 유도할 수 있습니다.  

     클라이언트가 글로벌 카탈로그를 통하거나 PKI 인증서를 사용하여 Configuration Manager 신뢰할 수 있는 루트 키를 다운로드할 수 없는 경우 클라이언트에 신뢰할 수 있는 루트 키를 사전 프로비전하여 허위 관리 지점으로 유도되지 않도록 방지하세요. 자세한 내용은 [Planning for the Trusted Root Key](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)을 참조하십시오.  

-   사이트 서버 서명 인증서  

     클라이언트는 관리 지점에서 다운로드하는 클라이언트 정책이 사이트 서버에서 서명되었음을 사이트 서버 서명 인증서를 사용하여 확인합니다. 이 인증서는 사이트 서버에서 자체 서명되었으며 Active Directory Domain Services에 게시됩니다.  

     클라이언트는 글로벌 카탈로그에서 사이트 서버 서명 인증서를 다운로드할 수 없으면 기본적으로 관리 지점에서 다운로드합니다. 관리 지점이 인터넷과 같은 신뢰할 수 없는 네트워크에 노출된 경우 사이트 서버 서명 인증서를 클라이언트에 수동으로 설치하여 해당 클라이언트가 손상된 관리 지점에서 무단 변경된 클라이언트 정책을 실행할 수 없도록 방지해야 합니다.  

     수동으로 사이트 서버 서명 인증서를 설치하려면 CCMSetup client.msi 속성 **SMSSIGNCERT**를 사용합니다. 자세한 내용은 [System Center Configuration Manager의 클라이언트 설치 속성 정보](../../../../core/clients/deploy/about-client-installation-properties.md)를 참조하세요.  

 **클라이언트가 연결한 첫 번째 관리 지점에서 신뢰할 수 있는 루트 키를 다운로드할 경우 자동 사이트 할당 사용 안 함**  

 이 보안 모범 사례는 앞의 항목과 연결됩니다. 새 클라이언트가 신뢰할 수 있는 루트 키를 허위 관리 지점에서 다운로드하지 못하도록 방지하려면 다음 시나리오에서만 자동 사이트 할당을 사용합니다.  

-   클라이언트가 Active Directory Domain Services에 게시되는 Configuration Manager 사이트 정보에 액세스할 수 있습니다.  

-   클라이언트에 신뢰할 수 있는 루트 키를 사전 프로비전합니다.  

-   엔터프라이즈 인증 기관의 PKI 인증서를 사용하여 클라이언트 및 관리 지점 간의 트러스트를 설정합니다.  

 신뢰할 수 있는 루트 키에 대한 자세한 내용은 [Planning for the Trusted Root Key](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)항목을 참조하세요.  

 **CCMSetup Client.msi 옵션 SMSDIRECTORYLOOKUP=NoWINS를 사용하여 클라이언트 컴퓨터 설치**  

 클라이언트가 사이트 및 관리 지점을 찾을 수 있는 가장 안전한 서비스 위치 검색 방법은 Active Directory Domain Services를 사용하는 것입니다. 예를 들어 Active Directory 스키마를 Configuration Manager에 대해 확장할 수 없거나 클라이언트가 트러스트되지 않은 포리스트 또는 작업 그룹에 있으므로 이 서비스를 사용할 수 없는 경우에는 대체 서비스 위치 검색 방법으로 DNS 게시를 사용하면 됩니다. 두 가지 방법이 모두 실패하면 클라이언트는 관리 지점이 HTTPS 클라이언트 연결에 대해 구성되지 않은 경우에 WINS 사용으로 대체할 수 있습니다.  

 WINS에 게시하는 방법은 다른 게시 방법보다 보안 수준이 낮기 때문에 SMSDIRECTORYLOOKUP=NoWINS를 지정하여 클라이언트 컴퓨터가 WINS 사용으로 대체하지 않도록 구성하세요. 서비스 위치 검색에 WINS를 사용해야 할 경우 SMSDIRECTORYLOOKUP=WINSSECURE(기본 설정)를 사용합니다. 이 설정은 Configuration Manager 신뢰할 수 있는 루트 키를 사용하여 관리 지점의 자체 서명된 인증서의 유효성을 검사합니다.  

> [!NOTE]  
>  클라이언트는 SMSDIRECTORYLOOKUP=WINSSECURE에 대해 구성되고 WINS에서 관리 지점을 검색할 경우 WMI에 있는 Configuration Manager 신뢰할 수 있는 루트 키의 해당 복사본을 확인합니다. 관리 지점 인증서의 서명이 클라이언트의 신뢰할 수 있는 루트 키 복사본과 일치하면 해당 인증서는 유효성 검사가 완료되고 클라이언트는 WINS를 사용하여 검색한 관리 지점과 통신합니다. 관리 지점 인증서의 서명이 클라이언트의 신뢰할 수 있는 루트 키 복사본과 일치하지 않으면 해당 인증서는 유효하지 않으므로 클라이언트는 WINS를 사용하여 검색한 관리 지점과 통신하지 않습니다.  

 **유지 관리 기간을 중요 소프트웨어 업데이트를 충분히 배포할 수 있을 만큼 설정**  

 Configuration Manager가 장치에 소프트웨어를 설치할 수 있는 횟수를 제한하도록 장치 컬렉션에 대한 유지 관리 기간을 구성할 수 있습니다. 유지 관리 기간을 너무 짧게 구성하면 클라이언트는 중요 소프트웨어 업데이트를 설치하지 못할 수도 있으며, 이 경우 클라이언트는 해당 소프트웨어 업데이트로 방지할 수 있었던 공격에 취약해집니다.  

 **쓰기 필터가 있는 Windows Embedded 장치에 대해, Configuration Manager에서 소프트웨어 설치 및 변경을 유지하기 위해 쓰기 필터를 해제할 경우 추가 보안 예방 조치를 실행하여 공격 노출 영역 최소화**  

 Windows Embedded 장치에 쓰기 필터가 설정되면 소프트웨어 설치 또는 변경 내용은 오버레이에만 적용되고 장치가 다시 시작된 후에는 유지되지 않습니다. 소프트웨어 설치 및 변경을 유지하기 위해 Configuration Manager를 사용하여 쓰기 필터를 일시적으로 해제하면 이 기간 동안 임베디드 장치의 공유 폴더를 포함한 모든 볼륨의 내용은 쉽게 변경이 가능합니다.  

 Configuration Manager는 이 기간 동안 로컬 관리자만 로그온할 수 있도록 컴퓨터를 잠그지만, 가능하면 추가 보안 예방 조치를 실행하여 컴퓨터를 더 효과적으로 보호하세요. 예를 들어 방화벽에 추가 제한을 구성하고 네트워크에서 장치의 연결을 끊을 수 있습니다.  

 유지 관리 기간을 활용해 변경 내용을 유지할 경우, 쓰기 필터의 해제 시간을 최소화하는 동시에 소프트웨어 설치 및 장치 재시작을 충분히 완료할 수 있도록 유지 관리 기간을 적절히 계획하세요.  

 **소프트웨어 업데이트 기반 클라이언트 설치를 사용하고 사이트에 클라이언트의 최신 버전을 설치할 경우 클라이언트가 최신 버전을 받을 수 있도록 소프트웨어 업데이트 지점에 게시된 소프트웨어 업데이트를 업데이트**  

 사이트를 업그레이드하는 경우처럼 사이트에 클라이언트의 최신 버전을 설치할 경우 소프트웨어 업데이트 지점에 게시된 클라이언트 배포용 소프트웨어 업데이트는 자동으로 업데이트되지 않습니다. Configuration Manager 클라이언트를 소프트웨어 업데이트 지점에 다시 게시하고 **예**를 클릭하여 버전 번호를 업데이트해야 합니다.  

 자세한 내용은 [소프트웨어 업데이트 기반 설치를 사용하여 Configuration Manager 클라이언트를 설치하는 방법](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP)의 "소프트웨어 업데이트 지점에 Configuration Manager 클라이언트를 게시하려면" 절차를 참조하세요.  

 **제한된 물리적 액세스 권한을 갖는 신뢰하는 컴퓨터에 대해서만 컴퓨터 에이전트 클라이언트 장치 설정 다시 시작 시 BitLocker PIN 항목 일시 중단을 항상으로 구성**  

 이 클라이언트 설정을 **항상**으로 설정하면 Configuration Manager는 소프트웨어 설치를 완료하고 이에 따라 중요 소프트웨어 업데이트가 설치되고 서비스가 다시 시작될 수 있습니다. 그러나 공격자는 다시 시작 프로세스를 가로채어 컴퓨터를 통제할 수도 있습니다. 이 설정은 컴퓨터를 신뢰하고 컴퓨터에 대한 물리적 액세스가 제한된 경우에만 사용하세요. 예를 들어 이 설정은 데이터 센터 내 서버에 적합할 수 있습니다.  

 **컴퓨터 에이전트 클라이언트 장치 설정 PowerShell 실행 정책을 바이패스로 구성 안 함**  

 이 클라이언트 설정으로 Configuration Manager 클라이언트는 서명되지 않은 PowerShell 스크립트를 실행할 수 있으며 이 경우 클라이언트 컴퓨터에서 맬웨어가 실행될 수 있습니다. 이 옵션을 선택해야 할 경우 사용자 지정 클라이언트 설정을 사용하고 이 설정을 서명되지 않은 PowerShell 스크립트를 실행해야 하는 클라이언트 컴퓨터에만 할당하세요.  

##  <a name="bkmk_mobile"></a> 모바일 장치에 대한 보안 모범 사례  
 **Configuration Manager에서 등록하고 인터넷에서 지원할 모바일 장치의 경우: 경계 네트워크에 등록 프록시 지점 설치 및 인트라넷에 등록 지점 설치**  

 이 역할 구분을 통해 등록 지점을 공격으로부터 보호할 수 있습니다. 등록 지점이 손상되면 공격자는 인증서를 가져와 인증에 사용하고 모바일 장치를 등록한 사용자의 자격 증명을 도용할 수 있습니다.  

 **모바일 장치의 경우: 암호 설정을 구성하여 무단 액세스로부터 모바일 장치 보호**  

 Configuration Manager에서 등록된 모바일 장치의 경우: 모바일 장치 구성 항목을 사용하여 암호 복잡도를 PIN으로 구성하고 최소 암호 길이에 대한 기본 길이 이상으로 설정합니다.  

 Configuration Manager 클라이언트가 설치되지 않았지만 Exchange Server 커넥터에서 관리되는 모바일 장치의 경우: Exchange Server 커넥터에 대한 **암호 설정**에서 암호 복잡도를 PIN으로 구성하고 최소 암호 길이에 대한 최소 기본 길이를 지정합니다.  

 **모바일 장치의 경우: 신뢰하는 기업에서 서명된 경우에만 응용 프로그램의 실행을 허용하여 인벤토리 정보 및 상태 정보의 무단 변경을 방지하고 서명되지 않은 파일의 설치를 허용하지 않음**  

 Configuration Manager에서 등록된 다른 모바일 장치의 경우: 모바일 장치 구성 항목을 사용하여 보안 설정 **서명되지 않은 응용 프로그램**을 **허용 안 함**으로 구성하고 **서명되지 않은 파일 설치**를 신뢰할 수 있는 원본으로 구성합니다.  

 Configuration Manager 클라이언트가 설치되지 않았지만 Exchange Server 커넥터에서 관리되는 모바일 장치의 경우: Exchange Server 커넥터에 대한 **응용 프로그램 설정**에서 **서명되지 않은 파일 설치** 및 **서명되지 않은 응용 프로그램**을 **허용 안 함**으로 구성합니다.  

 **모바일 장치의 경우: 사용되지 않는 모바일 장치를 잠그는 방식으로 권한 상승 공격 방지**  

 Configuration Manager에서 등록된 다른 모바일 장치의 경우: 모바일 장치 구성 항목을 사용하여 암호 설정 **다음 유휴 시간 후 모바일 장치 잠그기(분)**를 구성합니다.  

 Configuration Manager 클라이언트가 설치되지 않았지만 Exchange Server 커넥터에서 관리되는 모바일 장치의 경우: Exchange Server 커넥터에 대한 **암호 설정**에서 **다음 유휴 시간 후 모바일 장치 잠그기(분)**를 구성합니다.  

 **모바일 장치의 경우: 모바일 장치를 등록할 수 있는 사용자를 제한하여 권한 상승 방지**  

 기본 클라이언트 설정 대신 사용자 지정 클라이언트 설정을 사용하여 권한 있는 사용자만 모바일 장치를 등록할 수 있도록 합니다.  

 **모바일 장치의 경우: 다음 시나리오에서 Configuration Manager 또는 Microsoft Intune에서 등록된 모바일 장치를 보유한 사용자에게 응용 프로그램 배포 안 함:**  

-   모바일 장치를 둘 이상의 사용자가 사용합니다.  

-   장치가 사용자 대신 관리자에 의해 등록됩니다.  

-   사용 중지하고 다시 등록하지 않은 장치가 다른 사용자에게 양도됩니다.  

 등록 중 등록을 수행하는 사용자를 모바일 장치에 매핑하는 사용자 장치 선호도 관계가 만들어집니다. 다른 사용자가 모바일 장치를 사용하면 이 사용자는 원래 사용자에게 배포되었던 응용 프로그램을 실행할 수 있으며 이 경우 권한 상승이 발생할 수 있습니다. 마찬가지로 관리자가 사용자용 모바일 장치를 등록할 경우 해당 사용자에게 배포된 응용 프로그램이 모바일 장치에 설치되지 않고 대신 관리자에게 배포된 응용 프로그램이 설치될 수 있습니다.  

 Windows 컴퓨터에 대한 사용자 장치 선호도와 달리 Microsoft Intune에서 등록된 모바일 장치에 대한 사용자 장치 선호도 정보는 수동으로 정의할 수 없습니다.  

 Intune에서 등록된 모바일 장치의 소유권을 양도할 경우 Intune에서 해당 모바일 장치를 사용 중지하여 사용자 장치 선호도를 제거한 다음 현재 사용자에게 장치를 다시 등록하도록 요청해야 합니다.  

 **모바일 장치의 경우: 사용자가 자신의 모바일 장치를 Microsoft Intune에 등록해야 함**  

 등록 중 등록을 수행하는 사용자를 모바일 장치에 매핑하는 사용자 장치 선호도 관계가 만들어지므로, 관리자가 사용자용 모바일 장치를 등록할 경우 해당 사용자에게 배포된 응용 프로그램이 모바일 장치에 설치되지 않고 대신 관리자에게 배포된 응용 프로그램이 설치될 수 있습니다.  

 **Exchange Server 커넥터의 경우: Configuration Manager 사이트 서버와 Exchange Server 컴퓨터 간의 연결을 보호해야 함**  

 Exchange Server가 온-프레미스인 경우 IPsec을 사용합니다. 호스트되는 Exchange는 SSL을 사용하여 자동으로 연결을 보호합니다.  

 **Exchange Server 커넥터의 경우: 커넥터에 최소 권한의 원칙 사용**  

 Exchange Server 커넥터에 필요한 최소 cmdlet의 목록은 [System Center Configuration Manager와 Exchange를 사용하여 모바일 장치 관리](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)를 참조하세요.  

##  <a name="bkmk_macs"></a> Mac에 대한 보안 모범 사례  
 **Mac 컴퓨터의 경우: 보안 위치의 클라이언트 원본 파일에 저장 및 액세스**  

 Configuration Manager에서는 Mac 컴퓨터에 클라이언트를 설치하거나 등록하기 전에 이러한 클라이언트 원본 파일이 변조되었는지 확인하지 않습니다. 신뢰할 수 있는 원본에서 이러한 파일을 다운로드한 후 안전하게 저장하고 액세스하세요.  

 **Mac 컴퓨터의 경우: Configuration Manager와 별개로, 사용자에게 등록된 인증서의 유효 기간을 모니터링 및 추적**  

 무중단 업무를 보장하기 위해 Mac 컴퓨터에 대해 사용하는 인증서의 유효 기간을 모니터링 및 추적합니다. Configuration Manager는 이 인증서의 자동 갱신을 지원하지 않으며 대신 인증서의 만료를 알리는 경고를 보낼 수 있습니다. 일반적인 유효 기간은 1년입니다.  

 인증서를 갱신하는 방법에 대한 자세한 내용은  [Renewing the Mac Client Certificate Manually](../../../../core/clients/deploy/deploy-clients-to-macs.md#renewing-the-mac-client-certificate)항목을 참조하세요.  

 **Mac 컴퓨터의 경우: 권한 상승을 방지하려면 SSL 프로토콜만 신뢰할 수 있도록 신뢰할 수 있는 루트 CA 인증서 구성 고려**  

 Mac 컴퓨터를 등록할 때 Configuration Manager 클라이언트 관리용 사용자 인증서와 이 사용자 인증서가 연결되어 있는 신뢰할 수 있는 루트 인증서가 자동으로 함께 설치됩니다. 이 루트 인증서의 신뢰를 SSL 프로토콜로만 제한하려면 다음 절차를 수행하세요.  

 이 절차를 완료하면 SSL 이외의 프로토콜(예: Secure Mail(S/MIME), EAP(Extensible Authentication) 또는 코드 서명)에 대한 유효성을 검사할 때는 루트 인증서가 신뢰되지 않습니다.  

> [!NOTE]  
>  Configuration Manager와 별도로 클라이언트 인증서를 설치한 경우에도 이 절차를 수행할 수 있습니다.  

 루트 CA 인증서를 SSL 프로토콜로만 제한하려면  

1.  Mac 컴퓨터에서 터미널 창을 엽니다.  

2.  **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**명령을 입력합니다.  

3.  **키 집합 접근** 대화 상자의 **키 집합** 섹션에서 **시스템**을 클릭한 다음 **카테고리** 섹션에서 **인증서**를 클릭합니다.  

4.  Mac 클라이언트 인증서용 루트 CA 인증서를 찾은 다음 두 번 클릭합니다.  

5.  루트 CA 인증서의 대화 상자에서 **신뢰** 섹션을 확장하고 다음과 같이 변경합니다.  

    1.  **이 인증서 사용 시** 설정에서 **항상 신뢰** 기본 설정을 **시스템 기본값 사용**으로 변경합니다.  

    2.  **SSL(Secure Sockets Layer)** 설정에서 **값이 지정되지 않음** 을 **항상 신뢰**로 변경합니다.  

6.  대화 상자를 닫고 메시지가 나타나면 관리자 암호를 입력한 다음 **설정 업데이트**를 클릭합니다.  

##  <a name="BKMK_SecurityIssues_Clients"></a> Configuration Manager 클라이언트에 대한 보안 문제  
 다음 보안 문제는 최소화할 수 없습니다.  

-   상태 메시지가 인증되지 않음  

     상태 메시지에 대해 인증이 수행되지 않습니다. 관리 지점에서 HTTP 클라이언트 연결을 허용하면 모든 장치는 이 관리 지점에 상태 메시지를 보낼 수 있습니다. 관리 지점에서 HTTPS 클라이언트 연결만 허용하면, 장치는 신뢰할 수 있는 루트 인증 기관에서 유효한 클라이언트 인증 인증서를 가져와야 하지만 그 후에는 어떤 상태 메시지도 보낼 수 있습니다. 클라이언트가 유효하지 않은 상태 메시지를 보낼 경우 이 상태 메시지는 삭제됩니다.  

     이 취약점을 대상으로 몇 가지 공격이 발생할 수 있습니다. 공격자는 컬렉션에서 상태 메시지 쿼리에 기반한 멤버 자격을 얻기 위해 위조 상태 메시지를 보낼 수 있습니다. 모든 클라이언트는 상태 메시지를 대량으로 보냄으로써 관리 지점의 서비스 거부를 시작할 수 있습니다. 상태 메시지로 인해 상태 메시지 필터 규칙의 작업이 트리거될 경우 공격자는 상태 메시지 필터 규칙을 트리거할 수 있습니다. 또한 공격자는 보고 정보를 부정확하게 렌더링하는 상태 메시지를 보낼 수도 있습니다.  

-   정책의 대상이 원래 대상이 아닌 클라이언트로 다시 지정될 수 있습니다.  

     공격자는 여러 방법을 사용하여 일정한 클라이언트를 대상으로 한 정책이 완전히 다른 클라이언트에 적용되도록 할 수 있습니다. 예를 들어 신뢰할 수 있는 클라이언트에 있는 공격자는 허위 인벤토리 또는 검색 정보를 보낸 후 속해서는 안 되는 컬렉션에 자신의 컴퓨터를 추가한 다음 해당 컬렉션에 대한 모든 배포를 받을 수 있습니다. 공격자가 정책을 직접 수정할 수 없도록 방지하는 제어 기능이 있지만 공격자는 운영 체제를 초기화하고 다시 배포하는 기존 정책을 확보한 다음 이 정책을 다른 컴퓨터에 보내면 서비스 거부를 유발할 수 있습니다. 이러한 공격 유형은 정확한 시간 계산과 Configuration Manager 인프라에 대한 폭넓은 지식을 필요로 합니다.  

-   클라이언트 로그를 통한 사용자 액세스  

     모든 클라이언트 로그 파일은 사용자에게 읽기 액세스 권한 및 대화형 사용자 쓰기 액세스 권한을 허용합니다. 자세한 정보 로깅을 사용하도록 설정할 경우 공격자는 로그 파일을 읽어 호환성 또는 시스템 취약점에 대한 정보를 찾을 수도 있습니다. 사용자 컨텍스트로 수행되는 소프트웨어 설치와 같은 프로세스는 낮은 수준의 권한을 갖는 사용자 계정으로 로그에 쓸 수 있어야 합니다. 이는 곧 공격자도 낮은 수준의 권한을 갖는 계정을 사용하여 로그에 쓸 수 있다는 뜻입니다.  

     가장 심각한 문제는 공격자가 로그 파일에서 감사 및 침입 검색을 수행하는 관리자에게 필요할 수 있는 정보를 제거할 수 있다는 점입니다.  

-   컴퓨터는 모바일 장치 등록을 위해 만들어진 인증서를 가져오는 데 사용될 수 있습니다.  

     등록 요청을 처리하는 Configuration Manager 는 해당 요청이 컴퓨터가 아닌 모바일 장치에서 시작되었는지 여부를 확인할 수 없습니다. 컴퓨터에서 요청이 시작된 경우에도 Configuration Manager에 등록할 수 있도록 하는 PKI 인증서가 설치될 수 있습니다. 이 시나리오에서 권한 상승 공격을 방지하려면 신뢰할 수 있는 사용자만 자신의 모바일 장치를 등록할 수 있도록 허용하고 등록 작업을 자세히 모니터링하세요.  

-   클라이언트를 차단하더라도 해당 클라이언트에서 관리 지점으로의 연결은 제거되지 않으며 차단된 클라이언트는 관리 지점에 클라이언트 알림 패킷을 Keep-Alive 메시지로 계속 보낼 수 있습니다.  

     더 이상 신뢰하지 않는 클라이언트를 차단했지만 이 클라이언트에서 클라이언트 알림 통신을 설정한 경우 Configuration Manager는 세션의 연결을 끊지 않습니다. 차단된 클라이언트는 네트워크 연결이 끊어지지 않는 한 관리 지점에 계속 패킷을 보낼 수 있습니다. 이러한 패킷은 소량의 Keep-Alive 패킷일 뿐이므로 클라이언트는 차단 해제되기 전까지 Configuration Manager에서 관리되지 않습니다.  

-   자동 클라이언트 업그레이드를 사용하고 클라이언트에 관리 지점이 지정되어 클라이언트 원본 파일을 다운로드할 경우 이 관리 지점은 신뢰할 수 있는 원본으로 확인되지 않습니다.  

-   사용자가 Mac 컴퓨터를 처음 등록할 때 DNS 스푸핑의 위험이 있습니다.  

     등록 중에 Mac 컴퓨터에서 등록 프록시 지점에 연결할 때는 Mac 컴퓨터에 아직 루트 CA 인증서가 없을 가능성이 큽니다. 이때 Mac 컴퓨터에서 서버를 신뢰하지 않고 사용자에게 계속하라는 메시지를 표시합니다. Rogue DNS 서버에서 등록 프록시 지점의 정규화된 이름을 확인하면 Mac 컴퓨터를 Rogue 등록 프록시 지점으로 연결하고 신뢰할 수 없는 원본의 인증서를 설치할 수 있습니다. 이 위험을 줄이려면 사용 중인 환경에서 DNS 스푸핑을 방지하기 위한 모범 사례를 따르세요.  

-   Mac 등록은 인증서 요청을 제한하지 않습니다.  

     사용자는 매번 새 클라이언트 인증서를 요청하여 Mac 컴퓨터를 다시 등록할 수 있습니다. Configuration Manager에서는 단일 컴퓨터에서 수행하는 여러 요청을 확인하거나 요청하는 인증서의 수를 제한하지 않습니다. Rogue 사용자가 명령줄 등록 요청을 반복하는 스크립트를 실행하여 네트워크나 발급 CA(인증 기관)에서 서비스 거부가 발생할 수 있습니다. 이 위험을 줄이려면 발급 CA에서 이런 유형의 의심스러운 동작을 주의 깊게 모니터링하세요. 이 패턴의 동작을 보여 주는 컴퓨터는 즉시 Configuration Manager 계층 구조에서 차단해야 합니다.  

-   초기화 승인이 장치가 성공적으로 초기화되었는지를 확인하지 않습니다.  

     모바일 장치에 대해 초기화 작업을 시작하고 Configuration Manager에 승인할 초기화 상태가 표시되면 Configuration Manager에서 메시지를 보냈다는 것이지 장치에서 조치를 취했다는 의미가 아닙니다. 그리고 Exchange Server 커넥터에서 관리하는 모바일 장치의 경우 초기화 승인은 장치가 아니라 Exchange에서 명령을 받았음을 확인합니다.  

-   Windows Embedded 장치에 대해 변경 내용을 커밋하는 옵션을 사용할 경우 계정은 예상보다 더 빨리 잠길 수 있습니다.  

     Windows Embedded 장치가 Windows 7 이전의 운영 체제에서 실행되고 Configuration Manager에서 만들어진 변경 내용을 커밋하기 위해 쓰기 필터가 해제된 동안 사용자가 로그온을 시도하는 경우, 계정이 잠기기 전에 허용되는 잘못된 로그온 시도 횟수는 반으로 축소됩니다. 예를 들어 **계정 잠금 임계값** 이 6으로 구성된 경우 사용자가 암호를 3회 잘못 입력하면 계정이 잠기며 이에 따라 서비스 거부 상황이 발생하게 됩니다.  이 시나리오에서 사용자가 임베디드 장치에 반드시 로그온해야 할 경우 미리 잠금 임계값의 축소에 대해 주의를 주어야 합니다.  

##  <a name="BKMK_Privacy_Cliients"></a> Configuration Manager 클라이언트에 대한 개인 정보  
 Configuration Manager 클라이언트를 배포할 때 Configuration Manager 관리 기능을 사용하도록 클라이언트 설정을 구성할 수 있습니다. 관련 기능을 구성하는 데 사용하는 설정은 해당 클라이언트가 회사 네트워크에 직접 연결되었는지, 원격 세션을 통해 연결되었는지, 또는 인터넷에 연결되었지만 Configuration Manager에서 지원되는지 여부에 관계없이 Configuration Manager 계층 구조 내 모든 클라이언트에 적용될 수 있습니다.  

 클라이언트 정보는 Configuration Manager 데이터베이스에 저장되고 Microsoft로 전송되지 않습니다. 정보는 90일마다 반복되는 사이트 유지 관리 작업인 **오래된 검색 데이터 삭제** 에 의해 삭제될 때까지 데이터베이스에 유지됩니다. 삭제 간격은 필요에 따라 구성할 수 있습니다.  

 Configuration Manager 클라이언트를 구성하기 전에 개인 정보 요구 사항을 고려해야 합니다.  

### <a name="privacy-information-for-mobile-devices-that-are-enrolled-by-configuration-manager"></a>Configuration Manager에서 등록된 모바일 장치의 개인 정보  
 Configuration Manager에서 모바일 장치를 등록하는 경우에 대한 개인 정보는 [System Center Configuration Manager 개인정보취급방침 - 모바일 장치 추록](../../../../core/misc/privacy/privacy-statement-mobile-device-addendum.md)을 참조하세요.  

### <a name="client-status"></a>클라이언트 상태  
 Configuration Manager는 클라이언트의 작업을 모니터링하고 Configuration Manager 클라이언트 및 관련 종속성을 주기적으로 평가하여 재구성할 수 있습니다. 기본적으로 클라이언트 상태는 사용하도록 설정되며, 클라이언트 작업 확인에 서버 쪽 메트릭을 사용하는 반면 자체 점검, 재구성, Configuration Manager 사이트로 클라이언트 상태 정보 전송 등의 작업에는 클라이언트 쪽 작업을 사용합니다. 클라이언트는 구성 가능한 일정에 따라 자체 점검을 실행합니다. 클라이언트는 Configuration Manager 사이트로 검사 결과를 보냅니다. 이 정보는 전송 도중 암호화됩니다.  

 클라이언트 상태 정보는 Configuration Manager 데이터베이스에 저장되고 Microsoft로 전송되지 않습니다. 사이트 데이터베이스에서는 정보가 암호화되지 않은 형식으로 저장됩니다. 정보는 **다음 기간(일) 동안 클라이언트 상태 기록 유지** 클라이언트 상태 설정에 구성된 값에 따라 삭제되기 전까지 데이터베이스에 유지됩니다. 이 설정의 기본값은 31일입니다.  

 클라이언트 상태 점검과 함께 Configuration Manager 클라이언트를 설치하기 전에 개인 정보 요구 사항을 고려해야 합니다.  

##  <a name="BKMK_Privacy_ExchangeConnector"></a> Exchange Server 커넥터를 사용하여 관리하는 모바일 장치에 대한 개인 정보  
 Exchange Server 커넥터는 ActiveSync 프로토콜을 사용하여 온-프레미스이든 호스트된 버전이든 상관없이 Exchange Server에 연결된 장치를 검색하여 관리합니다. Exchange Server 커넥터로 검색된 레코드는 Configuration Manager 데이터베이스에 저장됩니다. 정보는 Exchange Server에서 수집되며, 여기에는 모바일 장치에서 Exchange Server로 전송된 정보 이외에 다른 추가 정보가 포함되지 않습니다.  

 모바일 장치 정보는 Microsoft로 전송되지 않으며, 모바일 장치 정보는 Configuration Manager 데이터베이스에 저장됩니다. 정보는 90일마다 반복되는 사이트 유지 관리 작업인 **오래된 검색 데이터 삭제** 에 의해 삭제될 때까지 데이터베이스에 유지됩니다. 삭제 간격은 필요에 따라 구성할 수 있습니다.  

 Exchange Server 커넥터를 설치하고 구성하기 전에 개인 정보 요구 사항을 고려해야 합니다.  
