---
title: "컬렉션 필수 조건"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager에서 컬렉션 사용에 대한 필수 조건을 확인합니다."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
caps.latest.revision: "7"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 5696a4cc81d8be889f6040a2f9610e1aec17d271
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2017
---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>System Center Configuration Manager에서 컬렉션에 대한 필수 조건

*적용 대상: System Center Configuration Manager(현재 분기)*

System Center Configuration Manager의 컬렉션에는 제품 내 종속성만 포함됩니다.  

## <a name="configuration-manager-dependencies"></a>Configuration Manager 종속성  

|종속성|추가 정보|  
|----------------|----------------------|  
|보고 서비스 지점|컬렉션에 대한 보고서 기능을 실행하려면 보고 서비스 지점의 사이트 시스템 역할이 설치되어 있어야 합니다. 자세한 내용은 [System Center Configuration Manager의 보고](../../../../core/servers/manage/reporting.md)를 참조하세요.|  
|컬렉션을 관리하려면 특정 보안 권한을 부여해야 합니다.|준수 설정을 관리하려면 다음 보안 권한이 있어야 합니다.<br /><br /> - 컬렉션을 만들고 관리하려면: **컬렉션** 개체에 대한 **만들기**, **삭제**, **수정**, **폴더 수정**, **개체 이동**, **읽기** 및 **리소스 읽기** 권한이 필요합니다.<br /><br /> - 컬렉션 설정을 관리하려면: **컬렉션** 개체에 대한 **컬렉션 설정 수정** 권한이 필요합니다.<br /><br /> 루트 폴더를 포함하여 모든 컬렉션 폴더에 **폴더 수정** 권한이 필요합니다.|  
