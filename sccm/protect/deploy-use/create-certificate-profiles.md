---
title: "SCEP 인증서 프로필을 만드는 방법"
titleSuffix: Configuration Manager
description: "인증서 프로필을 사용하여 System Center Configuration Manager에서 관리되는 장치를 필요한 인증서로 프로비전하는 방법을 알아봅니다."
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 634d612c-92d7-4c03-873a-b2e730c9a72d
caps.latest.revision: 
caps.handback.revision: 
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 827565bd4dac074e8599075b19c9dac678a21948
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2017
---
# <a name="create-certificate-profiles"></a>인증서 프로필 만들기

*적용 대상: System Center Configuration Manager(현재 분기)*


Configuration Manager(SCCM)에서 인증서 프로필을 사용하여 관리되는 장치를 회사 리소스에 액세스하는 데 필요한 인증서로 프로비전할 수 있습니다. 인증서 프로필을 만들기 전에 [System Center Configuration Manager에 대한 인증서 인프라 설정](certificate-infrastructure.md)에 설명된 대로 인증서 인프라를 설정합니다.  

이 항목에서는 신뢰할 수 있는 루트 인증서 및 SCEP 인증서 프로필을 만드는 방법을 설명합니다. PFX 인증서 프로필을 만들려는 경우 [PFX 인증서 프로필 만들기](../../protect/deploy-use/create-pfx-certificate-profiles.md)를 참조하세요.

인증서 프로필을 만들려면

1.  인증서 프로필 만들기 마법사를 시작합니다.
1.  인증서에 대한 일반 정보를 제공합니다.
1.  신뢰할 수 있는 CA(인증 기관) 인증서를 구성합니다.  
1.  SCEP 인증서 정보를 구성합니다(SCEP 인증서에만 해당).  
1.  인증서 프로필에 대해 지원되는 플랫폼을 지정합니다.


## <a name="start-the-create-certificate-profile-wizard"></a>인증서 프로필 만들기 마법사 시작  

1.  System Center Configuration Manager 콘솔에서 **자산 및 준수**를 클릭합니다.  

2.  **자산 및 호환성** 작업 영역에서 **호환성 설정**및 **회사 리소스 액세스**를 각각 확장하고 **인증서 프로필**을 클릭합니다.  

3.  **홈** 탭의 **만들기** 그룹에서 **인증서 프로필 만들기**를 클릭합니다.  

## <a name="provide-general-information-about-the-certificate-profile"></a>인증서 프로필에 대한 일반 정보 제공  

인증서 프로필 만들기 마법사의 **일반** 페이지에서 다음 정보를 지정합니다.  

-   **이름**: 인증서 프로필의 고유한 이름을 입력합니다. 최대 256자까지 사용할 수 있습니다.  

-   **설명**: 인증서 프로필에 대한 개략적인 정보를 제공하는 설명과 System Center Configuration Manager 콘솔에서 해당 프로필을 식별하는 데 도움이 되는 기타 관련 정보를 입력합니다. 최대 256자까지 사용할 수 있습니다.  

-   **만들려는 인증서 프로필의 유형을 지정합니다.**: 다음 인증서 프로필 유형 중 하나를 선택합니다.  

-   **신뢰할 수 있는 CA 인증서**: 사용자 또는 장치가 다른 장치를 인증해야 할 때 신뢰할 수 있는 루트 CA(인증 기관) 또는 중간 CA 인증서를 배포하여 인증서 신뢰 체인을 형성하려는 경우 이 인증서 프로필 유형을 선택합니다. 예를 들어 장치가 RADIUS(Remote Authentication Dial-In User Service) 서버 또는 VPN(가상 사설망) 서버일 수 있습니다. 또한 SCEP 인증서 프로필을 만들려면 먼저 신뢰할 수 있는 CA 인증서 프로필을 구성해야 합니다. 이러한 경우 신뢰할 수 있는 CA 인증서는 사용자 또는 장치에 인증서를 발급하는 CA(인증 기관)의 신뢰할 수 있는 루트 인증서여야 합니다.  

-   **SCEP(단순 인증서 등록 프로토콜) 설정**: 단순 인증서 등록 프로토콜 및 네트워크 장치 등록 서비스 역할 서비스를 사용하여 장치 또는 사용자의 인증서를 요청하려면 이 인증서 프로필 유형을 선택합니다.

