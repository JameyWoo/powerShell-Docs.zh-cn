---
title: 创建自定义控件 |Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c3baa406-cd33-4420-be5a-07ef09d93480
caps.latest.revision: 8
ms.openlocfilehash: 3504ab1d974c55e9279172d0e851961474ccb926
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72363376"
---
# <a name="creating-custom-controls"></a><span data-ttu-id="166dd-102">创建自定义控件</span><span class="sxs-lookup"><span data-stu-id="166dd-102">Creating Custom Controls</span></span>

<span data-ttu-id="166dd-103">自定义控件是最灵活的格式设置文件组件。</span><span class="sxs-lookup"><span data-stu-id="166dd-103">Custom controls are the most flexible components of a formatting file.</span></span> <span data-ttu-id="166dd-104">与定义数据的正式结构的表、列表和宽视图（如数据表）不同，自定义控件允许您定义单个数据片段的显示方式。</span><span class="sxs-lookup"><span data-stu-id="166dd-104">Unlike table, list, and wide views that define a formal structure of data, such as a table of data, custom controls allow you to define how an individual piece of data is displayed.</span></span> <span data-ttu-id="166dd-105">您可以定义一组公共自定义控件，这些控件可供格式设置文件的所有视图使用，您可以定义可用于特定视图的自定义控件，也可以定义一组可用于一组对象的控件。</span><span class="sxs-lookup"><span data-stu-id="166dd-105">You can define a common set of custom controls that are available to all the views of the formatting file, you can define custom controls that are available to a specific view, or you can define a set of controls that are available to a group of objects.</span></span>

## <a name="custom-control-example"></a><span data-ttu-id="166dd-106">自定义控件示例</span><span class="sxs-lookup"><span data-stu-id="166dd-106">Custom Control Example</span></span>

<span data-ttu-id="166dd-107">下面的示例显示了 types.ps1xml 文件中定义的自定义控件。</span><span class="sxs-lookup"><span data-stu-id="166dd-107">The following example shows a custom control that is defined in the Certificates.Format.ps1xml file.</span></span> <span data-ttu-id="166dd-108">此自定义控件用于分隔在表视图中显示的[system.object](/dotnet/api/System.Management.Automation.Signature)对象。</span><span class="sxs-lookup"><span data-stu-id="166dd-108">This custom control is used to separate the [System.Management.Automation.Signature](/dotnet/api/System.Management.Automation.Signature) objects displayed in a table view.</span></span>

```xml
<Controls>
  <Control>
    <Name>SignatureTypes-GroupingFormat</Name>
    <CustomControl>
      <CustomEntries>
        <CustomEntry>
          <CustomItem>
            <Frame>
              <LeftIndent>4</LeftIndent>
              <CustomItem>
                <Text AssemblyName="System.Management.Automation" BaseName="FileSystemProviderStrings"
                  ResourceId="DirectoryDisplayGrouping"/>
                <ExpressionBinding>
                  <ScriptBlock>split-path $_.Path</ScriptBlock>
                </ExpressionBinding>
                <NewLine/>
              </CustomItem>
            </Frame>
          </CustomItem>
        </CustomEntry>
      </CustomEntries>
    </CustomControl>
  </Control>
</Controls>

```

## <a name="see-also"></a><span data-ttu-id="166dd-109">另请参阅</span><span class="sxs-lookup"><span data-stu-id="166dd-109">See Also</span></span>

[<span data-ttu-id="166dd-110">编写 PowerShell 格式化文件</span><span class="sxs-lookup"><span data-stu-id="166dd-110">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
