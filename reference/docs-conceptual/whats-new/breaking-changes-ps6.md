---
ms.date: 05/17/2018
keywords: powershell, 核心
title: PowerShell 6.0 的重大更改
ms.openlocfilehash: df716fc3ad48d640ddefcfd87da445eaf104cfbe
ms.sourcegitcommit: e1027805385081c2e6f9250f9cd1167a45f035b0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72561262"
---
# <a name="breaking-changes-for-powershell-60"></a><span data-ttu-id="b23ef-103">PowerShell 6.0 的重大更改</span><span class="sxs-lookup"><span data-stu-id="b23ef-103">Breaking Changes for PowerShell 6.0</span></span>

## <a name="features-no-longer-available-in-powershell-core"></a><span data-ttu-id="b23ef-104">PowerShell Core 中不再可用的功能</span><span class="sxs-lookup"><span data-stu-id="b23ef-104">Features no longer available in PowerShell Core</span></span>

### <a name="powershell-workflow"></a><span data-ttu-id="b23ef-105">PowerShell 工作流</span><span class="sxs-lookup"><span data-stu-id="b23ef-105">PowerShell Workflow</span></span>

<span data-ttu-id="b23ef-106">[PowerShell 工作流][workflow]是基于可为长时间运行或并行化任务创建可靠 runbook 的 [Windows Workflow Foundation (WF)][workflow-foundation] 生成的 Windows PowerShell 中的一项功能。</span><span class="sxs-lookup"><span data-stu-id="b23ef-106">[PowerShell Workflow][workflow] is a feature in Windows PowerShell that builds on top of [Windows Workflow Foundation (WF)][workflow-foundation] that enables the creation of robust runbooks for long-running or parallelized tasks.</span></span>

<span data-ttu-id="b23ef-107">由于缺少对 .NET Core 中的 Windows Workflow Foundation 的支持，我们将不继续在 PowerShell Core 中支持 PowerShell 工作流。</span><span class="sxs-lookup"><span data-stu-id="b23ef-107">Due to the lack of support for Windows Workflow Foundation in .NET Core, we will not continue to support PowerShell Workflow in PowerShell Core.</span></span>

<span data-ttu-id="b23ef-108">将来，我们希望使用 PowerShell 语言启用本机并行/并发，而无需使用 PowerShell 工作流。</span><span class="sxs-lookup"><span data-stu-id="b23ef-108">In the future, we would like to enable native parallelism/concurrency in the PowerShell language without the need for PowerShell Workflow.</span></span>

<span data-ttu-id="b23ef-109">如果在操作系统重启后需要使用检查点来恢复脚本，建议在操作系统启动时使用任务计划程序运行脚本，但此脚本将需要维持自身的状态（例如将它保存到文件）。</span><span class="sxs-lookup"><span data-stu-id="b23ef-109">If there is a need to use checkpoints to resume a script after the OS restarts, we recommend using Task Scheduler to run a script on OS startup, but the script would need to maintain its own state (like persisting it to a file).</span></span>

[workflow]: https://docs.microsoft.com/powershell/scripting/core-powershell/workflows-guide
[workflow-foundation]: https://docs.microsoft.com/dotnet/framework/windows-workflow-foundation/

### <a name="custom-snap-ins"></a><span data-ttu-id="b23ef-110">自定义管理单元</span><span class="sxs-lookup"><span data-stu-id="b23ef-110">Custom snap-ins</span></span>

<span data-ttu-id="b23ef-111">[PowerShell 管理单元][snapin]是 PowerShell 社区中未广泛采用的 PowerShell 模块的前身。</span><span class="sxs-lookup"><span data-stu-id="b23ef-111">[PowerShell snap-ins][snapin] are a predecessor to PowerShell modules that do not have widespread adoption in the PowerShell community.</span></span>

<span data-ttu-id="b23ef-112">鉴于支持管理单元的复杂性及其缺乏在社区中的使用，我们不再支持 PowerShell Core 中的自定义管理单元。</span><span class="sxs-lookup"><span data-stu-id="b23ef-112">Due to the complexity of supporting snap-ins and their lack of usage in the community, we no longer support custom snap-ins in PowerShell Core.</span></span>

<span data-ttu-id="b23ef-113">现在，这将中断 Windows 和 Windows Server 中的 `ActiveDirectory` 和 `DnsClient` 模块。</span><span class="sxs-lookup"><span data-stu-id="b23ef-113">Today, this breaks the `ActiveDirectory` and `DnsClient` modules in Windows and Windows Server.</span></span>

[snapin]: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_pssnapins

### <a name="wmi-v1-cmdlets"></a><span data-ttu-id="b23ef-114">WMI v1 cmdlet</span><span class="sxs-lookup"><span data-stu-id="b23ef-114">WMI v1 cmdlets</span></span>

<span data-ttu-id="b23ef-115">鉴于支持两个基于 WMI 的模块集的复杂性，我们从 PowerShell Core 中删除 WMI v1 cmdlet：</span><span class="sxs-lookup"><span data-stu-id="b23ef-115">Due to the complexity of supporting two sets of WMI-based modules, we removed the WMI v1 cmdlets from PowerShell Core:</span></span>

- `Get-WmiObject`
- `Invoke-WmiMethod`
- `Register-WmiEvent`
- `Set-WmiInstance`

<span data-ttu-id="b23ef-116">我们转为建议使用 CIM（也称为 WMI v2）cmdlet，它们提供了与新功能及经过重新设计的语法相同的功能：</span><span class="sxs-lookup"><span data-stu-id="b23ef-116">Instead, we recommend that you the use the CIM (aka WMI v2) cmdlets which provide the same functionality with new functionality and a redesigned syntax:</span></span>

- `Get-CimAssociatedInstance`
- `Get-CimClass`
- `Get-CimInstance`
- `Get-CimSession`
- `Invoke-CimMethod`
- `New-CimInstance`
- `New-CimSession`
- `New-CimSessionOption`
- `Register-CimIndicationEvent`
- `Remove-CimInstance`
- `Remove-CimSession`
- `Set-CimInstance`

### <a name="microsoftpowershelllocalaccounts"></a><span data-ttu-id="b23ef-117">Microsoft.PowerShell.LocalAccounts</span><span class="sxs-lookup"><span data-stu-id="b23ef-117">Microsoft.PowerShell.LocalAccounts</span></span>

<span data-ttu-id="b23ef-118">由于使用了不受支持的 API 而从 PowerShell Core 中删除 `Microsoft.PowerShell.LocalAccounts`，直至找到更佳解决方案。</span><span class="sxs-lookup"><span data-stu-id="b23ef-118">Due to the use of unsupported APIs, `Microsoft.PowerShell.LocalAccounts` has been removed from PowerShell Core until a better solution is found.</span></span>

### <a name="-computer-cmdlets"></a><span data-ttu-id="b23ef-119">`*-Computer` cmdlet</span><span class="sxs-lookup"><span data-stu-id="b23ef-119">`*-Computer` cmdlets</span></span>

<span data-ttu-id="b23ef-120">由于使用了不受支持的 API，从 PowerShell Core 中删除了以下 cmdlet，直至找到更佳解决方案。</span><span class="sxs-lookup"><span data-stu-id="b23ef-120">Due to the use of unsupported APIs, the following cmdlets have been removed from PowerShell Core until a better solution is found.</span></span>

- <span data-ttu-id="b23ef-121">Add-Computer</span><span class="sxs-lookup"><span data-stu-id="b23ef-121">Add-Computer</span></span>
- <span data-ttu-id="b23ef-122">Checkpoint-Computer</span><span class="sxs-lookup"><span data-stu-id="b23ef-122">Checkpoint-Computer</span></span>
- <span data-ttu-id="b23ef-123">Remove-Computer</span><span class="sxs-lookup"><span data-stu-id="b23ef-123">Remove-Computer</span></span>
- <span data-ttu-id="b23ef-124">Restore-Computer</span><span class="sxs-lookup"><span data-stu-id="b23ef-124">Restore-Computer</span></span>