-   **개인 정보 교환 PKCS #12(PFX) 설정 - 가져오기**: PFX 인증서를 가져오려면 이 옵션을 선택합니다. PFX 인증서를 만드는 방법을 자세히 알아보려면 [PFX 인증서 프로필 가져오기](/sccm/mdm/deploy-use/import-pfx-certificate-profiles.md)를 참조하세요.

-   **개인 정보 교환 PKCS #12(PFX) 설정 - 만들기**: 이를 선택하여 인증 기관을 통해 PFX 인증서를 처리합니다. PFX 인증서를 만드는 방법을 자세히 알아보려면 [PFX 인증서 프로필 만들기](/sccm/mdm/deploy-use/create-pfx-certificate-profiles.md)를 참조하세요.


## <a name="configure-a-trusted-ca-certificate"></a>신뢰할 수 있는 CA 인증서 구성  

> [!IMPORTANT]  
>  SCEP 인증서 프로필을 만들려면 먼저 신뢰할 수 있는 CA 인증서 프로필을 하나 이상 구성해야 합니다.    
>  
>  인증서가 배포된 후 이러한 값을 하나라도 변경하면 새 인증서가 요청됩니다.
>  -  키 저장소 공급자
>  -  인증서 템플릿 이름
>  -  인증서 종류
>  -  주체 이름 형식
>  -  주체 대체 이름
>  -  인증서 유효 기간
>  -  키 사용
>  -  키 크기
>  -  확장 키 사용
>  -  루트 CA 인증서

1.  인증서 프로필 만들기 마법사의 **신뢰할 수 있는 CA 인증서** 페이지에서 다음 정보를 지정합니다.  

 -   **인증서 파일**: **가져오기** 를 클릭한 후 사용하려는 인증서 파일을 찾아 선택합니다.  

 -   **대상 저장소**: 장치에 둘 이상의 인증서 저장소가 있는 경우 인증서를 저장할 장소를 선택합니다. 장치에 저장소가 하나만 있는 경우 이 설정은 무시됩니다.  

2.  **인증서 지문** 값을 사용하여 올바른 인증서를 가져왔는지 확인합니다.  


## <a name="configure-scep-certificate-information-only-for-scep-certificates"></a>SCEP 인증서 정보 구성(SCEP 인증서에만 해당)  

1.  인증서 프로필 만들기 마법사의 **SCEP 서버** 페이지에서 SCEP를 통해 인증서를 발급할 NDES 서버의 URL을 지정합니다. 인증서 등록 지점 사이트 시스템 서버의 구성에 따라 NDES URL을 자동으로 지정하거나 URL을 수동으로 추가하도록 선택할 수 있습니다.  

