---
title: Teklif matrisi elde etmek
description: Verilen tarih için teklif matrisi alma. Aya göre geçmişi almak için filtreleri destekler.
ms.date: 02/11/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e53276c1170febab002d35a42c88c1f96f7b7428
ms.sourcegitcommit: 9e64d6358ef4e1ac2d3e0d36cd63490a5f760b38
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/01/2021
ms.locfileid: "113131306"
---
# <a name="get-an-offer-matrix"></a><span data-ttu-id="a79ac-104">Teklif matrisi elde etmek</span><span class="sxs-lookup"><span data-stu-id="a79ac-104">Get an offer matrix</span></span>

<span data-ttu-id="a79ac-105">Aşağıdakiler cihazlar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="a79ac-105">Applies to:</span></span>

- <span data-ttu-id="a79ac-106">Partner API</span><span class="sxs-lookup"><span data-stu-id="a79ac-106">Partner API</span></span>
- <span data-ttu-id="a79ac-107">M365/D365 Yeni Ticaret deneyimi teknik önizlemesi.</span><span class="sxs-lookup"><span data-stu-id="a79ac-107">The M365/D365 New Commerce experience technical preview.</span></span> <span data-ttu-id="a79ac-108">Aşağıdaki Yeni Ticaret değişiklikleri şu anda yalnızca M365/D365 yeni ticaret deneyimi teknik önizlemesinde yer alan iş ortakları tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a79ac-108">The below New Commerce changes are currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

<span data-ttu-id="a79ac-109">Bu konu başlığında, bir ay için teklif matrisinin nasıl elde tutulacakları açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a79ac-109">This topic explains how to get an offer matrix for a given month.</span></span> <span data-ttu-id="a79ac-110">Teklif matrisi, ürünler ve sku'lar için özellikler ve satın alma kuralları içerir.</span><span class="sxs-lookup"><span data-stu-id="a79ac-110">The offer matrix includes properties and purchase rules for the products and skus.</span></span> <span data-ttu-id="a79ac-111">Bu yöntem, aya göre geçmişi almak için filtreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="a79ac-111">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a79ac-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a79ac-112">Prerequisites</span></span>

