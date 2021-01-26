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
# <a name="update-a-lead-or-opportunity"></a><span data-ttu-id="c6635-103">Bir müşteri adayı veya fırsat güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="c6635-103">Update a lead or opportunity</span></span>

<span data-ttu-id="c6635-104">Aşağıdakiler cihazlar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="c6635-104">Applies to:</span></span>

- <span data-ttu-id="c6635-105">İş ortağı API 'SI</span><span class="sxs-lookup"><span data-stu-id="c6635-105">Partner API</span></span>

<span data-ttu-id="c6635-106">Bu konuda, müşteri adayı veya fırsat ayrıntılarının anlaşma değeri, tahmini kapanış tarihi gibi nasıl güncelleştirilmesi veya diğer ayrıntılar arasında satış aşamaları yönetimi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c6635-106">This topic explains how to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6635-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c6635-107">Prerequisites</span></span>

- <span data-ttu-id="c6635-108">[Iş ortağı API kimlik doğrulaması](api-authentication.md)bölümünde açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="c6635-108">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="c6635-109">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="c6635-109">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="c6635-110">Bu API Şu anda yalnızca iş ortaklarının şu rollerden birinde olması gereken Kullanıcı erişimini destekliyor: genel yönetici, başvuru Yöneticisi veya başvuru kullanıcısı.</span><span class="sxs-lookup"><span data-stu-id="c6635-110">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="c6635-111">REST Isteği</span><span class="sxs-lookup"><span data-stu-id="c6635-111">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c6635-112">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="c6635-112">Request syntax</span></span>

| <span data-ttu-id="c6635-113">Yöntem</span><span class="sxs-lookup"><span data-stu-id="c6635-113">Method</span></span>  | <span data-ttu-id="c6635-114">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="c6635-114">Request URI</span></span>                                                       |
|---------|-------------------------------------------------------------------|
| <span data-ttu-id="c6635-115">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="c6635-115">**PATCH**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="uri-parameter"></a><span data-ttu-id="c6635-116">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="c6635-116">URI parameter</span></span>


| <span data-ttu-id="c6635-117">Ad</span><span class="sxs-lookup"><span data-stu-id="c6635-117">Name</span></span>                   | <span data-ttu-id="c6635-118">Tür</span><span class="sxs-lookup"><span data-stu-id="c6635-118">Type</span></span>     | <span data-ttu-id="c6635-119">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c6635-119">Required</span></span> | <span data-ttu-id="c6635-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c6635-120">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="c6635-121">Id</span><span class="sxs-lookup"><span data-stu-id="c6635-121">Id</span></span>                      | <span data-ttu-id="c6635-122">string</span><span class="sxs-lookup"><span data-stu-id="c6635-122">string</span></span>   | <span data-ttu-id="c6635-123">Yes</span><span class="sxs-lookup"><span data-stu-id="c6635-123">Yes</span></span>       | <span data-ttu-id="c6635-124">Bir müşteri adayı veya ortak satış fırsatının benzersiz tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="c6635-124">The unique identifier for a lead or co-sell opportunity</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="c6635-125">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="c6635-125">Request headers</span></span>

