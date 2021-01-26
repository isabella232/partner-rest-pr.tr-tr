---
title: Müşteri adaylarının ve fırsatların bir listesini alın
description: Iş ortağı API 'sini kullanarak müşteri adaylarının ve fırsatların bir listesini alma.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 46243f8484a8068827e24e1d03f39ffddade1dbf
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770634"
---
# <a name="get-the-list-of-leads-and-opportunities"></a>Müşteri adaylarının ve fırsatların listesini alma

Aşağıdakiler cihazlar için geçerlidir:

- İş ortağı API 'SI

 Bu konu başlığı altında, Microsoft çözüm sağlayıcısı sayfasından alınan müşteri adaylarının listesinin yanı sıra Microsoft satıcılarından veya diğer iş ortaklarından alınan ortak satış fırsatlarının nasıl alınacağı açıklanmaktadır. Bu, kuruluşunuz tarafından oluşturulan ortak satış fırsatları veya işlem hattı anlaşmaları listesini de getirir.

> [!Note]
> Microsoft ticari Market 'ten (Azure Marketi ve AppSource) alınan müşteri adayları desteklenmez.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı API kimlik doğrulaması](api-authentication.md)bölümünde açıklandığı gibi kimlik bilgileri. Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.
- Bu API Şu anda yalnızca iş ortaklarının şu rollerden birinde olması gereken Kullanıcı erişimini destekliyor: genel yönetici, başvuru Yöneticisi veya başvuru kullanıcısı.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                    |
|:--------|:---------------------------------------------------------------|
| **Al** | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

#### <a name="supported-odata-operations"></a>Desteklenen OData işlemleri

| Ad     | Açıklama     | Gerekli    | Örnek                                                                                                                                                                                                                                                     |
|:---------|:----------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| $select  | Alanları seçer  | No          | `/referrals?$select=id,status,customerProfile`                                                                                                                                                                                                              |
| $filter  | Filtre sonuçları | Önerilen | `/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'` <br/> `/referrals?$filter=status eq 'New' and qualification eq 'SalesQualified'` <br/> `/referrals?$filter=customerProfile/address/country eq 'US' and direction eq 'Incoming'` |
| $orderby | Sipariş sonuçları  | Önerilen | `/referrals?$orderby=createdDateTime desc`                                                                                                                                                                                                                  |

#### <a name="supported-orderby-parameters"></a>Desteklenen OrderBy parametreleri

Müşteri adayları ve fırsatların listesini sıralamak için aşağıdaki $orderby parametrelerini kullanın

| Ad            | Tür     | Description                                       |
|:----------------|:---------|:--------------------------------------------------|
| Saati | DateTime | Müşteri adayının veya fırsatın Oluşturulma tarihi ve saati |
| updatedDateTime | DateTime | Müşteri adayının veya fırsatın tarih ve saatini güncelleştirme   |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı Rest üst bilgileri](headers.md) .

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$orderby=createdDateTime desc HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi bir [müşteri adayı ve/veya fırsat](referral-resources.md)koleksiyonu içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir [http durum kodu](error-codes.md) ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.

### <a name="response-example"></a>Yanıt örneği

``` http
HTTP/1.1 200 OK
Content-Type: application/json
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731

{
  "@odata.context": "http://api.partner.microsoft.com/v1.0/$metadata#Referrals",
  "@odata.count": 1,
  "value": [
    {
      "id": "c5fbb3b6-be74-4795-9fb5-4324c73fed37",
      "engagementId": "65edc0b5-3485-41b7-a17e-dfa9ef4706e2",
      "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
      "organizationName": "Contoso Company",
      "createdDateTime": "2020-10-30T21:03:00.0000000Z",
      "updatedDateTime": "2020-10-30T21:03:00.0000000Z",
      "status": "New",
      "substatus": "Pending",
      "qualification": "Direct",
      "type": "Independent",
      "direction": "Incoming",
      "customerProfile": {
        "name": "Fabrikam Customer Inc",
        "address": {
          "addressLine1": "One Microsoft Way",
          "addressLine2": "",
          "city": "Redmond",
          "state": "WA",
          "postalCode": "98052",
          "country": "US"
        }
      },
      "details": {
        "notes": "We are interested in deploying Microsoft 365 and are looking for support in training our employees. Can you help?",
        "dealValue": 10000,
        "currency": "USD",
        "closingDateTime": "2020-12-01T00:00:00Z",
        "requirements": {
            "industries": [ { "id": "Education" } ],
            "products": [ { "id": "Microsoft365" } ],
            "services": [ { "id": "LearningAndCertification" } ],
            "solutions": [ { "id": "SOL-Microsoft365", "name": "Microsoft365" }
          ]
        }
      },
      "links": {
        "relatedReferrals": {
          "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'",
          "method": "GET"
        },
        "self": {
          "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals/c5fbb3b6-be74-4795-9fb5-4324c73fed37",
          "method": "GET"
        }
      }
    }
  ],
  "@odata.nextLink": "http://api.partner.microsoft.com/v1.0/referrals?$skiptoken=k181pEdP0ykypkieJfcxX"
}
```

`@odata.nextLink`Sonuçların sonraki sayfasına ulaşmak için öğesini kullanın.

> [!Note]
> Yukarıdaki örnekteki illustratration alanları ayrıntılı değildir. Gerçek API yanıtı, müşteri ve iş ortağı takımları gibi daha fazla alan içerir. Desteklenen alanların tam listesi için bkz. [başvuru kaynakları](referral-resources.md).

## <a name="sample-requests"></a>Örnek istekler

1. En son gelen 10 ortak satış fırsatlarını alır. İstek, bir Microsoft satış temsilcisi veya başka bir iş ortağı tarafından başlatılan fırsatları sunarak, kuruluşunuzu ortak satış etkinliğine katılması için davet eder.
    
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(type eq 'Shared' and direction eq 'Incoming')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

2. Yanıt verilmeyen en son gelen müşteri adaylarını ve fırsatları alır.  

    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(direction eq 'Incoming' and substatus eq 'Pending')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

    > [!Important]
    > Ayrılan süre (Şu anda 14 gün) içinde bir müşteri adayına veya fırsata yanıt vermezse, bunu süresi dolduğunda, Microsoft veya size bu fırsatı gönderen iş ortağına bildirir.

3. Kuruluşunuz tarafından başlatılan ve belirli bir satıcı tarafından çalışan en son etkin ortak satış fırsatlarını alır.
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=status eq 'Active' and direction eq 'Outgoing' and type eq 'Shared' and team/any(t:t/email eq 'r2d2@contoso.com')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```