### <a name="-counter-cmdlets"></a><span data-ttu-id="b23ef-125">`*-Counter` cmdlet</span><span class="sxs-lookup"><span data-stu-id="b23ef-125">`*-Counter` cmdlets</span></span>

<span data-ttu-id="b23ef-126">由于使用了不受支持的 API 而从 PowerShell Core 中删除 `*-Counter`，直至找到更佳解决方案。</span><span class="sxs-lookup"><span data-stu-id="b23ef-126">Due to the use of unsupported APIs, the `*-Counter` has been removed from PowerShell Core until a better solution is found.</span></span>

### <a name="-eventlog-cmdlets"></a><span data-ttu-id="b23ef-127">`*-EventLog` cmdlet</span><span class="sxs-lookup"><span data-stu-id="b23ef-127">`*-EventLog` cmdlets</span></span>

<span data-ttu-id="b23ef-128">由于使用了不受支持的 API 而从 PowerShell Core 中了删除 `*-EventLog`。</span><span class="sxs-lookup"><span data-stu-id="b23ef-128">Due to the use of unsupported APIs, the `*-EventLog` has been removed from PowerShell Core.</span></span> <span data-ttu-id="b23ef-129">直到找到更佳解决方案。</span><span class="sxs-lookup"><span data-stu-id="b23ef-129">until a better solution is found.</span></span> <span data-ttu-id="b23ef-130">`Get-WinEvent` 和 `Create-WinEvent` 可用于在 Windows 上获取和创建事件。</span><span class="sxs-lookup"><span data-stu-id="b23ef-130">`Get-WinEvent` and `Create-WinEvent` are available to get and create events on Windows.</span></span>

## <a name="enginelanguage-changes"></a><span data-ttu-id="b23ef-131">引擎/语言更改</span><span class="sxs-lookup"><span data-stu-id="b23ef-131">Engine/language changes</span></span>

### <a name="rename-powershellexe-to-pwshexe-5101httpsgithubcompowershellpowershellissues5101"></a><span data-ttu-id="b23ef-132">将 `powershell.exe` 重命名为 `pwsh.exe` [#5101](https://github.com/PowerShell/PowerShell/issues/5101)</span><span class="sxs-lookup"><span data-stu-id="b23ef-132">Rename `powershell.exe` to `pwsh.exe` [#5101](https://github.com/PowerShell/PowerShell/issues/5101)</span></span>

<span data-ttu-id="b23ef-133">为了向用户提供在 Windows 上调用 PowerShell Core（而不是 Windows PowerShell）的确定方法，PowerShell Core 二进制文件在 Windows 上已更改为 `pwsh.exe`，在非 Windows 平台上已更改为 `pwsh`。</span><span class="sxs-lookup"><span data-stu-id="b23ef-133">In order to give users a deterministic way to call PowerShell Core on Windows (as opposed to Windows PowerShell), the PowerShell Core binary was changed to `pwsh.exe` on Windows and `pwsh` on non-Windows platforms.</span></span>

<span data-ttu-id="b23ef-134">缩短的名称也与非 Windows 平台上 shell 的命名一致。</span><span class="sxs-lookup"><span data-stu-id="b23ef-134">The shortened name is also consistent with naming of shells on non-Windows platforms.</span></span>

### <a name="dont-insert-line-breaks-to-output-except-for-tables-5193httpsgithubcompowershellpowershellissues5193"></a><span data-ttu-id="b23ef-135">不要将换行符插入到输出（表除外）[#5193](https://github.com/PowerShell/PowerShell/issues/5193)</span><span class="sxs-lookup"><span data-stu-id="b23ef-135">Don't insert line breaks to output (except for tables) [#5193](https://github.com/PowerShell/PowerShell/issues/5193)</span></span>

<span data-ttu-id="b23ef-136">以前，输出与控制台的宽度对齐，并且在控制台的端宽度添加换行符，这意味着如果重新设置终端的大小，输出不会按预期重格式化。</span><span class="sxs-lookup"><span data-stu-id="b23ef-136">Previously, output was aligned to the width of the console and line breaks were added at the end width of the console, meaning the output didn't get reformatted as expected if the terminal was resized.</span></span> <span data-ttu-id="b23ef-137">这一更改不适用于表格，因为换行符是保持列对齐所必需的。</span><span class="sxs-lookup"><span data-stu-id="b23ef-137">This change was not applied to tables, as the line breaks are necessary to keep the columns aligned.</span></span>

### <a name="skip-null-element-check-for-collections-with-a-value-type-element-type-5432httpsgithubcompowershellpowershellissues5432"></a><span data-ttu-id="b23ef-138">对具有值类型元素类型的集合，跳过 null 元素检查 [#5432](https://github.com/PowerShell/PowerShell/issues/5432)</span><span class="sxs-lookup"><span data-stu-id="b23ef-138">Skip null-element check for collections with a value-type element type [#5432](https://github.com/PowerShell/PowerShell/issues/5432)</span></span>

<span data-ttu-id="b23ef-139">对于 `Mandatory` 参数及 `ValidateNotNull` 和 `ValidateNotNullOrEmpty` 属性，如果集合的元素类型是值类型，则跳过 null 元素检查。</span><span class="sxs-lookup"><span data-stu-id="b23ef-139">For the `Mandatory` parameter and `ValidateNotNull` and `ValidateNotNullOrEmpty` attributes, skip the null-element check if the collection's element type is value type.</span></span>

### <a name="change-outputencoding-to-use-utf-8-nobom-encoding-rather-than-ascii-5369httpsgithubcompowershellpowershellissues5369"></a><span data-ttu-id="b23ef-140">更改 `$OutputEncoding` 以使用 `UTF-8 NoBOM` 编码，而不使用 ASCII [#5369](https://github.com/PowerShell/PowerShell/issues/5369)</span><span class="sxs-lookup"><span data-stu-id="b23ef-140">Change `$OutputEncoding` to use `UTF-8 NoBOM` encoding rather than ASCII [#5369](https://github.com/PowerShell/PowerShell/issues/5369)</span></span>

<span data-ttu-id="b23ef-141">以前的编码 ASCII（7 位）在某些情况下会导致输出的错误更改。</span><span class="sxs-lookup"><span data-stu-id="b23ef-141">The previous encoding, ASCII (7-bit), would result in incorrect alteration of the output in some cases.</span></span> <span data-ttu-id="b23ef-142">此更改将使 `UTF-8 NoBOM` 成为默认设置，从而保留具有大多数工具和操作系统支持的编码的 Unicode 输出。</span><span class="sxs-lookup"><span data-stu-id="b23ef-142">This change is to make `UTF-8 NoBOM` default, which preserves Unicode output with an encoding supported by most tools and operating systems.</span></span>

### <a name="remove-allscope-from-most-default-aliases-5268httpsgithubcompowershellpowershellissues5268"></a><span data-ttu-id="b23ef-143">从大多数默认别名中删除 `AllScope` [#5268](https://github.com/PowerShell/PowerShell/issues/5268)</span><span class="sxs-lookup"><span data-stu-id="b23ef-143">Remove `AllScope` from most default aliases [#5268](https://github.com/PowerShell/PowerShell/issues/5268)</span></span>

<span data-ttu-id="b23ef-144">为了加快作用域创建，从大多数默认别名中删除了 `AllScope`。</span><span class="sxs-lookup"><span data-stu-id="b23ef-144">To speed up scope creation, `AllScope` was removed from most default aliases.</span></span> <span data-ttu-id="b23ef-145">保留 `AllScope` 供查找速度更快的几个常用别名使用。</span><span class="sxs-lookup"><span data-stu-id="b23ef-145">`AllScope` was left for a few frequently used aliases where the lookup was faster.</span></span>

### <a name="-verbose-and--debug-no-longer-overrides-erroractionpreference-5113httpsgithubcompowershellpowershellissues5113"></a><span data-ttu-id="b23ef-146">`-Verbose` 和 `-Debug` 不再替代 `$ErrorActionPreference` [#5113](https://github.com/PowerShell/PowerShell/issues/5113)</span><span class="sxs-lookup"><span data-stu-id="b23ef-146">`-Verbose` and `-Debug` no longer overrides `$ErrorActionPreference` [#5113](https://github.com/PowerShell/PowerShell/issues/5113)</span></span>

