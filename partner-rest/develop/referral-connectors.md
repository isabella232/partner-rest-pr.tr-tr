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
# <a name="referral-connectors"></a><span data-ttu-id="5072e-103">Başvuru bağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="5072e-103">Referral connectors</span></span>

<span data-ttu-id="5072e-104">Müşteri ilişkileri yönetimi (CRM) müşteri adaylarıyla iş ortağı başvurularını eşleştirmek için başvuru bağlayıcıları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5072e-104">You can use referral connectors to synchronize partner referrals with customer relationship management (CRM) leads.</span></span> <span data-ttu-id="5072e-105">İş ortağı başvurularını almak için HTTPS uç noktası olarak [Microsoft Flow](https://flow.microsoft.com) kullanarak bir başvuru Bağlayıcısı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5072e-105">You can create a referral connector using [Microsoft Flow](https://flow.microsoft.com) as the HTTPS endpoint to receive partner referrals.</span></span> <span data-ttu-id="5072e-106">Daha sonra Flow tarafından alınan başvuruyu bir müşteri adayı olarak bir CRM sistemine yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5072e-106">You can then write the referral received by the flow to a CRM system as a lead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5072e-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="5072e-107">Prerequisites</span></span>

* <span data-ttu-id="5072e-108">Microsoft Flow aboneliği</span><span class="sxs-lookup"><span data-stu-id="5072e-108">Microsoft Flow subscription</span></span>
  * <span data-ttu-id="5072e-109">Bu aboneliğe yönetici erişimi olan hesap</span><span class="sxs-lookup"><span data-stu-id="5072e-109">Account with administrator access to this subscription</span></span>
* <span data-ttu-id="5072e-110">Azure Active Directory (Azure AD) uygulama KIMLIĞI, Kullanıcı kimliği, parola ve kiracı KIMLIĞI (Iş ortağı API 'sine erişmek için kullanılır).</span><span class="sxs-lookup"><span data-stu-id="5072e-110">Azure Active Directory (Azure AD) application ID, user id, password and tenant ID (used to access the Partner API).</span></span> <span data-ttu-id="5072e-111">Kurulum yönergeleri için bkz. [Iş ortağı kimlik doğrulaması](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5072e-111">For setup instructions, see [Partner authentication](api-authentication.md).</span></span>
* <span data-ttu-id="5072e-112">[Azure işlevi uygulama](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) aboneliği.</span><span class="sxs-lookup"><span data-stu-id="5072e-112">[Azure function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) subscription.</span></span>
* <span data-ttu-id="5072e-113">[Iş Ortağı Merkezi Web kancası olay](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) aboneliği [oluşturulan başvuru](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) ve [başvuru güncelleştirilmiş](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event) olayları.</span><span class="sxs-lookup"><span data-stu-id="5072e-113">[Partner Center webhook event](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) subscription to [Referral Created](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) and [Referral Updated](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event) events.</span></span>
* <span data-ttu-id="5072e-114">[Microsoft Dynamics 365](https://dynamics.microsoft.com) aboneliği</span><span class="sxs-lookup"><span data-stu-id="5072e-114">[Microsoft Dynamics 365](https://dynamics.microsoft.com) subscription</span></span>
  * <span data-ttu-id="5072e-115">Satış modülü etkin</span><span class="sxs-lookup"><span data-stu-id="5072e-115">Sales module enabled</span></span>
  * <span data-ttu-id="5072e-116">Bu aboneliğe yönetici erişimi olan hesap</span><span class="sxs-lookup"><span data-stu-id="5072e-116">Account with administrator access to this subscription</span></span>

## <a name="flow-overview"></a><span data-ttu-id="5072e-117">Akışa genel bakış</span><span class="sxs-lookup"><span data-stu-id="5072e-117">Flow overview</span></span>

<span data-ttu-id="5072e-118">Başvurular, CRM 'ye aşağıdaki akış kullanılarak aktarılır:</span><span class="sxs-lookup"><span data-stu-id="5072e-118">Referrals are imported into the CRM using the following flow:</span></span>

1. <span data-ttu-id="5072e-119">İş ortağı, başvuru bildirimleri almak için bir Web kancası ayarlıyor.</span><span class="sxs-lookup"><span data-stu-id="5072e-119">Partner sets up a webhook to receive referral notifications.</span></span>
2. <span data-ttu-id="5072e-120">İş ortağı, Web kancasını Iş Ortağı Merkezi 'ne kaydeder.</span><span class="sxs-lookup"><span data-stu-id="5072e-120">Partner registers the webhook with Partner Center.</span></span> <span data-ttu-id="5072e-121">İş ortağı Ayrıca başvuruların oluşturulma veya güncelleştirilme tarihi için Web kancası olaylarına abone olur.</span><span class="sxs-lookup"><span data-stu-id="5072e-121">The partner also subscribes to webhook events for when referrals are created or updated.</span></span>
3. <span data-ttu-id="5072e-122">Başvuru istemcisi bir başvuruyu oluşturur veya güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="5072e-122">Referral client creates or updates a referral.</span></span>
4. <span data-ttu-id="5072e-123">İş Ortağı Merkezi Web kancası sistemi, iş ortağının kaydını denetler ve Web kancasına bir bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="5072e-123">Partner Center webhook system checks for the partner's registration and sends a notification to the webhook.</span></span>
5. <span data-ttu-id="5072e-124">Web kancası bildirimi alır.</span><span class="sxs-lookup"><span data-stu-id="5072e-124">Webhook receives the notification.</span></span>
6. <span data-ttu-id="5072e-125">Microsoft Flow 'da akış belgesi, Iş ortağı merkezi başvuru API 'sine çağrı yapmak için bir belirteç kullanır.</span><span class="sxs-lookup"><span data-stu-id="5072e-125">Flow document in Microsoft flow uses a token to make a call to the Partner Center referral API.</span></span>
7. <span data-ttu-id="5072e-126">Akış uç noktası başvuruyu alır.</span><span class="sxs-lookup"><span data-stu-id="5072e-126">Flow endpoint gets the referral.</span></span>
8. <span data-ttu-id="5072e-127">Akış uç noktası, CRM lideri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5072e-127">Flow endpoint creates the CRM lead.</span></span>

![İş ortağı başvurularını CRM 'ye aktarmak için bu bölümdeki adımları gösteren akış grafiği.](../images/referralwebhook.png)

## <a name="flow-document-process"></a><span data-ttu-id="5072e-129">Flow belge işlemi</span><span class="sxs-lookup"><span data-stu-id="5072e-129">Flow document process</span></span>

<span data-ttu-id="5072e-130">Bir başvuru bağlayıcısının akış belgesi, Dynamics 365 ' dan bir CRM lideri olan iş ortağı başvurusunu eşitler.</span><span class="sxs-lookup"><span data-stu-id="5072e-130">The flow document for a referral connector synchronizes a partner referral with a CRM lead from Dynamics 365.</span></span>

1. <span data-ttu-id="5072e-131">Bağlayıcı, bağlanılacak bir belirteç alır `https://api.partner.microsoft.com/v1.0/engagements/referrals` .</span><span class="sxs-lookup"><span data-stu-id="5072e-131">Connector gets a token to connect to `https://api.partner.microsoft.com/v1.0/engagements/referrals`.</span></span>
2. <span data-ttu-id="5072e-132">Bağlayıcı, kullanarak bağlayıcıyı tetikleyen başvuruyu edinir `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}` .</span><span class="sxs-lookup"><span data-stu-id="5072e-132">Connector obtains referral that triggered the connector using `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}`.</span></span>
3. <span data-ttu-id="5072e-133">Bağlayıcı Dynamics 365 'e bağlanır.</span><span class="sxs-lookup"><span data-stu-id="5072e-133">Connector connects to Dynamics 365.</span></span>
4. <span data-ttu-id="5072e-134">Bağlayıcı yeni bir müşteri adayı oluşturur veya mevcut bir müşteri adayını başvuru hakkındaki en son bilgilerle güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="5072e-134">Connector creates a new lead or updates an existing lead with the latest information on the referral.</span></span>
5. <span data-ttu-id="5072e-135">Bağlayıcı güncelleştirmeleri, CRM Müşteri adayının en son güncelleştirmeleriyle birlikte yapılır.</span><span class="sxs-lookup"><span data-stu-id="5072e-135">Connector updates referral with the latest updates from the CRM lead.</span></span>

![Flow belge işlemi için bu bölümdeki adımları gösteren akış grafiği.](../images/ReferralFlowSteps.png)

## <a name="sample-referral-connector"></a><span data-ttu-id="5072e-137">Örnek başvuru Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="5072e-137">Sample referral connector</span></span>

<span data-ttu-id="5072e-138">Aşağıdaki *örnek başvuru Bağlayıcısı* , Dynamics 365 ' de Iş ortağı MERKEZI başvurularını CRM müşteri adaylarına nasıl eşitleyeceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5072e-138">The following *sample referral connector* shows how to synchronize Partner Center referrals to CRM leads in Dynamics 365.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5072e-139">Örnek koddaki [akış bağlayıcılarını](https://flow.microsoft.com/en-us/connectors/) değiştirerek farklı CRMS 'ye yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5072e-139">You can write to different CRMs by replacing the [flow connectors](https://flow.microsoft.com/en-us/connectors/) in the sample code.</span></span>

### <a name="import-flow-synchronization-package"></a><span data-ttu-id="5072e-140">Akış eşitleme paketini içeri aktar</span><span class="sxs-lookup"><span data-stu-id="5072e-140">Import flow synchronization package</span></span>

<span data-ttu-id="5072e-141">*Örnek kod paketini* indirip Microsoft Flow ve Dynamics 365 'e bağlanın:</span><span class="sxs-lookup"><span data-stu-id="5072e-141">Download and import the *sample code package* into Microsoft Flow and connect to Dynamics 365:</span></span>

1. <span data-ttu-id="5072e-142">[Akış eşitleme paketini](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) [GitHub deposundan](https://github.com/microsoft/Partner-Center-Referrals)indirin.</span><span class="sxs-lookup"><span data-stu-id="5072e-142">Download the [flow synchronization package](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) from the [GitHub repo](https://github.com/microsoft/Partner-Center-Referrals).</span></span>
2. <span data-ttu-id="5072e-143">[Microsoft Flow](https://flow.microsoft.com) için uygun kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5072e-143">Sign in to [Microsoft Flow](https://flow.microsoft.com) using the appropriate credentials.</span></span>
3. <span data-ttu-id="5072e-144">Gezinti menüsünde **Akışlarım** ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-144">Choose **My Flows** in the navigation menu.</span></span> <span data-ttu-id="5072e-145">Ardından **Içeri aktar**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-145">Then choose **Import**.</span></span>
4. <span data-ttu-id="5072e-146">**Paketi Içeri aktar** sayfasında, indirdiğiniz akış eşitleme paketini seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-146">On the **Import package** page, select the flow synchronization package that you downloaded.</span></span> <span data-ttu-id="5072e-147">Ardından **karşıya yükle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-147">Then choose **Upload**.</span></span>

    ![Paket dosyaları için paket ekranını içeri aktar](../images/importPackage.png)

5. <span data-ttu-id="5072e-149">Paket karşıya yüklemesi tamamlandıktan sonra, **paket Içeriğini gözden geçir** ' de karşıya yüklediğiniz paketi bulun.</span><span class="sxs-lookup"><span data-stu-id="5072e-149">After the package upload is complete, find the package you uploaded in the **Review Package Content** .</span></span>

    ![Paket içeri aktarma ekranının ayrıntıları](../images/importPackageDetails.png)

6. <span data-ttu-id="5072e-151">Karşıya yüklenen paketinizin **eylem** düğmesini (kurşun kalem simgesi) seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-151">Choose the **Action** button (pencil icon) for your uploaded package.</span></span> <span data-ttu-id="5072e-152">Bu, **Içeri aktarma kurulum** dikey penceresini açar.</span><span class="sxs-lookup"><span data-stu-id="5072e-152">This opens the **Import setup** blade.</span></span>
7. <span data-ttu-id="5072e-153">**Kurulum** türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-153">Choose your **Setup** type.</span></span>

    * <span data-ttu-id="5072e-154">Yeni bir akış oluşturmak için yeni **Oluştur**' u seçin ve yeni bir **kaynak adı** girin.</span><span class="sxs-lookup"><span data-stu-id="5072e-154">To create a new flow, select **Create as new**, and enter a new **Resource name**.</span></span>
    * <span data-ttu-id="5072e-155">Aynı ada sahip mevcut bir akışı güncelleştirmek için **Güncelleştir**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-155">To update an existing flow with the same name, select **Update**.</span></span>

    ![Yeni 'a paketi ekleyin ekranı oluştur veya güncelleştir](../images/CreateNewConnection.png)

8. <span data-ttu-id="5072e-157">**Paketi Içeri aktar** sayfasında, **Ilgili kaynaklar** altındaki **paket içeriğini gözden geçir** bölümünde Dynamics 365 bağlantınızı bulun.</span><span class="sxs-lookup"><span data-stu-id="5072e-157">On the **Import package** page, find your Dynamics 365 connection in the **Review Package Content** section under **Related Resources**.</span></span>
9. <span data-ttu-id="5072e-158">Dynamics 365 bağlantınız için **eylem** düğmesini (kurşun kalem simgesi) seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-158">Choose the **Action** button (pencil icon) for your Dynamics 365 connection.</span></span> <span data-ttu-id="5072e-159">Bu, ilgili kaynak için **Içeri aktarma kurulum** dikey penceresini açar.</span><span class="sxs-lookup"><span data-stu-id="5072e-159">This opens the **Import setup** blade for this related resource.</span></span>
10. <span data-ttu-id="5072e-160">Yeni bir Dynamics 365 bağlantısı oluşturmak için **Yeni oluştur** ' u seçin veya var olan bir bağlantıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-160">Choose **Create new** to create a new Dynamics 365 connection, or select an existing connection.</span></span>
11. <span data-ttu-id="5072e-161">**Paketi Içeri aktar** sayfasının şimdi seçili Flow kurulum türünü ve Dynamics 365 bağlantısını gösterdiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5072e-161">Verify that the **Import package** page now shows your selected flow setup type and Dynamics 365 connection.</span></span> <span data-ttu-id="5072e-162">Ardından **Içeri aktar**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-162">Then choose **Import**.</span></span>

    ![Paket durumunu içeri aktarma ekranı](../images/importStatus.png)

12. <span data-ttu-id="5072e-164">Flow kaynağınızın şimdi oluşturulduğunu veya güncelleştirildiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5072e-164">Verify that your flow resource is now created or updated.</span></span>

### <a name="configure-flow-parameters"></a><span data-ttu-id="5072e-165">Akış parametrelerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5072e-165">Configure flow parameters</span></span>

<span data-ttu-id="5072e-166">Akış kaynağınızın parametrelerini yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="5072e-166">Configure the parameters of your flow resource:</span></span>

1. <span data-ttu-id="5072e-167">[Microsoft Flow](https://flow.microsoft.com), gezinti menüsünde **Akışlarım** ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-167">In [Microsoft Flow](https://flow.microsoft.com), choose **My Flows** in the navigation menu.</span></span>
2. <span data-ttu-id="5072e-168">Önceki bölümde oluşturduğunuz veya güncelleştirdiğiniz Flow kaynağını seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-168">Choose the flow resource you created or updated in the previous section.</span></span>
3. <span data-ttu-id="5072e-169">Flow sayfasında **akışı Düzenle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-169">On the flow page, choose **Edit flow**.</span></span>
4. <span data-ttu-id="5072e-170">**AAD-Application (istemci) kimliği** değişkenini seçin ve Azure AD uygulamanızın kimliğini girin.</span><span class="sxs-lookup"><span data-stu-id="5072e-170">Choose the **AAD-Application (client) ID** variable and enter the ID of your Azure AD application.</span></span>
5. <span data-ttu-id="5072e-171">**UserID** değişkenini seçin ve Kullanıcı Kimliğinizi girin.</span><span class="sxs-lookup"><span data-stu-id="5072e-171">Choose the **UserId** variable and enter your user ID.</span></span>
6. <span data-ttu-id="5072e-172">**UserPassword** değişkenini seçin ve Kullanıcı parolanızı girin.</span><span class="sxs-lookup"><span data-stu-id="5072e-172">Choose the **UserPassword** variable and enter your user password.</span></span>
7. <span data-ttu-id="5072e-173">**AAD dizini (kiracı) kimlik** değişkenini seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-173">Select the **AAD-Directory (tenant) ID** variable.</span></span> <span data-ttu-id="5072e-174">Azure AD uygulamanızın kiracı KIMLIĞINI girin.</span><span class="sxs-lookup"><span data-stu-id="5072e-174">Enter the tenant ID of your Azure AD application.</span></span>
8. <span data-ttu-id="5072e-175">Akışınızı kaydetmek için **Kaydet** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-175">Choose **Save** to save your flow.</span></span>

    ![Akış değişkenleri ayarları ekranı](../images/SetFlowVariables.png)

### <a name="authenticate-the-callback"></a><span data-ttu-id="5072e-177">Geri aramanın kimliğini doğrulama</span><span class="sxs-lookup"><span data-stu-id="5072e-177">Authenticate the callback</span></span>

<span data-ttu-id="5072e-178">Iş Ortağı Merkezi 'nden geri çağırma olayının kimliğini doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="5072e-178">Authenticate the callback event from the Partner Center:</span></span>

> [!TIP]
> <span data-ttu-id="5072e-179">Bir örnek için, aşağıdaki bölümde [örnek işlev uygulama kodu](#sample-function-app-code) ' na bakın.</span><span class="sxs-lookup"><span data-stu-id="5072e-179">For an example, see the [sample function app code](#sample-function-app-code) in the following section.</span></span>

1. <span data-ttu-id="5072e-180">[Iş ortağı merkezinden geri çağırma olayının kimliğini doğrulayan](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback) [bir Azure işlev uygulaması oluşturun](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) .</span><span class="sxs-lookup"><span data-stu-id="5072e-180">[Create an Azure function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) that [authenticates the callback event from the Partner Center](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback).</span></span>

    1. <span data-ttu-id="5072e-181">Gerekli üstbilgilerin mevcut olduğunu doğrulayın (**Yetkilendirme**, **x-MS-Certificate-URL** ve **x-MS-Signature-algoritma**).</span><span class="sxs-lookup"><span data-stu-id="5072e-181">Verify that the required headers are present (**Authorization**, **x-ms-certificate-url**, and **x-ms-signature-algorithm**).</span></span>
    2. <span data-ttu-id="5072e-182">İçeriği imzalamak için kullanılan sertifikayı indirin (**x-MS-Certificate-URL**).</span><span class="sxs-lookup"><span data-stu-id="5072e-182">Download the certificate used to sign the content (**x-ms-certificate-url**).</span></span>
    3. <span data-ttu-id="5072e-183">Sertifika zincirini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5072e-183">Verify the certificate chain.</span></span>
    4. <span data-ttu-id="5072e-184">Sertifikanın **organizasyonunu** doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5072e-184">Verify the **Organization** of the certificate.</span></span>
    5. <span data-ttu-id="5072e-185">UTF-8 kodlamalı içeriği bir arabelleğe okur.</span><span class="sxs-lookup"><span data-stu-id="5072e-185">Read the content with UTF-8 encoding into a buffer.</span></span>
    6. <span data-ttu-id="5072e-186">Bir RSA şifreleme sağlayıcısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5072e-186">Create an RSA Crypto Provider.</span></span>
    7. <span data-ttu-id="5072e-187">İmzanın belirtilen karma algoritmasıyla imzalandığını (örneğin, SHA256) [eşleştirdiğini doğrulayın](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) .</span><span class="sxs-lookup"><span data-stu-id="5072e-187">[Verify that the signature matches](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) what was signed with the specified hash algorithm (for example, SHA256).</span></span>
    8. <span data-ttu-id="5072e-188">Doğrulama başarılı olursa, bir **Tamam** iletisi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="5072e-188">If the verification succeeds, an **OK** message is returned.</span></span>

2. <span data-ttu-id="5072e-189">İşlev uygulamanızın HTTP uç noktası için oluşturulan geri çağırma URI 'sini aklınızda edin.</span><span class="sxs-lookup"><span data-stu-id="5072e-189">Note the generated callback URI for your function app's HTTP endpoint.</span></span> <span data-ttu-id="5072e-190">Bu URI, işlev uygulamanızı oluşturduğunuzda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5072e-190">This URI is displayed when you create your function app.</span></span> <span data-ttu-id="5072e-191">Bu URI 'yi, işlev uygulamanızın Azure Kaynak sayfasında de bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5072e-191">You can also find this URI on your function app's Azure resource page.</span></span>
3. <span data-ttu-id="5072e-192">[Microsoft Flow](https://flow.microsoft.com), "Iş ortağı başvurusunu MICROSOFT Dynamics CRM müşteri adayına" bölümünü *[içeri aktarma akışı eşitleme paketi](#import-flow-synchronization-package)*' nde içeri aktardığınız akışı düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="5072e-192">In [Microsoft Flow](https://flow.microsoft.com), edit the flow "Partner Referral to Microsoft Dynamics CRM Lead" that you imported in the section *[Import flow synchronization package](#import-flow-synchronization-package)*.</span></span>

    1. <span data-ttu-id="5072e-193">İşlev uygulamasının URI değerini "Web kancası sertifikası doğrulama" adımına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5072e-193">Add the value of the function app's URI to the "web hook certificate validation" step.</span></span>
    2. <span data-ttu-id="5072e-194">İşlev uygulamanızın geri çağırma URI 'sini kopyalayın ve akış belgesine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="5072e-194">Copy and paste your function app's callback URI into the flow document.</span></span>
    3. <span data-ttu-id="5072e-195">Akış belgenizi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5072e-195">Save your flow document.</span></span>

#### <a name="sample-function-app-code"></a><span data-ttu-id="5072e-196">Örnek işlev uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="5072e-196">Sample function app code</span></span>

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

### <a name="register-flow-with-partner-center"></a><span data-ttu-id="5072e-197">Akışı Iş Ortağı Merkezi ile kaydetme</span><span class="sxs-lookup"><span data-stu-id="5072e-197">Register flow with Partner Center</span></span>

<span data-ttu-id="5072e-198">Akışı tetiklemek ve Web kancası olaylarını almak için akış kaynağınızı Iş Ortağı Merkezi ile kaydedin:</span><span class="sxs-lookup"><span data-stu-id="5072e-198">Register your flow resource with the Partner Center to trigger the flow and receive webhook events:</span></span>

1. <span data-ttu-id="5072e-199">[Microsoft Flow](https://flow.microsoft.com), gezinti menüsünde **Akışlarım** ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-199">In [Microsoft Flow](https://flow.microsoft.com), choose **My Flows** in the navigation menu.</span></span>
2. <span data-ttu-id="5072e-200">Oluşturduğunuz veya güncelleştirdiğiniz akışı seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-200">Choose the flow you created or updated.</span></span>
3. <span data-ttu-id="5072e-201">Flow sayfasında **akışı Düzenle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="5072e-201">On the flow page, choose **Edit flow**.</span></span>
4. <span data-ttu-id="5072e-202">Akışın **http gönderi URL 'sini** kopyalayıp kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5072e-202">Copy and save the flow's **HTTP POST URL**.</span></span> <span data-ttu-id="5072e-203">Akışı tetiklemek için bu URL 'YI kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5072e-203">You will need to use this URL to trigger the flow.</span></span>
5. <span data-ttu-id="5072e-204">Başvurular oluşturulduğunda veya güncelleştirilirken [Web kancası olaylarını almak Için kaydolun](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) .</span><span class="sxs-lookup"><span data-stu-id="5072e-204">[Register to receive webhook events](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) when referrals are created or updated.</span></span> <span data-ttu-id="5072e-205">Aşağıdaki gövde biçimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="5072e-205">Use the following body format:</span></span>

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
