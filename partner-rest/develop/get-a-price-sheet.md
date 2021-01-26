---
title: Fiyat listesi alma
description: Belirli bir Pazar ve görünüm için bir fiyat listesi alın. Aya göre geçmişi almak için filtreleri destekler.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 5195ebed6559bd71a7832a667e63ee801be1c82f
ms.sourcegitcommit: bb3f5f7ee0489bded86fe52e55018c1f4f5032e2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2020
ms.locfileid: "97770626"
---
# <a name="get-a-price-sheet"></a><span data-ttu-id="7faac-104">Fiyat listesi alma</span><span class="sxs-lookup"><span data-stu-id="7faac-104">Get a price sheet</span></span>

<span data-ttu-id="7faac-105">Aşağıdakiler cihazlar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="7faac-105">Applies to:</span></span>

- <span data-ttu-id="7faac-106">İş ortağı API 'SI</span><span class="sxs-lookup"><span data-stu-id="7faac-106">Partner API</span></span>

<span data-ttu-id="7faac-107">Bu konuda, belirli bir Pazar ve görünüm için fiyat listesi alma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7faac-107">This topic explains how to get a price sheet for a given market and view.</span></span> <span data-ttu-id="7faac-108">Bu yöntem, geçmişi aya göre almak için filtreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="7faac-108">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7faac-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7faac-109">Prerequisites</span></span>

- <span data-ttu-id="7faac-110">[Iş ortağı API kimlik doğrulaması](api-authentication.md)bölümünde açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7faac-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="7faac-111">Bu senaryo yalnızca uygulama kullanıcı kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="7faac-111">This scenario only supports application user authentication.</span></span> <span data-ttu-id="7faac-112">Application-ony henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="7faac-112">Application-ony is not yet supported.</span></span>
- <span data-ttu-id="7faac-113">Bu API Şu anda yalnızca iş ortaklarının şu rollerden birinde olması gereken Kullanıcı erişimini destekliyor: genel yönetici, Yönetim Aracısı veya satış Aracısı.</span><span class="sxs-lookup"><span data-stu-id="7faac-113">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="7faac-114">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="7faac-114">Details</span></span>

