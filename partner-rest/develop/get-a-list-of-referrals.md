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
# <a name="get-the-list-of-leads-and-opportunities"></a><span data-ttu-id="25861-103">Müşteri adaylarının ve fırsatların listesini alma</span><span class="sxs-lookup"><span data-stu-id="25861-103">Get the list of leads and opportunities</span></span>

<span data-ttu-id="25861-104">Aşağıdakiler cihazlar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="25861-104">Applies to:</span></span>

- <span data-ttu-id="25861-105">İş ortağı API 'SI</span><span class="sxs-lookup"><span data-stu-id="25861-105">Partner API</span></span>

 <span data-ttu-id="25861-106">Bu konu başlığı altında, Microsoft çözüm sağlayıcısı sayfasından alınan müşteri adaylarının listesinin yanı sıra Microsoft satıcılarından veya diğer iş ortaklarından alınan ortak satış fırsatlarının nasıl alınacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="25861-106">This topic explains how to get the list of leads received from Microsoft solution provider page and co-sell opportunities received from Microsoft sellers or other partners.</span></span> <span data-ttu-id="25861-107">Bu, kuruluşunuz tarafından oluşturulan ortak satış fırsatları veya işlem hattı anlaşmaları listesini de getirir.</span><span class="sxs-lookup"><span data-stu-id="25861-107">This will also fetch the list of co-sell opportunities or pipeline deals created by your organization.</span></span>

> [!Note]
> <span data-ttu-id="25861-108">Microsoft ticari Market 'ten (Azure Marketi ve AppSource) alınan müşteri adayları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="25861-108">Leads received from the Microsoft commercial marketplace (Azure Marketplace and AppSource) are not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25861-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="25861-109">Prerequisites</span></span>

- <span data-ttu-id="25861-110">[Iş ortağı API kimlik doğrulaması](api-authentication.md)bölümünde açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="25861-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="25861-111">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="25861-111">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="25861-112">Bu API Şu anda yalnızca iş ortaklarının şu rollerden birinde olması gereken Kullanıcı erişimini destekliyor: genel yönetici, başvuru Yöneticisi veya başvuru kullanıcısı.</span><span class="sxs-lookup"><span data-stu-id="25861-112">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="25861-113">REST isteği</span><span class="sxs-lookup"><span data-stu-id="25861-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="25861-114">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="25861-114">Request syntax</span></span>

| <span data-ttu-id="25861-115">Yöntem</span><span class="sxs-lookup"><span data-stu-id="25861-115">Method</span></span>  | <span data-ttu-id="25861-116">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="25861-116">Request URI</span></span>                                                    |
|:--------|:---------------------------------------------------------------|
| <span data-ttu-id="25861-117">**Al**</span><span class="sxs-lookup"><span data-stu-id="25861-117">**GET**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

#### <a name="supported-odata-operations"></a><span data-ttu-id="25861-118">Desteklenen OData işlemleri</span><span class="sxs-lookup"><span data-stu-id="25861-118">Supported OData operations</span></span>

