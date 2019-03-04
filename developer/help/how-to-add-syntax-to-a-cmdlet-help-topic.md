---
title: 如何将语法添加到 Cmdlet 帮助主题 |Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d0c6d03f-1c1a-43d8-928e-e3290e90e0bc
caps.latest.revision: 5
ms.openlocfilehash: 947d0c0188df5bba3a9fb617fe5abf0b3b28eb51
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2019
ms.locfileid: "56857993"
---
# <a name="how-to-add-syntax-to-a-cmdlet-help-topic"></a><span data-ttu-id="0eaad-102">如何向 Cmdlet 帮助主题添加语法</span><span class="sxs-lookup"><span data-stu-id="0eaad-102">How to Add Syntax to a Cmdlet Help Topic</span></span>

- [<span data-ttu-id="0eaad-103">参数特性</span><span class="sxs-lookup"><span data-stu-id="0eaad-103">Parameter Attributes</span></span>](#Parameter-Attributes)

- [<span data-ttu-id="0eaad-104">参数值属性</span><span class="sxs-lookup"><span data-stu-id="0eaad-104">Parameter Value Attributes</span></span>](#Parameter-Value-Attributes)

- [<span data-ttu-id="0eaad-105">正在收集语法信息</span><span class="sxs-lookup"><span data-stu-id="0eaad-105">Gathering Syntax Information</span></span>](#Gathering-Syntax-Information)

- [<span data-ttu-id="0eaad-106">编码 XML 的语法关系图</span><span class="sxs-lookup"><span data-stu-id="0eaad-106">Coding the Syntax Diagram XML</span></span>](#Coding-the-Syntax-Diagram-XML)

## <a name="things-to-know-about-the-syntax-diagram-in-cmdlet-help"></a><span data-ttu-id="0eaad-107">若要了解的 Cmdlet 帮助中的语法关系图的内容</span><span class="sxs-lookup"><span data-stu-id="0eaad-107">Things to Know About the Syntax Diagram in Cmdlet Help</span></span>

<span data-ttu-id="0eaad-108">在开始编写 cmdlet 帮助文件中的语法关系图的 XML 的代码之前，阅读此部分，获取清楚地了解你需要提供的数据，如参数属性和该数据的语法关系图中的显示方式的类型...</span><span class="sxs-lookup"><span data-stu-id="0eaad-108">Before you start to code the XML for the syntax diagram in the cmdlet Help file, read this section to get a clear picture of the kind of data you need to provide, such as the parameter attributes, and how that data is displayed in the syntax diagram..</span></span>

### <a name="parameter-attributes"></a><span data-ttu-id="0eaad-109">参数特性</span><span class="sxs-lookup"><span data-stu-id="0eaad-109">Parameter Attributes</span></span>

- <span data-ttu-id="0eaad-110">必需</span><span class="sxs-lookup"><span data-stu-id="0eaad-110">Required</span></span>

  - <span data-ttu-id="0eaad-111">如果为 true，该参数必须出现在使用参数集的所有命令。</span><span class="sxs-lookup"><span data-stu-id="0eaad-111">If true, the parameter must appear in all commands that use the parameter set.</span></span>

  - <span data-ttu-id="0eaad-112">如果为 false，则该参数是可选的参数集的所有命令。</span><span class="sxs-lookup"><span data-stu-id="0eaad-112">If false, the parameter is optional in all commands that use the parameter set.</span></span>

- <span data-ttu-id="0eaad-113">位置</span><span class="sxs-lookup"><span data-stu-id="0eaad-113">Position</span></span>

  - <span data-ttu-id="0eaad-114">如果名为，则需要参数名称。</span><span class="sxs-lookup"><span data-stu-id="0eaad-114">If named, the parameter name is required.</span></span>

  - <span data-ttu-id="0eaad-115">如果位置，参数名称是可选的。</span><span class="sxs-lookup"><span data-stu-id="0eaad-115">If positional, the parameter name is optional.</span></span> <span data-ttu-id="0eaad-116">如果省略，参数值必须在命令中指定的位置。</span><span class="sxs-lookup"><span data-stu-id="0eaad-116">When it is omitted, the parameter value must be in the specified position in the command.</span></span> <span data-ttu-id="0eaad-117">例如，如果值为位置 ="1"，参数值必须是第一个或唯一未命名的命令中的参数值。</span><span class="sxs-lookup"><span data-stu-id="0eaad-117">For example, if the value is position="1", the parameter value must be the first or only unnamed parameter value in the command.</span></span>

- <span data-ttu-id="0eaad-118">管道输入</span><span class="sxs-lookup"><span data-stu-id="0eaad-118">Pipeline Input</span></span>

  - <span data-ttu-id="0eaad-119">如果为 true (ByValue)，您可以通过管道将传递的参数输入。</span><span class="sxs-lookup"><span data-stu-id="0eaad-119">If true (ByValue), you can pipe input to the parameter.</span></span> <span data-ttu-id="0eaad-120">输入是关联 （"绑定到"） 与即使属性名称和对象类型与预期的类型不匹配的参数。</span><span class="sxs-lookup"><span data-stu-id="0eaad-120">The input is associated with ("bound to") the parameter even if the property name and the object type do not match the expected type.</span></span> <span data-ttu-id="0eaad-121">Windows PowerShell 中？参数绑定组件尝试将输入转换为正确的类型，并且仅当无法将类型转换时失败命令。</span><span class="sxs-lookup"><span data-stu-id="0eaad-121">The Windows PowerShell? parameter binding components try to convert the input to the correct type and fail the command only when the type cannot be converted.</span></span> <span data-ttu-id="0eaad-122">中的参数集只有一个参数可以按值相关联。</span><span class="sxs-lookup"><span data-stu-id="0eaad-122">Only one parameter in a parameter set can be associated by value.</span></span>

  - <span data-ttu-id="0eaad-123">如果为 true (ByPropertyName)，您可以通过管道将传递的参数输入。</span><span class="sxs-lookup"><span data-stu-id="0eaad-123">If true (ByPropertyName), you can pipe input to the parameter.</span></span> <span data-ttu-id="0eaad-124">但是，输入是属性的与参数关联，仅当该参数名称匹配的输入对象名称。</span><span class="sxs-lookup"><span data-stu-id="0eaad-124">However, the input is associated with the parameter only when the parameter name matches the name of a property of the input object.</span></span> <span data-ttu-id="0eaad-125">例如，如果参数名称为`Path`，仅当该对象具有名为路径的属性时，通过管道输送到 cmdlet 的对象是与该参数相关联。</span><span class="sxs-lookup"><span data-stu-id="0eaad-125">For example, if the parameter name is `Path`, objects piped to the cmdlet are associated with that parameter only when the object has a property named path.</span></span>

  - <span data-ttu-id="0eaad-126">如果 true （ByValue、 ByPropertyName），可以通过管道传递的参数输入属性名称或值。</span><span class="sxs-lookup"><span data-stu-id="0eaad-126">If true (ByValue, ByPropertyName), you can pipe input to the parameter either by property name or by value.</span></span> <span data-ttu-id="0eaad-127">中的参数集只有一个参数可以按值相关联。</span><span class="sxs-lookup"><span data-stu-id="0eaad-127">Only one parameter in a parameter set can be associated by value.</span></span>

  - <span data-ttu-id="0eaad-128">如果为 false，你不能通过管道传递给此参数的输入。</span><span class="sxs-lookup"><span data-stu-id="0eaad-128">If false, you cannot pipe input to this parameter.</span></span>

- <span data-ttu-id="0eaad-129">通配</span><span class="sxs-lookup"><span data-stu-id="0eaad-129">Globbing</span></span>

  - <span data-ttu-id="0eaad-130">如果为 true，用户键入的参数值的文本可以包含通配符字符。</span><span class="sxs-lookup"><span data-stu-id="0eaad-130">If true, the text that the user types for the parameter value can include wildcard characters.</span></span>

  - <span data-ttu-id="0eaad-131">如果为 false，用户键入的参数值的文本不能包含通配符字符。</span><span class="sxs-lookup"><span data-stu-id="0eaad-131">If false, the text that the user types for the parameter value cannot include wildcard characters.</span></span>

### <a name="parameter-value-attributes"></a><span data-ttu-id="0eaad-132">参数值属性</span><span class="sxs-lookup"><span data-stu-id="0eaad-132">Parameter Value Attributes</span></span>

- <span data-ttu-id="0eaad-133">必需</span><span class="sxs-lookup"><span data-stu-id="0eaad-133">Required</span></span>

  - <span data-ttu-id="0eaad-134">如果为 true，只要在命令中使用参数，就必须使用指定的值。</span><span class="sxs-lookup"><span data-stu-id="0eaad-134">If true, the specified value must be used whenever using the parameter in a command.</span></span>

  - <span data-ttu-id="0eaad-135">如果为 false，则参数值是可选的。</span><span class="sxs-lookup"><span data-stu-id="0eaad-135">If false, the parameter value is optional.</span></span> <span data-ttu-id="0eaad-136">通常情况下，值是可选的仅当它是一个多个有效的值对于参数，如枚举类型中。</span><span class="sxs-lookup"><span data-stu-id="0eaad-136">Typically, a value is optional only when it is one of several valid values for a parameter, such as in an enumerated type.</span></span>

<span data-ttu-id="0eaad-137">参数值的必需的特性是参数的不同的必需属性。</span><span class="sxs-lookup"><span data-stu-id="0eaad-137">The Required attribute of a parameter value is different from the Required attribute of a parameter.</span></span>

<span data-ttu-id="0eaad-138">参数的所需的属性指示是否参数 （和其值） 时必须包括调用该 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0eaad-138">The required attribute of a parameter indicates whether the parameter (and its value) must be included when invoking the cmdlet.</span></span> <span data-ttu-id="0eaad-139">与此相反，仅当该参数包含在命令中使用的参数值的必需的属性。</span><span class="sxs-lookup"><span data-stu-id="0eaad-139">In contrast, the required attribute of a parameter value is used only when the parameter is included in the command.</span></span> <span data-ttu-id="0eaad-140">它指示是否必须与参数一起使用该特定值。</span><span class="sxs-lookup"><span data-stu-id="0eaad-140">It indicates whether that particular value must be used with the parameter.</span></span>

<span data-ttu-id="0eaad-141">通常情况下，占位符的参数值是必需的和文本的参数值不是必需的因为它们可能与参数一起使用的多个值之一。</span><span class="sxs-lookup"><span data-stu-id="0eaad-141">Typically, parameter values that are placeholders are required and parameter values that are literal are not required, because they are one of several values that might be used with the parameter.</span></span>

### <a name="gathering-syntax-information"></a><span data-ttu-id="0eaad-142">正在收集语法信息</span><span class="sxs-lookup"><span data-stu-id="0eaad-142">Gathering Syntax Information</span></span>

1. <span data-ttu-id="0eaad-143">启动 cmdlet 名称。</span><span class="sxs-lookup"><span data-stu-id="0eaad-143">Start with the cmdlet name.</span></span>

   ```
   SYNTAX
       Get-Tech
   ```

2. <span data-ttu-id="0eaad-144">列出所有 cmdlet 的参数。</span><span class="sxs-lookup"><span data-stu-id="0eaad-144">List all the parameters of the cmdlet.</span></span> <span data-ttu-id="0eaad-145">键入短划线 （也称为"短划线"或"减号"(ASCII 45) 之前每个参数名称。</span><span class="sxs-lookup"><span data-stu-id="0eaad-145">Type a dash (also known as a "dash" or "minus sign" (ASCII 45) before each parameter name.</span></span> <span data-ttu-id="0eaad-146">为参数集 （某些 cmdlet 可能必须只有一个参数设置） 分隔参数。</span><span class="sxs-lookup"><span data-stu-id="0eaad-146">Separate the parameters into parameter sets (some cmdlets may have only one parameter set).</span></span> <span data-ttu-id="0eaad-147">在此示例中获取技术 cmdlet 具有两个参数集。</span><span class="sxs-lookup"><span data-stu-id="0eaad-147">In this example the Get-Tech cmdlet has two parameter sets.</span></span>

   ```
   SYNTAX
       Get-Tech -name -type
       Get-Tech -ID -list -type
   ```

   <span data-ttu-id="0eaad-148">开始使用 cmdlet 名称设置每个参数。</span><span class="sxs-lookup"><span data-stu-id="0eaad-148">Start each parameter set with the cmdlet name.</span></span>

   <span data-ttu-id="0eaad-149">列出首先设置的默认参数。</span><span class="sxs-lookup"><span data-stu-id="0eaad-149">List the default parameter set first.</span></span> <span data-ttu-id="0eaad-150">通过在 cmdlet 类指定默认参数。</span><span class="sxs-lookup"><span data-stu-id="0eaad-150">The default parameter is specified by the cmdlet class.</span></span>

   <span data-ttu-id="0eaad-151">对于每个参数集，列出其唯一参数，除非必须首先出现的位置参数。</span><span class="sxs-lookup"><span data-stu-id="0eaad-151">For each parameter set, list its unique parameter first, unless there are positional parameters that must appear first.</span></span> <span data-ttu-id="0eaad-152">在上一示例中，名称和 ID 参数是两个参数集的唯一参数 （每个参数集必须具有一个参数，它仅适用于该参数集）。</span><span class="sxs-lookup"><span data-stu-id="0eaad-152">In the previous example, the Name and ID parameters are unique parameters for the two parameter sets (each parameter set must have one parameter that is unique to that parameter set).</span></span> <span data-ttu-id="0eaad-153">这使用户更轻松地识别它们需要为参数提供哪些参数设置。</span><span class="sxs-lookup"><span data-stu-id="0eaad-153">This makes it easier for users to identify what parameter they need to supply for the parameter set.</span></span>

   <span data-ttu-id="0eaad-154">列表应出现在命令中的顺序中的参数。</span><span class="sxs-lookup"><span data-stu-id="0eaad-154">List the parameters in the order that they should appear in the command.</span></span> <span data-ttu-id="0eaad-155">如果顺序不重要，将相关的参数列在一起，或者首先列出最常用的参数。</span><span class="sxs-lookup"><span data-stu-id="0eaad-155">If the order does not matter, list related parameters together, or list the most frequently used parameters first.</span></span>

   <span data-ttu-id="0eaad-156">请确保如果该 cmdlet 支持 ShouldProcess 列出 WhatIf 和 Confirm 参数。</span><span class="sxs-lookup"><span data-stu-id="0eaad-156">Be sure to list the WhatIf and Confirm parameters if the cmdlet supports ShouldProcess.</span></span>

   <span data-ttu-id="0eaad-157">待办事项列表在语法关系图中的常见参数 （如 Verbose、 Debug 和 ErrorAction）。</span><span class="sxs-lookup"><span data-stu-id="0eaad-157">Do not list the common parameters (such as Verbose, Debug, and ErrorAction) in your syntax diagram.</span></span> <span data-ttu-id="0eaad-158">`Get-Help` Cmdlet 将添加你的该信息时显示的帮助主题。</span><span class="sxs-lookup"><span data-stu-id="0eaad-158">The `Get-Help` cmdlet adds that information for you when it displays the Help topic.</span></span>

3. <span data-ttu-id="0eaad-159">添加参数的值。</span><span class="sxs-lookup"><span data-stu-id="0eaad-159">Add the parameter values.</span></span> <span data-ttu-id="0eaad-160">在 Windows PowerShell？，由它们的.NET 类型表示参数值。</span><span class="sxs-lookup"><span data-stu-id="0eaad-160">In Windows PowerShell?, parameter values are represented by their .NET type.</span></span> <span data-ttu-id="0eaad-161">但是，类型名称可以采用缩写形式，如"string"的 System.String。</span><span class="sxs-lookup"><span data-stu-id="0eaad-161">However, the type name can be abbreviated, such as "string" for System.String.</span></span>

   ```
   SYNTAX
       Get-Tech -name string -type basic advanced
       Get-Tech -ID int -list -type basic advanced
   ```

   <span data-ttu-id="0eaad-162">将类型缩写，只要它们的含义是很清晰，如"string"的 System.String 和 System.Int32 为"int"。</span><span class="sxs-lookup"><span data-stu-id="0eaad-162">Abbreviate types as long as their meaning is clear, such as "string" for System.String and "int" for System.Int32.</span></span>

   <span data-ttu-id="0eaad-163">列出所有值的枚举，如在前面的示例-类型参数，针对可以设置为"基本"或"高级"。</span><span class="sxs-lookup"><span data-stu-id="0eaad-163">List all values of enumerations, such as the -type parameter in the previous example, wich can be set to "basic" or "advanced".</span></span>

   <span data-ttu-id="0eaad-164">切换参数，例如-上一示例中的列表，没有值。</span><span class="sxs-lookup"><span data-stu-id="0eaad-164">Switch parameters, such as -list in the previous example, do not have values.</span></span>

4. <span data-ttu-id="0eaad-165">将尖括号内添加到参数值的占位符，相比是文本的参数值。</span><span class="sxs-lookup"><span data-stu-id="0eaad-165">Add angle brackets to parameters values that are placeholder, as compared to parameter values that are literals.</span></span>

   ```
   SYNTAX
       Get-Tech -name <string> -type basic advanced
       Get-Tech -ID <int> -list -type basic advanced
   ```

5. <span data-ttu-id="0eaad-166">将可选参数和其值括在方括号中。</span><span class="sxs-lookup"><span data-stu-id="0eaad-166">Enclose optional parameters and their vales in square brackets.</span></span>

   ```
   SYNTAX
       Get-Tech -name <string> [-type basic advanced]
       Get-Tech -ID <int> [-list] [-type basic advanced]
   ```

6. <span data-ttu-id="0eaad-167">将可选参数 （对于位置参数） 的名称括在方括号中。</span><span class="sxs-lookup"><span data-stu-id="0eaad-167">Enclose optional parameters names (for positional parameters) in square brackets.</span></span> <span data-ttu-id="0eaad-168">不需要的命令中包含参数的位置，如以下示例中中的名称参数的名称。</span><span class="sxs-lookup"><span data-stu-id="0eaad-168">The name for parameters that are positional, such as the Name parameter in the following example, do not have to be included in the command.</span></span>

   ```
   SYNTAX
       Get-Tech [-name] <string> [-type basic advanced]
       Get-Tech -ID <int> [-list] [-type basic advanced]
   ```

7. <span data-ttu-id="0eaad-169">如果参数值可以包含多个值，例如 Name 参数中的名称的列表添加一对方括号紧接参数值。</span><span class="sxs-lookup"><span data-stu-id="0eaad-169">If a parameter value can contain multiple values, such as a list of names in the Name parameter, add a pair of square brackets directly following the parameter value.</span></span>

   ```
   SYNTAX
       Get-Tech [-name] <string[]> [-type basic advanced]
       Get-Tech -ID <int[]> [-list] [-type basic advanced]
   ```

8. <span data-ttu-id="0eaad-170">如果用户可以选择从参数或参数值，类型参数，如将这些选项括在大括号中，使用独占 OR symbol(;) 分隔。</span><span class="sxs-lookup"><span data-stu-id="0eaad-170">If the user can choose from parameters or parameter values, such as the Type parameter, enclose the choices in curly brackets and separate them with the exclusive OR symbol(;).</span></span>

   ```
   SYNTAX
       Get-Tech [-name] <string[]> [-type {basic | advanced}]
       Get-Tech -ID <int[]> [-list] [-type {basic | advanced}]
   ```

9. <span data-ttu-id="0eaad-171">如果参数值必须使用特定格式设置，例如双引号或括号内，在语法中显示格式。</span><span class="sxs-lookup"><span data-stu-id="0eaad-171">If the parameter value must use specific formatting, such as quotation marks or parentheses, show the format in the syntax.</span></span>

   ```
   SYNTAX
       Get-Tech [-name] <"string[]"> [-type {basic | advanced}]
       Get-Tech -ID <int[]> [-list] [-type {basic | advanced}]
   ```

## <a name="coding-the-syntax-diagram-xml"></a><span data-ttu-id="0eaad-172">编码 XML 的语法关系图</span><span class="sxs-lookup"><span data-stu-id="0eaad-172">Coding the Syntax Diagram XML</span></span>

<span data-ttu-id="0eaad-173">XML 的语法节点后说明节点，结尾，立即开始\</maml:description > 标记。</span><span class="sxs-lookup"><span data-stu-id="0eaad-173">The syntax node of the XML begins immediately after the description node, which ends with the \</maml:description> tag.</span></span> <span data-ttu-id="0eaad-174">有关收集的语法关系图中使用的数据的信息，请参阅[收集语法信息](#Gathering-Syntax-Information)。</span><span class="sxs-lookup"><span data-stu-id="0eaad-174">For information about gathering the data used in the syntax diagram, see [Gathering Syntax Information](#Gathering-Syntax-Information).</span></span>

### <a name="adding-a-syntax-node"></a><span data-ttu-id="0eaad-175">添加的语法节点</span><span class="sxs-lookup"><span data-stu-id="0eaad-175">Adding a Syntax Node</span></span>

<span data-ttu-id="0eaad-176">显示 cmdlet 帮助主题中的语法关系图的数据生成的 XML 的语法节点中。</span><span class="sxs-lookup"><span data-stu-id="0eaad-176">The syntax diagram displayed in the cmdlet Help topic is generated from the data in the syntax node of the XML.</span></span> <span data-ttu-id="0eaad-177">如果语法节点括在一对\<命令： 语法 > 标记。</span><span class="sxs-lookup"><span data-stu-id="0eaad-177">The syntax node is enclosed in a pair if \<command:syntax> tags.</span></span> <span data-ttu-id="0eaad-178">与 cmdlet 括在一对中的每个参数集\<命令： syntaxitem > 标记。</span><span class="sxs-lookup"><span data-stu-id="0eaad-178">With each parameter set of the cmdlet enclosed in a pair of \<command:syntaxitem> tags.</span></span> <span data-ttu-id="0eaad-179">数量没有限制\<命令： syntaxitem > 您可以添加的标记。</span><span class="sxs-lookup"><span data-stu-id="0eaad-179">There is no limit to the number of \<command:syntaxitem> tags that you can add.</span></span>

<span data-ttu-id="0eaad-180">下面的示例演示具有两个参数集的语法项节点的语法节点。</span><span class="sxs-lookup"><span data-stu-id="0eaad-180">The following example shows a syntax node that has syntax item nodes for two parameter sets.</span></span>

```xml
<command:syntax>
  <command:syntaxItem>
    ...
    <!--Parameter Set 1 (default parameter set) parameters go here-->
    ...
  </command:syntaxItem>
  <command:syntaxItem>
    ...
    <!--Parameter Set 2 parameters go here-->
    ...
  </command:syntaxItem>
</command:syntax>
```

### <a name="adding-the-cmdlet-name-to-the-parameter-set-data"></a><span data-ttu-id="0eaad-181">将 Cmdlet 名称添加到该参数集的数据</span><span class="sxs-lookup"><span data-stu-id="0eaad-181">Adding the Cmdlet Name to the Parameter Set Data</span></span>

<span data-ttu-id="0eaad-182">该 cmdlet 的每个参数集的语法项节点中指定。</span><span class="sxs-lookup"><span data-stu-id="0eaad-182">Each parameter set of the cmdlet is specified in a syntax item node.</span></span> <span data-ttu-id="0eaad-183">语法项的每个节点以开头的一对\<maml:name > 标记，其中包含该 cmdlet 的名称。</span><span class="sxs-lookup"><span data-stu-id="0eaad-183">Each syntax item node begins with a pair of \<maml:name> tags that include the name of the cmdlet.</span></span>

<span data-ttu-id="0eaad-184">下面的示例包含具有两个参数集的语法项节点的语法节点。</span><span class="sxs-lookup"><span data-stu-id="0eaad-184">The following example includes a syntax node that has syntax item nodes for two parameter sets.</span></span>

```xml
<command:syntax>
  <command:syntaxItem>
    <maml:name>Cmdlet-Name</maml:name>
  </command:syntaxItem>
  <command:syntaxItem>
    <maml:name>Cmdlet-Name</maml:name>
  </command:syntaxItem>
</command:syntax>
```

### <a name="adding-parameters"></a><span data-ttu-id="0eaad-185">添加参数</span><span class="sxs-lookup"><span data-stu-id="0eaad-185">Adding Parameters</span></span>

<span data-ttu-id="0eaad-186">添加到语法项节点的每个参数指定一对大\<命令： 参数 > 标记。</span><span class="sxs-lookup"><span data-stu-id="0eaad-186">Each parameter added to the syntax item node is specified within a pair of \<command:parameter> tags.</span></span> <span data-ttu-id="0eaad-187">需要一对\<命令： 参数 > 包含的参数集，但提供的 Windows PowerShell 通用参数在每个参数的标记？。</span><span class="sxs-lookup"><span data-stu-id="0eaad-187">You need a pair of \<command:parameter> tags for each parameter included in the parameter set, with the exception of the common parameters that are provided by Windows PowerShell?.</span></span>

<span data-ttu-id="0eaad-188">在打开的特性\<命令： 参数 > 标记确定参数的语法关系图中的显示方式。</span><span class="sxs-lookup"><span data-stu-id="0eaad-188">The attributes of the opening \<command:parameter> tag determine how the parameter appears in the syntax diagram.</span></span> <span data-ttu-id="0eaad-189">有关参数属性的信息，请参阅[参数特性](#Parameter-Attributes)。</span><span class="sxs-lookup"><span data-stu-id="0eaad-189">For information on parameter attributes, see [Parameter Attributes](#Parameter-Attributes).</span></span>

> [!NOTE]
> <span data-ttu-id="0eaad-190">\<命令： 参数 > 标记支持子元素\<maml:description > 永远不会显示其内容。</span><span class="sxs-lookup"><span data-stu-id="0eaad-190">The \<command:parameter> tag supports a child element \<maml:description> whose content is never displayed.</span></span> <span data-ttu-id="0eaad-191">参数说明中的 xml 的参数节点指定。</span><span class="sxs-lookup"><span data-stu-id="0eaad-191">The parameter descriptions are specified in the parameter node of the XML.</span></span> <span data-ttu-id="0eaad-192">若要避免出现不一致的语法项中的信息之间 bodes 和省略的参数节点 (\<maml:description > 或将其留空。</span><span class="sxs-lookup"><span data-stu-id="0eaad-192">To avoid inconsistencies between the information in the syntax item bodes and the parameter node, omit the (\<maml:description> or leave it empty.</span></span>

<span data-ttu-id="0eaad-193">下面的示例包含一个参数集使用两个参数的语法项节点。</span><span class="sxs-lookup"><span data-stu-id="0eaad-193">The following example includes a syntax item node for a parameter set with two parameters.</span></span>

```xml
<command:syntaxItem>
  <maml:name>Cmdlet-Name</maml:name>
  <command:parameter required="true" globbing="true"
    pipelineInput="true (ByValue)" position="1">
    <maml:name>ParameterName1</maml:name>
    <command:parameterValue required="true">
      string[]
    </command:parameterValue>
  </command:parameter>
  <command:parameter required="true" globbing="true"
    pipelineInput="true (ByPropertyName)">
    <maml:name>ParameterName2</maml:name>
    <command:parameterValue required="true">
      int32[]
    </command:parameterValue>
  </command:parameter>
</command:syntaxItem>
```