2.  인증서 프로필 만들기 마법사의 **SCEP 등록** 페이지를 완료합니다.

 -  **다시 시도**: 장치가 네트워크 장치 등록 서비스를 실행하는 서버에 대해 인증서 요청을 자동으로 시도하는 횟수를 지정합니다. 이 설정은, CA 관리자가 인증서 요청을 승인해야 인증서 요청이 허용되는 경우를 지원합니다. 이 설정은 일반적으로 보안 수준이 높은 환경 또는 엔터프라이즈 CA가 아닌 독립 실행형 발급 CA가 있는 경우에 사용됩니다. 또한 테스트 목적의 경우 발급 CA가 인증서 요청을 처리하기 전에 인증서 요청 옵션을 검사할 수 있도록 이 설정을 사용해야 합니다. 이 설정은 **다시 시도 지연 시간(분)** 설정과 함께 사용합니다.  

 -   **다시 시도 지연 시간(초)**: 발급 CA가 인증서 요청을 처리하기 전에 CA 관리자 승인을 사용하는 경우 각 등록 시도 간의 간격을 분으로 지정합니다. 테스트 목적으로 관리자 승인을 사용하는 경우 요청을 승인한 후 장치가 인증서 요청을 다시 시도할 때까지 오랜 시간을 기다리지 않도록 낮은 값을 지정할 수 있습니다. 하지만 프로덕션 네트워크에서 관리자 승인을 사용하는 경우 CA 관리자가 보류 중인 승인을 검사하고 승인 또는 거부할 충분한 시간을 가질 수 있도록 높은 값을 지정할 수 있습니다.  

 -   **갱신 임계값(%)**: 장치에서 인증서 갱신을 요청하기 전까지 남은 인증서 수명을 백분율로 지정합니다.  

 -   **KSP(키 저장소 공급자)**: 인증서에 키가 저장될 위치를 지정합니다. 다음 값 중 하나를 선택합니다.  

   -   **있는 경우 TPM(신뢰할 수 있는 플랫폼 모듈)에 설치**: TPM에 키를 설치합니다. TPM이 없는 경우 키는 소프트웨어 키의 저장소 공급자에 설치됩니다.  

   -   **TPM(신뢰할 수 있는 플랫폼 모듈)에 설치, 그렇지 않으면 실패**: TPM에 키를 설치합니다. TPM 모듈이 없는 경우 설치가 실패합니다.  

   -   **비즈니스용 Windows Hello에 설치, 그렇지 않으면 실패**: 이 옵션은 Windows 10 Desktop 및 Mobile 장치에 사용할 수 있습니다. [System Center Configuration Manager의 비즈니스용 Windows Hello 설정](../../protect/deploy-use/windows-hello-for-business-settings.md)에 설명된 대로 **비즈니스용 Windows Hello**에 키를 등록합니다. 또한 이 옵션을 사용하여 해당 장치에 인증서를 발급하기 전에 장치를 등록하는 동안 **다단계 인증을 요구** 할 수 있습니다. 자세한 내용은 [다단계 인증으로 Windows 장치 보호](https://technet.microsoft.com/library/dn889751.aspx) 를 참조하세요.

   > [!NOTE]  
   > 
   > 사용자가 비즈니스용 Windows Hello PIN을 만들면 Windows에서 Configuration Manager가 수신 대기하는 알림을 보냅니다. 이렇게 하면 Configuration Manager에서 Windows Hello PIN을 만든 사용자를 신속하게 파악할 수 있습니다. 그런 다음 Windows Hello가 인증서 프로필에서 키 저장소 공급자로 사용되는 경우 Configuration Manager에서 새로운 인증서를 발행할 수 있습니다.  

   -   **소프트웨어 키 저장소 공급자에 설치**: 소프트웨어 키의 저장소 공급자에 키를 설치합니다.  

 -   **인증서 등록용 장치**: 인증서 프로필을 사용자 컬렉션에 배포하는 경우 사용자의 기본 장치에만 인증서 등록을 허용할지, 아니면 사용자가 로그온하는 모든 장치에서 허용할지를 선택합니다. 인증서 프로필을 장치 컬렉션에 배포하는 경우 기본 사용자의 장치에만 인증서 등록을 허용할지, 아니면 장치에 로그온하는 모든 사용자에게 허용할지를 선택합니다.  

3.  인증서 프로필 만들기 마법사의 **인증서 속성** 페이지에서 다음 정보를 지정합니다.  

 -   **인증서 템플릿 이름**: **찾아보기** 를 클릭한 후 네트워크 장치 등록 서비스에서 사용하도록 구성되고 발급 CA에 추가된 인증서 템플릿의 이름을 선택합니다. 인증서 템플릿을 성공적으로 찾아보려면 System Center Configuration Manager 콘솔을 실행하는 데 사용하는 사용자 계정에 인증서 템플릿에 대한 읽기 권한이 있어야 합니다. 또는 **찾아보기**를 사용할 수 없는 경우 인증서 템플릿의 이름을 입력합니다.  

 > [!IMPORTANT]
 >   
 >  인증서 템플릿 이름에 비 ASCII 문자(예: 중국어 문자)가 포함된 경우 인증서가 배포되지 않습니다. 인증서가 배포되는지 확인하려면 먼저 CA에서 인증서 템플릿의 사본을 만든 후 ASCII 문자를 사용하여 이름을 바꿔야 합니다.  

   인증서 템플릿으로 이동하는지 아니면 인증서 이름을 입력하는지에 따라 다음 사항에 유의하세요.  

 -   이동하여 인증서 템플릿의 이름을 선택하는 경우 페이지의 일부 필드가 인증서 템플릿에서 자동으로 채워집니다. 일부 경우에 다른 인증서 템플릿을 선택하지 않으면 이러한 값을 변경할 수 없습니다.  

 -   인증서 템플릿의 이름을 입력하는 경우 이름이 네트워크 장치 등록 서비스를 실행하는 서버의 레지스트리에 나열된 인증서 템플릿 중 하나와 일치하는지 확인합니다. 또한 인증서 템플릿의 표시 이름이 아닌 인증서 템플릿 이름을 지정했는지 확인합니다.  

   인증서 템플릿의 이름을 찾으려면 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP 키로 이동합니다. 인증서 템플릿이 **EncryptionTemplate**, **GeneralPurposeTemplate**및 **SignatureTemplate**의 값으로 나열됩니다. 기본적으로 모든 세 인증서 템플릿의 값은 **IPSECIntermediateOffline**이며, 이는 **IPSec(오프라인 요청)**라는 템플릿 표시 이름으로 매핑됩니다.  

   > [!WARNING]  
   > 
   >  인증서 템플릿 이름을 찾아 선택하지 않고 직접 입력하는 경우 System Center Configuration Manager가 인증서 템플릿의 콘텐츠를 확인할 수 없으므로 인증서 템플릿에서 지원되지 않는 옵션을 선택하여 인증서 요청 실패가 발생하게 될 수도 있습니다. 이러한 경우 CPR.log 파일에서 CSR(인증서 서명 요청)의 템플릿 이름과 인증 질문이 일치하지 않는다는 w3wp.exe 관련 오류 메시지가 나타납니다.  
   >   
   >  **GeneralPurposeTemplate** 값에 지정된 인증서 템플릿의 이름을 입력하면 해당 인증서 프로필에 대해 **키 암호화** 및 **디지털 서명** 옵션을 선택해야 합니다. 하지만 이 인증서 프로필에서 **키 암호화** 옵션만 사용하도록 설정하려는 경우 **EncryptionTemplate** 키의 인증서 템플릿 이름을 지정해야 합니다. 마찬가지로 이 인증서 프로필에서 **디지털 서명** 옵션만 사용하도록 설정하려는 경우 **SignatureTemplate** 키의 인증서 템플릿 이름을 지정해야 합니다.  

 -   **인증서 유형**: 인증서를 장치에 배포할지 아니면 사용자에게 배포할지를 선택합니다.  
 -   **주체 이름 형식**: 인증서 요청 시 System Center Configuration Manager에서 자동으로 주체 이름을 만드는 방식을 목록에서 선택합니다. 사용자용 인증서인 경우 주체 이름에 사용자의 전자 메일 주소를 포함할 수도 있습니다. 
    
   > [!NOTE]  
   > 
   > **IMEI 번호** 또는 **일련 번호**를 선택하면 동일한 사용자가 소유한 여러 장치를 구분할 수 있습니다. 예를 들어 해당 장치는 일반 이름을 공유할 수 있지만 IMEI 번호 또는 일련 번호는 공유할 수 없습니다. 장치에서 IMEI 또는 일련 번호를 보고하지 않는 경우 일반 이름으로 인증서가 발급됩니다.

 -   **주체 대체 이름**: System Center Configuration Manager에서 인증서 요청의 SAN(주체 대체 이름) 값을 자동으로 만드는 방법을 지정합니다. 예를 들어 사용자 인증서 유형을 선택한 경우 주체 대체 이름에 UPN(사용자 계정 이름)을 포함할 수 있습니다.  클라이언트 인증서가 네트워크 정책 서버에 대한 인증에 사용되는 경우 주체 대체 이름을 UPN으로 설정해야 합니다.  

   > [!NOTE]  
   >  - iOS 장치는 SCEP 인증서에서 제한된 주체 이름 형식과 주체 대체 이름을 지원합니다. 지원되지 않는 형식을 지정하는 경우 인증서는 iOS 장치에 등록되지 않습니다. SCEP 인증서 프로필을 iOS 장치에 배포하도록 구성하는 경우 **주체 이름 형식** 에 **일반 이름**을 사용하고, **주체 대체 이름**에 **DNS 이름** , **전자 메일 주소** 또는 **UPN**을 사용하세요.  

 -   **인증서 유효 기간**: 발급 CA에 대해 사용자 지정 유효 기간을 허용하는 certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE 명령을 실행한 경우 인증서가 만료될 때까지 남은 기간을 지정할 수 있습니다. 이 명령에 대한 자세한 내용은 [System Center Configuration Manager의 인증서 인프라](../../protect/deploy-use/certificate-infrastructure.md) 항목을 참조하세요.  

   지정된 인증서 템플릿에서 유효 기간보다 작은 값은 지정할 수 있지만 높은 값은 지정할 수 없습니다. 예를 들어 인증서 템플릿의 인증서 유효 기간이 2년이면 값을 1년으로 지정할 수는 있어도 5년으로는 지정할 수 없습니다. 또한 이 값은 발급 CA 인증서의 남은 유효 기간보다 작아야 합니다.  

 -   **키 사용**: 인증서에 대한 키 사용 옵션을 지정합니다. 다음 옵션 중에서 선택할 수 있습니다.  

        -   **키 암호화**: 키가 암호화된 경우에만 키 교환을 허용합니다.  

        -   **디지털 서명**: 디지털 서명으로 키를 보호하는 경우에만 키 교환을 허용합니다.  

   **찾아보기**를 사용하여 인증서 템플릿을 선택한 경우 다른 인증서 템플릿을 선택하지 않으면 이러한 설정을 변경할 수 없습니다.  

   사용자가 선택한 인증서 템플릿은 위의 두 키 사용 옵션 중 하나 또는 둘 모두로 구성해야 합니다. 구성하지 않은 경우 인증서 등록 지점 로그 파일 **Crp.log** 에 **CSR의 키 사용과 인증 질문이 일치하지 않습니다.**메시지가 표시됩니다.  


   -   **키 크기(비트)**: 키의 크기(비트)를 선택합니다.  

   -   **확장 키 사용**: **선택**을 클릭하여 인증서의 용도에 대한 값을 추가합니다. 대부분의 경우 인증서는 사용자 또는 장치가 서버에 인증할 수 있는 **클라이언트 인증** 이 필요합니다. 그러나 필요에 따라 다른 키 사용을 추가할 수 있습니다.  


   -   **해시 알고리즘**: 이 인증서와 함께 사용할 수 있는 해시 알고리즘 유형 중 하나를 선택합니다. 연결 장치에서 지원되는 가장 강력한 보안 수준을 선택합니다.  

   > [!NOTE]  
   > 
   >  **SHA-2** 는 SHA-256, SHA-384 및 SHA-512를 지원합니다. **SHA-3** 은 SHA-3만 지원합니다.  

   -   **루트 CA 인증서**: **선택** 을 클릭하여 이전에 구성하고 사용자 또는 장치에 배포한 루트 CA 인증서 프로필을 선택합니다. 이 CA 인증서는 이 인증서 프로필에서 구성하려는 인증서를 발급할 CA에 대한 루트 인증서여야 합니다.  

   > [!IMPORTANT]  
   >  사용자 또는 장치에 배포되지 않은 루트 CA 인증서를 지정할 경우 System Center Configuration Manager는 이 인증서 프로필에서 구성 중인 인증서 요청을 시작하지 않습니다.  


##  <a name="specify-supported-platforms-for-the-certificate-profile"></a>인증서 프로필에 대해 지원되는 플랫폼 지정  

1. 인증서 프로필 만들기 마법사의 **지원되는 플랫폼** 페이지에서 인증서 프로필을 설치하려는 운영 체제를 선택합니다. 또는 **모두 선택** 을 클릭하여 사용 가능한 모든 운영 체제에 인증서 프로필을 설치합니다.
2. 마법사의 **요약** 페이지를 검토하고 **마침**을 선택합니다. 
 
 
**자산 및 준수** 작업 영역의 **인증서 프로필** 노드에 새 인증서 프로필이 나타나고, [System Center Configuration Manager에서 프로필을 배포하는 방법](deploy-wifi-vpn-email-cert-profiles.md)에 설명된 대로 사용자나 장치에 배포할 준비가 됩니다.  