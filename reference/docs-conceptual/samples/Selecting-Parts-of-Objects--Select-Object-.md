---
ms.date: 06/05/2017
keywords: powershell,cmdlet
title: 选择对象部件 (Select Objec)
ms.openlocfilehash: 4d4c89f0b5103e4701a3af3cd07fcd7c8f1c697f
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "67030120"
---
# <a name="selecting-parts-of-objects-select-object"></a>选择对象部件 (Select-Object)

可以使用 **Select-Object** cmdlet 创建新的自定义 Windows PowerShell 对象（包含从用于创建它们的对象中选择的属性）。 键入下面的命令以创建仅包括 Win32_LogicalDisk WMI 类的 Name 和 FreeSpace 属性的新对象：

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace

Name                                    FreeSpace
----                                    ---------
C:                                      50664845312
```

发出该命令后，无法看到数据类型，但是如果在 Select-Object 后将结果发送到 Get-Member，可以说明你拥有新类型的对象 PSCustomObject：

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace| Get-Member

   TypeName: System.Management.Automation.PSCustomObject

Name        MemberType   Definition
----        ----------   ----------
Equals      Method       System.Boolean Equals(Object obj)
GetHashCode Method       System.Int32 GetHashCode()
GetType     Method       System.Type GetType()
ToString    Method       System.String ToString()
FreeSpace   NoteProperty  FreeSpace=...
Name        NoteProperty System.String Name=C:
```

Select-Object 有许多用途。 其中之一就是复制你稍后可修改的数据。 现在，我们可以处理在上一节中遇到的问题。 我们可以在新建对象中更新 FreeSpace 的值，输出内容将包括描述性标签：

```
Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0; $_}
Name                                                                  FreeSpace
----                                                                  ---------
C:                                                                48317.7265625
```
