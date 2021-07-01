---
title: Fiyat listesi alma
description: Belirli bir Pazar ve görünüm için bir fiyat listesi alın. Aya göre geçmişi almak için filtreleri destekler.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 7571e8fce861dbfe463000a1ac4094115af08ffa
ms.sourcegitcommit: 9e64d6358ef4e1ac2d3e0d36cd63490a5f760b38
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/01/2021
ms.locfileid: "113125525"
---
# <a name="get-a-price-sheet"></a><span data-ttu-id="bde2e-104">Fiyat listesi alma</span><span class="sxs-lookup"><span data-stu-id="bde2e-104">Get a price sheet</span></span>

<span data-ttu-id="bde2e-105">Aşağıdakiler cihazlar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="bde2e-105">Applies to:</span></span>

- <span data-ttu-id="bde2e-106">İş ortağı API 'SI</span><span class="sxs-lookup"><span data-stu-id="bde2e-106">Partner API</span></span>

<span data-ttu-id="bde2e-107">Bu konuda, belirli bir Pazar ve görünüm için fiyat listesi alma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bde2e-107">This topic explains how to get a price sheet for a given market and view.</span></span> <span data-ttu-id="bde2e-108">Bu yöntem, geçmişi aya göre almak için filtreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="bde2e-108">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bde2e-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="bde2e-109">Prerequisites</span></span>

- <span data-ttu-id="bde2e-110">[Iş ortağı API kimlik doğrulaması](api-authentication.md)bölümünde açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="bde2e-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="bde2e-111">Bu senaryo yalnızca uygulama kullanıcı kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="bde2e-111">This scenario only supports application user authentication.</span></span> <span data-ttu-id="bde2e-112">Yalnızca uygulama henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="bde2e-112">Application-only is not yet supported.</span></span> <span data-ttu-id="bde2e-113">Http hatasıyla karşılaşan iş ortakları **: 400** [iş ortağı API kimlik doğrulama](api-authentication.md) belgelerine başvurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bde2e-113">Partners that experience **http error:400** should consult the [Partner API authentication](api-authentication.md) documentation.</span></span>
- <span data-ttu-id="bde2e-114">Bu API Şu anda yalnızca iş ortaklarının şu rollerden birinde olması gereken Kullanıcı erişimini destekliyor: genel yönetici, Yönetim Aracısı veya satış Aracısı.</span><span class="sxs-lookup"><span data-stu-id="bde2e-114">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="bde2e-115">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="bde2e-115">Details</span></span>