<span data-ttu-id="c6635-126">Daha fazla bilgi için bkz. [Iş ortağı Rest üst bilgileri](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="c6635-126">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="c6635-127">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="c6635-127">Request body</span></span>

<span data-ttu-id="c6635-128">İstek gövdesi [JSON yaması](https://tools.ietf.org/html/rfc6902) biçimini izler.</span><span class="sxs-lookup"><span data-stu-id="c6635-128">The request body follows the [Json Patch](https://tools.ietf.org/html/rfc6902) format.</span></span> <span data-ttu-id="c6635-129">JSON yama belgesinde bir dizi işlem vardır.</span><span class="sxs-lookup"><span data-stu-id="c6635-129">A JSON Patch document has an array of operations.</span></span> <span data-ttu-id="c6635-130">Her işlem belirli bir değişiklik türünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c6635-130">Each operation identifies a particular type of change.</span></span> <span data-ttu-id="c6635-131">Bu tür değişikliklere örnek olarak bir dizi öğesi ekleme veya bir özellik değeri değiştirme sayılabilir.</span><span class="sxs-lookup"><span data-stu-id="c6635-131">Examples of such changes include adding an array element or replacing a property value.</span></span>

> [!Important]
> <span data-ttu-id="c6635-132">API Şu anda yalnızca `replace` ve işlemlerini destekler `add` .</span><span class="sxs-lookup"><span data-stu-id="c6635-132">The API currently only supports the `replace` and `add` operations.</span></span>

### <a name="request-example"></a><span data-ttu-id="c6635-133">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="c6635-133">Request example</span></span>

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
> <span data-ttu-id="c6635-134">**IF-Match** üst bilgisi geçiriliyorsa eşzamanlılık denetimi için kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="c6635-134">If the **If-Match** header is passed, it will be used for concurrency control.</span></span>

## <a name="rest-response"></a><span data-ttu-id="c6635-135">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="c6635-135">REST Response</span></span>

<span data-ttu-id="c6635-136">Başarılı olursa, yanıt gövdesi güncelleştirilmiş [müşteri adayını veya fırsatı](referral-resources.md)içerir.</span><span class="sxs-lookup"><span data-stu-id="c6635-136">If successful, the response body contains the updated [lead or opportunity](referral-resources.md).</span></span>


### <a name="response-success-and-error-codes"></a><span data-ttu-id="c6635-137">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="c6635-137">Response success and error codes</span></span>

<span data-ttu-id="c6635-138">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir [http durum kodu](error-codes.md) ile gelir.</span><span class="sxs-lookup"><span data-stu-id="c6635-138">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c6635-139">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c6635-139">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="c6635-140">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="c6635-140">Response example</span></span>

``` http
HTTP/1.1 204 No Content
Content-Length: 0
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
```

> [!Tip]
> <span data-ttu-id="c6635-141">Yanıt gövdesi **tercih** edilen üstbilgiye bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c6635-141">The response body depends on the **Prefer** header.</span></span> <span data-ttu-id="c6635-142">İstek içinde üst bilgi değeri atlanırsa, yanıt gövdesi 204 HTTP durum koduyla boştur.</span><span class="sxs-lookup"><span data-stu-id="c6635-142">If the header value is omitted in the request, the response body is empty with a HTTP Status code 204.</span></span> <span data-ttu-id="c6635-143">`Prefer: return=representation`Güncelleştirilmiş müşteri adayını veya fırsatı almak için üstbilgiye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c6635-143">Add `Prefer: return=representation` to the header to get the updated lead or opportunity.</span></span>

## <a name="sample-requests"></a><span data-ttu-id="c6635-144">Örnek istekler</span><span class="sxs-lookup"><span data-stu-id="c6635-144">Sample requests</span></span>

1. <span data-ttu-id="c6635-145">10000 'e fırsat için anlaşma değerini güncelleştirir ve notları güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c6635-145">Updates the deal value for the opportunity to 10000 and updates the notes.</span></span> <span data-ttu-id="c6635-146">Üst bilgi bağlanılabilirliğinin olmaması nedeniyle eşzamanlılık denetimi yok `If-Match` .</span><span class="sxs-lookup"><span data-stu-id="c6635-146">There are no concurrency checks because of the absense of the `If-Match` header.</span></span>
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace","path":"/details/dealValue","value":"10000"},
        {"op":"replace","path":"/details/notes","value":"Lorem ipsum dolor sit amet."}
    ]
    ```

2. <span data-ttu-id="c6635-147">Bir müşteri adayının veya kazanılan fırsatın durumunu güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c6635-147">Updates the status of a lead or opportunity to Won.</span></span>
    
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
    > <span data-ttu-id="c6635-148">`status`Ve `substatus` alanları, [burada](referral-resources.md)açıklandığı gibi izin verilen geçiş değerleri kümesine uymalıdır.</span><span class="sxs-lookup"><span data-stu-id="c6635-148">The `status` and `substatus` fields should conform to the allowed set of transition values as described [here](referral-resources.md).</span></span>

3. <span data-ttu-id="c6635-149">Kuruluşunuzdaki müşteri adayına veya fırsat ekibine yeni bir üye ekler.</span><span class="sxs-lookup"><span data-stu-id="c6635-149">Adds a new member from your organization to the lead or opportunity team.</span></span> <span data-ttu-id="c6635-150">Bu yanıt, üst bilgi varlığı nedeniyle güncelleştirilmiş müşteri adayını veya fırsatı içerecektir `Prefer: return=representation` .</span><span class="sxs-lookup"><span data-stu-id="c6635-150">The response will contain the updated lead or opportunity because of the presence of the `Prefer: return=representation` header.</span></span>

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
