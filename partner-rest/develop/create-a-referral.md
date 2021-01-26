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
# <a name="create-a-referral"></a><span data-ttu-id="53174-103">Bir referans oluşturma</span><span class="sxs-lookup"><span data-stu-id="53174-103">Create a referral</span></span>

<span data-ttu-id="53174-104">Aşağıdakiler cihazlar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="53174-104">Applies to:</span></span>

- <span data-ttu-id="53174-105">İş ortağı API 'SI</span><span class="sxs-lookup"><span data-stu-id="53174-105">Partner API</span></span>

<span data-ttu-id="53174-106">Bu konu, bir başvurunun nasıl oluşturulacağını açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="53174-106">This topic explains how to create a referral.</span></span> <span data-ttu-id="53174-107">İki tür [ReferralType](referral-resources.md#referraltype)vardır:</span><span class="sxs-lookup"><span data-stu-id="53174-107">There are two types of [ReferralType](referral-resources.md#referraltype):</span></span>

1. <span data-ttu-id="53174-108">Bağımsız: bir başvurunun bir iş ortağı tarafından görünür olduğu yer.</span><span class="sxs-lookup"><span data-stu-id="53174-108">Independent: Where a referral is visible to one partner.</span></span>
2. <span data-ttu-id="53174-109">Paylaşıldı: bir başvurunun birlikte çalışan iki taraflarca görünür olduğu durumlar.</span><span class="sxs-lookup"><span data-stu-id="53174-109">Shared: Where a referral is visible to two parties that are working together.</span></span> <span data-ttu-id="53174-110">Örneğin, Microsoft ve iş ortağı bir ortak satış anlaşmayla birlikte çalışıyorsa, her iki taraf arasında bir başvuru paylaşılabilir.</span><span class="sxs-lookup"><span data-stu-id="53174-110">For example, if Microsoft and a partner are working together in a co-selling deal, a referral can be shared between both parties.</span></span> <span data-ttu-id="53174-111">Daha fazla bilgi için, [paylaşılan bir başvuru oluşturma](#create-a-shared-referral)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="53174-111">For more information, see the section [Creating a shared referral](#create-a-shared-referral).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53174-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="53174-112">Prerequisites</span></span>

- <span data-ttu-id="53174-113">[Iş ortağı API kimlik doğrulaması](api-authentication.md)bölümünde açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="53174-113">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="53174-114">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="53174-114">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="53174-115">REST Isteği</span><span class="sxs-lookup"><span data-stu-id="53174-115">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="53174-116">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="53174-116">Request syntax</span></span>

| <span data-ttu-id="53174-117">Yöntem</span><span class="sxs-lookup"><span data-stu-id="53174-117">Method</span></span>  | <span data-ttu-id="53174-118">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="53174-118">Request URI</span></span>                                                  |
|---------|--------------------------------------------------------------|
| <span data-ttu-id="53174-119">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="53174-119">**POST**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

### <a name="request-headers"></a><span data-ttu-id="53174-120">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="53174-120">Request headers</span></span>

- <span data-ttu-id="53174-121">Daha fazla bilgi için bkz. [Iş ortağı API Rest üst bilgileri](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="53174-121">See [Partner API REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="53174-122">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="53174-122">Request body</span></span>

<span data-ttu-id="53174-123">Bu tablo, yeni bir başvuru için istek gövdesinde [başvuru](referral-resources.md) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="53174-123">This table describes the [Referral](referral-resources.md) properties in the request body for a brand new referral.</span></span>

| <span data-ttu-id="53174-124">Özellik</span><span class="sxs-lookup"><span data-stu-id="53174-124">Property</span></span>            | <span data-ttu-id="53174-125">Tür</span><span class="sxs-lookup"><span data-stu-id="53174-125">Type</span></span>                                                                 | <span data-ttu-id="53174-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="53174-126">Description</span></span>                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="53174-127">Ad</span><span class="sxs-lookup"><span data-stu-id="53174-127">Name</span></span>                | <span data-ttu-id="53174-128">string</span><span class="sxs-lookup"><span data-stu-id="53174-128">string</span></span>                                                               | <span data-ttu-id="53174-129">Başvurunun adı.</span><span class="sxs-lookup"><span data-stu-id="53174-129">The name of the Referral.</span></span>                                                                                            |
| <span data-ttu-id="53174-130">Externalreferenceıd</span><span class="sxs-lookup"><span data-stu-id="53174-130">ExternalReferenceId</span></span> | <span data-ttu-id="53174-131">string</span><span class="sxs-lookup"><span data-stu-id="53174-131">string</span></span>                                                               | <span data-ttu-id="53174-132">Başvuru için bir dış tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="53174-132">An external identifier for the referral.</span></span> <span data-ttu-id="53174-133">Örneğin, kendi Dynamics 365 müşteri adayı veya fırsat KIMLIĞINIZ.</span><span class="sxs-lookup"><span data-stu-id="53174-133">For example, your own Dynamics 365 lead or opportunity ID.</span></span>                   |
| <span data-ttu-id="53174-134">Durum</span><span class="sxs-lookup"><span data-stu-id="53174-134">Status</span></span>              | [<span data-ttu-id="53174-135">ReferralStatus</span><span class="sxs-lookup"><span data-stu-id="53174-135">ReferralStatus</span></span>](referral-resources.md#referralstatus)               | <span data-ttu-id="53174-136">Başvuru durumunu gösteren değerleri içeren bir [sabit listesi](https://docs.microsoft.com/dotnet/api/system.enum) .</span><span class="sxs-lookup"><span data-stu-id="53174-136">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.</span></span>          |
| <span data-ttu-id="53174-137">Dosya</span><span class="sxs-lookup"><span data-stu-id="53174-137">Substatus</span></span>           | [<span data-ttu-id="53174-138">ReferralSubstatus</span><span class="sxs-lookup"><span data-stu-id="53174-138">ReferralSubstatus</span></span>](referral-resources.md#referralsubstatus)         | <span data-ttu-id="53174-139">Başvuru alt durumu belirten değerleri olan bir [sabit listesi](https://docs.microsoft.com/dotnet/api/system.enum) .</span><span class="sxs-lookup"><span data-stu-id="53174-139">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral substatus.</span></span>       |
| <span data-ttu-id="53174-140">StatusReason</span><span class="sxs-lookup"><span data-stu-id="53174-140">StatusReason</span></span>        | <span data-ttu-id="53174-141">string</span><span class="sxs-lookup"><span data-stu-id="53174-141">string</span></span>                                                               | <span data-ttu-id="53174-142">Durum hakkında açıklayıcı bir ileti.</span><span class="sxs-lookup"><span data-stu-id="53174-142">A descriptive message about the status.</span></span> <span data-ttu-id="53174-143">Örneğin, başvurunun neden kaybolduğunu açıklayın.</span><span class="sxs-lookup"><span data-stu-id="53174-143">For example, explain why the referral was lost.</span></span>                            |
| <span data-ttu-id="53174-144">ReferralType</span><span class="sxs-lookup"><span data-stu-id="53174-144">ReferralType</span></span>        | [<span data-ttu-id="53174-145">ReferralType</span><span class="sxs-lookup"><span data-stu-id="53174-145">ReferralType</span></span>](referral-resources.md#referraltype)                   | <span data-ttu-id="53174-146">Başvuru türünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="53174-146">Represents the referral type.</span></span> <span data-ttu-id="53174-147">**Gerekli.**</span><span class="sxs-lookup"><span data-stu-id="53174-147">**Required.**</span></span>                                                                                        |
| <span data-ttu-id="53174-148">Eleme</span><span class="sxs-lookup"><span data-stu-id="53174-148">Qualification</span></span>       | [<span data-ttu-id="53174-149">ReferralQualification</span><span class="sxs-lookup"><span data-stu-id="53174-149">ReferralQualification</span></span>](referral-resources.md#referralqualification) | <span data-ttu-id="53174-150">Başvurunun kalitesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="53174-150">Represents the quality of the referral.</span></span>                                                                              |
| <span data-ttu-id="53174-151">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="53174-151">CustomerProfile</span></span>     | [<span data-ttu-id="53174-152">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="53174-152">CustomerProfile</span></span>](referral-resources.md#customerprofile)             | <span data-ttu-id="53174-153">Müşteri iletişim bilgileri.</span><span class="sxs-lookup"><span data-stu-id="53174-153">Customer contact information.</span></span>  <span data-ttu-id="53174-154">**Gerekli.**</span><span class="sxs-lookup"><span data-stu-id="53174-154">**Required.**</span></span>                                                                                      |
| <span data-ttu-id="53174-155">Onay</span><span class="sxs-lookup"><span data-stu-id="53174-155">Consent</span></span>             | [<span data-ttu-id="53174-156">Onay</span><span class="sxs-lookup"><span data-stu-id="53174-156">Consent</span></span>](referral-resources.md#consent)                             | <span data-ttu-id="53174-157">Diğer kuruluşlarla bilgi paylaşma ve kullanıcıların kullanıcılarla iletişim kurmasına izin verme bayrakları. **Gerekli.**</span><span class="sxs-lookup"><span data-stu-id="53174-157">Consent flags around sharing information with other organizations and allowing them to contact users.**Required.**</span></span>               |
| <span data-ttu-id="53174-158">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="53174-158">Details</span></span>             | [<span data-ttu-id="53174-159">ReferralDetails</span><span class="sxs-lookup"><span data-stu-id="53174-159">ReferralDetails</span></span>](referral-resources.md#referraldetails)             | <span data-ttu-id="53174-160">Müşteri ayrıntıları, notlar, anlaşma değeri, para birimi kapanış tarihi.</span><span class="sxs-lookup"><span data-stu-id="53174-160">Customer details, notes, deal value, currency closing date.</span></span> <span data-ttu-id="53174-161">**Gerekli.**</span><span class="sxs-lookup"><span data-stu-id="53174-161">**Required.**</span></span>                                                           |
| <span data-ttu-id="53174-162">Takım</span><span class="sxs-lookup"><span data-stu-id="53174-162">Team</span></span>                | [<span data-ttu-id="53174-163">Üye</span><span class="sxs-lookup"><span data-stu-id="53174-163">Member</span></span>](referral-resources.md#member)                               | <span data-ttu-id="53174-164">İş ortağı katılımında yer alan kuruluşlardaki kullanıcıları temsil eder.</span><span class="sxs-lookup"><span data-stu-id="53174-164">Represents users in the organizations that are involved in the partner engagement.</span></span>                                   |
| <span data-ttu-id="53174-165">Davet edilen Tecontext</span><span class="sxs-lookup"><span data-stu-id="53174-165">InviteContext</span></span>       | [<span data-ttu-id="53174-166">Davet edilen Tecontext</span><span class="sxs-lookup"><span data-stu-id="53174-166">InviteContext</span></span>](referral-resources.md#invitecontext)                 | <span data-ttu-id="53174-167">Bir kullanıcının iş ortağı katılımında başka bir kuruluş davet ederken sağlayasun, daha fazla bilgi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="53174-167">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span> |
| <span data-ttu-id="53174-168">Hedef</span><span class="sxs-lookup"><span data-stu-id="53174-168">Target</span></span>         | [<span data-ttu-id="53174-169">ReferralTarget</span><span class="sxs-lookup"><span data-stu-id="53174-169">ReferralTarget</span></span>](referral-resources.md#target)        | <span data-ttu-id="53174-170">Bir kullanıcının iş ortağı katılımında başka bir kuruluş davet ederken sağlayasun, daha fazla bilgi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="53174-170">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span>  |

#### <a name="status--substatus-transition-states"></a><span data-ttu-id="53174-171">Durum & alt durum geçiş durumları</span><span class="sxs-lookup"><span data-stu-id="53174-171">Status & Substatus transition states</span></span>

| <span data-ttu-id="53174-172">Durum</span><span class="sxs-lookup"><span data-stu-id="53174-172">Status</span></span> | <span data-ttu-id="53174-173">İzin verilen durum geçişi</span><span class="sxs-lookup"><span data-stu-id="53174-173">Allowed status transition</span></span> | <span data-ttu-id="53174-174">İzin verilen alt durum</span><span class="sxs-lookup"><span data-stu-id="53174-174">Allowed substatus</span></span>            |
|--------|---------------------------|------------------------------|
| <span data-ttu-id="53174-175">Yeni</span><span class="sxs-lookup"><span data-stu-id="53174-175">New</span></span>    | <span data-ttu-id="53174-176">Yeni, etkin, kapalı</span><span class="sxs-lookup"><span data-stu-id="53174-176">New, Active, Closed</span></span>       | <span data-ttu-id="53174-177">Bekliyor, alındı</span><span class="sxs-lookup"><span data-stu-id="53174-177">Pending, Received</span></span>            |
| <span data-ttu-id="53174-178">Etkin</span><span class="sxs-lookup"><span data-stu-id="53174-178">Active</span></span> | <span data-ttu-id="53174-179">Etkin, kapalı</span><span class="sxs-lookup"><span data-stu-id="53174-179">Active, Closed</span></span>            | <span data-ttu-id="53174-180">Kabul edildi</span><span class="sxs-lookup"><span data-stu-id="53174-180">Accepted</span></span>                     |
| <span data-ttu-id="53174-181">Kapatıldı</span><span class="sxs-lookup"><span data-stu-id="53174-181">Closed</span></span> | <span data-ttu-id="53174-182">Kapatıldı</span><span class="sxs-lookup"><span data-stu-id="53174-182">Closed</span></span>                    | <span data-ttu-id="53174-183">Kazanıldı, kaybedildi, reddedildi, zaman aşımına uğradı</span><span class="sxs-lookup"><span data-stu-id="53174-183">Won, Lost, Declined, Expired</span></span> |

### <a name="request-example"></a><span data-ttu-id="53174-184">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="53174-184">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="53174-185">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="53174-185">REST Response</span></span>

<span data-ttu-id="53174-186">Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [başvuru](referral-resources.md) kaynağını döndürür.</span><span class="sxs-lookup"><span data-stu-id="53174-186">If successful, this method returns the populated [Referral](referral-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="53174-187">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="53174-187">Response success and error codes</span></span>

<span data-ttu-id="53174-188">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="53174-188">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="53174-189">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="53174-189">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="53174-190">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="53174-190">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="53174-191">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="53174-191">Response example</span></span>

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

## <a name="create-a-shared-referral"></a><span data-ttu-id="53174-192">Paylaşılan bir başvuru oluştur</span><span class="sxs-lookup"><span data-stu-id="53174-192">Create a shared referral</span></span>

<span data-ttu-id="53174-193">**Paylaşılan** [başvuru türünün](referral-resources.md#referraltype)bir başvurusunu oluşturmak için iki adım vardır.</span><span class="sxs-lookup"><span data-stu-id="53174-193">There are two steps to create a referral of the **Shared** [referral type](referral-resources.md#referraltype).</span></span>

1. [<span data-ttu-id="53174-194">Paylaşılan başvuruyu oluşturma</span><span class="sxs-lookup"><span data-stu-id="53174-194">Create your shared referral</span></span>](#create-your-referral)
2. [<span data-ttu-id="53174-195">İkinci taraf için bağlı bir başvuru oluşturun</span><span class="sxs-lookup"><span data-stu-id="53174-195">Create a connected referral for the second party</span></span>](#create-a-connected-referral)

<span data-ttu-id="53174-196">Aşağıdaki akış grafiğinde, paylaşılan bir başvuru oluşturma konusunda bu iki adım gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="53174-196">The following flow chart illustrates these two steps in creating a shared referral.</span></span>

![Microsoft Iş ortağı API 'siyle bağlantılı 2 başvuru ile paylaşılan bir başvuruyu gösteren akış grafiği](../images/SharedReferral.png)

### <a name="create-your-referral"></a><span data-ttu-id="53174-198">Başvuruyu oluşturma</span><span class="sxs-lookup"><span data-stu-id="53174-198">Create your referral</span></span>

1. <span data-ttu-id="53174-199">[ReferralType](referral-resources.md#referraltype) ayarlanmış bir başvuruyu paylaşılan olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="53174-199">Create a referral with [ReferralType](referral-resources.md#referraltype) set to shared.</span></span>
2. <span data-ttu-id="53174-200">Dönüş yanıtından **engagementId** kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="53174-200">Copy the **engagementId** from the return response.</span></span>

<span data-ttu-id="53174-201">Başvuru için [ReferralTarget](referral-resources.md#target) örneği</span><span class="sxs-lookup"><span data-stu-id="53174-201">[ReferralTarget](referral-resources.md#target) sample for referral</span></span>

```json
"target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-ABC-DEF"
        }
    ]
```

### <a name="create-a-connected-referral"></a><span data-ttu-id="53174-202">Bağlı bir başvuru oluştur</span><span class="sxs-lookup"><span data-stu-id="53174-202">Create a connected referral</span></span>

1. <span data-ttu-id="53174-203">Microsoft için başka bir başvuru oluşturun.</span><span class="sxs-lookup"><span data-stu-id="53174-203">Create another referral for Microsoft.</span></span>
2. <span data-ttu-id="53174-204">Başvurınızdan, birlikte birbirlerine bağlı olmaları için **Enagementıd** 'yi dahil edin.</span><span class="sxs-lookup"><span data-stu-id="53174-204">Include the **enagementId** from your referral so they are tied together.</span></span>

<span data-ttu-id="53174-205">Microsoft başvurusu için [ReferralTarget](referral-resources.md#target) örneği</span><span class="sxs-lookup"><span data-stu-id="53174-205">[ReferralTarget](referral-resources.md#target) sample for Microsoft referral</span></span>

```json
"target": [
        {
            "type": "BusinessProfileLocation",
            "id": "msft"
        }
    ]
```