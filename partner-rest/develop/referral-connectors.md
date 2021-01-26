---
title: Başvuru bağlayıcıları.
description: Microsoft Flow kullanarak, iş ortağı başvurularını Dynamics 365 CRM müşteri adaylarıyla eşitler.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0a62023feb03114bb7ba1136b7700875f24c2e01
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770594"
---
# <a name="referral-connectors"></a>Başvuru bağlayıcıları

Müşteri ilişkileri yönetimi (CRM) müşteri adaylarıyla iş ortağı başvurularını eşleştirmek için başvuru bağlayıcıları kullanabilirsiniz. İş ortağı başvurularını almak için HTTPS uç noktası olarak [Microsoft Flow](https://flow.microsoft.com) kullanarak bir başvuru Bağlayıcısı oluşturabilirsiniz. Daha sonra Flow tarafından alınan başvuruyu bir müşteri adayı olarak bir CRM sistemine yazabilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

* Microsoft Flow aboneliği
  * Bu aboneliğe yönetici erişimi olan hesap
* Azure Active Directory (Azure AD) uygulama KIMLIĞI, Kullanıcı kimliği, parola ve kiracı KIMLIĞI (Iş ortağı API 'sine erişmek için kullanılır). Kurulum yönergeleri için bkz. [Iş ortağı kimlik doğrulaması](api-authentication.md).
* [Azure işlevi uygulama](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) aboneliği.
* [Iş Ortağı Merkezi Web kancası olay](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) aboneliği [oluşturulan başvuru](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) ve [başvuru güncelleştirilmiş](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event) olayları.
* [Microsoft Dynamics 365](https://dynamics.microsoft.com) aboneliği
  * Satış modülü etkin
  * Bu aboneliğe yönetici erişimi olan hesap

## <a name="flow-overview"></a>Akışa genel bakış

Başvurular, CRM 'ye aşağıdaki akış kullanılarak aktarılır:

1. İş ortağı, başvuru bildirimleri almak için bir Web kancası ayarlıyor.
2. İş ortağı, Web kancasını Iş Ortağı Merkezi 'ne kaydeder. İş ortağı Ayrıca başvuruların oluşturulma veya güncelleştirilme tarihi için Web kancası olaylarına abone olur.
3. Başvuru istemcisi bir başvuruyu oluşturur veya güncelleştirir.
4. İş Ortağı Merkezi Web kancası sistemi, iş ortağının kaydını denetler ve Web kancasına bir bildirim gönderir.
5. Web kancası bildirimi alır.
6. Microsoft Flow 'da akış belgesi, Iş ortağı merkezi başvuru API 'sine çağrı yapmak için bir belirteç kullanır.
7. Akış uç noktası başvuruyu alır.
8. Akış uç noktası, CRM lideri oluşturur.

![İş ortağı başvurularını CRM 'ye aktarmak için bu bölümdeki adımları gösteren akış grafiği.](../images/referralwebhook.png)

## <a name="flow-document-process"></a>Flow belge işlemi

Bir başvuru bağlayıcısının akış belgesi, Dynamics 365 ' dan bir CRM lideri olan iş ortağı başvurusunu eşitler.

1. Bağlayıcı, bağlanılacak bir belirteç alır `https://api.partner.microsoft.com/v1.0/engagements/referrals` .
2. Bağlayıcı, kullanarak bağlayıcıyı tetikleyen başvuruyu edinir `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}` .
3. Bağlayıcı Dynamics 365 'e bağlanır.
4. Bağlayıcı yeni bir müşteri adayı oluşturur veya mevcut bir müşteri adayını başvuru hakkındaki en son bilgilerle güncelleştirir.
5. Bağlayıcı güncelleştirmeleri, CRM Müşteri adayının en son güncelleştirmeleriyle birlikte yapılır.

![Flow belge işlemi için bu bölümdeki adımları gösteren akış grafiği.](../images/ReferralFlowSteps.png)

## <a name="sample-referral-connector"></a>Örnek başvuru Bağlayıcısı

Aşağıdaki *örnek başvuru Bağlayıcısı* , Dynamics 365 ' de Iş ortağı MERKEZI başvurularını CRM müşteri adaylarına nasıl eşitleyeceğiniz gösterilmektedir.

> [!IMPORTANT]
> Örnek koddaki [akış bağlayıcılarını](https://flow.microsoft.com/en-us/connectors/) değiştirerek farklı CRMS 'ye yazabilirsiniz.

### <a name="import-flow-synchronization-package"></a>Akış eşitleme paketini içeri aktar

*Örnek kod paketini* indirip Microsoft Flow ve Dynamics 365 'e bağlanın:

1. [Akış eşitleme paketini](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) [GitHub deposundan](https://github.com/microsoft/Partner-Center-Referrals)indirin.
2. [Microsoft Flow](https://flow.microsoft.com) için uygun kimlik bilgilerini kullanarak oturum açın.
3. Gezinti menüsünde **Akışlarım** ' ı seçin. Ardından **Içeri aktar**' ı seçin.
4. **Paketi Içeri aktar** sayfasında, indirdiğiniz akış eşitleme paketini seçin. Ardından **karşıya yükle**' yi seçin.

    ![Paket dosyaları için paket ekranını içeri aktar](../images/importPackage.png)

5. Paket karşıya yüklemesi tamamlandıktan sonra, **paket Içeriğini gözden geçir** ' de karşıya yüklediğiniz paketi bulun.

    ![Paket içeri aktarma ekranının ayrıntıları](../images/importPackageDetails.png)

6. Karşıya yüklenen paketinizin **eylem** düğmesini (kurşun kalem simgesi) seçin. Bu, **Içeri aktarma kurulum** dikey penceresini açar.
7. **Kurulum** türünü seçin.

    * Yeni bir akış oluşturmak için yeni **Oluştur**' u seçin ve yeni bir **kaynak adı** girin.
    * Aynı ada sahip mevcut bir akışı güncelleştirmek için **Güncelleştir**' i seçin.

    ![Yeni 'a paketi ekleyin ekranı oluştur veya güncelleştir](../images/CreateNewConnection.png)

8. **Paketi Içeri aktar** sayfasında, **Ilgili kaynaklar** altındaki **paket içeriğini gözden geçir** bölümünde Dynamics 365 bağlantınızı bulun.
9. Dynamics 365 bağlantınız için **eylem** düğmesini (kurşun kalem simgesi) seçin. Bu, ilgili kaynak için **Içeri aktarma kurulum** dikey penceresini açar.
10. Yeni bir Dynamics 365 bağlantısı oluşturmak için **Yeni oluştur** ' u seçin veya var olan bir bağlantıyı seçin.
11. **Paketi Içeri aktar** sayfasının şimdi seçili Flow kurulum türünü ve Dynamics 365 bağlantısını gösterdiğini doğrulayın. Ardından **Içeri aktar**' ı seçin.

    ![Paket durumunu içeri aktarma ekranı](../images/importStatus.png)

12. Flow kaynağınızın şimdi oluşturulduğunu veya güncelleştirildiğini doğrulayın.

### <a name="configure-flow-parameters"></a>Akış parametrelerini yapılandırma

Akış kaynağınızın parametrelerini yapılandırın:

1. [Microsoft Flow](https://flow.microsoft.com), gezinti menüsünde **Akışlarım** ' ı seçin.
2. Önceki bölümde oluşturduğunuz veya güncelleştirdiğiniz Flow kaynağını seçin.
3. Flow sayfasında **akışı Düzenle**' yi seçin.
4. **AAD-Application (istemci) kimliği** değişkenini seçin ve Azure AD uygulamanızın kimliğini girin.
5. **UserID** değişkenini seçin ve Kullanıcı Kimliğinizi girin.
6. **UserPassword** değişkenini seçin ve Kullanıcı parolanızı girin.
7. **AAD dizini (kiracı) kimlik** değişkenini seçin. Azure AD uygulamanızın kiracı KIMLIĞINI girin.
8. Akışınızı kaydetmek için **Kaydet** ' i seçin.

    ![Akış değişkenleri ayarları ekranı](../images/SetFlowVariables.png)

### <a name="authenticate-the-callback"></a>Geri aramanın kimliğini doğrulama

Iş Ortağı Merkezi 'nden geri çağırma olayının kimliğini doğrulayın:

> [!TIP]
> Bir örnek için, aşağıdaki bölümde [örnek işlev uygulama kodu](#sample-function-app-code) ' na bakın.

1. [Iş ortağı merkezinden geri çağırma olayının kimliğini doğrulayan](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback) [bir Azure işlev uygulaması oluşturun](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) .

    1. Gerekli üstbilgilerin mevcut olduğunu doğrulayın (**Yetkilendirme**, **x-MS-Certificate-URL** ve **x-MS-Signature-algoritma**).
    2. İçeriği imzalamak için kullanılan sertifikayı indirin (**x-MS-Certificate-URL**).
    3. Sertifika zincirini doğrulayın.
    4. Sertifikanın **organizasyonunu** doğrulayın.
    5. UTF-8 kodlamalı içeriği bir arabelleğe okur.
    6. Bir RSA şifreleme sağlayıcısı oluşturun.
    7. İmzanın belirtilen karma algoritmasıyla imzalandığını (örneğin, SHA256) [eşleştirdiğini doğrulayın](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) .
    8. Doğrulama başarılı olursa, bir **Tamam** iletisi döndürülür.

2. İşlev uygulamanızın HTTP uç noktası için oluşturulan geri çağırma URI 'sini aklınızda edin. Bu URI, işlev uygulamanızı oluşturduğunuzda görüntülenir. Bu URI 'yi, işlev uygulamanızın Azure Kaynak sayfasında de bulabilirsiniz.
3. [Microsoft Flow](https://flow.microsoft.com), "Iş ortağı başvurusunu MICROSOFT Dynamics CRM müşteri adayına" bölümünü *[içeri aktarma akışı eşitleme paketi](#import-flow-synchronization-package)*' nde içeri aktardığınız akışı düzenleyin.

    1. İşlev uygulamasının URI değerini "Web kancası sertifikası doğrulama" adımına ekleyin.
    2. İşlev uygulamanızın geri çağırma URI 'sini kopyalayın ve akış belgesine yapıştırın.
    3. Akış belgenizi kaydedin.

#### <a name="sample-function-app-code"></a>Örnek işlev uygulama kodu

```csharp
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using Microsoft.Azure.WebJobs;
using Microsoft.Extensions.Logging;
using System;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Security.Cryptography.X509Certificates;
using System.Text;
using System.Threading.Tasks;

public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
{
    string requestBody = null;
    if (!string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-certificate-url")) && !string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-signature-algorithm")))
    {
        var certificateUrl = req?.Headers["x-ms-certificate-url"].First();
        try
        {
            string resultContent = null;
            using (var client = new HttpClient())
            {
                var result = await client.GetAsync(req.Headers["x-ms-certificate-url"].First());
                resultContent = await result.Content.ReadAsStringAsync();
                log.LogInformation(resultContent);
            }
            if (!string.IsNullOrEmpty(resultContent))
            {
                var certificate = new X509Certificate2(Encoding.UTF8.GetBytes(resultContent));
                var validationResult = certificate.Verify() && certificate.Issuer.Contains("O=Microsoft Corporation");
                if (validationResult)
                {
                    return new OkResult();
                }
                else
                {
                    return new BadRequestResult();
                }
            }
        }
        catch (Exception)
        {
            new BadRequestObjectResult("Certificate could not be retrieved, invalid caller to flow");
        }

        requestBody = await new StreamReader(req.Body).ReadToEndAsync();
        dynamic data = JsonConvert.DeserializeObject(requestBody);
    }
    else
    {
        new BadRequestObjectResult("Missing headers");
    }

    return new BadRequestObjectResult("Certificate validation failed");
}

private static string GetFirstValueFromHeader(HttpRequest request, string headerName)
{
    StringValues matchingHeaderValues;
    request.Headers.TryGetValue(headerName, out matchingHeaderValues);
    return matchingHeaderValues.Count != 0 ? matchingHeaderValues.First() : string.Empty;
}
```

### <a name="register-flow-with-partner-center"></a>Akışı Iş Ortağı Merkezi ile kaydetme

Akışı tetiklemek ve Web kancası olaylarını almak için akış kaynağınızı Iş Ortağı Merkezi ile kaydedin:

1. [Microsoft Flow](https://flow.microsoft.com), gezinti menüsünde **Akışlarım** ' ı seçin.
2. Oluşturduğunuz veya güncelleştirdiğiniz akışı seçin.
3. Flow sayfasında **akışı Düzenle**' yi seçin.
4. Akışın **http gönderi URL 'sini** kopyalayıp kaydedin. Akışı tetiklemek için bu URL 'YI kullanmanız gerekir.
5. Başvurular oluşturulduğunda veya güncelleştirilirken [Web kancası olaylarını almak Için kaydolun](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) . Aşağıdaki gövde biçimini kullanın:

```json
{
    "WebhookUrl": "<<FlowUrl>>",
    "WebhookEvents": [
        "referral-created",
        "referral-updated"
    ],
    "signatureTokenToMsSignatureHeader": true
}
```
