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
# <a name="programmatically-manage-leads-and-co-sell-opportunities-in-partner-center"></a>Program aracılığıyla müşteri adaylarını ve ortak satış fırsatlarını Iş Ortağı Merkezi 'nde yönetme

Bu makale, Microsoft çözüm sağlayıcısı sayfasından aldığınız müşteri adaylarını ve Microsoft satış temsilcisinden veya diğer iş ortaklarından aldığınız ortak satış fırsatlarını programlama yoluyla nasıl yönetebileceğinizi anlamanıza yardımcı olur. Bu API 'leri, şirketinizin satış işlem hattını programlı bir şekilde paylaşmak veya olası fırsatlarda işbirliği yapmak üzere Microsoft satış temsilcilerini davet etmek için de kullanabilirsiniz. 

## <a name="manage-leads-and-opportunities"></a>Müşteri adaylarını ve fırsatları yönetme

- [Müşteri adayları ve fırsatların listesini alın](get-a-list-of-referrals.md) -Microsoft çözüm sağlayıcısı sayfasından gelen müşteri adaylarının listesini alır ve Microsoft satıcılarından veya diğer iş ortaklarından ortak satış fırsatları elde edin. Bu, kuruluşunuz tarafından oluşturulan fırsatların listesini de içerecektir.
- [Kimliğe göre bir müşteri adayı veya fırsat alın](get-a-referral-by-Id.md) -bir müşteri adayını veya bir fırsatı kimliğe göre alır.
- [Müşteri adayını veya fırsatı güncelleştirme](patch-a-referral.md) -teslim değeri, tahmini kapanış tarihi gibi müşteri adaylarını veya fırsat ayrıntılarını güncelleştirmenize veya diğer ayrıntılar arasından satış aşamalarını yönetmenize olanak sağlar.
- [Yeni bir fırsat oluşturun](create-a-referral.md) -yeni bir ortak satış fırsatı veya özel anlaşma oluşturmanızı sağlar.
- [Referans kaynakları](referral-resources.md)

> [!Note]
> Microsoft ticari marketi 'nden (Azure Marketi ve AppSource) alınan müşteri adayları, Iş Ortağı Merkezi API 'leri kullanılarak yönetilemez.