---
ms.date: 06/05/2017
keywords: powershell,cmdlet
title: 执行网络任务
ms.openlocfilehash: e581296b4b7609b374f206c447c4f797e3e2c400
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "67030854"
---
# <a name="performing-networking-tasks"></a>执行网络任务

由于 TCP/IP 是最常用的网络协议，因此大多数低级别网络协议管理任务都涉及 TCP/IP。 在本部分中，我们使用 Windows PowerShell 和 WMI 来执行这些任务。

## <a name="listing-ip-addresses-for-a-computer"></a>列出计算机的 IP 地址

若要获取本地计算机上使用的所有 IP 地址，请使用以下命令：

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Format-Table -Property IPAddress
```

此命令的输出与大多数属性列表不同，因为值括在大括号中：

```output
IPAddress
---------
{192.168.1.80}
{192.168.148.1}
{192.168.171.1}
{0.0.0.0}
```

若要了解大括号出现的原因，请使用 Get-Member cmdlet 检查 **IPAddress** 属性：

```
PS> Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Get-Member -Name IPAddress


TypeName: System.Management.ManagementObject#root\cimv2\Win32_NetworkAdapterConfiguration

Name      MemberType Definition
----      ---------- ----------
IPAddress Property   System.String[] IPAddress {get;}
```

每个网络适配器的 IPAddress 属性实际上是一个数组。 定义中的大括号指示 **IPAddress** 不是 **System.String** 值，而是由 **System.String** 值组成的数组。

## <a name="listing-ip-configuration-data"></a>列出 IP 配置数据

若要显示每个网络适配器的详细 IP 配置数据，请使用以下命令：

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName .
```

网络适配器配置对象的默认显示为一组非常精简的可用信息。 对于深入检查和疑难解答，请使用 Select-Object 或格式设置 cmdlet（例如 Format-List）来指定要显示的属性。

如果你对 IPX 或 WINS 属性不感兴趣（可能是在使用现代 TCP/IP 网络的情况下），则可以使用 Select-Object 的 ExcludeProperty 参数来隐藏其名称以“WINS”或“IPX:”开头的属性

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Select-Object -Property [a-z]* -ExcludeProperty IPX*,WINS*
```

此命令返回有关 DHCP、DNS、路由以及其他次要 IP 配置属性的详细信息。

## <a name="pinging-computers"></a>Ping 计算机

你可以使用 **Win32_PingStatus** 对计算机执行简单的 Ping 操作。 下面的命令执行 Ping 操作，但返回冗长的输出：

```powershell
Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName .
```

摘要信息是更为有用的形式，它显示下面的命令生成的 Address、ResponseTime 以及 StatusCode 属性。 Format-Table 的 Autosize 参数调整表列的大小，以使其正确显示在 Windows PowerShell 中。

```
PS> Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName . | Format-Table -Property Address,ResponseTime,StatusCode -Autosize

Address   ResponseTime StatusCode
-------   ------------ ----------
127.0.0.1            0          0
```

如果 StatusCode 为 0，指明 ping 操作成功。

你可以使用数组借助单个命令对计算机执行 Ping 操作。 由于存在多个地址，因此请使用 **ForEach-Object** 单独对每个地址执行 Ping 操作：

```powershell
'127.0.0.1','localhost','research.microsoft.com' | ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='" + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

可以使用相同的命令格式对一个子网（例如使用网络号码 (192.168.1.0) 和标准 C 类子网掩码 (255.255.255.0) 的专用网）上的所有计算机执行 Ping 操作。仅在 192.168.1.1 到 192.168.1.254 范围内的地址为合法本地地址（0 始终为网络号码保留，255 是子网广播地址）。

若要在 Windows PowerShell 中表示从 1 到 254 范围内的数字数组，请使用语句 **1..254**。 可以通过生成数组，然后将值添加到 ping 语句中的部分地址上，执行完整的子网 Ping 操作：

```powershell
1..254| ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='192.168.1." + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

请注意，这一用于生成一系列地址的方法也可用于其他地方。 你可以使用以下方式生成完整的地址集：

```powershell
$ips = 1..254 | ForEach-Object -Process {'192.168.1.' + $_}
```

## <a name="retrieving-network-adapter-properties"></a>检索网络适配器属性

在本用户指南的前面部分中，我们提到过你可以使用 **Win32_NetworkAdapterConfiguration** 来检索常规配置属性。 尽管不是严格的 TCP/IP 信息，但网络适配器信息（例如 MAC 地址和适配器类型）也可用于了解计算机的运行情况。 若要获取此信息的摘要，请使用下面的命令：

```powershell
Get-WmiObject -Class Win32_NetworkAdapter -ComputerName .
```

## <a name="assigning-the-dns-domain-for-a-network-adapter"></a>为网络适配器分配 DNS 域

若要分配 DNS 域以便进行自动名称解析，请使用 **Win32_NetworkAdapterConfiguration SetDNSDomain** 方法。 由于你单独为每个网络适配器配置分配 DNS 域，因此需要使用 **ForEach-Object** 语句将域分配给每个适配器：

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process { $_. SetDNSDomain('fabrikam.com') }
```

筛选语句“IPEnabled=$true”是必需的，因为即使是在仅使用 TCP/IP 的网络上，计算机上的多个网络适配器配置也不是真正的 TCP/IP 适配器；它们是支持 RAS、PPTP、QoS 和其他适用于所有适配器的服务的常规软件元素，因此没有自己的地址。

