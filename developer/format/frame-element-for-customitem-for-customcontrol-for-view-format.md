---
title: 对的帧元素的 CustomItem CustomControl 视图 （格式） |Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e1a13100-41a4-4847-9f07-458c85783505
caps.latest.revision: 6
ms.openlocfilehash: 925ef86e61801f5a66f89dd25e0756f00dd35155
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2019
ms.locfileid: "58054775"
---
# <a name="frame-element-for-customitem-for-customcontrol-for-view-format"></a><span data-ttu-id="cd4fb-102">Frame Element for CustomItem for CustomControl for View (Format)</span><span class="sxs-lookup"><span data-stu-id="cd4fb-102">Frame Element for CustomItem for CustomControl for View (Format)</span></span>

<span data-ttu-id="cd4fb-103">定义如何显示数据，如向左或向右移位数据。</span><span class="sxs-lookup"><span data-stu-id="cd4fb-103">Defines how the data is displayed, such as shifting the data to the left or right.</span></span> <span data-ttu-id="cd4fb-104">定义自定义控件视图时，将使用此元素。</span><span class="sxs-lookup"><span data-stu-id="cd4fb-104">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="cd4fb-105">配置元素 （格式） ViewDefinitions 元素 （格式） 视图元素 （格式） CustomControl 元素 （格式） CustomEntries 元素 CustomControl 视图 （格式） 的视图 （格式） CustomItem 元素 CustomEntries CustomEntry 元素CustomEntry CustomControlView （格式） 的视图 （格式） 的 CustomControl CustomItem 框架元素</span><span class="sxs-lookup"><span data-stu-id="cd4fb-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format) CustomItem Element for CustomEntry for CustomControlView (Format) Frame Element for CustomItem for CustomControl for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="cd4fb-106">语法</span><span class="sxs-lookup"><span data-stu-id="cd4fb-106">Syntax</span></span>

