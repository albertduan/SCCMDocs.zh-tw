---
title: "遠端控制 | Microsoft Docs"
description: "了解 System Center Configuration Manager 的遠端控制簡介。"
ms.custom: na
ms.date: 12/26/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 29350919-6a25-446b-a0da-05e8914fbb26
caps.latest.revision: 4
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 9206b82eca02877c30eebf146d42bcca7290eb42
ms.openlocfilehash: 47bfeec5bd5d9b843e9064560d0cd0b14bd7d6a1
ms.lasthandoff: 12/30/2016


---
# <a name="introduction-to-remote-control-in-system-center-configuration-manager"></a>System Center Configuration Manager 的遠端控制簡介

適用於：System Center Configuration Manager (最新分支)

使用遠端控制可遠端管理、提供協助，或檢視階層中的任何用戶端電腦。 您可以使用遠端控制功能來疑難排解用戶端電腦上的硬體和軟體設定問題，以及提供支援。 Configuration Manager 支援遠端控制工作群組電腦和已加入網域的電腦。  

Configuration Manager 也可讓您設定用戶端設定，以從 Configuration Manager 主控台執行 Windows 遠端桌面和遠端協助。  

> [!NOTE]  
>  在下列情況中，您無法透過 Configuration Manager 主控台建立用戶端電腦上的遠端協助工作階段：  
>   
>  -   用戶端電腦位於工作群組中。  
> -   Configuration Manager 主控台的執行電腦是執行 Windows XP Service Pack 3，但是主機電腦並非執行 Windows XP Service Pack 3。 如需詳細資訊，請參閱 Windows 遠端協助文件。  

 您可以透過 Configuration Manager 主控台的任何裝置集合、Windows 命令提示字元視窗，或 Windows [開始] 功能表，啟動遠端控制工作階段。  