| <span data-ttu-id="25861-119">Ad</span><span class="sxs-lookup"><span data-stu-id="25861-119">Name</span></span>     | <span data-ttu-id="25861-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="25861-120">Description</span></span>     | <span data-ttu-id="25861-121">Gerekli</span><span class="sxs-lookup"><span data-stu-id="25861-121">Required</span></span>    | <span data-ttu-id="25861-122">Örnek</span><span class="sxs-lookup"><span data-stu-id="25861-122">Example</span></span>                                                                                                                                                                                                                                                     |
|:---------|:----------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="25861-123">$select</span><span class="sxs-lookup"><span data-stu-id="25861-123">$select</span></span>  | <span data-ttu-id="25861-124">Alanları seçer</span><span class="sxs-lookup"><span data-stu-id="25861-124">Selects fields</span></span>  | <span data-ttu-id="25861-125">No</span><span class="sxs-lookup"><span data-stu-id="25861-125">No</span></span>          | `/referrals?$select=id,status,customerProfile`                                                                                                                                                                                                              |
| <span data-ttu-id="25861-126">$filter</span><span class="sxs-lookup"><span data-stu-id="25861-126">$filter</span></span>  | <span data-ttu-id="25861-127">Filtre sonuçları</span><span class="sxs-lookup"><span data-stu-id="25861-127">Filters results</span></span> | <span data-ttu-id="25861-128">Önerilen</span><span class="sxs-lookup"><span data-stu-id="25861-128">Recommended</span></span> | `/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'` <br/> `/referrals?$filter=status eq 'New' and qualification eq 'SalesQualified'` <br/> `/referrals?$filter=customerProfile/address/country eq 'US' and direction eq 'Incoming'` |
| <span data-ttu-id="25861-129">$orderby</span><span class="sxs-lookup"><span data-stu-id="25861-129">$orderby</span></span> | <span data-ttu-id="25861-130">Sipariş sonuçları</span><span class="sxs-lookup"><span data-stu-id="25861-130">Orders results</span></span>  | <span data-ttu-id="25861-131">Önerilen</span><span class="sxs-lookup"><span data-stu-id="25861-131">Recommended</span></span> | `/referrals?$orderby=createdDateTime desc`                                                                                                                                                                                                                  |

#### <a name="supported-orderby-parameters"></a><span data-ttu-id="25861-132">Desteklenen OrderBy parametreleri</span><span class="sxs-lookup"><span data-stu-id="25861-132">Supported orderby parameters</span></span>

<span data-ttu-id="25861-133">Müşteri adayları ve fırsatların listesini sıralamak için aşağıdaki $orderby parametrelerini kullanın</span><span class="sxs-lookup"><span data-stu-id="25861-133">Use the following $orderby parameters to sort the list of leads and opportunities</span></span>

| <span data-ttu-id="25861-134">Ad</span><span class="sxs-lookup"><span data-stu-id="25861-134">Name</span></span>            | <span data-ttu-id="25861-135">Tür</span><span class="sxs-lookup"><span data-stu-id="25861-135">Type</span></span>     | <span data-ttu-id="25861-136">Description</span><span class="sxs-lookup"><span data-stu-id="25861-136">Description</span></span>                                       |
|:----------------|:---------|:--------------------------------------------------|
| <span data-ttu-id="25861-137">Saati</span><span class="sxs-lookup"><span data-stu-id="25861-137">createdDateTime</span></span> | <span data-ttu-id="25861-138">DateTime</span><span class="sxs-lookup"><span data-stu-id="25861-138">DateTime</span></span> | <span data-ttu-id="25861-139">Müşteri adayının veya fırsatın Oluşturulma tarihi ve saati</span><span class="sxs-lookup"><span data-stu-id="25861-139">Creation date and time of the lead or opportunity</span></span> |
| <span data-ttu-id="25861-140">updatedDateTime</span><span class="sxs-lookup"><span data-stu-id="25861-140">updatedDateTime</span></span> | <span data-ttu-id="25861-141">DateTime</span><span class="sxs-lookup"><span data-stu-id="25861-141">DateTime</span></span> | <span data-ttu-id="25861-142">Müşteri adayının veya fırsatın tarih ve saatini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="25861-142">Update date and time of the lead or opportunity</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="25861-143">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="25861-143">Request headers</span></span>

