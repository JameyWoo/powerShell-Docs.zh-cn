---
ms.date: 06/12/2017
keywords: dsc,powershell,配置,安装程序
title: SendMetaConfigurationApply 方法
ms.openlocfilehash: b2e420bafb8ea22aea43800f6e429d3ed785d1e8
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "71954874"
---
# <a name="sendmetaconfigurationapply-method"></a><span data-ttu-id="06ac1-103">SendMetaConfigurationApply 方法</span><span class="sxs-lookup"><span data-stu-id="06ac1-103">SendMetaConfigurationApply method</span></span>

<span data-ttu-id="06ac1-104">设置用于控制配置代理的本地配置管理器设置。</span><span class="sxs-lookup"><span data-stu-id="06ac1-104">Sets the Local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

## <a name="syntax"></a><span data-ttu-id="06ac1-105">语法</span><span class="sxs-lookup"><span data-stu-id="06ac1-105">Syntax</span></span>

```mof
uint32 SendMetaConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="06ac1-106">参数</span><span class="sxs-lookup"><span data-stu-id="06ac1-106">Parameters</span></span>

<span data-ttu-id="06ac1-107">ConfigurationData  \[in\]：配置的环境数据。</span><span class="sxs-lookup"><span data-stu-id="06ac1-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="06ac1-108">force  \[in\]：若为 true  ，强制停止配置。</span><span class="sxs-lookup"><span data-stu-id="06ac1-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="06ac1-109">返回值</span><span class="sxs-lookup"><span data-stu-id="06ac1-109">Return value</span></span>

<span data-ttu-id="06ac1-110">如果成功，则返回零；否则返回错误代码。</span><span class="sxs-lookup"><span data-stu-id="06ac1-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="06ac1-111">备注</span><span class="sxs-lookup"><span data-stu-id="06ac1-111">Remarks</span></span>

<span data-ttu-id="06ac1-112">这是一种静态方法。</span><span class="sxs-lookup"><span data-stu-id="06ac1-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="06ac1-113">要求</span><span class="sxs-lookup"><span data-stu-id="06ac1-113">Requirements</span></span>

<span data-ttu-id="06ac1-114">**MOF：** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="06ac1-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="06ac1-115">**命名空间**：Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="06ac1-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="06ac1-116">另请参阅</span><span class="sxs-lookup"><span data-stu-id="06ac1-116">See also</span></span>

[<span data-ttu-id="06ac1-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="06ac1-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
