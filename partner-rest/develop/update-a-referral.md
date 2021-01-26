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
# <a name="update-a-lead-or-opportunity-obsolete"></a><span data-ttu-id="7b99f-104">Müşteri adayını veya fırsatı güncelleştirme (eski)</span><span class="sxs-lookup"><span data-stu-id="7b99f-104">Update a lead or opportunity (Obsolete)</span></span>

<span data-ttu-id="7b99f-105">Aşağıdakiler cihazlar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="7b99f-105">Applies to:</span></span>

- <span data-ttu-id="7b99f-106">İş ortağı API 'SI</span><span class="sxs-lookup"><span data-stu-id="7b99f-106">Partner API</span></span>

<span data-ttu-id="7b99f-107">Bu konuda, müşteri adayı veya fırsat ayrıntılarının anlaşma değeri, tahmini kapanış tarihi gibi nasıl güncelleştirilmesi veya diğer ayrıntılar arasında satış aşamaları yönetimi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7b99f-107">This topic explains how to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.</span></span> 


> [!IMPORTANT]
<span data-ttu-id="7b99f-108">Bir müşteri adayını veya fırsatı güncelleştirme yöntemi artık kullanılmıyor. bunun yerine [Düzeltme Eki](patch-a-referral.md) çağrısını kullanarak yeniden yürütülüyor.</span><span class="sxs-lookup"><span data-stu-id="7b99f-108">This method of updating a lead or opportunity is obsolete and we recommmend using the [PATCH](patch-a-referral.md) call instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b99f-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7b99f-109">Prerequisites</span></span>

- <span data-ttu-id="7b99f-110">[Iş ortağı API kimlik doğrulaması](api-authentication.md)bölümünde açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7b99f-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="7b99f-111">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="7b99f-111">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="7b99f-112">Bu API Şu anda yalnızca iş ortaklarının şu rollerden birinde olması gereken Kullanıcı erişimini destekliyor: genel yönetici, başvuru Yöneticisi veya başvuru kullanıcısı.</span><span class="sxs-lookup"><span data-stu-id="7b99f-112">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="7b99f-113">REST Isteği</span><span class="sxs-lookup"><span data-stu-id="7b99f-113">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7b99f-114">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7b99f-114">Request syntax</span></span>

| <span data-ttu-id="7b99f-115">Yöntem</span><span class="sxs-lookup"><span data-stu-id="7b99f-115">Method</span></span>  | <span data-ttu-id="7b99f-116">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="7b99f-116">Request URI</span></span>                                                       |
|---------|-------------------------------------------------------------------|
| <span data-ttu-id="7b99f-117">**PUT**</span><span class="sxs-lookup"><span data-stu-id="7b99f-117">**PUT**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="request-headers"></a><span data-ttu-id="7b99f-118">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="7b99f-118">Request headers</span></span>

