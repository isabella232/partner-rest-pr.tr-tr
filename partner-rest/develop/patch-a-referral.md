---
title: Bir müşteri adayı veya fırsat güncelleştirme
description: Müşteri adayının veya fırsat ayrıntılarının güncelleştirilmesini sağlar.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: abfe7308f46cd65b9358b369f6fa05bcca4c1df2
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770642"
---
# <a name="update-a-lead-or-opportunity"></a>Bir müşteri adayı veya fırsat güncelleştirme

Aşağıdakiler cihazlar için geçerlidir:

- İş ortağı API 'SI

Bu konuda, müşteri adayı veya fırsat ayrıntılarının anlaşma değeri, tahmini kapanış tarihi gibi nasıl güncelleştirilmesi veya diğer ayrıntılar arasında satış aşamaları yönetimi açıklanmaktadır.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı API kimlik doğrulaması](api-authentication.md)bölümünde açıklandığı gibi kimlik bilgileri. Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.
- Bu API Şu anda yalnızca iş ortaklarının şu rollerden birinde olması gereken Kullanıcı erişimini destekliyor: genel yönetici, başvuru Yöneticisi veya başvuru kullanıcısı.

## <a name="rest-request"></a>REST Isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                       |
|---------|-------------------------------------------------------------------|
| **DÜZELTMESI** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="uri-parameter"></a>URI parametresi


| Ad                   | Tür     | Gerekli | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Id                      | string   | Yes       | Bir müşteri adayı veya ortak satış fırsatının benzersiz tanımlayıcısı       |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı Rest üst bilgileri](headers.md) .

### <a name="request-body"></a>İstek gövdesi

İstek gövdesi [JSON yaması](https://tools.ietf.org/html/rfc6902) biçimini izler. JSON yama belgesinde bir dizi işlem vardır. Her işlem belirli bir değişiklik türünü tanımlar. Bu tür değişikliklere örnek olarak bir dizi öğesi ekleme veya bir özellik değeri değiştirme sayılabilir.

> [!Important]
> API Şu anda yalnızca `replace` ve işlemlerini destekler `add` .

### <a name="request-example"></a>İstek örneği

```http
PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
Authorization: Bearer <token>
Content-Type: application/json
Prefer: return=representation

[
    {
        "op": "replace",
        "path": "/details/dealValue",
        "value": "10000"
    },
    {
        "op": "add",
        "path": "/team/-",
        "value": {
            "email": "jane.doe@contoso.com",
            "firstName": "Jane",
            "lastName": "Doe",
            "phoneNumber": "0000000001"
        }
    }
]
```

> [!Note]
> **IF-Match** üst bilgisi geçiriliyorsa eşzamanlılık denetimi için kullanılacaktır.

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi güncelleştirilmiş [müşteri adayını veya fırsatı](referral-resources.md)içerir.


### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir [http durum kodu](error-codes.md) ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.

### <a name="response-example"></a>Yanıt örneği

``` http
HTTP/1.1 204 No Content
Content-Length: 0
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
```

> [!Tip]
> Yanıt gövdesi **tercih** edilen üstbilgiye bağlıdır. İstek içinde üst bilgi değeri atlanırsa, yanıt gövdesi 204 HTTP durum koduyla boştur. `Prefer: return=representation`Güncelleştirilmiş müşteri adayını veya fırsatı almak için üstbilgiye ekleyin.

## <a name="sample-requests"></a>Örnek istekler

1. 10000 'e fırsat için anlaşma değerini güncelleştirir ve notları güncelleştirir. Üst bilgi bağlanılabilirliğinin olmaması nedeniyle eşzamanlılık denetimi yok `If-Match` .
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace","path":"/details/dealValue","value":"10000"},
        {"op":"replace","path":"/details/notes","value":"Lorem ipsum dolor sit amet."}
    ]
    ```

2. Bir müşteri adayının veya kazanılan fırsatın durumunu güncelleştirir.
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace", "path":"/status", "value":"Closed"},
        {"op":"replace", "path":"/substatus", "value":"Won"}
    ]
    ```

    > [!Important]
    > `status`Ve `substatus` alanları, [burada](referral-resources.md)açıklandığı gibi izin verilen geçiş değerleri kümesine uymalıdır.

3. Kuruluşunuzdaki müşteri adayına veya fırsat ekibine yeni bir üye ekler. Bu yanıt, üst bilgi varlığı nedeniyle güncelleştirilmiş müşteri adayını veya fırsatı içerecektir `Prefer: return=representation` .

    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    Prefer: return=representation
    
    [
        {
            "op": "add",
            "path": "/team/-",
            "value": {
                "email": "jane.doe@contoso.com",
                "firstName": "Jane",
                "lastName": "Doe",
                "phoneNumber": "0000000001"
            }
        }
    ]
    ```