<span data-ttu-id="b23ef-147">以前，如果已指定 `-Verbose` 或 `-Debug`，则它会替代 `$ErrorActionPreference` 的行为。</span><span class="sxs-lookup"><span data-stu-id="b23ef-147">Previously, if `-Verbose` or `-Debug` were specified, it overrode the behavior of `$ErrorActionPreference`.</span></span> <span data-ttu-id="b23ef-148">进行此更改后，`-Verbose` 和 `-Debug` 不再影响 `$ErrorActionPreference` 的行为。</span><span class="sxs-lookup"><span data-stu-id="b23ef-148">With this change, `-Verbose` and `-Debug` no longer affect the behavior of `$ErrorActionPreference`.</span></span>

## <a name="cmdlet-changes"></a><span data-ttu-id="b23ef-149">Cmdlet 更改</span><span class="sxs-lookup"><span data-stu-id="b23ef-149">Cmdlet changes</span></span>

### <a name="invoke-restmethod-doesnt-return-useful-info-when-no-data-is-returned-5320httpsgithubcompowershellpowershellissues5320"></a><span data-ttu-id="b23ef-150">在没有返回任何数据时，Invoke-RestMethod 不返回有用的信息。</span><span class="sxs-lookup"><span data-stu-id="b23ef-150">Invoke-RestMethod doesn't return useful info when no data is returned.</span></span> [<span data-ttu-id="b23ef-151">#5320</span><span class="sxs-lookup"><span data-stu-id="b23ef-151">#5320</span></span>](https://github.com/PowerShell/PowerShell/issues/5320)

<span data-ttu-id="b23ef-152">当 API 仅返回 `null` 时，Invoke-RestMethod 将其序列化为字符串 `"null"`，而不是 `$null`。</span><span class="sxs-lookup"><span data-stu-id="b23ef-152">When an API returns just `null`, Invoke-RestMethod was serializing this as the string `"null"` instead of `$null`.</span></span> <span data-ttu-id="b23ef-153">此项更改修复了 `Invoke-RestMethod` 中的逻辑，以便将有效的单个值 JSON `null` 文本正确序列化为 `$null`。</span><span class="sxs-lookup"><span data-stu-id="b23ef-153">This change fixes the logic in `Invoke-RestMethod` to properly serialize a valid single value JSON `null` literal as `$null`.</span></span>

### <a name="remove--protocol-from--computer-cmdlets-5277httpsgithubcompowershellpowershellissues5277"></a><span data-ttu-id="b23ef-154">从 `*-Computer` cmdlet 中删除 `-Protocol` [#5277](https://github.com/PowerShell/PowerShell/issues/5277)</span><span class="sxs-lookup"><span data-stu-id="b23ef-154">Remove `-Protocol` from `*-Computer` cmdlets [#5277](https://github.com/PowerShell/PowerShell/issues/5277)</span></span>

<span data-ttu-id="b23ef-155">由于 CoreFX 中的 RPC 远程处理出现问题（特别是在非 Windows 平台上）以及为确保在 PowerShell 中获得一致的远程处理体验，已将 `-Protocol` 参数从 `\*-Computer` cmdlet 中删除。</span><span class="sxs-lookup"><span data-stu-id="b23ef-155">Due to issues with RPC remoting in CoreFX (particularly on non-Windows platforms) and ensuring a consistent remoting experience in PowerShell, the `-Protocol` parameter was removed from the `\*-Computer` cmdlets.</span></span> <span data-ttu-id="b23ef-156">远程处理功能不再支持 DCOM。</span><span class="sxs-lookup"><span data-stu-id="b23ef-156">DCOM is no longer supported for remoting.</span></span> <span data-ttu-id="b23ef-157">以下 cmdlet 仅支持 WSMAN 远程处理：</span><span class="sxs-lookup"><span data-stu-id="b23ef-157">The following cmdlets only support WSMAN remoting:</span></span>

- <span data-ttu-id="b23ef-158">Rename-Computer</span><span class="sxs-lookup"><span data-stu-id="b23ef-158">Rename-Computer</span></span>
- <span data-ttu-id="b23ef-159">Restart-Computer</span><span class="sxs-lookup"><span data-stu-id="b23ef-159">Restart-Computer</span></span>
- <span data-ttu-id="b23ef-160">Stop-Computer</span><span class="sxs-lookup"><span data-stu-id="b23ef-160">Stop-Computer</span></span>

### <a name="remove--computername-from--service-cmdlets-5090httpsgithubcompowershellpowershellissues5094"></a><span data-ttu-id="b23ef-161">从 `*-Service` cmdlet 中删除 `-ComputerName` [#5090](https://github.com/PowerShell/PowerShell/issues/5094)</span><span class="sxs-lookup"><span data-stu-id="b23ef-161">Remove `-ComputerName` from `*-Service` cmdlets [#5090](https://github.com/PowerShell/PowerShell/issues/5094)</span></span>

<span data-ttu-id="b23ef-162">为了鼓励一致地使用 PSRP，已将 `-ComputerName` 参数从 `*-Service` cmdlet 中删除。</span><span class="sxs-lookup"><span data-stu-id="b23ef-162">In order to encourage the consistent use of PSRP, the `-ComputerName` parameter was removed from `*-Service` cmdlets.</span></span>

### <a name="fix-get-item--literalpath-ab-if-ab-doesnt-actually-exist-to-return-error-5197httpsgithubcompowershellpowershellissues5197"></a><span data-ttu-id="b23ef-163">如果 `a*b` 实际上不存在，则修复 `Get-Item -LiteralPath a*b` 以返回错误 [#5197](https://github.com/PowerShell/PowerShell/issues/5197)</span><span class="sxs-lookup"><span data-stu-id="b23ef-163">Fix `Get-Item -LiteralPath a*b` if `a*b` doesn't actually exist to return error [#5197](https://github.com/PowerShell/PowerShell/issues/5197)</span></span>

<span data-ttu-id="b23ef-164">以前，给定通配符的 `-LiteralPath` 将其视为与 `-Path` 相同，如果该通配符未找到任何文件，则会以无提示方式退出。</span><span class="sxs-lookup"><span data-stu-id="b23ef-164">Previously, `-LiteralPath` given a wildcard would treat it the same as `-Path` and if the wildcard found no files, it would silently exit.</span></span> <span data-ttu-id="b23ef-165">正确的行为应该是 `-LiteralPath` 是文本，因此，如果文件不存在，它应显示错误。</span><span class="sxs-lookup"><span data-stu-id="b23ef-165">Correct behavior should be that `-LiteralPath` is literal so if the file doesn't exist, it should error.</span></span> <span data-ttu-id="b23ef-166">更改就是将与 `-Literal` 一起使用的通配符视作文本。</span><span class="sxs-lookup"><span data-stu-id="b23ef-166">Change is to treat wildcards used with `-Literal` as literal.</span></span>

### <a name="import-csv-should-apply-pstypenames-upon-import-when-type-information-is-present-in-the-csv-5134httpsgithubcompowershellpowershellissues5134"></a><span data-ttu-id="b23ef-167">当类型信息以 CSV 显示时，`Import-Csv` 应在导入时应用 `PSTypeNames` [#5134](https://github.com/PowerShell/PowerShell/issues/5134)</span><span class="sxs-lookup"><span data-stu-id="b23ef-167">`Import-Csv` should apply `PSTypeNames` upon import when type information is present in the CSV [#5134](https://github.com/PowerShell/PowerShell/issues/5134)</span></span>

<span data-ttu-id="b23ef-168">以前，使用 `Export-CSV` 导出的对象（带有使用 `ConvertFrom-Csv` 导入的 `TypeInformation`）已不保留类型信息。</span><span class="sxs-lookup"><span data-stu-id="b23ef-168">Previously, objects exported using `Export-CSV` with `TypeInformation` imported with `ConvertFrom-Csv` were not retaining the type information.</span></span> <span data-ttu-id="b23ef-169">此更改会将类型信息添加到 `PSTypeNames` 成员（若可从 CSV 文件中获得）。</span><span class="sxs-lookup"><span data-stu-id="b23ef-169">This change adds the type information to `PSTypeNames` member if available from the CSV file.</span></span>

