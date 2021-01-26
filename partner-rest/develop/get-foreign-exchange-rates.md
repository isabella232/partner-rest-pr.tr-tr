---
title: Döviz kurlarını alma
description: Belirli bir ay için yabancı Exchange ücretleri alın.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 1e718624db54dcc2ed2b5d2d93dfd1cef0e6f96f
ms.sourcegitcommit: bb3f5f7ee0489bded86fe52e55018c1f4f5032e2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2020
ms.locfileid: "97770629"
---
# <a name="get-foreign-exchange-rates"></a>Döviz kurlarını alma

Aşağıdakiler cihazlar için geçerlidir:

- İş ortağı API 'SI

Bu konu, belirli bir ay için yabancı Exchange tarifelerinin nasıl alınacağını açıklamaktadır.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı API kimlik doğrulaması](api-authentication.md)bölümünde açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama kullanıcı kimlik doğrulamasını destekler. Yalnızca uygulama henüz desteklenmiyor.
- Bu API Şu anda yalnızca iş ortaklarının şu rollerden birinde olması gereken Kullanıcı erişimini destekliyor: genel yönetici, Yönetim Aracısı veya satış Aracısı.


## <a name="details"></a>Ayrıntılar

- Şu anda, Azure planı CSP yerel para birimleri için beklenen ücretleri hesaplamak üzere [Fiyat Tablosu API 'si al](get-a-price-sheet.md) ile kullanılır.
- Yabancı Exchange ücretleri, nakledildikleri tüm ay için doğru bir tutar.
- Azure plan [fiyatlandırması](pricing.md) hakkında daha fazla bilgi için [Azure plan fiyatlandırma belgelerinde](https://docs.microsoft.com/partner-center/azure-plan-price-list)bulabilirsiniz.
- İş ortağı fiyatlandırması ve yabancı değişim oranı API 'Leri, [Iş Ortağı Merkezi SDK 'sının](https://docs.microsoft.com/partner-center/develop/get-started)bir parçası değildir.
- Bu yöntem, sonuçları bir dosya akışı olarak döndürür. Dosya akışı bir. csv dosyası ya da. csv 'nin zip ile sıkıştırılmış bir sürümüdür. Sıkıştırılmış dosyaları isteme hakkındaki ayrıntılar aşağıda verilmiştir.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Al** | https://api.partner.microsoft.com/v1.0/sales/fxrates(Month=' {month} ')/$value                                  |

### <a name="uri-required-parameters"></a>URI gerekli parametreler

İstediğiniz sayıda yabancı döviz kurunu istemek için aşağıdaki yol parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Ay                      | string   | Yes       | YYYıMM biçiminde olmalıdır. Atlanırsa, varsayılan olarak geçerli ay olur.       |

### <a name="request-headers"></a>İstek üst bilgileri

- Daha fazla bilgi için bkz. [Iş ortağı Rest üst bilgileri](headers.md) .

Yukarıdaki üst bilgilere ek olarak, dosyalar sıkıştırılmış bant genişliği ve indirme süreleriyle sıkıştırılmış olarak alınabilir. Dosyalar varsayılan olarak sıkıştırılmaz. Dosyaların sıkıştırılmış sürümlerini almak için aşağıdaki üst bilgi değerini ekleyebilirsiniz. Sıkıştırılan sayfaların yalnızca 2020 Nisan 'dan kullanılabildiğini, 2020 Nisan 'dan önceki tüm isteklerin yalnızca sıkıştırılmamış olarak kullanılabildiğini unutmayın.

| Üst bilgi                   | Değer Türü     | Değer | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| string   | Söndür| İsteğe bağlı. Atlanan dosya akışı sıkıştırmamışsa.       |

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='201909')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem bir dosya akışı olarak yabancı Exchange ücretleri döndürür. Dosya akışı bir. csv dosyası ya da. csv 'nin zip ile sıkıştırılmış bir sürümüdür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 18548
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=fxrates
Request-ID: 65fb6e59-051b-42f7-8771-c8c139b3c901
Date: Wed, 02 Oct 2019 03:42:54 GMT

"CurrencyCode","USDPerUnit","Month"
"AED","0.27224589249009701","2019”
======= Truncated ==============

```