- <span data-ttu-id="7faac-115">Geçerli, yalnızca Azure planı tüketimi ve rezervasyon ürünleri için verileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="7faac-115">Current returns data only for Azure plan consumption and reservation products.</span></span>
- <span data-ttu-id="7faac-116">Geçerli [fiyatlandırma](pricing.md) , geçerli ay boyunca API 'nin çağrıldığı tarihe kadar sunulan tüm ölçümleri ve ürünleri içerir.</span><span class="sxs-lookup"><span data-stu-id="7faac-116">Current [pricing](pricing.md) includes all meters and products available during the current month to the date the API is called.</span></span> <span data-ttu-id="7faac-117">Önceki aylar, belirli bir ay için kullanılabilen tüm ölçümleri ve ürünleri içerir.</span><span class="sxs-lookup"><span data-stu-id="7faac-117">Previous months include all meters and products available for the given month.</span></span>
- <span data-ttu-id="7faac-118">Tüketim ölçümü fiyatları yalnızca ABD doları cinsindendir, iş ortakları yerel para birimi maliyetlerini hesaplamak için yabancı Exchange ücretleri API 'sini kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="7faac-118">Consumption meter prices are only in USD, partners are to use the foreign exchange rates API to calculate local currency costs.</span></span>
- <span data-ttu-id="7faac-119">Tüketim ölçümü fiyatları, tahmini perakende fiyatlarıdır.</span><span class="sxs-lookup"><span data-stu-id="7faac-119">Consumption meter prices are estimated retail prices.</span></span> <span data-ttu-id="7faac-120">İş ortağı indirimleri, [iş ortağı tarafından kazanılan kredi](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation)aracılığıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7faac-120">Partner discounts are available via [partner earned credit](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span></span>
- <span data-ttu-id="7faac-121">Rezervasyonların ölçüm fiyatları, CSP iş ortağı indirimlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="7faac-121">Reservations meter prices include the CSP partner discounts.</span></span> <span data-ttu-id="7faac-122">Rezervasyonlar için tahmini perakende fiyatları, Iş Ortağı Merkezi "fiyatlandırma ve teklifler" sayfasında indirilebilir olan rezervasyonlar paylaşılan hizmetlerinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7faac-122">Estimated retail prices for reservations can be found in the reservations shared services downloadable from the Partner Center "Pricing and offers" page.</span></span>
- <span data-ttu-id="7faac-123">Azure plan fiyatlandırması hakkında daha fazla bilgi için [Azure plan fiyatlandırma belgelerinde](https://docs.microsoft.com/partner-center/azure-plan-price-list)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7faac-123">More information about Azure plan pricing can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="7faac-124">İş ortağı fiyatlandırması ve yabancı değişim oranı API 'Leri, [Iş Ortağı Merkezi SDK 'sının](https://docs.microsoft.com/partner-center/develop/get-started)bir parçası değildir.</span><span class="sxs-lookup"><span data-stu-id="7faac-124">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="7faac-125">Bu yöntem, bir dosya akışı olarak fiyat listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="7faac-125">This method returns the price list as a file stream.</span></span> <span data-ttu-id="7faac-126">Dosya akışı bir. csv dosyası ya da. csv 'nin zip ile sıkıştırılmış bir sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="7faac-126">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="7faac-127">Sıkıştırılmış dosyaları isteme hakkındaki ayrıntılar aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7faac-127">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="7faac-128">REST isteği</span><span class="sxs-lookup"><span data-stu-id="7faac-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7faac-129">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7faac-129">Request syntax</span></span>

| <span data-ttu-id="7faac-130">Yöntem</span><span class="sxs-lookup"><span data-stu-id="7faac-130">Method</span></span>   | <span data-ttu-id="7faac-131">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="7faac-131">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7faac-132">**Al**</span><span class="sxs-lookup"><span data-stu-id="7faac-132">**GET**</span></span> | <span data-ttu-id="7faac-133"> https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market=' {Market} ', PricesheetView = ' {View} ')/$value</span><span class="sxs-lookup"><span data-stu-id="7faac-133">https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value</span></span>                                     |

### <a name="uri-required-parameters"></a><span data-ttu-id="7faac-134">URI gerekli parametreler</span><span class="sxs-lookup"><span data-stu-id="7faac-134">URI required parameters</span></span>

<span data-ttu-id="7faac-135">Hangi tür fiyatları ve istediğiniz fiyat listesini istemek için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7faac-135">Use the following path parameters to request which market and type of price sheet you want.</span></span>

| <span data-ttu-id="7faac-136">Ad</span><span class="sxs-lookup"><span data-stu-id="7faac-136">Name</span></span>                   | <span data-ttu-id="7faac-137">Tür</span><span class="sxs-lookup"><span data-stu-id="7faac-137">Type</span></span>     | <span data-ttu-id="7faac-138">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7faac-138">Required</span></span> | <span data-ttu-id="7faac-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7faac-139">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="7faac-140">Pazara</span><span class="sxs-lookup"><span data-stu-id="7faac-140">Market</span></span>                      | <span data-ttu-id="7faac-141">string</span><span class="sxs-lookup"><span data-stu-id="7faac-141">string</span></span>   | <span data-ttu-id="7faac-142">Yes</span><span class="sxs-lookup"><span data-stu-id="7faac-142">Yes</span></span>       | <span data-ttu-id="7faac-143">İstenen Pazar için iki harfli ülke kodu</span><span class="sxs-lookup"><span data-stu-id="7faac-143">Two letter country code for the market being requested</span></span>       |
|<span data-ttu-id="7faac-144">PricesheetView</span><span class="sxs-lookup"><span data-stu-id="7faac-144">PricesheetView</span></span> | <span data-ttu-id="7faac-145">string</span><span class="sxs-lookup"><span data-stu-id="7faac-145">string</span></span>   | <span data-ttu-id="7faac-146">Yes</span><span class="sxs-lookup"><span data-stu-id="7faac-146">Yes</span></span>       | <span data-ttu-id="7faac-147">İstenen Fiyat listesi türü, azure_consumption veya azure_reservations olabilir</span><span class="sxs-lookup"><span data-stu-id="7faac-147">The type of price sheet being requested, this can be azure_consumption or azure_reservations</span></span>       |

### <a name="uri-filter-parameters"></a><span data-ttu-id="7faac-148">URI filtresi parametreleri</span><span class="sxs-lookup"><span data-stu-id="7faac-148">URI filter parameters</span></span>

<span data-ttu-id="7faac-149">Aşağıdaki filtre parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7faac-149">Use the following filter parameters.</span></span>

| <span data-ttu-id="7faac-150">Ad</span><span class="sxs-lookup"><span data-stu-id="7faac-150">Name</span></span>                   | <span data-ttu-id="7faac-151">Tür</span><span class="sxs-lookup"><span data-stu-id="7faac-151">Type</span></span>     | <span data-ttu-id="7faac-152">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7faac-152">Required</span></span> | <span data-ttu-id="7faac-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7faac-153">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="7faac-154">Zaman çizelgesi</span><span class="sxs-lookup"><span data-stu-id="7faac-154">Timeline</span></span>| <span data-ttu-id="7faac-155">dize</span><span class="sxs-lookup"><span data-stu-id="7faac-155">string</span></span>   | <span data-ttu-id="7faac-156">No</span><span class="sxs-lookup"><span data-stu-id="7faac-156">No</span></span>| <span data-ttu-id="7faac-157">Geçirilmemişse varsayılan değeri geçerli olarak belirler.</span><span class="sxs-lookup"><span data-stu-id="7faac-157">Defaults to current if not passed.</span></span> <span data-ttu-id="7faac-158">Olası değerler geçmiş, güncel ve gelecekteki değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="7faac-158">Possible values are history, current and future.</span></span>       |
|<span data-ttu-id="7faac-159">Ay</span><span class="sxs-lookup"><span data-stu-id="7faac-159">Month</span></span>| <span data-ttu-id="7faac-160">dize</span><span class="sxs-lookup"><span data-stu-id="7faac-160">string</span></span>   | <span data-ttu-id="7faac-161">No</span><span class="sxs-lookup"><span data-stu-id="7faac-161">No</span></span>| <span data-ttu-id="7faac-162">Yalnızca geçmiş isteniyorsa gereklidir, istenen fiyat listesi için YYYYMM 'ye uymalıdır.</span><span class="sxs-lookup"><span data-stu-id="7faac-162">Only required if history is requested, must adhere to YYYYMM for the price sheet being requested.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="7faac-163">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="7faac-163">Request headers</span></span>

- <span data-ttu-id="7faac-164">Daha fazla bilgi için bkz. [Iş ortağı Rest üst bilgileri](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="7faac-164">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="7faac-165">Yukarıdaki üst bilgilere ek olarak, fiyatlandırma dosyaları sıkıştırılmış bant genişliği ve indirme süreleriyle sıkıştırılmış olarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="7faac-165">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="7faac-166">Dosyalar varsayılan olarak sıkıştırılmaz.</span><span class="sxs-lookup"><span data-stu-id="7faac-166">By default the files are not compressed.</span></span> <span data-ttu-id="7faac-167">Dosyaların sıkıştırılmış sürümlerini almak için aşağıdaki üst bilgi değerini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7faac-167">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="7faac-168">Sıkıştırılan sayfaların yalnızca 2020 Nisan 'dan kullanılabildiğini, 2020 Nisan 'dan önceki tüm sayfaların yalnızca sıkıştırılmamış olarak kullanılabildiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7faac-168">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="7faac-169">Üst bilgi</span><span class="sxs-lookup"><span data-stu-id="7faac-169">Header</span></span>                   | <span data-ttu-id="7faac-170">Değer Türü</span><span class="sxs-lookup"><span data-stu-id="7faac-170">Value Type</span></span>     | <span data-ttu-id="7faac-171">Değer</span><span class="sxs-lookup"><span data-stu-id="7faac-171">Value</span></span> | <span data-ttu-id="7faac-172">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7faac-172">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="7faac-173">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="7faac-173">Accept-Encoding</span></span>| <span data-ttu-id="7faac-174">string</span><span class="sxs-lookup"><span data-stu-id="7faac-174">string</span></span>   | <span data-ttu-id="7faac-175">Söndür</span><span class="sxs-lookup"><span data-stu-id="7faac-175">deflate</span></span>| <span data-ttu-id="7faac-176">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="7faac-176">Optional.</span></span> <span data-ttu-id="7faac-177">Atlanan dosya akışı sıkıştırmamışsa.</span><span class="sxs-lookup"><span data-stu-id="7faac-177">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="7faac-178">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="7faac-178">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="7faac-179">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="7faac-179">REST response</span></span>

<span data-ttu-id="7faac-180">Başarılı olursa, bu yöntem bir dosya akışı olarak fiyat listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="7faac-180">If successful, this method returns the price list as a file stream.</span></span> <span data-ttu-id="7faac-181">Dosya akışı bir. csv dosyası ya da. csv 'nin zip ile sıkıştırılmış bir sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="7faac-181">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7faac-182">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="7faac-182">Response success and error codes</span></span>

<span data-ttu-id="7faac-183">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="7faac-183">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7faac-184">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7faac-184">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7faac-185">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7faac-185">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7faac-186">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="7faac-186">Response example</span></span>

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=pricesheet
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Oct 2019 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","Publisher","SkuDescription","UnitOfMeasure","TermDuration","Market","Currency","UnitPrice","PricingTierRangeMin","PricingTierRangeMax","EffectiveStartDate","EffectiveEndDate","MeterIds","MeterType","Tags“
"Advanced Data Security - SQL Database","DZH318Z0C16V","001J","Advanced Data Security - SQL Database - Standard - US East 2","Microsoft","Advanced Data Security - SQL Database - Standard - US East 2","1 Node/Month","payG-1","US","USD","15","","","3/1/2018 12:00:00 AM","11/30/9999 11:59:59 PM","cb0969aa-aaaa-4d6c-ab4b-7e182fa06aff","1 Node/Month","Azure“
======= Truncated ==============

```