### <a name="-notypeinformation-should-be-default-on-export-csv-5131httpsgithubcompowershellpowershellissues5131"></a><span data-ttu-id="b23ef-170">`-NoTypeInformation` 在 `Export-Csv` 上应为默认设置 [#5131](https://github.com/PowerShell/PowerShell/issues/5131)</span><span class="sxs-lookup"><span data-stu-id="b23ef-170">`-NoTypeInformation` should be default on `Export-Csv` [#5131](https://github.com/PowerShell/PowerShell/issues/5131)</span></span>

<span data-ttu-id="b23ef-171">此更改旨在解决客户对 `Export-CSV` 的默认行为的反馈，以包括类型信息。</span><span class="sxs-lookup"><span data-stu-id="b23ef-171">This change was made to address customer feedback on the default behavior of `Export-CSV` to include type information.</span></span>

<span data-ttu-id="b23ef-172">以前，该 cmdlet 将输出一条注释作为包含对象的类型名称的第一行。</span><span class="sxs-lookup"><span data-stu-id="b23ef-172">Previously, the cmdlet would output a comment as the first line containing the type name of the object.</span></span> <span data-ttu-id="b23ef-173">此更改是为了默认取消此行为，因为大多数工具不理解该行为。</span><span class="sxs-lookup"><span data-stu-id="b23ef-173">The change is to suppress this by default as it's not understood by most tools.</span></span> <span data-ttu-id="b23ef-174">使用 `-IncludeTypeInformation` 以保留以前的行为。</span><span class="sxs-lookup"><span data-stu-id="b23ef-174">Use `-IncludeTypeInformation` to retain the previous behavior.</span></span>

### <a name="web-cmdlets-should-warn-when--credential-is-sent-over-unencrypted-connections-5112httpsgithubcompowershellpowershellissues5112"></a><span data-ttu-id="b23ef-175">通过未加密的连接发送 `-Credential` 时，Web Cmdlet 应发出警告 [#5112](https://github.com/PowerShell/PowerShell/issues/5112)</span><span class="sxs-lookup"><span data-stu-id="b23ef-175">Web Cmdlets should warn when `-Credential` is sent over unencrypted connections [#5112](https://github.com/PowerShell/PowerShell/issues/5112)</span></span>

<span data-ttu-id="b23ef-176">使用 HTTP 时，包括密码在内的内容将以明文形式发送。</span><span class="sxs-lookup"><span data-stu-id="b23ef-176">When using HTTP, content including passwords are sent as clear-text.</span></span> <span data-ttu-id="b23ef-177">此更改默认不允许此操作，并且如果以不安全的方式传递凭据，则返回错误。</span><span class="sxs-lookup"><span data-stu-id="b23ef-177">This change is to not allow this by default and return an error if credentials are being passed in an insecure manner.</span></span> <span data-ttu-id="b23ef-178">用户可以使用 `-AllowUnencryptedAuthentication` 开关来绕过此操作。</span><span class="sxs-lookup"><span data-stu-id="b23ef-178">Users can bypass this by using the `-AllowUnencryptedAuthentication` switch.</span></span>

## <a name="api-changes"></a><span data-ttu-id="b23ef-179">API 更改</span><span class="sxs-lookup"><span data-stu-id="b23ef-179">API changes</span></span>

### <a name="remove-addtypecommandbase-class-5407httpsgithubcompowershellpowershellissues5407"></a><span data-ttu-id="b23ef-180">删除 `AddTypeCommandBase` 类 [#5407](https://github.com/PowerShell/PowerShell/issues/5407)</span><span class="sxs-lookup"><span data-stu-id="b23ef-180">Remove `AddTypeCommandBase` class [#5407](https://github.com/PowerShell/PowerShell/issues/5407)</span></span>

<span data-ttu-id="b23ef-181">从 `Add-Type` 删除 `AddTypeCommandBase` 类以提高性能。</span><span class="sxs-lookup"><span data-stu-id="b23ef-181">The `AddTypeCommandBase` class was removed from `Add-Type` to improve performance.</span></span> <span data-ttu-id="b23ef-182">此类仅供 Add-Type cmdlet 使用，不应影响用户。</span><span class="sxs-lookup"><span data-stu-id="b23ef-182">This class is only used by the Add-Type cmdlet and should not impact users.</span></span>

### <a name="unify-cmdlets-with-parameter--encoding-to-be-of-type-systemtextencoding-5080httpsgithubcompowershellpowershellissues5080"></a><span data-ttu-id="b23ef-183">将带有参数 `-Encoding` 的 cmdlet 统一为 `System.Text.Encoding` 类型 [#5080](https://github.com/PowerShell/PowerShell/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="b23ef-183">Unify cmdlets with parameter `-Encoding` to be of type `System.Text.Encoding` [#5080](https://github.com/PowerShell/PowerShell/issues/5080)</span></span>

<span data-ttu-id="b23ef-184">`-Encoding` 值 `Byte` 已从文件系统提供程序 cmdlet 中删除。</span><span class="sxs-lookup"><span data-stu-id="b23ef-184">The `-Encoding` value `Byte` has been removed from the filesystem provider cmdlets.</span></span> <span data-ttu-id="b23ef-185">新参数 `-AsByteStream` 现可用于指定需要一个字节流作为输入，或用于指定输出是一个字节流。</span><span class="sxs-lookup"><span data-stu-id="b23ef-185">A new parameter, `-AsByteStream`, is now used to specify that a byte stream is required as input or that the output is a stream of bytes.</span></span>

### <a name="add-better-error-message-for-empty-and-null--uformat-parameter-5055httpsgithubcompowershellpowershellissues5055"></a><span data-ttu-id="b23ef-186">为空和 null `-UFormat` 参数添加更好的错误消息 [#5055](https://github.com/PowerShell/PowerShell/issues/5055)</span><span class="sxs-lookup"><span data-stu-id="b23ef-186">Add better error message for empty and null `-UFormat` parameter [#5055](https://github.com/PowerShell/PowerShell/issues/5055)</span></span>

<span data-ttu-id="b23ef-187">以前，在将空格式字符串传递到 `-UFormat` 时，会出现毫无用处的错误消息。</span><span class="sxs-lookup"><span data-stu-id="b23ef-187">Previously, when passing an empty format string to `-UFormat`, an unhelpful error message would appear.</span></span> <span data-ttu-id="b23ef-188">已添加一个更具描述性的错误。</span><span class="sxs-lookup"><span data-stu-id="b23ef-188">A more descriptive error has been added.</span></span>

### <a name="clean-up-console-code-4995httpsgithubcompowershellpowershellissues4995"></a><span data-ttu-id="b23ef-189">清理控制台代码 [#4995](https://github.com/PowerShell/PowerShell/issues/4995)</span><span class="sxs-lookup"><span data-stu-id="b23ef-189">Clean up console code [#4995](https://github.com/PowerShell/PowerShell/issues/4995)</span></span>

<span data-ttu-id="b23ef-190">已删除以下功能，因为它们在 PowerShell Core 中不受支持，也没有计划添加支持，因为它们出于适用于 Windows PowerShell 旧版的原因而存在：`-psconsolefile` 开关和代码、`-importsystemmodules` 开关和代码以及字体更改代码。</span><span class="sxs-lookup"><span data-stu-id="b23ef-190">The following features were removed as they are not supported in PowerShell Core, and there are no plans to add support as they exist for legacy reasons for Windows PowerShell: `-psconsolefile` switch and code, `-importsystemmodules` switch and code, and font changing code.</span></span>

### <a name="removed-runspaceconfiguration-support-4942httpsgithubcompowershellpowershellissues4942"></a><span data-ttu-id="b23ef-191">已删除 `RunspaceConfiguration` 支持 [#4942](https://github.com/PowerShell/PowerShell/issues/4942)</span><span class="sxs-lookup"><span data-stu-id="b23ef-191">Removed `RunspaceConfiguration` support [#4942](https://github.com/PowerShell/PowerShell/issues/4942)</span></span>