- <span data-ttu-id="bde2e-116">Geçerli, yalnızca Azure planı tüketimi ve rezervasyon ürünleri için verileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="bde2e-116">Current returns data only for Azure plan consumption and reservation products.</span></span>
- <span data-ttu-id="bde2e-117">Geçerli [fiyatlandırma](pricing.md) , geçerli ay boyunca API 'nin çağrıldığı tarihe kadar sunulan tüm ölçümleri ve ürünleri içerir.</span><span class="sxs-lookup"><span data-stu-id="bde2e-117">Current [pricing](pricing.md) includes all meters and products available during the current month to the date the API is called.</span></span> <span data-ttu-id="bde2e-118">Önceki aylar, belirli bir ay için kullanılabilen tüm ölçümleri ve ürünleri içerir.</span><span class="sxs-lookup"><span data-stu-id="bde2e-118">Previous months include all meters and products available for the given month.</span></span>
- <span data-ttu-id="bde2e-119">Tüketim ölçümü fiyatları yalnızca ABD doları cinsindendir, iş ortakları yerel para birimi maliyetlerini hesaplamak için yabancı Exchange ücretleri API 'sini kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="bde2e-119">Consumption meter prices are only in USD, partners are to use the foreign exchange rates API to calculate local currency costs.</span></span>
- <span data-ttu-id="bde2e-120">Tüketim ölçümü fiyatları, tahmini perakende fiyatlarıdır.</span><span class="sxs-lookup"><span data-stu-id="bde2e-120">Consumption meter prices are estimated retail prices.</span></span> <span data-ttu-id="bde2e-121">İş ortağı indirimleri, [iş ortağı tarafından kazanılan kredi](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation)aracılığıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bde2e-121">Partner discounts are available via [partner earned credit](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span></span>
- <span data-ttu-id="bde2e-122">Rezervasyonların ölçüm fiyatları, CSP iş ortağı indirimlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="bde2e-122">Reservations meter prices include the CSP partner discounts.</span></span> <span data-ttu-id="bde2e-123">Rezervasyonlar için tahmini perakende fiyatları, Iş Ortağı Merkezi "fiyatlandırma ve teklifler" sayfasında indirilebilir olan rezervasyonlar paylaşılan hizmetlerinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="bde2e-123">Estimated retail prices for reservations can be found in the reservations shared services downloadable from the Partner Center "Pricing and offers" page.</span></span>
- <span data-ttu-id="bde2e-124">Azure plan fiyatlandırması hakkında daha fazla bilgi için [Azure plan fiyatlandırma belgelerinde](https://docs.microsoft.com/partner-center/azure-plan-price-list)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bde2e-124">More information about Azure plan pricing can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="bde2e-125">İş ortağı fiyatlandırması ve yabancı değişim oranı API 'Leri, [Iş Ortağı Merkezi SDK 'sının](https://docs.microsoft.com/partner-center/develop/get-started)bir parçası değildir.</span><span class="sxs-lookup"><span data-stu-id="bde2e-125">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="bde2e-126">Bu yöntem, bir dosya akışı olarak fiyat listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="bde2e-126">This method returns the price list as a file stream.</span></span> <span data-ttu-id="bde2e-127">Dosya akışı, .csv bir .csv dosyası ya da zip ile sıkıştırılmış bir sürümdür.</span><span class="sxs-lookup"><span data-stu-id="bde2e-127">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="bde2e-128">Sıkıştırılmış dosyaları isteme hakkındaki ayrıntılar aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bde2e-128">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="bde2e-129">REST isteği</span><span class="sxs-lookup"><span data-stu-id="bde2e-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bde2e-130">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="bde2e-130">Request syntax</span></span>

| <span data-ttu-id="bde2e-131">Yöntem</span><span class="sxs-lookup"><span data-stu-id="bde2e-131">Method</span></span>   | <span data-ttu-id="bde2e-132">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="bde2e-132">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bde2e-133">**Al**</span><span class="sxs-lookup"><span data-stu-id="bde2e-133">**GET**</span></span> | <span data-ttu-id="bde2e-134"> https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market=' {Market} ', PricesheetView = ' {View} ')/$value</span><span class="sxs-lookup"><span data-stu-id="bde2e-134">https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value</span></span>                                     |

### <a name="uri-required-parameters"></a><span data-ttu-id="bde2e-135">URI gerekli parametreler</span><span class="sxs-lookup"><span data-stu-id="bde2e-135">URI required parameters</span></span>

<span data-ttu-id="bde2e-136">Hangi tür fiyatları ve istediğiniz fiyat listesini istemek için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="bde2e-136">Use the following path parameters to request which market and type of price sheet you want.</span></span>

| <span data-ttu-id="bde2e-137">Ad</span><span class="sxs-lookup"><span data-stu-id="bde2e-137">Name</span></span>                   | <span data-ttu-id="bde2e-138">Tür</span><span class="sxs-lookup"><span data-stu-id="bde2e-138">Type</span></span>     | <span data-ttu-id="bde2e-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bde2e-139">Required</span></span> | <span data-ttu-id="bde2e-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bde2e-140">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="bde2e-141">Pazara</span><span class="sxs-lookup"><span data-stu-id="bde2e-141">Market</span></span>                      | <span data-ttu-id="bde2e-142">string</span><span class="sxs-lookup"><span data-stu-id="bde2e-142">string</span></span>   | <span data-ttu-id="bde2e-143">Yes</span><span class="sxs-lookup"><span data-stu-id="bde2e-143">Yes</span></span>       | <span data-ttu-id="bde2e-144">İstenen Pazar için iki harfli ülke kodu</span><span class="sxs-lookup"><span data-stu-id="bde2e-144">Two letter country code for the market being requested</span></span>       |
|<span data-ttu-id="bde2e-145">PricesheetView</span><span class="sxs-lookup"><span data-stu-id="bde2e-145">PricesheetView</span></span> | <span data-ttu-id="bde2e-146">string</span><span class="sxs-lookup"><span data-stu-id="bde2e-146">string</span></span>   | <span data-ttu-id="bde2e-147">Yes</span><span class="sxs-lookup"><span data-stu-id="bde2e-147">Yes</span></span>       | <span data-ttu-id="bde2e-148">İstenen Fiyat listesi türü, bu azure_consumption, azure_reservations veya updatedlicensebased olabilir.</span><span class="sxs-lookup"><span data-stu-id="bde2e-148">The type of price sheet being requested, this can be azure_consumption, azure_reservations or updatedlicensebased.</span></span>  |

> [!Note]
> <span data-ttu-id="bde2e-149">updatedlicensebased PriceSheetView Şu anda yalnızca M365/D365 yeni ticaret deneyimi Technical Preview 'ın parçası olan iş ortakları tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bde2e-149">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

### <a name="uri-filter-parameters"></a><span data-ttu-id="bde2e-150">URI filtresi parametreleri</span><span class="sxs-lookup"><span data-stu-id="bde2e-150">URI filter parameters</span></span>

<span data-ttu-id="bde2e-151">Aşağıdaki filtre parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="bde2e-151">Use the following filter parameters.</span></span>

| <span data-ttu-id="bde2e-152">Ad</span><span class="sxs-lookup"><span data-stu-id="bde2e-152">Name</span></span>                   | <span data-ttu-id="bde2e-153">Tür</span><span class="sxs-lookup"><span data-stu-id="bde2e-153">Type</span></span>     | <span data-ttu-id="bde2e-154">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bde2e-154">Required</span></span> | <span data-ttu-id="bde2e-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bde2e-155">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="bde2e-156">Zaman çizelgesi</span><span class="sxs-lookup"><span data-stu-id="bde2e-156">Timeline</span></span>| <span data-ttu-id="bde2e-157">dize</span><span class="sxs-lookup"><span data-stu-id="bde2e-157">string</span></span>   | <span data-ttu-id="bde2e-158">No</span><span class="sxs-lookup"><span data-stu-id="bde2e-158">No</span></span>| <span data-ttu-id="bde2e-159">Geçirilmemişse varsayılan değeri geçerli olarak belirler.</span><span class="sxs-lookup"><span data-stu-id="bde2e-159">Defaults to current if not passed.</span></span> <span data-ttu-id="bde2e-160">Olası değerler geçmiş, güncel ve gelecekteki değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="bde2e-160">Possible values are history, current and future.</span></span>       |
|<span data-ttu-id="bde2e-161">Ay</span><span class="sxs-lookup"><span data-stu-id="bde2e-161">Month</span></span>| <span data-ttu-id="bde2e-162">dize</span><span class="sxs-lookup"><span data-stu-id="bde2e-162">string</span></span>   | <span data-ttu-id="bde2e-163">No</span><span class="sxs-lookup"><span data-stu-id="bde2e-163">No</span></span>| <span data-ttu-id="bde2e-164">Yalnızca geçmiş isteniyorsa gereklidir, istenen fiyat listesi için YYYYMM 'ye uymalıdır.</span><span class="sxs-lookup"><span data-stu-id="bde2e-164">Only required if history is requested, must adhere to YYYYMM for the price sheet being requested.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="bde2e-165">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="bde2e-165">Request headers</span></span>

- <span data-ttu-id="bde2e-166">Daha fazla bilgi için bkz. [Iş ortağı Rest üst bilgileri](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="bde2e-166">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="bde2e-167">Yukarıdaki üst bilgilere ek olarak, fiyatlandırma dosyaları sıkıştırılmış bant genişliği ve indirme süreleriyle sıkıştırılmış olarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="bde2e-167">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="bde2e-168">Dosyalar varsayılan olarak sıkıştırılmaz.</span><span class="sxs-lookup"><span data-stu-id="bde2e-168">By default the files are not compressed.</span></span> <span data-ttu-id="bde2e-169">Dosyaların sıkıştırılmış sürümlerini almak için aşağıdaki üst bilgi değerini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bde2e-169">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="bde2e-170">Sıkıştırılan sayfaların yalnızca 2020 Nisan 'dan kullanılabildiğini, 2020 Nisan 'dan önceki tüm sayfaların yalnızca sıkıştırılmamış olarak kullanılabildiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bde2e-170">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="bde2e-171">Üst bilgi</span><span class="sxs-lookup"><span data-stu-id="bde2e-171">Header</span></span>                   | <span data-ttu-id="bde2e-172">Değer Türü</span><span class="sxs-lookup"><span data-stu-id="bde2e-172">Value Type</span></span>     | <span data-ttu-id="bde2e-173">Değer</span><span class="sxs-lookup"><span data-stu-id="bde2e-173">Value</span></span> | <span data-ttu-id="bde2e-174">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bde2e-174">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="bde2e-175">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="bde2e-175">Accept-Encoding</span></span>| <span data-ttu-id="bde2e-176">string</span><span class="sxs-lookup"><span data-stu-id="bde2e-176">string</span></span>   | <span data-ttu-id="bde2e-177">Söndür</span><span class="sxs-lookup"><span data-stu-id="bde2e-177">deflate</span></span>| <span data-ttu-id="bde2e-178">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="bde2e-178">Optional.</span></span> <span data-ttu-id="bde2e-179">Atlanan dosya akışı sıkıştırmamışsa.</span><span class="sxs-lookup"><span data-stu-id="bde2e-179">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="bde2e-180">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="bde2e-180">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```
### <a name="request-example-for-new-commerce"></a><span data-ttu-id="bde2e-181">Yeni Ticaret için istek örneği</span><span class="sxs-lookup"><span data-stu-id="bde2e-181">Request example for new commerce</span></span>

> [!Note]
> <span data-ttu-id="bde2e-182">updatedlicensebased PriceSheetView Şu anda yalnızca M365/D365 yeni ticaret deneyimi Technical Preview 'ın parçası olan iş ortakları tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bde2e-182">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='US',PricesheetView='updatedlicensebased')/$value?timeline=history&month=202101 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="bde2e-183">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="bde2e-183">REST response</span></span>

<span data-ttu-id="bde2e-184">Başarılı olursa, bu yöntem bir dosya akışı olarak fiyat listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="bde2e-184">If successful, this method returns the price list as a file stream.</span></span> <span data-ttu-id="bde2e-185">Dosya akışı, .csv bir .csv dosyası ya da zip ile sıkıştırılmış bir sürümdür.</span><span class="sxs-lookup"><span data-stu-id="bde2e-185">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bde2e-186">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="bde2e-186">Response success and error codes</span></span>

<span data-ttu-id="bde2e-187">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="bde2e-187">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bde2e-188">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="bde2e-188">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bde2e-189">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="bde2e-189">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bde2e-190">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="bde2e-190">Response example</span></span>

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

### <a name="response-example-for-new-commerce"></a><span data-ttu-id="bde2e-191">Yeni Ticaret için yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="bde2e-191">Response example for new commerce</span></span>

> [!Note]
> <span data-ttu-id="bde2e-192">updatedlicensebased PriceSheetView Şu anda yalnızca M365/D365 yeni ticaret deneyimi Technical Preview 'ın parçası olan iş ortakları tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bde2e-192">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=sheets.csv
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Feb 2021 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","Publisher","SkuDescription","UnitOfMeasure","TermDuration","BillingPlan","Market","Currency","UnitPrice","PricingTierRangeMin","PricingTierRangeMax","EffectiveStartDate","EffectiveEndDate","Tags","ERP Price“
"Advanced Communications","CFQ7TTC0HDK0","0001","Advanced Communications","Microsoft Corporation","Advanced meetings, calling, workflow integration, and management tools for IT.","","P1Y","Annual","US","USD","115.2","","","2/1/2019 12:00:00 AM","2/4/2021 8:35:31 PM","License","144"
======= Truncated ==============

```
