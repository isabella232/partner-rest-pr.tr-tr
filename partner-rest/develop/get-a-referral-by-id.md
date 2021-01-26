---
title: Kimliğe göre bir müşteri adayı veya fırsat alma
description: Kimliğe göre bir müşteri adayı veya fırsat alın.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: dcfaea393afc6a9d09946b4c31b7168ba26aa255
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770637"
---
# <a name="get-a-lead-or-opportunity-by-id"></a><span data-ttu-id="7544e-103">Kimliğe göre bir müşteri adayı veya fırsat alma</span><span class="sxs-lookup"><span data-stu-id="7544e-103">Get a lead or opportunity by Id</span></span>

<span data-ttu-id="7544e-104">Aşağıdakiler cihazlar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="7544e-104">Applies to:</span></span>

- <span data-ttu-id="7544e-105">İş ortağı API 'SI</span><span class="sxs-lookup"><span data-stu-id="7544e-105">Partner API</span></span>

<span data-ttu-id="7544e-106">Bu konuda, kimliğe göre bir müşteri adayı veya ortak satış fırsatı alma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7544e-106">This topic explains how to get a lead or co-sell opportunity by Id.</span></span>

> [!Note]
> <span data-ttu-id="7544e-107">Microsoft ticari Market 'ten (Azure Marketi ve AppSource) alınan müşteri adayları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="7544e-107">Leads received from the Microsoft commercial marketplace (Azure Marketplace and AppSource) are not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7544e-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7544e-108">Prerequisites</span></span>

- <span data-ttu-id="7544e-109">[Iş ortağı API kimlik doğrulaması](api-authentication.md)bölümünde açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7544e-109">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="7544e-110">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="7544e-110">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="7544e-111">Bu API Şu anda yalnızca iş ortaklarının şu rollerden birinde olması gereken Kullanıcı erişimini destekliyor: genel yönetici, başvuru Yöneticisi veya başvuru kullanıcısı.</span><span class="sxs-lookup"><span data-stu-id="7544e-111">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="7544e-112">REST isteği</span><span class="sxs-lookup"><span data-stu-id="7544e-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7544e-113">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7544e-113">Request syntax</span></span>

| <span data-ttu-id="7544e-114">Yöntem</span><span class="sxs-lookup"><span data-stu-id="7544e-114">Method</span></span>   | <span data-ttu-id="7544e-115">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="7544e-115">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7544e-116">**Al**</span><span class="sxs-lookup"><span data-stu-id="7544e-116">**GET**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}>                                     |

### <a name="uri-parameter"></a><span data-ttu-id="7544e-117">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="7544e-117">URI parameter</span></span>


| <span data-ttu-id="7544e-118">Ad</span><span class="sxs-lookup"><span data-stu-id="7544e-118">Name</span></span>                   | <span data-ttu-id="7544e-119">Tür</span><span class="sxs-lookup"><span data-stu-id="7544e-119">Type</span></span>     | <span data-ttu-id="7544e-120">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7544e-120">Required</span></span> | <span data-ttu-id="7544e-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7544e-121">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="7544e-122">Id</span><span class="sxs-lookup"><span data-stu-id="7544e-122">Id</span></span>                      | <span data-ttu-id="7544e-123">string</span><span class="sxs-lookup"><span data-stu-id="7544e-123">string</span></span>   | <span data-ttu-id="7544e-124">Yes</span><span class="sxs-lookup"><span data-stu-id="7544e-124">Yes</span></span>       | <span data-ttu-id="7544e-125">Bir müşteri adayı veya ortak satış fırsatının benzersiz tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="7544e-125">The unique identifier for a lead or co-sell opportunity</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="7544e-126">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="7544e-126">Request headers</span></span>

<span data-ttu-id="7544e-127">Daha fazla bilgi için bkz. [Iş ortağı Rest üst bilgileri](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="7544e-127">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="7544e-128">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="7544e-128">Request body</span></span>

<span data-ttu-id="7544e-129">Yok.</span><span class="sxs-lookup"><span data-stu-id="7544e-129">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7544e-130">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="7544e-130">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id} HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="7544e-131">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="7544e-131">REST response</span></span>

<span data-ttu-id="7544e-132">Başarılı olursa, yanıt gövdesi kimliği eşleşen [müşteri adayını veya fırsatı](referral-resources.md) içerir.</span><span class="sxs-lookup"><span data-stu-id="7544e-132">If successful, the response body contains the [lead or opportunity](referral-resources.md) matching the Id.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7544e-133">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="7544e-133">Response success and error codes</span></span>

<span data-ttu-id="7544e-134">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir [http durum kodu](error-codes.md) ile gelir.</span><span class="sxs-lookup"><span data-stu-id="7544e-134">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7544e-135">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7544e-135">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="7544e-136">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="7544e-136">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Type: application/json
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731

{
    "@odata.context": "https://api.partner.microsoft.com/v1.0/engagments/referrals/$metadata#Referrals/$entity",
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
      "notes": "We are interested in deploying Microsoft 365 and are looking forsupport in training our employees. Can you help?",
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
        "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'",
        "method": "GET"
      },
      "self": {
        "uri": "https://api.partner.microsoft.com/v1.0/engagements/referralsc5fbb3b6-be74-4795-9fb5-4324c73fed37",
        "method": "GET"
      }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\""
}
```

> [!Note]
> <span data-ttu-id="7544e-137">Yukarıdaki örnekteki illustratration alanları ayrıntılı değildir.</span><span class="sxs-lookup"><span data-stu-id="7544e-137">The fields in the example illustratration above are not exhaustive.</span></span> <span data-ttu-id="7544e-138">Gerçek API yanıtı, müşteri ve iş ortağı takımları gibi daha fazla alan içerir.</span><span class="sxs-lookup"><span data-stu-id="7544e-138">The actual API response contains more fields like the customer and partner teams.</span></span> <span data-ttu-id="7544e-139">Desteklenen alanların tam listesi için bkz. [başvuru kaynakları](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="7544e-139">For the full list of supported fields, see [referral resources](referral-resources.md).</span></span>