---
title: Müşteri adayını veya fırsatı güncelleştirme (eski)
description: Müşteri adayının veya fırsat ayrıntılarının güncelleştirilmesini sağlar. Bir müşteri adayını veya fırsatı güncelleştirme yöntemi artık kullanılmıyor. bunun yerine düzeltme eki çağrısını kullanarak yeniden yürütülüyor.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 9705db1c21dbec7099cfefebdc7bb23ec65e428c
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770645"
---
# <a name="update-a-lead-or-opportunity-obsolete"></a>Müşteri adayını veya fırsatı güncelleştirme (eski)

Aşağıdakiler cihazlar için geçerlidir:

- İş ortağı API 'SI

Bu konuda, müşteri adayı veya fırsat ayrıntılarının anlaşma değeri, tahmini kapanış tarihi gibi nasıl güncelleştirilmesi veya diğer ayrıntılar arasında satış aşamaları yönetimi açıklanmaktadır. 


> [!IMPORTANT]
Bir müşteri adayını veya fırsatı güncelleştirme yöntemi artık kullanılmıyor. bunun yerine [Düzeltme Eki](patch-a-referral.md) çağrısını kullanarak yeniden yürütülüyor.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı API kimlik doğrulaması](api-authentication.md)bölümünde açıklandığı gibi kimlik bilgileri. Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.
- Bu API Şu anda yalnızca iş ortaklarının şu rollerden birinde olması gereken Kullanıcı erişimini destekliyor: genel yönetici, başvuru Yöneticisi veya başvuru kullanıcısı.

## <a name="rest-request"></a>REST Isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                       |
|---------|-------------------------------------------------------------------|
| **PUT** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="request-headers"></a>İstek üst bilgileri

- Daha fazla bilgi için bkz. [Iş ortağı API Rest üstbilgileri](headers.md).

> [!IMPORTANT]
> **IF-Match** üst bilgisini ayarladığınızdan emin olun.

### <a name="request-body"></a>İstek gövdesi

Bu tablo, istek gövdesinde [başvuru](referral-resources.md) özelliklerini açıklar.

| Özellik            | Tür                                                                 | Description                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Id                  | string                                                               | Bu başvurunun KIMLIĞI.                                                                                            |
| EngagementId        | string                                                               | Bu başvuru için EngagementID. Birden çok başvuru tek bir EngagementID ilişkilendirilebilir                    |
| Name                | string                                                               | Başvurunun adı.                                                                                            |
| Externalreferenceıd | string                                                               | Başvuru için bir dış tanımlayıcı. Örnek: kendi Dynamics 365 müşteri adayı/fırsat KIMLIĞINIZI depolayın                    |
| CreatedDateTime     | UTC Tarih saat biçiminde dize                                       | Başvurunun oluşturulduğu tarih.                                                                                   |
| UpdatedDateTime     | UTC Tarih saat biçiminde dize                                       | Başvurunun en son güncelleştirildiği tarih.                                                                              |
| ExpirationDateTime  | UTC Tarih saat biçiminde dize                                       | Başvurunun sona ereceği tarih.                                                                                   |
| Durum              | [ReferralStatus](referral-resources.md#referralstatus)               | Başvuru durumunu gösteren değerleri içeren bir [sabit listesi](https://docs.microsoft.com/dotnet/api/system.enum) .          |
| Dosya           | [ReferralSubstatus](referral-resources.md#referralsubstatus)         | Başvuru alt durumunu gösteren değerler içeren bir [enum](https://docs.microsoft.com/dotnet/api/system.enum) .      |
| StatusReason        | string                                                               | Durum hakkında açıklayıcı bir ileti. Örneğin, başvurunun neden kaybolduğunu açıklayın.                              |
| ReferralType        | [ReferralType](referral-resources.md#referraltype)                   | Başvuru türünü temsil eder.                                                                                        |
| Eleme       | [ReferralQualification](referral-resources.md#referralqualification) | Başvurunun kalitesini temsil eder.                                                                              |
| CustomerProfile     | [CustomerProfile](referral-resources.md#customerprofile)             | Müşteri iletişim bilgileri.                                                                                        |
| Onay             | [Onay](referral-resources.md#consent)                             | Diğer kuruluşlarla bilgi paylaşma ve kullanıcıların kullanıcılarla iletişim kurmasına izin verme bayrakları.                |
| Ayrıntılar             | [ReferralDetails](referral-resources.md#referraldetails)             | Müşteri ayrıntıları, notlar, anlaşma değeri, para birimi kapanış tarihi.                                                          |
| Takım                | [Üye](referral-resources.md#member)                               | İş ortağı katılımında yer alan kuruluşlardaki kullanıcıları temsil eder.                                   |
| Davet edilen Tecontext       | [Davet edilen Tecontext](referral-resources.md#invitecontext)                 | Bir kullanıcının iş ortağı katılımında başka bir kuruluş davet ederken sağlayasun, daha fazla bilgi temsil eder. |
| Hedef         | [ReferralTarget](referral-resources.md#target)        | Bir kullanıcının iş ortağı katılımında başka bir kuruluş davet ederken sağlayasun, daha fazla bilgi temsil eder.  |

### <a name="status-and-substatus-transition-states"></a>Durum ve alt durum geçiş durumları

| Durum | İzin verilen durum geçişi | İzin verilen alt durum            |
|--------|---------------------------|------------------------------|
| Yeni    | Yeni, etkin, kapalı       | Bekliyor, alındı            |
| Etkin | Etkin, kapalı            | Kabul edildi                     |
| Kapatıldı | Kapatıldı                    | Kazanıldı, kaybedildi, reddedildi, zaman aşımına uğradı |

### <a name="request-example"></a>İstek örneği

```http
PUT https://api.partner.microsoft.com/v1.0/engagements/referrals/49d90c72-3326-4f61-aacc-2cb57970448c HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "id": "49d90c72-3326-4f61-aacc-2cb57970448c",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:40:42.6178337Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "closingDateTime": "2018-11-14T00:00:00Z",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",

}
```

> [!IMPORTANT]
> `"links": { }`NESNEYI put kaynağından kaldırın.

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [başvuru](referral-resources.md) kaynağını döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:43:38.9948636Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",
    "links": {
        "relatedReferrals": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals?$filter=engagementId eq '37ef26aa-1d15-4533-9f93-a69bd33ab1e5'",
            "method": "GET"
        },
        "self": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals/4111fffc-f9ee-4d53-bba6-569135228642",
            "method": "GET"
        }
    }
}
```