- <span data-ttu-id="7b99f-119">Daha fazla bilgi için bkz. [Iş ortağı API Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7b99f-119">For more information, see [Partner API REST headers](headers.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b99f-120">**IF-Match** üst bilgisini ayarladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7b99f-120">Be sure to set the **If-Match** header.</span></span>

### <a name="request-body"></a><span data-ttu-id="7b99f-121">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="7b99f-121">Request body</span></span>

<span data-ttu-id="7b99f-122">Bu tablo, istek gövdesinde [başvuru](referral-resources.md) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="7b99f-122">This table describes the [Referral](referral-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="7b99f-123">Özellik</span><span class="sxs-lookup"><span data-stu-id="7b99f-123">Property</span></span>            | <span data-ttu-id="7b99f-124">Tür</span><span class="sxs-lookup"><span data-stu-id="7b99f-124">Type</span></span>                                                                 | <span data-ttu-id="7b99f-125">Description</span><span class="sxs-lookup"><span data-stu-id="7b99f-125">Description</span></span>                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7b99f-126">Id</span><span class="sxs-lookup"><span data-stu-id="7b99f-126">Id</span></span>                  | <span data-ttu-id="7b99f-127">string</span><span class="sxs-lookup"><span data-stu-id="7b99f-127">string</span></span>                                                               | <span data-ttu-id="7b99f-128">Bu başvurunun KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="7b99f-128">The ID for this Referral.</span></span>                                                                                            |
| <span data-ttu-id="7b99f-129">EngagementId</span><span class="sxs-lookup"><span data-stu-id="7b99f-129">EngagementId</span></span>        | <span data-ttu-id="7b99f-130">string</span><span class="sxs-lookup"><span data-stu-id="7b99f-130">string</span></span>                                                               | <span data-ttu-id="7b99f-131">Bu başvuru için EngagementID.</span><span class="sxs-lookup"><span data-stu-id="7b99f-131">The EngagementID for this Referral.</span></span> <span data-ttu-id="7b99f-132">Birden çok başvuru tek bir EngagementID ilişkilendirilebilir</span><span class="sxs-lookup"><span data-stu-id="7b99f-132">Multiple referrals can be associated to a single EngagementID</span></span>                    |
| <span data-ttu-id="7b99f-133">Name</span><span class="sxs-lookup"><span data-stu-id="7b99f-133">Name</span></span>                | <span data-ttu-id="7b99f-134">string</span><span class="sxs-lookup"><span data-stu-id="7b99f-134">string</span></span>                                                               | <span data-ttu-id="7b99f-135">Başvurunun adı.</span><span class="sxs-lookup"><span data-stu-id="7b99f-135">The name of the Referral.</span></span>                                                                                            |
| <span data-ttu-id="7b99f-136">Externalreferenceıd</span><span class="sxs-lookup"><span data-stu-id="7b99f-136">ExternalReferenceId</span></span> | <span data-ttu-id="7b99f-137">string</span><span class="sxs-lookup"><span data-stu-id="7b99f-137">string</span></span>                                                               | <span data-ttu-id="7b99f-138">Başvuru için bir dış tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="7b99f-138">An external identifier for the referral.</span></span> <span data-ttu-id="7b99f-139">Örnek: kendi Dynamics 365 müşteri adayı/fırsat KIMLIĞINIZI depolayın</span><span class="sxs-lookup"><span data-stu-id="7b99f-139">Example: Store your own Dynamics 365 lead/opportunity ID</span></span>                    |
| <span data-ttu-id="7b99f-140">CreatedDateTime</span><span class="sxs-lookup"><span data-stu-id="7b99f-140">CreatedDateTime</span></span>     | <span data-ttu-id="7b99f-141">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="7b99f-141">string in UTC date time format</span></span>                                       | <span data-ttu-id="7b99f-142">Başvurunun oluşturulduğu tarih.</span><span class="sxs-lookup"><span data-stu-id="7b99f-142">The date the referral was created.</span></span>                                                                                   |
| <span data-ttu-id="7b99f-143">UpdatedDateTime</span><span class="sxs-lookup"><span data-stu-id="7b99f-143">UpdatedDateTime</span></span>     | <span data-ttu-id="7b99f-144">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="7b99f-144">string in UTC date time format</span></span>                                       | <span data-ttu-id="7b99f-145">Başvurunun en son güncelleştirildiği tarih.</span><span class="sxs-lookup"><span data-stu-id="7b99f-145">The date the referral was last updated.</span></span>                                                                              |
| <span data-ttu-id="7b99f-146">ExpirationDateTime</span><span class="sxs-lookup"><span data-stu-id="7b99f-146">ExpirationDateTime</span></span>  | <span data-ttu-id="7b99f-147">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="7b99f-147">string in UTC date time format</span></span>                                       | <span data-ttu-id="7b99f-148">Başvurunun sona ereceği tarih.</span><span class="sxs-lookup"><span data-stu-id="7b99f-148">The date the referral will expire.</span></span>                                                                                   |
| <span data-ttu-id="7b99f-149">Durum</span><span class="sxs-lookup"><span data-stu-id="7b99f-149">Status</span></span>              | [<span data-ttu-id="7b99f-150">ReferralStatus</span><span class="sxs-lookup"><span data-stu-id="7b99f-150">ReferralStatus</span></span>](referral-resources.md#referralstatus)               | <span data-ttu-id="7b99f-151">Başvuru durumunu gösteren değerleri içeren bir [sabit listesi](https://docs.microsoft.com/dotnet/api/system.enum) .</span><span class="sxs-lookup"><span data-stu-id="7b99f-151">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.</span></span>          |
| <span data-ttu-id="7b99f-152">Dosya</span><span class="sxs-lookup"><span data-stu-id="7b99f-152">Substatus</span></span>           | [<span data-ttu-id="7b99f-153">ReferralSubstatus</span><span class="sxs-lookup"><span data-stu-id="7b99f-153">ReferralSubstatus</span></span>](referral-resources.md#referralsubstatus)         | <span data-ttu-id="7b99f-154">Başvuru alt durumunu gösteren değerler içeren bir [enum](https://docs.microsoft.com/dotnet/api/system.enum) .</span><span class="sxs-lookup"><span data-stu-id="7b99f-154">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral sub status.</span></span>      |
| <span data-ttu-id="7b99f-155">StatusReason</span><span class="sxs-lookup"><span data-stu-id="7b99f-155">StatusReason</span></span>        | <span data-ttu-id="7b99f-156">string</span><span class="sxs-lookup"><span data-stu-id="7b99f-156">string</span></span>                                                               | <span data-ttu-id="7b99f-157">Durum hakkında açıklayıcı bir ileti.</span><span class="sxs-lookup"><span data-stu-id="7b99f-157">A descriptive message about the status.</span></span> <span data-ttu-id="7b99f-158">Örneğin, başvurunun neden kaybolduğunu açıklayın.</span><span class="sxs-lookup"><span data-stu-id="7b99f-158">For example, explain why the referral was lost.</span></span>                              |
| <span data-ttu-id="7b99f-159">ReferralType</span><span class="sxs-lookup"><span data-stu-id="7b99f-159">ReferralType</span></span>        | [<span data-ttu-id="7b99f-160">ReferralType</span><span class="sxs-lookup"><span data-stu-id="7b99f-160">ReferralType</span></span>](referral-resources.md#referraltype)                   | <span data-ttu-id="7b99f-161">Başvuru türünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7b99f-161">Represents the referral type.</span></span>                                                                                        |
| <span data-ttu-id="7b99f-162">Eleme</span><span class="sxs-lookup"><span data-stu-id="7b99f-162">Qualification</span></span>       | [<span data-ttu-id="7b99f-163">ReferralQualification</span><span class="sxs-lookup"><span data-stu-id="7b99f-163">ReferralQualification</span></span>](referral-resources.md#referralqualification) | <span data-ttu-id="7b99f-164">Başvurunun kalitesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7b99f-164">Represents the quality of the referral.</span></span>                                                                              |
| <span data-ttu-id="7b99f-165">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="7b99f-165">CustomerProfile</span></span>     | [<span data-ttu-id="7b99f-166">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="7b99f-166">CustomerProfile</span></span>](referral-resources.md#customerprofile)             | <span data-ttu-id="7b99f-167">Müşteri iletişim bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7b99f-167">Customer contact information.</span></span>                                                                                        |
| <span data-ttu-id="7b99f-168">Onay</span><span class="sxs-lookup"><span data-stu-id="7b99f-168">Consent</span></span>             | [<span data-ttu-id="7b99f-169">Onay</span><span class="sxs-lookup"><span data-stu-id="7b99f-169">Consent</span></span>](referral-resources.md#consent)                             | <span data-ttu-id="7b99f-170">Diğer kuruluşlarla bilgi paylaşma ve kullanıcıların kullanıcılarla iletişim kurmasına izin verme bayrakları.</span><span class="sxs-lookup"><span data-stu-id="7b99f-170">Consent flags around sharing information with other organizations and allowing them to contact users.</span></span>                |
| <span data-ttu-id="7b99f-171">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="7b99f-171">Details</span></span>             | [<span data-ttu-id="7b99f-172">ReferralDetails</span><span class="sxs-lookup"><span data-stu-id="7b99f-172">ReferralDetails</span></span>](referral-resources.md#referraldetails)             | <span data-ttu-id="7b99f-173">Müşteri ayrıntıları, notlar, anlaşma değeri, para birimi kapanış tarihi.</span><span class="sxs-lookup"><span data-stu-id="7b99f-173">Customer details, notes, deal value, currency closing date.</span></span>                                                          |
| <span data-ttu-id="7b99f-174">Takım</span><span class="sxs-lookup"><span data-stu-id="7b99f-174">Team</span></span>                | [<span data-ttu-id="7b99f-175">Üye</span><span class="sxs-lookup"><span data-stu-id="7b99f-175">Member</span></span>](referral-resources.md#member)                               | <span data-ttu-id="7b99f-176">İş ortağı katılımında yer alan kuruluşlardaki kullanıcıları temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7b99f-176">Represents users in the organizations that are involved in the partner engagement.</span></span>                                   |
| <span data-ttu-id="7b99f-177">Davet edilen Tecontext</span><span class="sxs-lookup"><span data-stu-id="7b99f-177">InviteContext</span></span>       | [<span data-ttu-id="7b99f-178">Davet edilen Tecontext</span><span class="sxs-lookup"><span data-stu-id="7b99f-178">InviteContext</span></span>](referral-resources.md#invitecontext)                 | <span data-ttu-id="7b99f-179">Bir kullanıcının iş ortağı katılımında başka bir kuruluş davet ederken sağlayasun, daha fazla bilgi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7b99f-179">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span> |
| <span data-ttu-id="7b99f-180">Hedef</span><span class="sxs-lookup"><span data-stu-id="7b99f-180">Target</span></span>         | [<span data-ttu-id="7b99f-181">ReferralTarget</span><span class="sxs-lookup"><span data-stu-id="7b99f-181">ReferralTarget</span></span>](referral-resources.md#target)        | <span data-ttu-id="7b99f-182">Bir kullanıcının iş ortağı katılımında başka bir kuruluş davet ederken sağlayasun, daha fazla bilgi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7b99f-182">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span>  |

### <a name="status-and-substatus-transition-states"></a><span data-ttu-id="7b99f-183">Durum ve alt durum geçiş durumları</span><span class="sxs-lookup"><span data-stu-id="7b99f-183">Status and substatus transition states</span></span>

| <span data-ttu-id="7b99f-184">Durum</span><span class="sxs-lookup"><span data-stu-id="7b99f-184">Status</span></span> | <span data-ttu-id="7b99f-185">İzin verilen durum geçişi</span><span class="sxs-lookup"><span data-stu-id="7b99f-185">Allowed Status Transition</span></span> | <span data-ttu-id="7b99f-186">İzin verilen alt durum</span><span class="sxs-lookup"><span data-stu-id="7b99f-186">Allowed Substatus</span></span>            |
|--------|---------------------------|------------------------------|
| <span data-ttu-id="7b99f-187">Yeni</span><span class="sxs-lookup"><span data-stu-id="7b99f-187">New</span></span>    | <span data-ttu-id="7b99f-188">Yeni, etkin, kapalı</span><span class="sxs-lookup"><span data-stu-id="7b99f-188">New, Active, Closed</span></span>       | <span data-ttu-id="7b99f-189">Bekliyor, alındı</span><span class="sxs-lookup"><span data-stu-id="7b99f-189">Pending, Received</span></span>            |
| <span data-ttu-id="7b99f-190">Etkin</span><span class="sxs-lookup"><span data-stu-id="7b99f-190">Active</span></span> | <span data-ttu-id="7b99f-191">Etkin, kapalı</span><span class="sxs-lookup"><span data-stu-id="7b99f-191">Active, Closed</span></span>            | <span data-ttu-id="7b99f-192">Kabul edildi</span><span class="sxs-lookup"><span data-stu-id="7b99f-192">Accepted</span></span>                     |
| <span data-ttu-id="7b99f-193">Kapatıldı</span><span class="sxs-lookup"><span data-stu-id="7b99f-193">Closed</span></span> | <span data-ttu-id="7b99f-194">Kapatıldı</span><span class="sxs-lookup"><span data-stu-id="7b99f-194">Closed</span></span>                    | <span data-ttu-id="7b99f-195">Kazanıldı, kaybedildi, reddedildi, zaman aşımına uğradı</span><span class="sxs-lookup"><span data-stu-id="7b99f-195">Won, Lost, Declined, Expired</span></span> |

### <a name="request-example"></a><span data-ttu-id="7b99f-196">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="7b99f-196">Request example</span></span>

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
> <span data-ttu-id="7b99f-197">`"links": { }`NESNEYI put kaynağından kaldırın.</span><span class="sxs-lookup"><span data-stu-id="7b99f-197">Remove the `"links": { }` object from the PUT resource.</span></span>

## <a name="rest-response"></a><span data-ttu-id="7b99f-198">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="7b99f-198">REST Response</span></span>

<span data-ttu-id="7b99f-199">Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [başvuru](referral-resources.md) kaynağını döndürür.</span><span class="sxs-lookup"><span data-stu-id="7b99f-199">If successful, this method returns the populated [referral](referral-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7b99f-200">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="7b99f-200">Response success and error codes</span></span>

<span data-ttu-id="7b99f-201">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="7b99f-201">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7b99f-202">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7b99f-202">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7b99f-203">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7b99f-203">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7b99f-204">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="7b99f-204">Response example</span></span>

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