<span data-ttu-id="b23ef-192">以前，在使用 API 以编程方式创建 PowerShell 运行空间时，可以使用旧版 [`RunspaceConfiguration`][runspaceconfig] 或较新的 [`InitialSessionState`][iss]。</span><span class="sxs-lookup"><span data-stu-id="b23ef-192">Previously, when creating a PowerShell runspace programmatically using the API you could use the legacy [`RunspaceConfiguration`][runspaceconfig] or the newer [`InitialSessionState`][iss].</span></span> <span data-ttu-id="b23ef-193">此更改不再支持 `RunspaceConfiguration` 并仅支持 `InitialSessionState`。</span><span class="sxs-lookup"><span data-stu-id="b23ef-193">This change removed support for `RunspaceConfiguration` and only supports `InitialSessionState`.</span></span>

[runspaceconfig]: https://docs.microsoft.com/dotnet/api/system.management.automation.runspaces.runspaceconfiguration
[iss]: https://docs.microsoft.com/dotnet/api/system.management.automation.runspaces.initialsessionstate

### <a name="commandinvocationintrinsicsinvokescript-bind-arguments-to-input-instead-of-args-4923httpsgithubcompowershellpowershellissues4923"></a><span data-ttu-id="b23ef-194">`CommandInvocationIntrinsics.InvokeScript` 将参数绑定到 `$input` 而不是 `$args` [#4923](https://github.com/PowerShell/PowerShell/issues/4923)</span><span class="sxs-lookup"><span data-stu-id="b23ef-194">`CommandInvocationIntrinsics.InvokeScript` bind arguments to `$input` instead of `$args` [#4923](https://github.com/PowerShell/PowerShell/issues/4923)</span></span>

<span data-ttu-id="b23ef-195">形参的位置不正确会导致将实参作为输入而不是实参进行传递。</span><span class="sxs-lookup"><span data-stu-id="b23ef-195">An incorrect position of a parameter resulted in the args passed as input instead of as args.</span></span>

### <a name="remove-unsupported--showwindow-switch-from-get-help-4903httpsgithubcompowershellpowershellissues4903"></a><span data-ttu-id="b23ef-196">从 `Get-Help` 中删除不受支持的 `-showwindow` 开关 [#4903](https://github.com/PowerShell/PowerShell/issues/4903)</span><span class="sxs-lookup"><span data-stu-id="b23ef-196">Remove unsupported `-showwindow` switch from `Get-Help` [#4903](https://github.com/PowerShell/PowerShell/issues/4903)</span></span>

<span data-ttu-id="b23ef-197">`-showwindow` 依赖于 WPF，这在 CoreCLR 上不受支持。</span><span class="sxs-lookup"><span data-stu-id="b23ef-197">`-showwindow` relies on WPF, which is not supported on CoreCLR.</span></span>

### <a name="allow--to-be-used-in-registry-path-for-remove-item-4866httpsgithubcompowershellpowershellissues4866"></a><span data-ttu-id="b23ef-198">允许为 `Remove-Item` 在注册表路径中使用 \* [#4866](https://github.com/PowerShell/PowerShell/issues/4866)</span><span class="sxs-lookup"><span data-stu-id="b23ef-198">Allow \* to be used in registry path for `Remove-Item` [#4866](https://github.com/PowerShell/PowerShell/issues/4866)</span></span>

<span data-ttu-id="b23ef-199">以前，给定通配符的 `-LiteralPath` 将其视为与 `-Path` 相同，如果该通配符未找到任何文件，则会以无提示方式退出。</span><span class="sxs-lookup"><span data-stu-id="b23ef-199">Previously, `-LiteralPath` given a wildcard would treat it the same as `-Path` and if the wildcard found no files, it would silently exit.</span></span> <span data-ttu-id="b23ef-200">正确的行为应该是 `-LiteralPath` 是文本，因此，如果文件不存在，它应显示错误。</span><span class="sxs-lookup"><span data-stu-id="b23ef-200">Correct behavior should be that `-LiteralPath` is literal so if the file doesn't exist, it should error.</span></span> <span data-ttu-id="b23ef-201">更改就是将与 `-Literal` 一起使用的通配符视作文本。</span><span class="sxs-lookup"><span data-stu-id="b23ef-201">Change is to treat wildcards used with `-Literal` as literal.</span></span>

### <a name="fix-set-service-failing-test-4802httpsgithubcompowershellpowershellissues4802"></a><span data-ttu-id="b23ef-202">修复 `Set-Service` 失败测试 [#4802](https://github.com/PowerShell/PowerShell/issues/4802)</span><span class="sxs-lookup"><span data-stu-id="b23ef-202">Fix `Set-Service` failing test [#4802](https://github.com/PowerShell/PowerShell/issues/4802)</span></span>

<span data-ttu-id="b23ef-203">以前，如果使用了 `New-Service -StartupType foo`，则忽略 `foo`，并使用一些默认的启动类型创建服务。</span><span class="sxs-lookup"><span data-stu-id="b23ef-203">Previously, if `New-Service -StartupType foo` was used, `foo` was ignored and the service was created with some default startup type.</span></span> <span data-ttu-id="b23ef-204">此更改是以显式方式来为无效启动类型引发错误。</span><span class="sxs-lookup"><span data-stu-id="b23ef-204">This change is to explicitly throw an error for an invalid startup type.</span></span>

### <a name="rename-isosx-to-ismacos-4700httpsgithubcompowershellpowershellissues4700"></a><span data-ttu-id="b23ef-205">将 `$IsOSX` 重命名为 `$IsMacOS` [#4700](https://github.com/PowerShell/PowerShell/issues/4700)</span><span class="sxs-lookup"><span data-stu-id="b23ef-205">Rename `$IsOSX` to `$IsMacOS` [#4700](https://github.com/PowerShell/PowerShell/issues/4700)</span></span>

<span data-ttu-id="b23ef-206">PowerShell 中的命名应与我们的命名保持一致，并符合 Apple 对 macOS 而不是 OSX 的使用。</span><span class="sxs-lookup"><span data-stu-id="b23ef-206">The naming in PowerShell should be consistent with our naming and conform to Apple's use of macOS instead of OSX.</span></span> <span data-ttu-id="b23ef-207">但是，出于可读性考虑，我们一直保持 Pascal 大小写格式。</span><span class="sxs-lookup"><span data-stu-id="b23ef-207">However, for readability and consistently we are staying with Pascal casing.</span></span>

### <a name="make-error-message-consistent-when-invalid-script-is-passed-to--file-better-error-when-passed-ambiguous-argument-4573httpsgithubcompowershellpowershellissues4573"></a><span data-ttu-id="b23ef-208">在将无效脚本传递到 -File 时，使错误消息保持一致，在传递不确定的参数时提示更好的错误 [#4573](https://github.com/PowerShell/PowerShell/issues/4573)</span><span class="sxs-lookup"><span data-stu-id="b23ef-208">Make error message consistent when invalid script is passed to -File, better error when passed ambiguous argument [#4573](https://github.com/PowerShell/PowerShell/issues/4573)</span></span>

<span data-ttu-id="b23ef-209">更改 `pwsh.exe` 的退出代码以与 Unix 约定保持一致</span><span class="sxs-lookup"><span data-stu-id="b23ef-209">Change the exit codes of `pwsh.exe` to align with Unix conventions</span></span>

### <a name="removal-of-localaccount-and-cmdlets-from--diagnostics-modules-4302httpsgithubcompowershellpowershellissues4302-4303httpsgithubcompowershellpowershellissues4303"></a><span data-ttu-id="b23ef-210">从 `Diagnostics` 模块删除 `LocalAccount` 和 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b23ef-210">Removal of `LocalAccount` and cmdlets from  `Diagnostics` modules.</span></span> <span data-ttu-id="b23ef-211">[#4302](https://github.com/PowerShell/PowerShell/issues/4302) [#4303](https://github.com/PowerShell/PowerShell/issues/4303)</span><span class="sxs-lookup"><span data-stu-id="b23ef-211">[#4302](https://github.com/PowerShell/PowerShell/issues/4302) [#4303](https://github.com/PowerShell/PowerShell/issues/4303)</span></span>