```xml
<Frame>
  <LeftIndent>NumberOfCharactersToShift</LeftIndent>
  <RightIndent>NumberOfCharactersToShift</RightIndent>
  <FirstLineHanging>NumberOfCharactersToShift</FirstLineHanging>
  <FirstLineIndent>NumberOfCharactersToShift</FirstLineIndent>
  <CustomItem>...</CustomItem>
</Frame>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="cd4fb-107">属性和元素</span><span class="sxs-lookup"><span data-stu-id="cd4fb-107">Attributes and Elements</span></span>

<span data-ttu-id="cd4fb-108">以下各节描述了特性、 子元素和父元素的`Frame`元素。</span><span class="sxs-lookup"><span data-stu-id="cd4fb-108">The following sections describe attributes, child elements, and the parent element of the `Frame` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="cd4fb-109">属性</span><span class="sxs-lookup"><span data-stu-id="cd4fb-109">Attributes</span></span>

<span data-ttu-id="cd4fb-110">无。</span><span class="sxs-lookup"><span data-stu-id="cd4fb-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="cd4fb-111">子元素</span><span class="sxs-lookup"><span data-stu-id="cd4fb-111">Child Elements</span></span>

|<span data-ttu-id="cd4fb-112">元素</span><span class="sxs-lookup"><span data-stu-id="cd4fb-112">Element</span></span>|<span data-ttu-id="cd4fb-113">说明</span><span class="sxs-lookup"><span data-stu-id="cd4fb-113">Description</span></span>|
|-------------|-----------------|
|`CustomItem Element`|<span data-ttu-id="cd4fb-114">所需的元素</span><span class="sxs-lookup"><span data-stu-id="cd4fb-114">Required Element</span></span>|
|[<span data-ttu-id="cd4fb-115">FirstLineHanging 元素</span><span class="sxs-lookup"><span data-stu-id="cd4fb-115">FirstLineHanging Element</span></span>](./firstlinehanging-element-for-frame-for-customcontrol-for-view-format.md)|<span data-ttu-id="cd4fb-116">可选元素。</span><span class="sxs-lookup"><span data-stu-id="cd4fb-116">Optional element.</span></span><br /><br /> <span data-ttu-id="cd4fb-117">指定向左移动数据的第一行的字符数。</span><span class="sxs-lookup"><span data-stu-id="cd4fb-117">Specifies how many characters the first line of data is shifted to the left.</span></span>|
|[<span data-ttu-id="cd4fb-118">FirstLineIndent 元素</span><span class="sxs-lookup"><span data-stu-id="cd4fb-118">FirstLineIndent Element</span></span>](./firstlineindent-element-for-frame-for-customcontrol-for-view-format.md)|<span data-ttu-id="cd4fb-119">可选元素。</span><span class="sxs-lookup"><span data-stu-id="cd4fb-119">Optional element.</span></span><br /><br /> <span data-ttu-id="cd4fb-120">指定向右移动数据的第一行的字符数。</span><span class="sxs-lookup"><span data-stu-id="cd4fb-120">Specifies how many characters the first line of data is shifted to the right.</span></span>|
|[<span data-ttu-id="cd4fb-121">LeftIndent 元素</span><span class="sxs-lookup"><span data-stu-id="cd4fb-121">LeftIndent Element</span></span>](./leftindent-element-for-frame-for-customcontrol-for-view-format.md)|<span data-ttu-id="cd4fb-122">可选元素。</span><span class="sxs-lookup"><span data-stu-id="cd4fb-122">Optional element.</span></span><br /><br /> <span data-ttu-id="cd4fb-123">指定左边距远离数据向右移的字符数。</span><span class="sxs-lookup"><span data-stu-id="cd4fb-123">Specifies how many characters the data is shifted away from the left margin.</span></span>|
|[<span data-ttu-id="cd4fb-124">RightIndent 元素</span><span class="sxs-lookup"><span data-stu-id="cd4fb-124">RightIndent Element</span></span>](./rightindent-element-for-frame-for-customcontrol-for-view-format.md)|<span data-ttu-id="cd4fb-125">可选元素。</span><span class="sxs-lookup"><span data-stu-id="cd4fb-125">Optional element.</span></span><br /><br /> <span data-ttu-id="cd4fb-126">指定数据向右移离开右边距的字符数。</span><span class="sxs-lookup"><span data-stu-id="cd4fb-126">Specifies how many characters the data is shifted away from the right margin.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="cd4fb-127">父元素</span><span class="sxs-lookup"><span data-stu-id="cd4fb-127">Parent Elements</span></span>

|<span data-ttu-id="cd4fb-128">元素</span><span class="sxs-lookup"><span data-stu-id="cd4fb-128">Element</span></span>|<span data-ttu-id="cd4fb-129">说明</span><span class="sxs-lookup"><span data-stu-id="cd4fb-129">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="cd4fb-130">视图 （格式） 的 CustomEntry CustomItem 元素</span><span class="sxs-lookup"><span data-stu-id="cd4fb-130">CustomItem Element for CustomEntry for View (Format)</span></span>](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)|<span data-ttu-id="cd4fb-131">定义由控件显示的数据和显示方式。</span><span class="sxs-lookup"><span data-stu-id="cd4fb-131">Defines what data is displayed by the control and how it is displayed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="cd4fb-132">备注</span><span class="sxs-lookup"><span data-stu-id="cd4fb-132">Remarks</span></span>

<span data-ttu-id="cd4fb-133">不能指定[FirstLineHanging](./firstlinehanging-element-for-frame-for-customcontrol-for-view-format.md)并[FirstLineIndent](./firstlineindent-element-for-frame-for-customcontrol-for-view-format.md)中相同的元素`Frame`元素。</span><span class="sxs-lookup"><span data-stu-id="cd4fb-133">You cannot specify the [FirstLineHanging](./firstlinehanging-element-for-frame-for-customcontrol-for-view-format.md) and the [FirstLineIndent](./firstlineindent-element-for-frame-for-customcontrol-for-view-format.md) elements in the same `Frame` element.</span></span>

## <a name="see-also"></a><span data-ttu-id="cd4fb-134">另请参阅</span><span class="sxs-lookup"><span data-stu-id="cd4fb-134">See Also</span></span>

[<span data-ttu-id="cd4fb-135">FirstLineHanging 元素</span><span class="sxs-lookup"><span data-stu-id="cd4fb-135">FirstLineHanging Element</span></span>](./firstlinehanging-element-for-frame-for-customcontrol-for-view-format.md)

[<span data-ttu-id="cd4fb-136">FirstLineIndent 元素</span><span class="sxs-lookup"><span data-stu-id="cd4fb-136">FirstLineIndent Element</span></span>](./firstlineindent-element-for-frame-for-customcontrol-for-view-format.md)

[<span data-ttu-id="cd4fb-137">LeftIndent 元素</span><span class="sxs-lookup"><span data-stu-id="cd4fb-137">LeftIndent Element</span></span>](./leftindent-element-for-frame-for-customcontrol-for-view-format.md)

[<span data-ttu-id="cd4fb-138">RightIndent 元素</span><span class="sxs-lookup"><span data-stu-id="cd4fb-138">RightIndent Element</span></span>](./rightindent-element-for-frame-for-customcontrol-for-view-format.md)

[<span data-ttu-id="cd4fb-139">视图 （格式） 的 CustomEntry CustomItem 元素</span><span class="sxs-lookup"><span data-stu-id="cd4fb-139">CustomItem Element for CustomEntry for View (Format)</span></span>](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)

[<span data-ttu-id="cd4fb-140">编写 PowerShell 格式设置文件</span><span class="sxs-lookup"><span data-stu-id="cd4fb-140">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)