可以使用 **Where-Object** cmdlet，而不是使用 **Get-WmiObject** 筛选器筛选命令。

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -ComputerName . | Where-Object -FilterScript {$_.IPEnabled} | ForEach-Object -Process {$_.SetDNSDomain('fabrikam.com')}
```

## <a name="performing-dhcp-configuration-tasks"></a>执行 DHCP 配置任务

修改 DHCP 详细信息需处理一组网络适配器，与 DNS 配置的操作相同。 你可通过使用 WMI 执行多种不同的操作，我们将逐步介绍一些常见操作。

### <a name="determining-dhcp-enabled-adapters"></a>确定启用 DHCP 的适配器

若要查找计算机上启用了 DHCP 的适配器，请使用下面的命令：

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName .
```

若要排除有IP 配置问题的适配器，可以仅检索已启用 IP 的适配器：

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName .
```

### <a name="retrieving-dhcp-properties"></a>检索 DHCP 属性

因为适配器的 DHCP 相关属性通常以“DHCP”开头，所以你可使用 Format-Table 的 Property 参数来仅显示那些属性：

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName . | Format-Table -Property DHCP*
```

### <a name="enabling-dhcp-on-each-adapter"></a>在每个适配器上启用 DHCP

若要在所有适配器上启用 DHCP，请使用下面的命令：

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process {$_.EnableDHCP()}
```

可以使用 Filter 语句“IPEnabled=$true and DHCPEnabled=$false”，以免在已启用 DHCP 的适配器上再次启用它，但忽略这一步也不会导致错误出现  。

### <a name="releasing-and-renewing-dhcp-leases-on-specific-adapters"></a>释放和续订特定适配器上的 DHCP 租约

**Win32_NetworkAdapterConfiguration** 类具有 **ReleaseDHCPLease** 和 **RenewDHCPLease** 方法。 这两种方法的使用方式相同。 一般情况下，在仅需释放或续订特定子网上的适配器地址时使用这些方法。 在子网上筛选器适配器的最简单方法是仅选择使用该子网的网关的适配器配置。 例如，下面的命令释放本地计算机上适配器上的所有 DHCP 租约，这些适配器正在从 192.168.1.254 获得 DHCP 租约：

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

续订 DHCP 租约的唯一更改是使用 **RenewDHCPLease** 方法，而不是 **ReleaseDHCPLease** 方法：

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

> [!NOTE]
> 在远程计算机上使用这些方法时，请注意，如果你通过已释放或已续订租约的适配器连接到远程系统，则可能会失去对该系统的访问权限。

### <a name="releasing-and-renewing-dhcp-leases-on-all-adapters"></a>释放和续订所有适配器上的 DHCP 租约

可以通过使用 **Win32_NetworkAdapterConfiguration** 方法、**ReleaseDHCPLeaseAll** 和 **RenewDHCPLeaseAll** 对所有适配器指定全局 DHCP 地址释放或续订。 但是，该命令必须适用于 WMI 类，而不是特定的适配器，因为全局释放和续订租约是对该类执行的，而不是对特定适配器执行的。

可以通过列出所有 WMI 类，然后按名称仅选择所需类来获取对 WMI 类而不是类实例的引用。 例如，下面的命令将返回 Win32_NetworkAdapterConfiguration 类：

```powershell
Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'}
```

可以将整个命令视为类，并在其上调用**ReleaseDHCPAdapterLease** 方法。 在下面的命令中，**Get-WmiObject** 和 **Where-Object** 管道元素两边的括号指示 Windows PowerShell 先对其进行评估：

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).ReleaseDHCPLeaseAll()
```

可以使用相同的命令格式来调用 **RenewDHCPLeaseAll** 方法：

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).RenewDHCPLeaseAll()
```

## <a name="creating-a-network-share"></a>创建网络共享

若要创建网络共享，请使用 **Win32_Share Create** 方法：

```powershell
(Get-WmiObject -List -ComputerName . | Where-Object -FilterScript {$_.Name -eq 'Win32_Share'}).Create('C:\temp','TempShare',0,25,'test share of the temp folder')
```

还可以在 Windows PowerShell 中使用 **net share** 来创建共享：

```powershell
net share tempshare=c:\temp /users:25 /remark:"test share of the temp folder"
```

## <a name="removing-a-network-share"></a>删除网络共享

可以使用 **Win32_Share** 删除网络共享，但是该过程与创建共享略有不同，因为需要检索要删除的特定共享，而不是 **Win32_Share** 类。 下面的语句删除共享“TempShare”：

```powershell
(Get-WmiObject -Class Win32_Share -ComputerName . -Filter "Name='TempShare'").Delete()
```

**Net share** 也可实现此操作：

```
PS> net share tempshare /delete

tempshare was deleted successfully.
```

## <a name="connecting-a-windows-accessible-network-drive"></a>连接 Windows 可访问网络驱动器

**New-PSDrive** cmdlet 可创建 Windows PowerShell 驱动器，但使用这种方法创建的驱动器仅适用于 Windows PowerShell。 若要创建新的联网驱动器，可以使用 **WScript.Network** COM 对象。 下面的命令将共享 \\\\FPS01\\users 映射到本地驱动器 B：

```powershell
(New-Object -ComObject WScript.Network).MapNetworkDrive('B:', '\\FPS01\users')
```

**net use** 命令也可实现此操作：

```powershell
net use B: \\FPS01\users
```

使用 **WScript.Network** 或 net use 映射的驱动器可立即用于 Windows PowerShell。
