---
title: Bir referans oluşturma
description: Iş ortağı API 'sinde bağımsız veya paylaşılan başvurular oluşturun.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6aab4b5f45030c3c16294b2929b1a6d3086fb951
ms.sourcegitcommit: 3c165938f544ff226cbe11ca21ed5aa00448d9b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "97770610"
---
# <a name="create-a-referral"></a>Bir referans oluşturma

Aşağıdakiler cihazlar için geçerlidir:

- İş ortağı API 'SI

Bu konu, bir başvurunun nasıl oluşturulacağını açıklamaktadır. İki tür [ReferralType](referral-resources.md#referraltype)vardır:

1. Bağımsız: bir başvurunun bir iş ortağı tarafından görünür olduğu yer.
2. Paylaşıldı: bir başvurunun birlikte çalışan iki taraflarca görünür olduğu durumlar. Örneğin, Microsoft ve iş ortağı bir ortak satış anlaşmayla birlikte çalışıyorsa, her iki taraf arasında bir başvuru paylaşılabilir. Daha fazla bilgi için, [paylaşılan bir başvuru oluşturma](#create-a-shared-referral)bölümüne bakın.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı API kimlik doğrulaması](api-authentication.md)bölümünde açıklandığı gibi kimlik bilgileri. Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="rest-request"></a>REST Isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                  |
|---------|--------------------------------------------------------------|
| **Yayınla** | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

### <a name="request-headers"></a>İstek üst bilgileri

- Daha fazla bilgi için bkz. [Iş ortağı API Rest üst bilgileri](headers.md) .

### <a name="request-body"></a>İstek gövdesi

Bu tablo, yeni bir başvuru için istek gövdesinde [başvuru](referral-resources.md) özelliklerini açıklar.

| Özellik            | Tür                                                                 | Açıklama                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Ad                | string                                                               | Başvurunun adı.                                                                                            |
| Externalreferenceıd | string                                                               | Başvuru için bir dış tanımlayıcı. Örneğin, kendi Dynamics 365 müşteri adayı veya fırsat KIMLIĞINIZ.                   |
| Durum              | [ReferralStatus](referral-resources.md#referralstatus)               | Başvuru durumunu gösteren değerleri içeren bir [sabit listesi](https://docs.microsoft.com/dotnet/api/system.enum) .          |
| Dosya           | [ReferralSubstatus](referral-resources.md#referralsubstatus)         | Başvuru alt durumu belirten değerleri olan bir [sabit listesi](https://docs.microsoft.com/dotnet/api/system.enum) .       |
| StatusReason        | string                                                               | Durum hakkında açıklayıcı bir ileti. Örneğin, başvurunun neden kaybolduğunu açıklayın.                            |
| ReferralType        | [ReferralType](referral-resources.md#referraltype)                   | Başvuru türünü temsil eder. **Gerekli.**                                                                                        |
| Eleme       | [ReferralQualification](referral-resources.md#referralqualification) | Başvurunun kalitesini temsil eder.                                                                              |
| CustomerProfile     | [CustomerProfile](referral-resources.md#customerprofile)             | Müşteri iletişim bilgileri.  **Gerekli.**                                                                                      |
| Onay             | [Onay](referral-resources.md#consent)                             | Diğer kuruluşlarla bilgi paylaşma ve kullanıcıların kullanıcılarla iletişim kurmasına izin verme bayrakları. **Gerekli.**               |
| Ayrıntılar             | [ReferralDetails](referral-resources.md#referraldetails)             | Müşteri ayrıntıları, notlar, anlaşma değeri, para birimi kapanış tarihi. **Gerekli.**                                                           |
| Takım                | [Üye](referral-resources.md#member)                               | İş ortağı katılımında yer alan kuruluşlardaki kullanıcıları temsil eder.                                   |
| Davet edilen Tecontext       | [Davet edilen Tecontext](referral-resources.md#invitecontext)                 | Bir kullanıcının iş ortağı katılımında başka bir kuruluş davet ederken sağlayasun, daha fazla bilgi temsil eder. |
| Hedef         | [ReferralTarget](referral-resources.md#target)        | Bir kullanıcının iş ortağı katılımında başka bir kuruluş davet ederken sağlayasun, daha fazla bilgi temsil eder.  |

#### <a name="status--substatus-transition-states"></a>Durum & alt durum geçiş durumları

| Durum | İzin verilen durum geçişi | İzin verilen alt durum            |
|--------|---------------------------|------------------------------|
| Yeni    | Yeni, etkin, kapalı       | Bekliyor, alındı            |
| Etkin | Etkin, kapalı            | Kabul edildi                     |
| Kapatıldı | Kapatıldı                    | Kazanıldı, kaybedildi, reddedildi, zaman aşımına uğradı |

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partner.microsoft.com/v1.0/engagements/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "name": "Test Cosell Invite_20",
    "status": "New",
    "substatus": "Pending",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
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
    }
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [başvuru](referral-resources.md) kaynağını döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "name": "Test Cosell Invite_20",
    "externalReferenceId": null,
    "createdDateTime": "2019-02-23T02:05:23.2931817Z",
    "updatedDateTime": "2019-02-23T02:05:23.2931817Z",
    "expirationDateTime": null,
    "status": "Active",
    "substatus": "Accepted",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "eTag": "\"00006d10-0000-0000-0000-5c70aa630000\"",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
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

## <a name="create-a-shared-referral"></a>Paylaşılan bir başvuru oluştur

**Paylaşılan** [başvuru türünün](referral-resources.md#referraltype)bir başvurusunu oluşturmak için iki adım vardır.

1. [Paylaşılan başvuruyu oluşturma](#create-your-referral)
2. [İkinci taraf için bağlı bir başvuru oluşturun](#create-a-connected-referral)

Aşağıdaki akış grafiğinde, paylaşılan bir başvuru oluşturma konusunda bu iki adım gösterilmektedir.

![Microsoft Iş ortağı API 'siyle bağlantılı 2 başvuru ile paylaşılan bir başvuruyu gösteren akış grafiği](../images/SharedReferral.png)

### <a name="create-your-referral"></a>Başvuruyu oluşturma

1. [ReferralType](referral-resources.md#referraltype) ayarlanmış bir başvuruyu paylaşılan olarak oluşturun.
2. Dönüş yanıtından **engagementId** kopyalayın.

Başvuru için [ReferralTarget](referral-resources.md#target) örneği

```json
"target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-ABC-DEF"
        }
    ]
```

### <a name="create-a-connected-referral"></a>Bağlı bir başvuru oluştur

1. Microsoft için başka bir başvuru oluşturun.
2. Başvurınızdan, birlikte birbirlerine bağlı olmaları için **Enagementıd** 'yi dahil edin.

Microsoft başvurusu için [ReferralTarget](referral-resources.md#target) örneği

```json
"target": [
        {
            "type": "BusinessProfileLocation",
            "id": "msft"
        }
    ]
```