<span data-ttu-id="25861-144">Daha fazla bilgi için bkz. [Iş ortağı Rest üst bilgileri](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="25861-144">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="25861-145">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="25861-145">Request body</span></span>

<span data-ttu-id="25861-146">Yok.</span><span class="sxs-lookup"><span data-stu-id="25861-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="25861-147">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="25861-147">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$orderby=createdDateTime desc HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="25861-148">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="25861-148">REST response</span></span>

<span data-ttu-id="25861-149">Başarılı olursa, yanıt gövdesi bir [müşteri adayı ve/veya fırsat](referral-resources.md)koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="25861-149">If successful, the response body contains a collection of [leads and/or opportunities](referral-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="25861-150">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="25861-150">Response success and error codes</span></span>

<span data-ttu-id="25861-151">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir [http durum kodu](error-codes.md) ile gelir.</span><span class="sxs-lookup"><span data-stu-id="25861-151">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="25861-152">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="25861-152">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="25861-153">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="25861-153">Response example</span></span>

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

<span data-ttu-id="25861-154">`@odata.nextLink`Sonuçların sonraki sayfasına ulaşmak için öğesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="25861-154">Use the `@odata.nextLink` to get the next page of results.</span></span>

> [!Note]
> <span data-ttu-id="25861-155">Yukarıdaki örnekteki illustratration alanları ayrıntılı değildir.</span><span class="sxs-lookup"><span data-stu-id="25861-155">The fields in the example illustratration above are not exhaustive.</span></span> <span data-ttu-id="25861-156">Gerçek API yanıtı, müşteri ve iş ortağı takımları gibi daha fazla alan içerir.</span><span class="sxs-lookup"><span data-stu-id="25861-156">The actual API response contains more fields like the customer and partner teams.</span></span> <span data-ttu-id="25861-157">Desteklenen alanların tam listesi için bkz. [başvuru kaynakları](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="25861-157">For the full list of supported fields, see [referral resources](referral-resources.md).</span></span>

## <a name="sample-requests"></a><span data-ttu-id="25861-158">Örnek istekler</span><span class="sxs-lookup"><span data-stu-id="25861-158">Sample requests</span></span>

1. <span data-ttu-id="25861-159">En son gelen 10 ortak satış fırsatlarını alır.</span><span class="sxs-lookup"><span data-stu-id="25861-159">Gets the top 10 most recent inbound co-sell opportunities.</span></span> <span data-ttu-id="25861-160">İstek, bir Microsoft satış temsilcisi veya başka bir iş ortağı tarafından başlatılan fırsatları sunarak, kuruluşunuzu ortak satış etkinliğine katılması için davet eder.</span><span class="sxs-lookup"><span data-stu-id="25861-160">The request will fetch opportunities initiated by a Microsoft sales representative or another partner, inviting your organization to participate in a co-selling activity.</span></span>
    
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(type eq 'Shared' and direction eq 'Incoming')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

2. <span data-ttu-id="25861-161">Yanıt verilmeyen en son gelen müşteri adaylarını ve fırsatları alır.</span><span class="sxs-lookup"><span data-stu-id="25861-161">Gets the most recent inbound leads and opportunities that have not been responded to.</span></span>  

    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(direction eq 'Incoming' and substatus eq 'Pending')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

    > [!Important]
    > <span data-ttu-id="25861-162">Ayrılan süre (Şu anda 14 gün) içinde bir müşteri adayına veya fırsata yanıt vermezse, bunu süresi dolduğunda, Microsoft veya size bu fırsatı gönderen iş ortağına bildirir.</span><span class="sxs-lookup"><span data-stu-id="25861-162">If you don't respond to a lead or opportunity within the allotted time (currently 14 days), we'll archive it as Expired and notify either Microsoft or the partner who sent you this opportunity.</span></span>

3. <span data-ttu-id="25861-163">Kuruluşunuz tarafından başlatılan ve belirli bir satıcı tarafından çalışan en son etkin ortak satış fırsatlarını alır.</span><span class="sxs-lookup"><span data-stu-id="25861-163">Gets the most recent active co-sell opportunities initiated by your organization and being worked on by a specific seller.</span></span>
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=status eq 'Active' and direction eq 'Outgoing' and type eq 'Shared' and team/any(t:t/email eq 'r2d2@contoso.com')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```