- <span data-ttu-id="a79ac-113">kimlik doğrulamasında açıklandığı gibi [Partner API bilgileri.](api-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a79ac-113">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="a79ac-114">Bu senaryo yalnızca uygulama kullanıcısı kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="a79ac-114">This scenario only supports application user authentication.</span></span> <span data-ttu-id="a79ac-115">Yalnızca uygulama henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="a79ac-115">Application-only is not yet supported.</span></span> <span data-ttu-id="a79ac-116">**Http hatası:400 ile ilgili iş** ortaklarının kimlik doğrulaması Partner API [bakın.](api-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a79ac-116">Partners that experience **http error:400** should consult the [Partner API authentication](api-authentication.md) documentation.</span></span>
- <span data-ttu-id="a79ac-117">Bu API şu anda yalnızca iş ortaklarının şu rollerden biri olması gereken kullanıcı erişimini destekler: Genel Yönetici, Yönetici Aracısı veya Satış Aracısı.</span><span class="sxs-lookup"><span data-stu-id="a79ac-117">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="a79ac-118">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="a79ac-118">Details</span></span>

- <span data-ttu-id="a79ac-119">Geçerli, yalnızca güncelleştirilmiş yeni ticari lisans tabanlı ürünler için verileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="a79ac-119">Current returns data only for updated new commerce license-based products.</span></span>
- <span data-ttu-id="a79ac-120">Geçerli fiyatlandırma, API'nin çağrıldı olduğu tarihe kadar geçerli ay boyunca kullanılabilen ürünleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a79ac-120">Current pricing includes products available during the current month to the date the API is called.</span></span> <span data-ttu-id="a79ac-121">Önceki aylar, seçilen ayın son gününden itibaren tarihi içerir.</span><span class="sxs-lookup"><span data-stu-id="a79ac-121">Previous months include date as of the last day of the selected month.</span></span>
- <span data-ttu-id="a79ac-122">Bu yöntem verileri bir dosya akışı olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="a79ac-122">This method returns data as a file stream.</span></span> <span data-ttu-id="a79ac-123">Dosya akışı, .csv dosya veya dosyanın sıkıştırılmış zip sürümü .csv.</span><span class="sxs-lookup"><span data-stu-id="a79ac-123">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="a79ac-124">Sıkıştırılmış dosyaları nasıl talep etmekle ilgili ayrıntılar aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a79ac-124">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="a79ac-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="a79ac-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a79ac-126">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="a79ac-126">Request syntax</span></span>

| <span data-ttu-id="a79ac-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="a79ac-127">Method</span></span>   | <span data-ttu-id="a79ac-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="a79ac-128">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a79ac-129">**Al**</span><span class="sxs-lookup"><span data-stu-id="a79ac-129">**GET**</span></span> | <span data-ttu-id="a79ac-130"> https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='{date}')/$value</span><span class="sxs-lookup"><span data-stu-id="a79ac-130">https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='{date}')/$value</span></span> |

### <a name="uri-filter-parameters"></a><span data-ttu-id="a79ac-131">URI filtre parametreleri</span><span class="sxs-lookup"><span data-stu-id="a79ac-131">URI filter parameters</span></span>

<span data-ttu-id="a79ac-132">Aşağıdaki filtre parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a79ac-132">Use the following filter parameters.</span></span>

| <span data-ttu-id="a79ac-133">Ad</span><span class="sxs-lookup"><span data-stu-id="a79ac-133">Name</span></span>                   | <span data-ttu-id="a79ac-134">Tür</span><span class="sxs-lookup"><span data-stu-id="a79ac-134">Type</span></span>     | <span data-ttu-id="a79ac-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a79ac-135">Required</span></span> | <span data-ttu-id="a79ac-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a79ac-136">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="a79ac-137">Ay</span><span class="sxs-lookup"><span data-stu-id="a79ac-137">Month</span></span>| <span data-ttu-id="a79ac-138">dize</span><span class="sxs-lookup"><span data-stu-id="a79ac-138">string</span></span>   | <span data-ttu-id="a79ac-139">No</span><span class="sxs-lookup"><span data-stu-id="a79ac-139">No</span></span> | <span data-ttu-id="a79ac-140">İstenen fiyat listesi için YYYYMM'ye bağlı kalmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="a79ac-140">Must adhere to YYYYMM for the price sheet being requested.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a79ac-141">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="a79ac-141">Request headers</span></span>

- <span data-ttu-id="a79ac-142">Daha [fazla bilgi için bkz. İş](headers.md) ortağı REST üst bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a79ac-142">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="a79ac-143">Yukarıdaki üst bilgilerine ek olarak, fiyatlandırma dosyaları bant genişliğini ve indirme süresini azaltan sıkıştırılmış olarak alınabiliyor.</span><span class="sxs-lookup"><span data-stu-id="a79ac-143">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="a79ac-144">Varsayılan olarak dosyalar sıkıştırılır.</span><span class="sxs-lookup"><span data-stu-id="a79ac-144">By default the files are not compressed.</span></span> <span data-ttu-id="a79ac-145">Dosyaların sıkıştırılmış sürümlerini almak için aşağıdaki üst bilgi değerini dahil edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a79ac-145">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="a79ac-146">Sıkıştırılmış sayfaların yalnızca Nisan 2020'den itibaren kullanılabilir olduğunu, Nisan 2020'den önceki tüm sayfaların yalnızca sıkıştırılmış olarak kullanılabilir olduğunu fark etmek.</span><span class="sxs-lookup"><span data-stu-id="a79ac-146">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="a79ac-147">Üst bilgi</span><span class="sxs-lookup"><span data-stu-id="a79ac-147">Header</span></span>                   | <span data-ttu-id="a79ac-148">Değer Türü</span><span class="sxs-lookup"><span data-stu-id="a79ac-148">Value Type</span></span>     | <span data-ttu-id="a79ac-149">Değer</span><span class="sxs-lookup"><span data-stu-id="a79ac-149">Value</span></span> | <span data-ttu-id="a79ac-150">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a79ac-150">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="a79ac-151">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="a79ac-151">Accept-Encoding</span></span>| <span data-ttu-id="a79ac-152">string</span><span class="sxs-lookup"><span data-stu-id="a79ac-152">string</span></span>   | <span data-ttu-id="a79ac-153">Deflate</span><span class="sxs-lookup"><span data-stu-id="a79ac-153">deflate</span></span>| <span data-ttu-id="a79ac-154">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="a79ac-154">Optional.</span></span> <span data-ttu-id="a79ac-155">Atlanmış dosya akışı sıkıştırilmezse.</span><span class="sxs-lookup"><span data-stu-id="a79ac-155">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="a79ac-156">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="a79ac-156">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='202101')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="a79ac-157">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="a79ac-157">REST response</span></span>

<span data-ttu-id="a79ac-158">Başarılı olursa, bu yöntem dosya akışı olarak bir teklif matrisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="a79ac-158">If successful, this method returns an offer matrix as a file stream.</span></span> <span data-ttu-id="a79ac-159">Dosya akışı, .csv dosya veya dosyanın sıkıştırılmış zip sürümü .csv.</span><span class="sxs-lookup"><span data-stu-id="a79ac-159">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a79ac-160">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="a79ac-160">Response success and error codes</span></span>

<span data-ttu-id="a79ac-161">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="a79ac-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a79ac-162">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a79ac-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a79ac-163">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a79ac-163">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a79ac-164">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="a79ac-164">Response example</span></span>

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=updatedoffice.csv
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Feb 2021 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","ProvisioningId","ProvisioningString","MinLicenses","MaxLicenses","AssetOwnershipLimit","AssetOwnershipLimitType","ProductSkuPreRequisites","ProductSkuConversion","Description","AllowedCountries" 
"Microsoft 365 Business Basic","CFQ7TTC0LH18","0001","Microsoft 365 Business Basic","3b555118-da6a-4418-894f-7df1e2096870","O365_BUSINESS_ESSENTIALS","1","300","2","ConcurrentCount","","CFQ7TTC0LDPB/0001,CFQ7TTC0LF8Q/0001","Best for businesses that need professional...","AD;AE;AF;AG;AI;AL;AM;AO..."
======= Truncated ==============

```
