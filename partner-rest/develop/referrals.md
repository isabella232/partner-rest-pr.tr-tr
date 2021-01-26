---
title: Program aracılığıyla müşteri adaylarını ve ortak satış fırsatlarını Iş Ortağı Merkezi 'nde yönetme
description: Bu bölümde, iş ortaklarının müşteri adaylarını ve ortak satış fırsatlarını programlama yoluyla yönetmek için Iş ortağı API 'Lerini nasıl kullanabileceği açıklanmaktadır.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0da725c9b2459a6c5631b7cc7e21b46e9a7191b8
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770638"
---
# <a name="programmatically-manage-leads-and-co-sell-opportunities-in-partner-center"></a><span data-ttu-id="359e6-103">Program aracılığıyla müşteri adaylarını ve ortak satış fırsatlarını Iş Ortağı Merkezi 'nde yönetme</span><span class="sxs-lookup"><span data-stu-id="359e6-103">Programmatically manage leads and co-sell opportunities in Partner Center</span></span>

<span data-ttu-id="359e6-104">Bu makale, Microsoft çözüm sağlayıcısı sayfasından aldığınız müşteri adaylarını ve Microsoft satış temsilcisinden veya diğer iş ortaklarından aldığınız ortak satış fırsatlarını programlama yoluyla nasıl yönetebileceğinizi anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="359e6-104">This article will help you understand how you can programmatically manage the leads that you receive from Microsoft solution provider page and the co-sell opportunities that you receive from Microsoft sales representative or other partners.</span></span> <span data-ttu-id="359e6-105">Bu API 'leri, şirketinizin satış işlem hattını programlı bir şekilde paylaşmak veya olası fırsatlarda işbirliği yapmak üzere Microsoft satış temsilcilerini davet etmek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="359e6-105">You can also use these api's to programmatically share your company's sales pipeline or invite Microsoft sales representatives to collaborate on potential opportunities.</span></span> 

## <a name="manage-leads-and-opportunities"></a><span data-ttu-id="359e6-106">Müşteri adaylarını ve fırsatları yönetme</span><span class="sxs-lookup"><span data-stu-id="359e6-106">Manage leads and opportunities</span></span>

- <span data-ttu-id="359e6-107">[Müşteri adayları ve fırsatların listesini alın](get-a-list-of-referrals.md) -Microsoft çözüm sağlayıcısı sayfasından gelen müşteri adaylarının listesini alır ve Microsoft satıcılarından veya diğer iş ortaklarından ortak satış fırsatları elde edin.</span><span class="sxs-lookup"><span data-stu-id="359e6-107">[Get the list of leads and opportunities](get-a-list-of-referrals.md) - Gets the list of leads from Microsoft solution provider page and co-sell opportunities from Microsoft sellers or other partners.</span></span> <span data-ttu-id="359e6-108">Bu, kuruluşunuz tarafından oluşturulan fırsatların listesini de içerecektir.</span><span class="sxs-lookup"><span data-stu-id="359e6-108">This will also contain the list of opportunities created by your organization.</span></span>
- <span data-ttu-id="359e6-109">[Kimliğe göre bir müşteri adayı veya fırsat alın](get-a-referral-by-Id.md) -bir müşteri adayını veya bir fırsatı kimliğe göre alır.</span><span class="sxs-lookup"><span data-stu-id="359e6-109">[Get a lead or opportunity by Id](get-a-referral-by-Id.md) - Gets a lead or opportunity by Id.</span></span>
- <span data-ttu-id="359e6-110">[Müşteri adayını veya fırsatı güncelleştirme](patch-a-referral.md) -teslim değeri, tahmini kapanış tarihi gibi müşteri adaylarını veya fırsat ayrıntılarını güncelleştirmenize veya diğer ayrıntılar arasından satış aşamalarını yönetmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="359e6-110">[Update a lead or opportunity](patch-a-referral.md) - Allows you to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.</span></span>
- <span data-ttu-id="359e6-111">[Yeni bir fırsat oluşturun](create-a-referral.md) -yeni bir ortak satış fırsatı veya özel anlaşma oluşturmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="359e6-111">[Create a new opportunity](create-a-referral.md) - Enables you to create a new co-sell opportunity or private deal.</span></span>
- [<span data-ttu-id="359e6-112">Referans kaynakları</span><span class="sxs-lookup"><span data-stu-id="359e6-112">Referral resources</span></span>](referral-resources.md)

> [!Note]
> <span data-ttu-id="359e6-113">Microsoft ticari marketi 'nden (Azure Marketi ve AppSource) alınan müşteri adayları, Iş Ortağı Merkezi API 'leri kullanılarak yönetilemez.</span><span class="sxs-lookup"><span data-stu-id="359e6-113">Leads received from the Microsoft commercial marketplace (Azure Marketplace and AppSource) cannot be managed using Partner Center api's.</span></span>