<span data-ttu-id="b23ef-212">由于不受支持的 API，会删除 `LocalAccounts` 模块和 `Diagnostics` 模块中的 `Counter` cmdlet，直到找到更好的解决方案。</span><span class="sxs-lookup"><span data-stu-id="b23ef-212">Due to unsupported APIs, the `LocalAccounts` module and the `Counter` cmdlets in the `Diagnostics` module were removed until a better solution is found.</span></span>

### <a name="executing-powershell-script-with-bool-parameter-does-not-work-4036httpsgithubcompowershellpowershellissues4036"></a><span data-ttu-id="b23ef-213">使用 bool 参数执行 PowerShell 脚本不起作用 [#4036](https://github.com/PowerShell/PowerShell/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="b23ef-213">Executing PowerShell script with bool parameter does not work [#4036](https://github.com/PowerShell/PowerShell/issues/4036)</span></span>

<span data-ttu-id="b23ef-214">以前，使用 powershell.exe  （现在使用 pwsh.exe  ）执行 PowerShell 脚本，使用 `-File` 无法将 `$true`/`$false` 作为参数值进行传递。</span><span class="sxs-lookup"><span data-stu-id="b23ef-214">Previously, using **powershell.exe** (now **pwsh.exe**) to execute a PowerShell script using `-File` provided no way to pass `$true`/`$false` as parameter values.</span></span> <span data-ttu-id="b23ef-215">添加了支持将 `$true`/`$false` 作为参数的解析值。</span><span class="sxs-lookup"><span data-stu-id="b23ef-215">Support for `$true`/`$false` as parsed values to parameters was added.</span></span> <span data-ttu-id="b23ef-216">由于当前记录的语法不起作用，也支持开关值。</span><span class="sxs-lookup"><span data-stu-id="b23ef-216">Switch values are also supported as currently documented syntax doesn't work.</span></span>

### <a name="remove-clrversion-property-from-psversiontable-4027httpsgithubcompowershellpowershellissues4027"></a><span data-ttu-id="b23ef-217">从 `$PSVersionTable` 删除 `ClrVersion` 属性 [#4027](https://github.com/PowerShell/PowerShell/issues/4027)</span><span class="sxs-lookup"><span data-stu-id="b23ef-217">Remove `ClrVersion` property from `$PSVersionTable` [#4027](https://github.com/PowerShell/PowerShell/issues/4027)</span></span>

<span data-ttu-id="b23ef-218">`$PSVersionTable` 的 `ClrVersion` 属性对 CoreCLR 用处不大，最终用户不应使用该值来确定兼容性。</span><span class="sxs-lookup"><span data-stu-id="b23ef-218">The `ClrVersion` property of `$PSVersionTable` is not useful with CoreCLR, end users should not be using that value to determine compatibility.</span></span>

### <a name="change-positional-parameter-for-powershellexe-from--command-to--file-4019httpsgithubcompowershellpowershellissues4019"></a><span data-ttu-id="b23ef-219">将 `powershell.exe` 的位置参数从 `-Command` 更改为 `-File` [#4019](https://github.com/PowerShell/PowerShell/issues/4019)</span><span class="sxs-lookup"><span data-stu-id="b23ef-219">Change positional parameter for `powershell.exe` from `-Command` to `-File` [#4019](https://github.com/PowerShell/PowerShell/issues/4019)</span></span>

<span data-ttu-id="b23ef-220">在非 Windows 平台上启用 PowerShell 的整个使用。</span><span class="sxs-lookup"><span data-stu-id="b23ef-220">Enable shebang use of PowerShell on non-Windows platforms.</span></span> <span data-ttu-id="b23ef-221">这意味着，在基于 Unix 的系统上，可以创建脚本可执行文件，以自动调用 PowerShell 而不是显式调用 `pwsh`。</span><span class="sxs-lookup"><span data-stu-id="b23ef-221">This means on Unix based systems, you can make a script executable that would invoke PowerShell automatically rather than explicitly invoking `pwsh`.</span></span> <span data-ttu-id="b23ef-222">这也意味着，现在可以执行诸如 `powershell foo.ps1` 或 `powershell fooScript` 的操作，而无需指定 `-File`。</span><span class="sxs-lookup"><span data-stu-id="b23ef-222">This also means that you can now do things like `powershell foo.ps1` or `powershell fooScript` without specifying `-File`.</span></span> <span data-ttu-id="b23ef-223">但是，此更改现在要求在尝试执行诸如 `powershell.exe Get-Command` 的操作时，显式指定 `-c` 或 `-Command`。</span><span class="sxs-lookup"><span data-stu-id="b23ef-223">However, this change now requires that you explicitly specify `-c` or `-Command` when trying to do things like `powershell.exe Get-Command`.</span></span>

### <a name="implement-unicode-escape-parsing-3958httpsgithubcompowershellpowershellissues3958"></a><span data-ttu-id="b23ef-224">实现 Unicode 转义分析 [#3958](https://github.com/PowerShell/PowerShell/issues/3958)</span><span class="sxs-lookup"><span data-stu-id="b23ef-224">Implement Unicode escape parsing [#3958](https://github.com/PowerShell/PowerShell/issues/3958)</span></span>

