---
title: Fiyat listesi alma
description: Verilen pazar ve görünüm için bir fiyat listesi elde edin. Aya göre geçmişi almak için filtreleri destekler.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0185a61ef0a3747aee1b06f88a7a8d6f1279f9e3
ms.sourcegitcommit: 1a183f9b37d646be240a48fc60e5902f409e8ac1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2021
ms.locfileid: "122989707"
---
# <a name="get-a-price-sheet"></a>Fiyat listesi alma

Aşağıdakiler cihazlar için geçerlidir:

- Partner API

Bu konu başlığında, verilen bir pazar ve görünüm için fiyat listesi alma açıklanmıştır. Bu yöntem, aya göre geçmişi almak için filtreleri destekler.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [Partner API bilgileri.](api-authentication.md) Bu senaryo yalnızca uygulama kullanıcısı kimlik doğrulamasını destekler. Yalnızca uygulama henüz desteklenmiyor. **http hatası:400 ile ilgili iş** ortaklarının kimlik doğrulaması [belgelerine Partner API gerekir.](api-authentication.md)
- Bu API şu anda yalnızca iş ortaklarının şu rollerden biri olması gereken kullanıcı erişimini destekler: Genel Yönetici, Yönetici Aracısı veya Satış Aracısı.

## <a name="details"></a>Ayrıntılar

- Geçerli dönüş verileri yalnızca Azure planı tüketimi ve rezervasyon ürünleri için döndürür.
- Geçerli [fiyatlandırma,](pricing.md) API'nin çağrıldı olduğu tarihe kadar geçerli ay boyunca kullanılabilen tüm metreleri ve ürünleri içerir. Önceki aylar, verilen ay için kullanılabilen tüm metreleri ve ürünleri içerir.
- Tüketim ölçümü fiyatları yalnızca ABD doları cinsindendir, iş ortaklarının yerel para birimi maliyetlerini hesaplamak için döviz kurları API'sini kullanmaları gerekir.
- Tüketim ölçümü fiyatları tahmini perakende fiyatlarıdır. İş ortağı indirimleri, iş [ortağı tarafından kazanılan kredi aracılığıyla kullanılabilir.](/partner-center/partner-earned-credit-explanation)
- Rezervasyon ölçümü fiyatları CSP iş ortağı indirimlerini içerir. Rezervasyonlar için tahmini perakende fiyatları, "Fiyatlandırma ve teklifler" sayfasından İş Ortağı Merkezi paylaşılan hizmetlerde bulunabilir.
- Azure planı fiyatlandırması hakkında daha fazla bilgiyi [Azure planı fiyatlandırma belgelerinde bulabilirsiniz.](/partner-center/azure-plan-price-list)
- İş ortağı fiyatlandırması ve döviz kuru API'leri, [İş Ortağı Merkezi SDK'sı.](get-started.md)
- Bu yöntem fiyat listesini dosya akışı olarak döndürür. Dosya akışı bir .csv dosyası veya dosyanın sıkıştırılmış zip .csv. Sıkıştırılmış dosyaları nasıl talep etmekle ilgili ayrıntılar aşağıda verilmiştir.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **AL** | https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value                                     |

### <a name="uri-required-parameters"></a>URI gerekli parametreler

Hangi pazar ve fiyat listesi türünü istediğinize istekte etmek için aşağıdaki yol parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Pazar                      | string   | Yes       | Pazar için istenen iki harfli ülke kodu       |
|PricesheetView | string   | Yes       | İstenen fiyat listesi türü, bu değer azure_consumption, azure_reservations veya güncelleştirilebilir.  |

> [!Note]
> güncelleştirilmiş lisanslı PriceSheetView şu anda yalnızca M365/D365 yeni ticari deneyim teknik önizlemesi kapsamında olan iş ortakları tarafından kullanılabilir.

### <a name="uri-filter-parameters"></a>URI filtre parametreleri

Aşağıdaki filtre parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Zaman çizelgesi| dize   | No| Geçirilse varsayılan olarak geçerli olur. Olası değerler geçmiş, geçerli ve gelecek değerleridir.       |
|Ay| dize   | No| Yalnızca geçmiş istenecekse, istenen fiyat listesi için YYYYMM'ye bağlı kalmaları gerekir.       |

### <a name="request-headers"></a>İstek üst bilgileri

- Daha [fazla bilgi için bkz. İş](headers.md) ortağı REST üst bilgileri.

Yukarıdaki üst bilgilere ek olarak, fiyatlandırma dosyaları bant genişliğini ve indirme süresini azaltarak sıkıştırılmış olarak alınabiliyor. Varsayılan olarak dosyalar sıkıştırılır. Dosyaların sıkıştırılmış sürümlerini almak için aşağıdaki üst bilgi değerini dahil edebilirsiniz. Sıkıştırılmış sayfaların yalnızca Nisan 2020'den itibaren kullanılabilir olduğunu, Nisan 2020'den önceki tüm sayfaların yalnızca sıkıştırılmış olarak kullanılabilir olmadığını fark etmek.

| Üst bilgi                   | Değer Türü     | Değer | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| string   | Deflate| İsteğe bağlı. Atlanmış dosya akışı sıkıştırilmezse.       |

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Host: api.partner.microsoft.com

```
### <a name="request-example-for-new-commerce"></a>Yeni ticaret için istek örneği

> [!Note]
> güncelleştirilmiş lisanslı PriceSheetView şu anda yalnızca M365/D365 yeni ticari deneyim teknik önizlemesi kapsamında olan iş ortakları tarafından kullanılabilir.

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='US',PricesheetView='updatedlicensebased')/$value?timeline=history&month=202101 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST yanıtı

Bu yöntem başarılı olursa fiyat listesini dosya akışı olarak döndürür. Dosya akışı bir .csv dosyası veya dosyanın sıkıştırılmış zip .csv.

### <a name="response-example-for-new-commerce"></a>Yeni ticaret için yanıt örneği

> [!Note]
> güncelleştirilmiş lisanslı PriceSheetView şu anda yalnızca M365/D365 yeni ticari deneyim teknik önizlemesi kapsamında olan iş ortakları tarafından kullanılabilir.

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=sheets.csv
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Feb 2021 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","Publisher","SkuDescription","UnitOfMeasure","TermDuration","BillingPlan","Market","Currency","UnitPrice","PricingTierRangeMin","PricingTierRangeMax","EffectiveStartDate","EffectiveEndDate","Tags","ERP Price“
"Advanced Communications","CFQ7TTC0HDK0","0001","Advanced Communications","Microsoft Corporation","Advanced meetings, calling, workflow integration, and management tools for IT.","","P1Y","Annual","US","USD","115.2","","","2/1/2019 12:00:00 AM","2/4/2021 8:35:31 PM","License","144"
======= Truncated ==============

```

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)
