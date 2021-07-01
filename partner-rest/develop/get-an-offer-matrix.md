---
title: Teklif matrisi elde etmek
description: Verilen tarih için teklif matrisi alma. Aya göre geçmişi almak için filtreleri destekler.
ms.date: 02/11/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e53276c1170febab002d35a42c88c1f96f7b7428
ms.sourcegitcommit: 9e64d6358ef4e1ac2d3e0d36cd63490a5f760b38
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/01/2021
ms.locfileid: "113131306"
---
# <a name="get-an-offer-matrix"></a>Teklif matrisi elde etmek

Aşağıdakiler cihazlar için geçerlidir:

- Partner API
- M365/D365 Yeni Ticaret deneyimi teknik önizlemesi. Aşağıdaki Yeni Ticaret değişiklikleri şu anda yalnızca M365/D365 yeni ticaret deneyimi teknik önizlemesinde yer alan iş ortakları tarafından kullanılabilir.

Bu konu başlığında, bir ay için teklif matrisinin nasıl elde tutulacakları açıklanmıştır. Teklif matrisi, ürünler ve sku'lar için özellikler ve satın alma kuralları içerir. Bu yöntem, aya göre geçmişi almak için filtreleri destekler.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [Partner API bilgileri.](api-authentication.md) Bu senaryo yalnızca uygulama kullanıcısı kimlik doğrulamasını destekler. Yalnızca uygulama henüz desteklenmiyor. **Http hatası:400 ile ilgili iş** ortaklarının kimlik doğrulaması Partner API [bakın.](api-authentication.md)
- Bu API şu anda yalnızca iş ortaklarının şu rollerden biri olması gereken kullanıcı erişimini destekler: Genel Yönetici, Yönetici Aracısı veya Satış Aracısı.

## <a name="details"></a>Ayrıntılar

- Geçerli, yalnızca güncelleştirilmiş yeni ticari lisans tabanlı ürünler için verileri döndürür.
- Geçerli fiyatlandırma, API'nin çağrıldı olduğu tarihe kadar geçerli ay boyunca kullanılabilen ürünleri içerir. Önceki aylar, seçilen ayın son gününden itibaren tarihi içerir.
- Bu yöntem verileri bir dosya akışı olarak döndürür. Dosya akışı, .csv dosya veya dosyanın sıkıştırılmış zip sürümü .csv. Sıkıştırılmış dosyaları nasıl talep etmekle ilgili ayrıntılar aşağıda verilmiştir.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Al** | https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='{date}')/$value |

### <a name="uri-filter-parameters"></a>URI filtre parametreleri

Aşağıdaki filtre parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Ay| dize   | No | İstenen fiyat listesi için YYYYMM'ye bağlı kalmaları gerekir. |

### <a name="request-headers"></a>İstek üst bilgileri

- Daha [fazla bilgi için bkz. İş](headers.md) ortağı REST üst bilgileri.

Yukarıdaki üst bilgilerine ek olarak, fiyatlandırma dosyaları bant genişliğini ve indirme süresini azaltan sıkıştırılmış olarak alınabiliyor. Varsayılan olarak dosyalar sıkıştırılır. Dosyaların sıkıştırılmış sürümlerini almak için aşağıdaki üst bilgi değerini dahil edebilirsiniz. Sıkıştırılmış sayfaların yalnızca Nisan 2020'den itibaren kullanılabilir olduğunu, Nisan 2020'den önceki tüm sayfaların yalnızca sıkıştırılmış olarak kullanılabilir olduğunu fark etmek.

| Üst bilgi                   | Değer Türü     | Değer | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| string   | Deflate| İsteğe bağlı. Atlanmış dosya akışı sıkıştırilmezse.       |

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='202101')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem dosya akışı olarak bir teklif matrisi döndürür. Dosya akışı, .csv dosya veya dosyanın sıkıştırılmış zip sürümü .csv.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=updatedoffice.csv
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Feb 2021 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","ProvisioningId","ProvisioningString","MinLicenses","MaxLicenses","AssetOwnershipLimit","AssetOwnershipLimitType","ProductSkuPreRequisites","ProductSkuConversion","Description","AllowedCountries" 
"Microsoft 365 Business Basic","CFQ7TTC0LH18","0001","Microsoft 365 Business Basic","3b555118-da6a-4418-894f-7df1e2096870","O365_BUSINESS_ESSENTIALS","1","300","2","ConcurrentCount","","CFQ7TTC0LDPB/0001,CFQ7TTC0LF8Q/0001","Best for businesses that need professional...","AD;AE;AF;AG;AI;AL;AM;AO..."
======= Truncated ==============

```