<span data-ttu-id="b23ef-225">将 `` `u####`` 或 `` `u{####}`` 转换为相应的 Unicode 字符。</span><span class="sxs-lookup"><span data-stu-id="b23ef-225">`` `u####`` or `` `u{####}`` is converted to the corresponding Unicode character.</span></span> <span data-ttu-id="b23ef-226">若要输出文本 `` `u``，转义反引号：``` ``u```。</span><span class="sxs-lookup"><span data-stu-id="b23ef-226">To output a literal `` `u``, escape the backtick: ``` ``u```.</span></span>

### <a name="change-new-modulemanifest-encoding-to-utf8nobom-on-non-windows-platforms-3940httpsgithubcompowershellpowershellissues3940"></a><span data-ttu-id="b23ef-227">在非 Windows 平台上将 `New-ModuleManifest` 编码更改为 `UTF8NoBOM` [#3940](https://github.com/PowerShell/PowerShell/issues/3940)</span><span class="sxs-lookup"><span data-stu-id="b23ef-227">Change `New-ModuleManifest` encoding to `UTF8NoBOM` on non-Windows platforms [#3940](https://github.com/PowerShell/PowerShell/issues/3940)</span></span>

<span data-ttu-id="b23ef-228">以前，`New-ModuleManifest` 创建带有 BOM 的 UTF-16 格式的 psd1 清单，这为 Linux 工具带来了一个问题。</span><span class="sxs-lookup"><span data-stu-id="b23ef-228">Previously, `New-ModuleManifest` creates psd1 manifests in UTF-16 with BOM, creating a problem for Linux tools.</span></span> <span data-ttu-id="b23ef-229">这一重大更改将 `New-ModuleManifest` 的编码更改为非 Windows 平台中的 UTF（无 BOM）。</span><span class="sxs-lookup"><span data-stu-id="b23ef-229">This breaking change changes the encoding of `New-ModuleManifest` to be UTF (no BOM) in non-Windows platforms.</span></span>

### <a name="prevent-get-childitem-from-recursing-into-symlinks-1875-3780httpsgithubcompowershellpowershellissues3780"></a><span data-ttu-id="b23ef-230">防止 `Get-ChildItem` 递归到符号链接中 (#1875)。</span><span class="sxs-lookup"><span data-stu-id="b23ef-230">Prevent `Get-ChildItem` from recursing into symlinks (#1875).</span></span> [<span data-ttu-id="b23ef-231">#3780</span><span class="sxs-lookup"><span data-stu-id="b23ef-231">#3780</span></span>](https://github.com/PowerShell/PowerShell/issues/3780)

<span data-ttu-id="b23ef-232">此更改使 `Get-ChildItem` 更符合 Unix `ls -r` 和 Windows `dir /s` 本机命令。</span><span class="sxs-lookup"><span data-stu-id="b23ef-232">This change brings `Get-ChildItem` more in line with the Unix `ls -r` and the Windows `dir /s` native commands.</span></span> <span data-ttu-id="b23ef-233">如上述命令一样，该 cmdlet 显示在递归期间找到的目录的符号链接，但不会递归到它们中。</span><span class="sxs-lookup"><span data-stu-id="b23ef-233">Like the mentioned commands, the cmdlet displays symbolic links to directories found during recursion, but does not recurse into them.</span></span>

### <a name="fix-get-content--delimiter-to-not-include-the-delimiter-in-the-returned-lines-3706httpsgithubcompowershellpowershellissues3706"></a><span data-ttu-id="b23ef-234">修复 `Get-Content -Delimiter` 以便不在返回的行中包含分隔符 [#3706](https://github.com/PowerShell/PowerShell/issues/3706)</span><span class="sxs-lookup"><span data-stu-id="b23ef-234">Fix `Get-Content -Delimiter` to not include the delimiter in the returned lines [#3706](https://github.com/PowerShell/PowerShell/issues/3706)</span></span>

<span data-ttu-id="b23ef-235">以前，使用 `Get-Content -Delimiter` 时的输出不一致且不方便，因为它需要进一步处理数据才能删除分隔符。</span><span class="sxs-lookup"><span data-stu-id="b23ef-235">Previously, the output while using `Get-Content -Delimiter` was inconsistent and inconvenient as it required further processing of the data to remove the delimiter.</span></span> <span data-ttu-id="b23ef-236">此更改删除返回行中的分隔符。</span><span class="sxs-lookup"><span data-stu-id="b23ef-236">This change removes the delimiter in returned lines.</span></span>

### <a name="implement-format-hex-in-c-3320httpsgithubcompowershellpowershellissues3320"></a><span data-ttu-id="b23ef-237">使用 C# 实现 Format-Hex [#3320](https://github.com/PowerShell/PowerShell/issues/3320)</span><span class="sxs-lookup"><span data-stu-id="b23ef-237">Implement Format-Hex in C# [#3320](https://github.com/PowerShell/PowerShell/issues/3320)</span></span>

<span data-ttu-id="b23ef-238">`-Raw` 参数现在是一个“no-op”（因为它不执行任何操作）。</span><span class="sxs-lookup"><span data-stu-id="b23ef-238">The `-Raw` parameter is now a "no-op" (in that it does nothing).</span></span> <span data-ttu-id="b23ef-239">今后，所有输出将显示数字的真实表示，其中包含其类型的所有字节（`-Raw` 参数在执行此更改之前正式执行的操作）。</span><span class="sxs-lookup"><span data-stu-id="b23ef-239">Going forward all of the output will be displayed with a true representation of numbers that includes all of the bytes for its type (what the `-Raw` parameter was formally doing prior to this change).</span></span>

### <a name="powershell-as-a-default-shell-doesnt-work-with-script-command-3319httpsgithubcompowershellpowershellissues3319"></a><span data-ttu-id="b23ef-240">作为默认 shell 的 PowerShell 对脚本命令不起作用 [#3319](https://github.com/PowerShell/PowerShell/issues/3319)</span><span class="sxs-lookup"><span data-stu-id="b23ef-240">PowerShell as a default shell doesn't work with script command [#3319](https://github.com/PowerShell/PowerShell/issues/3319)</span></span>

<span data-ttu-id="b23ef-241">在 Unix 上，对于交互式 shell 而言，shell 通常会接受 `-i`，许多工具都期待这一行为（例如，`script`，以及在将 PowerShell 设置为默认 shell 时），并使用 `-i` 开关来调用 shell。</span><span class="sxs-lookup"><span data-stu-id="b23ef-241">On Unix, it is a convention for shells to accept `-i` for an interactive shell and many tools expect this behavior (`script` for example, and when setting PowerShell as the default shell) and calls the shell with the `-i` switch.</span></span> <span data-ttu-id="b23ef-242">此更改具有突破性，因为 `-i` 以前可用作速记以匹配 `-inputformat`，它现在需要使用 `-in`。</span><span class="sxs-lookup"><span data-stu-id="b23ef-242">This change is breaking in that `-i` previously could be used as short hand to match `-inputformat`, which now needs to be `-in`.</span></span>

### <a name="typo-fix-in-get-computerinfo-property-name-3167httpsgithubcompowershellpowershellissues3167"></a><span data-ttu-id="b23ef-243">Get-ComputerInfo 属性名中的拼写错误修复 [#3167](https://github.com/PowerShell/PowerShell/issues/3167)</span><span class="sxs-lookup"><span data-stu-id="b23ef-243">Typo fix in Get-ComputerInfo property name [#3167](https://github.com/PowerShell/PowerShell/issues/3167)</span></span>

<span data-ttu-id="b23ef-244">`BiosSerialNumber` 被错误地拼写为 `BiosSeralNumber`，并被更改为正确的拼写。</span><span class="sxs-lookup"><span data-stu-id="b23ef-244">`BiosSerialNumber` was misspelled as `BiosSeralNumber` and has been changed to the correct spelling.</span></span>

### <a name="add-get-stringhash-and-get-filehash-cmdlets-3024httpsgithubcompowershellpowershellissues3024"></a><span data-ttu-id="b23ef-245">添加 `Get-StringHash` 和 `Get-FileHash` cmdlet [#3024](https://github.com/PowerShell/PowerShell/issues/3024)</span><span class="sxs-lookup"><span data-stu-id="b23ef-245">Add `Get-StringHash` and `Get-FileHash` cmdlets [#3024](https://github.com/PowerShell/PowerShell/issues/3024)</span></span>

<span data-ttu-id="b23ef-246">此更改是 CoreFX 不支持的一些哈希算法，因此它们将不再可用：</span><span class="sxs-lookup"><span data-stu-id="b23ef-246">This change is that some hash algorithms are not supported by CoreFX, therefore they are no longer available:</span></span>

- `MACTripleDES`
- `RIPEMD160`

### <a name="add-validation-on-get--cmdlets-where-passing-null-returns-all-objects-instead-of-error-2672httpsgithubcompowershellpowershellissues2672"></a><span data-ttu-id="b23ef-247">在传递 $null 返回所有对象而不是错误时在 `Get-*` cmdlet 上添加验证 [#2672](https://github.com/PowerShell/PowerShell/issues/2672)</span><span class="sxs-lookup"><span data-stu-id="b23ef-247">Add validation on `Get-*` cmdlets where passing $null returns all objects instead of error [#2672](https://github.com/PowerShell/PowerShell/issues/2672)</span></span>

<span data-ttu-id="b23ef-248">将 `$null` 传递给以下任何项，现在会引发错误：</span><span class="sxs-lookup"><span data-stu-id="b23ef-248">Passing `$null` to any of the following now throws an error:</span></span>

- `Get-Credential -UserName`
- `Get-Event -SourceIdentifier`
- `Get-EventSubscriber -SourceIdentifier`
- `Get-Help -Name`
- `Get-PSBreakpoint -Script`
- `Get-PSProvider -PSProvider`
- `Get-PSSessionConfiguration -Name`
- `Get-PSSnapin -Name`
- `Get-Runspace -Name`
- `Get-RunspaceDebug -RunspaceName`
- `Get-Service -Name`
- `Get-TraceSource -Name`
- `Get-Variable -Name`
- `Get-WmiObject -Class`
- `Get-WmiObject -Property`

### <a name="add-support-w3c-extended-log-file-format-in-import-csv-2482httpsgithubcompowershellpowershellissues2482"></a><span data-ttu-id="b23ef-249">在 `Import-Csv` 中添加支持 W3C 扩展日志文件格式 [#2482](https://github.com/PowerShell/PowerShell/issues/2482)</span><span class="sxs-lookup"><span data-stu-id="b23ef-249">Add support W3C Extended Log File Format in `Import-Csv` [#2482](https://github.com/PowerShell/PowerShell/issues/2482)</span></span>

<span data-ttu-id="b23ef-250">以前，`Import-Csv` cmdlet 不能用于直接导入采用 W3C 扩展日志格式的日志文件，并且需要执行其他操作。</span><span class="sxs-lookup"><span data-stu-id="b23ef-250">Previously, the `Import-Csv` cmdlet cannot be used to directly import the log files in W3C extended log format and additional action would be required.</span></span> <span data-ttu-id="b23ef-251">进行此更改后，支持 W3C 扩展日志格式。</span><span class="sxs-lookup"><span data-stu-id="b23ef-251">With this change, W3C extended log format is supported.</span></span>

### <a name="parameter-binding-problem-with-valuefromremainingarguments-in-ps-functions-2035httpsgithubcompowershellpowershellissues2035"></a><span data-ttu-id="b23ef-252">PS 函数中 `ValueFromRemainingArguments` 的参数绑定问题 [#2035](https://github.com/PowerShell/PowerShell/issues/2035)</span><span class="sxs-lookup"><span data-stu-id="b23ef-252">Parameter binding problem with `ValueFromRemainingArguments` in PS functions [#2035](https://github.com/PowerShell/PowerShell/issues/2035)</span></span>

<span data-ttu-id="b23ef-253">`ValueFromRemainingArguments` 现在返回一些值作为数组，而不是本身是数组的单个值。</span><span class="sxs-lookup"><span data-stu-id="b23ef-253">`ValueFromRemainingArguments` now returns the values as an array instead of a single value which itself is an array.</span></span>

### <a name="buildversion-is-removed-from-psversiontable-1415httpsgithubcompowershellpowershellissues1415"></a><span data-ttu-id="b23ef-254">从 `$PSVersionTable` 中删除 `BuildVersion` [#1415](https://github.com/PowerShell/PowerShell/issues/1415)</span><span class="sxs-lookup"><span data-stu-id="b23ef-254">`BuildVersion` is removed from `$PSVersionTable` [#1415](https://github.com/PowerShell/PowerShell/issues/1415)</span></span>

<span data-ttu-id="b23ef-255">从 `$PSVersionTable` 中删除 `BuildVersion` 属性。</span><span class="sxs-lookup"><span data-stu-id="b23ef-255">Remove the `BuildVersion` property from `$PSVersionTable`.</span></span> <span data-ttu-id="b23ef-256">此属性与 Windows 内部版本相关。</span><span class="sxs-lookup"><span data-stu-id="b23ef-256">This property was tied to the Windows build version.</span></span> <span data-ttu-id="b23ef-257">我们建议使用 `GitCommitId` 检索 PowerShell Core 的确切内部版本。</span><span class="sxs-lookup"><span data-stu-id="b23ef-257">Instead, we recommend that you use `GitCommitId` to retrieve the exact build version of PowerShell Core.</span></span>

### <a name="changes-to-web-cmdlets"></a><span data-ttu-id="b23ef-258">对 Web Cmdlet 的更改</span><span class="sxs-lookup"><span data-stu-id="b23ef-258">Changes to Web Cmdlets</span></span>

<span data-ttu-id="b23ef-259">Web Cmdlet 的基础 .NET API 已更改为 `System.Net.Http.HttpClient`。</span><span class="sxs-lookup"><span data-stu-id="b23ef-259">The underlying .NET API of the Web Cmdlets has been changed to `System.Net.Http.HttpClient`.</span></span> <span data-ttu-id="b23ef-260">此更改提供了许多好处。</span><span class="sxs-lookup"><span data-stu-id="b23ef-260">This change provides many benefits.</span></span> <span data-ttu-id="b23ef-261">但是，此更改以及缺乏与 Internet Explorer 的互操作性导致了 `Invoke-WebRequest` 和 `Invoke-RestMethod` 中的几次重大更改。</span><span class="sxs-lookup"><span data-stu-id="b23ef-261">However, this change along with a lack of interoperability with Internet Explorer have resulted in several breaking changes within `Invoke-WebRequest` and `Invoke-RestMethod`.</span></span>

- <span data-ttu-id="b23ef-262">`Invoke-WebRequest` 现在仅支持基本 HTML 分析。</span><span class="sxs-lookup"><span data-stu-id="b23ef-262">`Invoke-WebRequest` now supports basic HTML Parsing only.</span></span> <span data-ttu-id="b23ef-263">`Invoke-WebRequest` 始终返回一个 `BasicHtmlWebResponseObject` 对象。</span><span class="sxs-lookup"><span data-stu-id="b23ef-263">`Invoke-WebRequest` always returns a `BasicHtmlWebResponseObject` object.</span></span> <span data-ttu-id="b23ef-264">已删除 `ParsedHtml` 和 `Forms` 属性。</span><span class="sxs-lookup"><span data-stu-id="b23ef-264">The `ParsedHtml` and `Forms` properties have been removed.</span></span>
- <span data-ttu-id="b23ef-265">`BasicHtmlWebResponseObject.Headers` 值现在是 `String[]` 而不是 `String`。</span><span class="sxs-lookup"><span data-stu-id="b23ef-265">`BasicHtmlWebResponseObject.Headers` values are now `String[]` instead of `String`.</span></span>
- <span data-ttu-id="b23ef-266">`BasicHtmlWebResponseObject.BaseResponse` 现在是一个 `System.Net.Http.HttpResponseMessage` 对象。</span><span class="sxs-lookup"><span data-stu-id="b23ef-266">`BasicHtmlWebResponseObject.BaseResponse` is now a `System.Net.Http.HttpResponseMessage` object.</span></span>
- <span data-ttu-id="b23ef-267">Web Cmdlet 异常上的 `Response` 属性现在是一个 `System.Net.Http.HttpResponseMessage` 对象。</span><span class="sxs-lookup"><span data-stu-id="b23ef-267">The `Response` property on Web Cmdlet exceptions is now a `System.Net.Http.HttpResponseMessage` object.</span></span>
- <span data-ttu-id="b23ef-268">对于 `-Headers` 和 `-UserAgent` 参数，严格的 RFC 标头分析是默认设置。</span><span class="sxs-lookup"><span data-stu-id="b23ef-268">Strict RFC header parsing is now default for the `-Headers` and `-UserAgent` parameter.</span></span> <span data-ttu-id="b23ef-269">这可以使用 `-SkipHeaderValidation` 绕过。</span><span class="sxs-lookup"><span data-stu-id="b23ef-269">This can be bypassed with `-SkipHeaderValidation`.</span></span>
- <span data-ttu-id="b23ef-270">不再支持 `file://` 和 `ftp://` URI 方案。</span><span class="sxs-lookup"><span data-stu-id="b23ef-270">`file://` and `ftp://` URI schemes are no longer supported.</span></span>
- <span data-ttu-id="b23ef-271">不再采用 `System.Net.ServicePointManager` 设置。</span><span class="sxs-lookup"><span data-stu-id="b23ef-271">`System.Net.ServicePointManager` settings are no longer honored.</span></span>
- <span data-ttu-id="b23ef-272">目前在 macOS 上尚无基于证书的身份验证。</span><span class="sxs-lookup"><span data-stu-id="b23ef-272">There is currently no certificate based authentication available on macOS.</span></span>
- <span data-ttu-id="b23ef-273">通过 `http://` URI 使用 `-Credential` 将导致错误。</span><span class="sxs-lookup"><span data-stu-id="b23ef-273">Use of `-Credential` over an `http://` URI will result in an error.</span></span> <span data-ttu-id="b23ef-274">使用 `https://` URI 或提供 `-AllowUnencryptedAuthentication` 参数来阻止此错误。</span><span class="sxs-lookup"><span data-stu-id="b23ef-274">Use an `https://` URI or supply the `-AllowUnencryptedAuthentication` parameter to suppress the error.</span></span>
- <span data-ttu-id="b23ef-275">现在当重定向尝试超过提供的限制时，`-MaximumRedirection` 会生成终止错误时，而不是返回最后一次重定向的结果。</span><span class="sxs-lookup"><span data-stu-id="b23ef-275">`-MaximumRedirection` now produces a terminating error when redirection attempts exceed the provided limit instead of returning the results of the last redirection.</span></span>
