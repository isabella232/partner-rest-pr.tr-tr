---
title: Fiyat listesi alma
description: Belirli bir Pazar ve görünüm için bir fiyat listesi alın. Aya göre geçmişi almak için filtreleri destekler.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 7571e8fce861dbfe463000a1ac4094115af08ffa
ms.sourcegitcommit: 9e64d6358ef4e1ac2d3e0d36cd63490a5f760b38
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/01/2021
ms.locfileid: "113125525"
---
# <a name="get-a-price-sheet"></a>Fiyat listesi alma

Aşağıdakiler cihazlar için geçerlidir:

- İş ortağı API 'SI

Bu konuda, belirli bir Pazar ve görünüm için fiyat listesi alma açıklanmaktadır. Bu yöntem, geçmişi aya göre almak için filtreleri destekler.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı API kimlik doğrulaması](api-authentication.md)bölümünde açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama kullanıcı kimlik doğrulamasını destekler. Yalnızca uygulama henüz desteklenmiyor. Http hatasıyla karşılaşan iş ortakları **: 400** [iş ortağı API kimlik doğrulama](api-authentication.md) belgelerine başvurmalıdır.
- Bu API Şu anda yalnızca iş ortaklarının şu rollerden birinde olması gereken Kullanıcı erişimini destekliyor: genel yönetici, Yönetim Aracısı veya satış Aracısı.

## <a name="details"></a>Ayrıntılar

- Geçerli, yalnızca Azure planı tüketimi ve rezervasyon ürünleri için verileri döndürür.
- Geçerli [fiyatlandırma](pricing.md) , geçerli ay boyunca API 'nin çağrıldığı tarihe kadar sunulan tüm ölçümleri ve ürünleri içerir. Önceki aylar, belirli bir ay için kullanılabilen tüm ölçümleri ve ürünleri içerir.
- Tüketim ölçümü fiyatları yalnızca ABD doları cinsindendir, iş ortakları yerel para birimi maliyetlerini hesaplamak için yabancı Exchange ücretleri API 'sini kullanmaktır.
- Tüketim ölçümü fiyatları, tahmini perakende fiyatlarıdır. İş ortağı indirimleri, [iş ortağı tarafından kazanılan kredi](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation)aracılığıyla kullanılabilir.
- Rezervasyonların ölçüm fiyatları, CSP iş ortağı indirimlerini içerir. Rezervasyonlar için tahmini perakende fiyatları, Iş Ortağı Merkezi "fiyatlandırma ve teklifler" sayfasında indirilebilir olan rezervasyonlar paylaşılan hizmetlerinde bulunabilir.
- Azure plan fiyatlandırması hakkında daha fazla bilgi için [Azure plan fiyatlandırma belgelerinde](https://docs.microsoft.com/partner-center/azure-plan-price-list)bulabilirsiniz.
- İş ortağı fiyatlandırması ve yabancı değişim oranı API 'Leri, [Iş Ortağı Merkezi SDK 'sının](https://docs.microsoft.com/partner-center/develop/get-started)bir parçası değildir.
- Bu yöntem, bir dosya akışı olarak fiyat listesini döndürür. Dosya akışı, .csv bir .csv dosyası ya da zip ile sıkıştırılmış bir sürümdür. Sıkıştırılmış dosyaları isteme hakkındaki ayrıntılar aşağıda verilmiştir.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Al** | https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market=' {Market} ', PricesheetView = ' {View} ')/$value                                     |

### <a name="uri-required-parameters"></a>URI gerekli parametreler

Hangi tür fiyatları ve istediğiniz fiyat listesini istemek için aşağıdaki yol parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Pazara                      | string   | Yes       | İstenen Pazar için iki harfli ülke kodu       |
|PricesheetView | string   | Yes       | İstenen Fiyat listesi türü, bu azure_consumption, azure_reservations veya updatedlicensebased olabilir.  |

> [!Note]
> updatedlicensebased PriceSheetView Şu anda yalnızca M365/D365 yeni ticaret deneyimi Technical Preview 'ın parçası olan iş ortakları tarafından kullanılabilir.

### <a name="uri-filter-parameters"></a>URI filtresi parametreleri

Aşağıdaki filtre parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Zaman çizelgesi| dize   | No| Geçirilmemişse varsayılan değeri geçerli olarak belirler. Olası değerler geçmiş, güncel ve gelecekteki değerlerdir.       |
|Ay| dize   | No| Yalnızca geçmiş isteniyorsa gereklidir, istenen fiyat listesi için YYYYMM 'ye uymalıdır.       |

### <a name="request-headers"></a>İstek üst bilgileri

- Daha fazla bilgi için bkz. [Iş ortağı Rest üst bilgileri](headers.md) .

Yukarıdaki üst bilgilere ek olarak, fiyatlandırma dosyaları sıkıştırılmış bant genişliği ve indirme süreleriyle sıkıştırılmış olarak alınabilir. Dosyalar varsayılan olarak sıkıştırılmaz. Dosyaların sıkıştırılmış sürümlerini almak için aşağıdaki üst bilgi değerini ekleyebilirsiniz. Sıkıştırılan sayfaların yalnızca 2020 Nisan 'dan kullanılabildiğini, 2020 Nisan 'dan önceki tüm sayfaların yalnızca sıkıştırılmamış olarak kullanılabildiğini unutmayın.

| Üst bilgi                   | Değer Türü     | Değer | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| string   | Söndür| İsteğe bağlı. Atlanan dosya akışı sıkıştırmamışsa.       |

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```
### <a name="request-example-for-new-commerce"></a>Yeni Ticaret için istek örneği

> [!Note]
> updatedlicensebased PriceSheetView Şu anda yalnızca M365/D365 yeni ticaret deneyimi Technical Preview 'ın parçası olan iş ortakları tarafından kullanılabilir.

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='US',PricesheetView='updatedlicensebased')/$value?timeline=history&month=202101 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem bir dosya akışı olarak fiyat listesini döndürür. Dosya akışı, .csv bir .csv dosyası ya da zip ile sıkıştırılmış bir sürümdür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=pricesheet
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Oct 2019 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","Publisher","SkuDescription","UnitOfMeasure","TermDuration","Market","Currency","UnitPrice","PricingTierRangeMin","PricingTierRangeMax","EffectiveStartDate","EffectiveEndDate","MeterIds","MeterType","Tags“
"Advanced Data Security - SQL Database","DZH318Z0C16V","001J","Advanced Data Security - SQL Database - Standard - US East 2","Microsoft","Advanced Data Security - SQL Database - Standard - US East 2","1 Node/Month","payG-1","US","USD","15","","","3/1/2018 12:00:00 AM","11/30/9999 11:59:59 PM","cb0969aa-aaaa-4d6c-ab4b-7e182fa06aff","1 Node/Month","Azure“
======= Truncated ==============

```

### <a name="response-example-for-new-commerce"></a>Yeni Ticaret için yanıt örneği

> [!Note]
> updatedlicensebased PriceSheetView Şu anda yalnızca M365/D365 yeni ticaret deneyimi Technical Preview 'ın parçası olan iş ortakları tarafından kullanılabilir.

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
