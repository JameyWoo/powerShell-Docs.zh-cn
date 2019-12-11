---
ms.date: 06/05/2017
keywords: powershell,cmdlet
title: 为多个对象重复执行任务 (ForEach Object)
ms.openlocfilehash: 1442507c4213476f65df3401c1021f8d0fc31956
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "67030815"
---
# <a name="repeating-a-task-for-multiple-objects-foreach-object"></a>为多个对象重复执行任务 (ForEach-Object)

ForEach-Object  cmdlet 对当前管道对象使用脚本块和 `$_` 描述符，以便你可以对管道中的每个对象运行命令。 这可用于执行某些复杂的任务。

一种有帮助的情况就是操纵数据使其更为有用。 例如，WMI 的 Win32_LogicalDisk 类可用于返回每个本地磁盘的可用空间信息。 返回以字节表示的数据，但是，这也将增加阅读的难度：

```
PS> Get-WmiObject -Class Win32_LogicalDisk

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 50665070592
Size         : 203912880128
VolumeName   : Local Disk
```

我们可以通过将每个值除以 1024 两次来将 FreeSpace 值转换为兆字节；第一次除法后，该数据将以千字节为单位，而完成第二次除法后，该值则以兆字节为单位。 你可通过键入以下内容在 ForEach-Object 脚本块中实现此操作：

```
PS> Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {($_.FreeSpace)/1024.0/1024.0}
48318.01171875
```

遗憾的是，该输出现在是没有关联标签的数据。 因为这样的 WMI 属性为只读，所以不能直接转换 FreeSpace。 如果键入以下内容：

```powershell
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

则将收到错误消息：

```output
"FreeSpace" is a ReadOnly property.
At line:1 char:70
+ Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.F <<<< r
eeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

可以通过使用一些高级技术重新组织数据，但更简单的方法是通过使用 **Select-Object** 创建新对象。
