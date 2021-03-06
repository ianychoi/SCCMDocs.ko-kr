---
title: "하이브리드 배포를 위해 사용자 소유의 장치 등록"
titleSuffix: Configuration Manager
description: "Configuration Manager를 사용하여 하이브리드 배포를 위해 사용자 소유 장치를 등록하는 다양한 방법을 알아봅니다."
ms.custom: na
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bdaa8a7-6a64-4b0e-b617-309dcd912c45
caps.latest.revision: "13"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 9bc0e23680ff2c7a5099938e546e50e03f998f5e
ms.sourcegitcommit: 1132886e07d0c0a87dcc7eeef4577dd8d8840023
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/01/2017
---
# <a name="enroll-user-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Configuration Manager를 사용하는 하이브리드 배포를 위해 사용자 소유 장치 등록

*적용 대상: System Center Configuration Manager(현재 분기)*

“자체 장치 가져오기(BYOD, Bring Your Own Devices)”라고도 하는 프로세스를 통해 사용자 소유 장치를 등록하여 관리로 가져올 수 있습니다.  사용자는 회사 포털 앱을 설치하고 장치(iOS, macOS 및 Android)에 로그인하거나, 직장 또는 학교 계정을 장치에 추가하고 도메인에 연결하여(Windows) 이 작업을 수행합니다. 이 프로세스에서는 장치를 Intune에 등록하여 사용자에게 Intune으로 관리되는 리소스에 대한 액세스를 부여하고 Intune이 PIN 요구 등과 같은 특정 장치 설정을 관리하게 합니다.

장치를 관리로 가져오려면 먼저 관리자가 [모바일 장치 관리를 설정하고](setup-hybrid-mdm.md) [등록을 활성화](enable-platform-enrollment.md)합니다. 등록이 활성화되면 사용자가 자체 장치를 등록할 수 있습니다. 사용자와의 공유에 대한 고려 사항과 절차는 [Microsoft Intune에 대한 최종 사용자 교육 방법](https://docs.microsoft.com/intune/end-user-educate)을 참조하세요.

장치를 구매한 회사 또는 학교에서는 [회사 소유 장치의 관리](enroll-company-owned-devices.md)를 제공하는 프로그램을 활용할 수 있습니다.
