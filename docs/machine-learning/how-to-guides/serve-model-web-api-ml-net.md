---
title: 在 ASP.NET Core Web API 中提供機器學習模型
description: 使用 ASP.NET Core Web API 在網際網路上提供 ML.NET 情感分析機器學習模型
ms.date: 03/05/2019
ms.custom: mvc,how-to
ms.openlocfilehash: 0cc13ec22b3a8805ec4aa17bf10560b2564ccd63
ms.sourcegitcommit: 77854e8704b9689b73103d691db34d71c2bf1dad
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2019
ms.locfileid: "58307911"
---
# <a name="how-to-serve-machine-learning-model-through-aspnet-core-web-api"></a><span data-ttu-id="15ba5-103">操作說明：透過 ASP.NET Core Web API 提供機器學習模型</span><span class="sxs-lookup"><span data-stu-id="15ba5-103">How-To: Serve Machine Learning Model Through ASP.NET Core Web API</span></span>

<span data-ttu-id="15ba5-104">此操作說明會顯示如何使用 ASP.NET Core Web API 將預先建置的 ML.NET 機器學習模型提供給 Web。</span><span class="sxs-lookup"><span data-stu-id="15ba5-104">This how-to shows how to serve a pre-built ML.NET machine learning model to the web using an ASP.NET Core Web API.</span></span> <span data-ttu-id="15ba5-105">透過這種方式，它可讓使用者透過標準 HTTP 方法，針對預測目的存取 API。</span><span class="sxs-lookup"><span data-stu-id="15ba5-105">By doing so it allows for users to access the API for prediction purposes via standard HTTP methods.</span></span>

> [!NOTE]
> <span data-ttu-id="15ba5-106">本主題涉及 ML.NET，此功能目前為公開預覽版，因此内容可能會有變更。</span><span class="sxs-lookup"><span data-stu-id="15ba5-106">This topic refers to ML.NET, which is currently in Preview, and material may be subject to change.</span></span> <span data-ttu-id="15ba5-107">如需詳細資訊，請瀏覽 [ML.NET 簡介](https://www.microsoft.com/net/learn/apps/machine-learning-and-ai/ml-dotnet) (英文)。</span><span class="sxs-lookup"><span data-stu-id="15ba5-107">For more information, visit [the ML.NET introduction](https://www.microsoft.com/net/learn/apps/machine-learning-and-ai/ml-dotnet).</span></span>

<span data-ttu-id="15ba5-108">本操作說明與關聯的範例目前是使用 **ML.NET 0.10 版**。</span><span class="sxs-lookup"><span data-stu-id="15ba5-108">This how-to and related sample are currently using **ML.NET version 0.10**.</span></span> <span data-ttu-id="15ba5-109">如需詳細資訊，請參閱 [dotnet/machinelearning GitHub 存放庫](https://github.com/dotnet/machinelearning/tree/master/docs/release-notes) \(英文\) 中的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="15ba5-109">For more information, see the release notes at the [dotnet/machinelearning github repo](https://github.com/dotnet/machinelearning/tree/master/docs/release-notes).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15ba5-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="15ba5-110">Prerequisites</span></span>

- <span data-ttu-id="15ba5-111">已安裝「.NET Core 跨平台開發」工作負載的 [Visual Studio 2017 15.6 或更新版本](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。</span><span class="sxs-lookup"><span data-stu-id="15ba5-111">[Visual Studio 2017 15.6 or later](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) with the ".NET Core cross-platform development" workload installed.</span></span>
- <span data-ttu-id="15ba5-112">PowerShell。</span><span class="sxs-lookup"><span data-stu-id="15ba5-112">Powershell.</span></span>
- <span data-ttu-id="15ba5-113">預先定型的模型。</span><span class="sxs-lookup"><span data-stu-id="15ba5-113">Pre-trained model.</span></span>
    - <span data-ttu-id="15ba5-114">使用 [ ML.NET 情感分析教學課程](../tutorials/sentiment-analysis.md)建置您自己的模型。</span><span class="sxs-lookup"><span data-stu-id="15ba5-114">Use the [ML.NET Sentiment Analysis tutorial](../tutorials/sentiment-analysis.md) to build your own model.</span></span>
    - <span data-ttu-id="15ba5-115">下載此[預先定型的情感分析機器學習模型](https://github.com/dotnet/samples/blob/master/machine-learning/models/sentimentanalysis/sentiment_model.zip)</span><span class="sxs-lookup"><span data-stu-id="15ba5-115">Download this [pre-trained sentiment analysis machine learning model](https://github.com/dotnet/samples/blob/master/machine-learning/models/sentimentanalysis/sentiment_model.zip)</span></span>

## <a name="create-aspnet-core-web-api-project"></a><span data-ttu-id="15ba5-116">建立 ASP.NET Core Web API 專案</span><span class="sxs-lookup"><span data-stu-id="15ba5-116">Create ASP.NET Core Web API Project</span></span>

1. <span data-ttu-id="15ba5-117">開啟 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="15ba5-117">Open Visual Studio 2017.</span></span> <span data-ttu-id="15ba5-118">從功能表列中選取 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="15ba5-118">Select **File > New > Project** from the menu bar.</span></span> <span data-ttu-id="15ba5-119">在 [新增專案] 對話方塊中，選取 [Visual C#] 節點，然後選取 [Web] 節點。</span><span class="sxs-lookup"><span data-stu-id="15ba5-119">In the New Project dialog, select the **Visual C#** node followed by the **Web** node.</span></span> <span data-ttu-id="15ba5-120">然後，選取 [ASP.NET Core Web 應用程式] 專案範本。</span><span class="sxs-lookup"><span data-stu-id="15ba5-120">Then select the **ASP.NET Core Web Application** project template.</span></span> <span data-ttu-id="15ba5-121">在 [名稱] 文字方塊中，輸入 "SentimentAnalysisWebAPI"，然後選取 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="15ba5-121">In the **Name** text box, type "SentimentAnalysisWebAPI" and then select the **OK** button.</span></span>
1. <span data-ttu-id="15ba5-122">在顯示不同類型的 ASP.NET Core 專案的視窗中，選取 [API]，然後選取 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="15ba5-122">In the window that displays the different types of ASP.NET Core Projects, select **API** and the select the **OK** button.</span></span>
1. <span data-ttu-id="15ba5-123">在專案中建立名為 *MLModels* 的目錄，以儲存您預先建置的機器學習模型檔案：</span><span class="sxs-lookup"><span data-stu-id="15ba5-123">Create a directory named *MLModels* in your project to save your pre-built machine learning model files:</span></span>

    <span data-ttu-id="15ba5-124">在 [方案總管] 中，以滑鼠右鍵按一下您的專案，然後選取 [新增] > [新增資料夾]。</span><span class="sxs-lookup"><span data-stu-id="15ba5-124">In Solution Explorer, right-click on your project and select Add > New Folder.</span></span> <span data-ttu-id="15ba5-125">輸入 "MLModels"，然後按 Enter。</span><span class="sxs-lookup"><span data-stu-id="15ba5-125">Type "MLModels" and hit Enter.</span></span>

1. <span data-ttu-id="15ba5-126">安裝「Microsoft.ML NuGet 套件」：</span><span class="sxs-lookup"><span data-stu-id="15ba5-126">Install the **Microsoft.ML NuGet Package**:</span></span>

    <span data-ttu-id="15ba5-127">在 [方案總管] 中，於您的專案上按一下滑鼠右鍵，然後選取 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="15ba5-127">In Solution Explorer, right-click on your project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="15ba5-128">選擇 "nuget.org" 作為 [套件來源]、選取 [瀏覽] 索引標籤、搜尋 **Microsoft.ML**、從清單中選取該套件，然後選取 [安裝] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="15ba5-128">Choose "nuget.org" as the Package source, select the Browse tab, search for **Microsoft.ML**, select that package in the list, and select the Install button.</span></span> <span data-ttu-id="15ba5-129">在 [預覽變更] 對話方塊上，選取 [確定] 按鈕，然後在 [授權接受] 對話方塊上，如果您同意所列套件的授權條款，請選取 [我接受]。</span><span class="sxs-lookup"><span data-stu-id="15ba5-129">Select the **OK** button on the **Preview Changes** dialog and then select the **I Accept** button on the License Acceptance dialog if you agree with the license terms for the packages listed.</span></span>

### <a name="add-model-to-aspnet-core-web-api-project"></a><span data-ttu-id="15ba5-130">將模型新增至 ASP.NET Core Web API 專案</span><span class="sxs-lookup"><span data-stu-id="15ba5-130">Add Model to ASP.NET Core Web API Project</span></span>

1. <span data-ttu-id="15ba5-131">將預先建置的模型複製到 *MLModels* 目錄</span><span class="sxs-lookup"><span data-stu-id="15ba5-131">Copy your pre-built model to the *MLModels* directory</span></span>
1. <span data-ttu-id="15ba5-132">在 [方案總管] 中，以滑鼠右鍵按一下模型 zip 檔案，並選取 [內容]。</span><span class="sxs-lookup"><span data-stu-id="15ba5-132">In Solution Explorer, right-click the model zip file and select Properties.</span></span> <span data-ttu-id="15ba5-133">在 [進階] 下，將 [複製到輸出目錄] 的值變更為 [有更新才複製]。</span><span class="sxs-lookup"><span data-stu-id="15ba5-133">Under Advanced, change the value of Copy to Output Directory to Copy if newer.</span></span>

## <a name="build-data-models"></a><span data-ttu-id="15ba5-134">建置資料模型</span><span class="sxs-lookup"><span data-stu-id="15ba5-134">Build Data Models</span></span>

<span data-ttu-id="15ba5-135">您必須為輸入資料和預測建立一些類別。</span><span class="sxs-lookup"><span data-stu-id="15ba5-135">You need to create some classes for your input data and predictions.</span></span> <span data-ttu-id="15ba5-136">將新類別新增至專案：</span><span class="sxs-lookup"><span data-stu-id="15ba5-136">Add a new class to your project:</span></span>

1. <span data-ttu-id="15ba5-137">在您的專案中建立名為 *DataModels* 的目錄以儲存資料模型：</span><span class="sxs-lookup"><span data-stu-id="15ba5-137">Create a directory named *DataModels* in your project to save your data models:</span></span>

    <span data-ttu-id="15ba5-138">在 [方案總管] 中，以滑鼠右鍵按一下您的專案，然後選取 [新增] > [新增資料夾]。</span><span class="sxs-lookup"><span data-stu-id="15ba5-138">In Solution Explorer, right-click on your project and select Add > New Folder.</span></span> <span data-ttu-id="15ba5-139">輸入 "DataModels"，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="15ba5-139">Type "DataModels" and hit **Enter**.</span></span>

2. <span data-ttu-id="15ba5-140">在 [方案總管] 中，以滑鼠右鍵按一下 *DataModels* 目錄，然後選取 [新增] > [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="15ba5-140">In Solution Explorer, right-click the *DataModels* directory, and then select Add > New Item.</span></span>
3. <span data-ttu-id="15ba5-141">在 [新增項目] 對話方塊中，選取 [類別]，然後將 [名稱] 欄位變更為 *SentimentData.cs*。</span><span class="sxs-lookup"><span data-stu-id="15ba5-141">In the **Add New Item** dialog box, select **Class** and change the **Name** field to *SentimentData.cs*.</span></span> <span data-ttu-id="15ba5-142">接著，選取 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="15ba5-142">Then, select the **Add** button.</span></span> <span data-ttu-id="15ba5-143">*SentimentData.cs* 檔案隨即在程式碼編輯器中開啟。</span><span class="sxs-lookup"><span data-stu-id="15ba5-143">The *SentimentData.cs* file opens in the code editor.</span></span> <span data-ttu-id="15ba5-144">將下列 using 陳述式新增至 *SentimentData.cs* 頂端：</span><span class="sxs-lookup"><span data-stu-id="15ba5-144">Add the following using statement to the top of *SentimentData.cs*:</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.ML.Data;
```

<span data-ttu-id="15ba5-145">移除現有的類別定義，然後將下列程式碼新增至 **SentimentData.cs** 檔案：</span><span class="sxs-lookup"><span data-stu-id="15ba5-145">Remove the existing class definition and add the following code to the **SentimentData.cs** file:</span></span>

```csharp
public class SentimentData
{
    [LoadColumn(0)]
    public bool Label { get; set; }
    [LoadColumn(1)]
    public string Text { get; set; }   
}
```

4. <span data-ttu-id="15ba5-146">在 [方案總管] 中，以滑鼠右鍵按一下 *DataModels* 目錄，然後選取 [新增] > [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="15ba5-146">In Solution Explorer, right-click the *DataModels* directory, and then select **Add > New Item**.</span></span>
5. <span data-ttu-id="15ba5-147">在 [加入新項目] 對話方塊中，選取 [類別]，然後將 [名稱] 欄位變更為 *SentimentPrediction.cs*。</span><span class="sxs-lookup"><span data-stu-id="15ba5-147">In the **Add New Item** dialog box, select **Class** and change the **Name** field to *SentimentPrediction.cs*.</span></span> <span data-ttu-id="15ba5-148">接著，選取 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="15ba5-148">Then, select the Add button.</span></span> <span data-ttu-id="15ba5-149">*SentimentPrediction.cs* 檔案隨即在程式碼編輯器中開啟。</span><span class="sxs-lookup"><span data-stu-id="15ba5-149">The *SentimentPrediction.cs* file opens in the code editor.</span></span> <span data-ttu-id="15ba5-150">將下列 using 陳述式新增至 *SentimentPrediction.cs* 頂端：</span><span class="sxs-lookup"><span data-stu-id="15ba5-150">Add the following using statement to the top of *SentimentPrediction.cs*:</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.ML.Data;
```

<span data-ttu-id="15ba5-151">移除現有的類別定義，然後將下列程式碼新增至 *SentimentPrediction.cs* 檔案：</span><span class="sxs-lookup"><span data-stu-id="15ba5-151">Remove the existing class definition and add the following code to the *SentimentPrediction.cs* file:</span></span>

```csharp
public class SentimentPrediction
{
    [ColumnName("PredictedLabel")]
    public bool Prediction { get; set; }
}
```

## <a name="register-predictionengine-for-use-in-application"></a><span data-ttu-id="15ba5-152">註冊 PredictionEngine 以便在應用程式中使用</span><span class="sxs-lookup"><span data-stu-id="15ba5-152">Register PredictionEngine for Use in Application</span></span>

<span data-ttu-id="15ba5-153">若要進行單一預測，您可以使用 `PredictionEngine`。</span><span class="sxs-lookup"><span data-stu-id="15ba5-153">To make a single prediction, you can use `PredictionEngine`.</span></span> <span data-ttu-id="15ba5-154">若要在您的應用程式中使用 `PredictionEngine`，必須在每次需要時建立。</span><span class="sxs-lookup"><span data-stu-id="15ba5-154">In order to use `PredictionEngine` in your application you will have to create it every time it is needed.</span></span> <span data-ttu-id="15ba5-155">在此情況下，要考慮的最佳做法是 ASP.NET Core 的相依性插入。</span><span class="sxs-lookup"><span data-stu-id="15ba5-155">In that case, a best practice to consider is ASP.NET Core dependency injection.</span></span>

<span data-ttu-id="15ba5-156">如果您想要深入了解[相依性插入](https://docs.microsoft.com/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-2.1)，下列連結提供詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="15ba5-156">The following link provides more information if you want to learn about [dependency injection](https://docs.microsoft.com/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-2.1).</span></span>

1. <span data-ttu-id="15ba5-157">開啟 *Startup.cs* 類別，並將下列 using 陳述式新增至檔案頂端：</span><span class="sxs-lookup"><span data-stu-id="15ba5-157">Open the *Startup.cs* class and add the following using statement to the top of the file:</span></span>

```csharp
using System.IO;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Hosting;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.ML;
using Microsoft.ML.Core.Data;
using SentimentAnalysisWebAPI.DataModels;
```

2. <span data-ttu-id="15ba5-158">將下列程式碼加入 *ConfigureServices* 類別：</span><span class="sxs-lookup"><span data-stu-id="15ba5-158">Add the following lines of code to the *ConfigureServices* method:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);

    services.AddScoped<MLContext>();
    services.AddScoped<PredictionEngine<SentimentData, SentimentPrediction>>((ctx) =>
    {
        MLContext mlContext = ctx.GetRequiredService<MLContext>();
        string modelFilePathName = "MLModels/sentiment_model.zip";

        //Load model from file
        ITransformer model;
        using (var stream = File.OpenRead(modelFilePathName))
        {
            model = mlContext.Model.Load(stream);
        }

        // Return prediction engine
        return model.CreatePredictionEngine<SentimentData, SentimentPrediction>(mlContext);
    });
}
```

> [!WARNING]
> <span data-ttu-id="15ba5-159">`PredictionEngine` 不是安全執行緒。</span><span class="sxs-lookup"><span data-stu-id="15ba5-159">`PredictionEngine` is not thread-safe.</span></span> <span data-ttu-id="15ba5-160">您可以用來限制建立物件成本的方式為使其服務存留期「具範圍」。</span><span class="sxs-lookup"><span data-stu-id="15ba5-160">A way that you can limit the cost of creating the object is by making its service lifetime *Scoped*.</span></span> <span data-ttu-id="15ba5-161">「具範圍」物件在要求內相同，但在不同的要求之間會不同。</span><span class="sxs-lookup"><span data-stu-id="15ba5-161">*Scoped* objects are the same within a request but different across requests.</span></span> <span data-ttu-id="15ba5-162">請前往下列連結以深入了解[服務存留期](/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-2.1#service-lifetimes)。</span><span class="sxs-lookup"><span data-stu-id="15ba5-162">Visit the following link to learn more about [service lifetimes](/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-2.1#service-lifetimes).</span></span>

<span data-ttu-id="15ba5-163">概括而言，此程式碼會在應用程式要求時自動初始化物件和服務，不必手動執行。</span><span class="sxs-lookup"><span data-stu-id="15ba5-163">At a high level, this code initializes the objects and services automatically when requested by the application instead of having to manually do it.</span></span>

## <a name="create-predict-controller"></a><span data-ttu-id="15ba5-164">建立預測控制器</span><span class="sxs-lookup"><span data-stu-id="15ba5-164">Create Predict Controller</span></span>

<span data-ttu-id="15ba5-165">若要處理傳入的 HTTP 要求，您需要建立一個控制器。</span><span class="sxs-lookup"><span data-stu-id="15ba5-165">To process your incoming HTTP requests, you need to create a controller.</span></span>

1. <span data-ttu-id="15ba5-166">在 [方案總管] 中，以滑鼠右鍵按一下 *Controllers* 目錄，然後選取 [新增] > [控制器]。</span><span class="sxs-lookup"><span data-stu-id="15ba5-166">In Solution Explorer, right-click the *Controllers* directory, and then select **Add > Controller**.</span></span>
1. <span data-ttu-id="15ba5-167">在 [加入新項目] 對話方塊中，選取 [API 控制器 - 空白]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="15ba5-167">In the **Add New Item** dialog box, select **API Controller Empty** and select **Add**.</span></span>
1. <span data-ttu-id="15ba5-168">在提示中，將 [控制器名稱] 欄位變更為 *PredictController.cs*。</span><span class="sxs-lookup"><span data-stu-id="15ba5-168">In the prompt change the **Controller Name** field to *PredictController.cs*.</span></span> <span data-ttu-id="15ba5-169">接著，選取 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="15ba5-169">Then, select the Add button.</span></span> <span data-ttu-id="15ba5-170">*PredictController.cs* 檔案隨即在程式碼編輯器中開啟。</span><span class="sxs-lookup"><span data-stu-id="15ba5-170">The *PredictController.cs* file opens in the code editor.</span></span> <span data-ttu-id="15ba5-171">將下列 using 陳述式新增至 *PredictController.cs* 頂端：</span><span class="sxs-lookup"><span data-stu-id="15ba5-171">Add the following using statement to the top of *PredictController.cs*:</span></span>

```csharp
using System;
using Microsoft.AspNetCore.Mvc;
using SentimentAnalysisWebAPI.DataModels;
using Microsoft.ML;
```

<span data-ttu-id="15ba5-172">移除現有的類別定義，然後將下列程式碼新增至 *PredictController.cs* 檔案：</span><span class="sxs-lookup"><span data-stu-id="15ba5-172">Remove the existing class definition and add the following code to the *PredictController.cs* file:</span></span>

```csharp
public class PredictController : ControllerBase
{
    
    private readonly PredictionEngine<SentimentData,SentimentPrediction> _predictionEngine;

    public PredictController(PredictionEngine<SentimentData, SentimentPrediction> predictionEngine)
    {
        _predictionEngine = predictionEngine; //Define prediction engine
    }

    [HttpPost]
    public ActionResult<string> Post([FromBody]SentimentData input)
    {
        if(!ModelState.IsValid)
        {
            return BadRequest();
        }

        // Make a prediction
        SentimentPrediction prediction = _predictionEngine.Predict(input);

        //If prediction is true then it is toxic. If it is false, the it is not.
        string isToxic = Convert.ToBoolean(prediction.Prediction) ? "Toxic" : "Not Toxic";

        return Ok(isToxic);
    }
    
}
```

<span data-ttu-id="15ba5-173">這是透過將預測服務傳遞至控制器的建構函式 (透過相依性插入取得) 來指派 `PredictionEngine`。</span><span class="sxs-lookup"><span data-stu-id="15ba5-173">This is assigning the `PredictionEngine` by passing it to the controller's constructor which you get via dependency injection.</span></span> <span data-ttu-id="15ba5-174">然後，在此控制器的 POST 方法中，`PredictionEngine` 會用來進行預測，並在成功時將結果傳回給使用者。</span><span class="sxs-lookup"><span data-stu-id="15ba5-174">Then, in the POST method of this controller the `PredictionEngine` is being used to make predictions and return the results back to the user if successful.</span></span>

## <a name="test-web-api-locally"></a><span data-ttu-id="15ba5-175">在本機測試 Web API</span><span class="sxs-lookup"><span data-stu-id="15ba5-175">Test Web API Locally</span></span>

<span data-ttu-id="15ba5-176">一切都設定好後，就可以開始測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="15ba5-176">Once everything is set up, it's time to test the application.</span></span>

1. <span data-ttu-id="15ba5-177">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="15ba5-177">Run the application.</span></span>
1. <span data-ttu-id="15ba5-178">開啟 Powershell 並輸入下列程式碼，其中 PORT 是應用程式正在接聽的連接埠。</span><span class="sxs-lookup"><span data-stu-id="15ba5-178">Open Powershell and enter the following code where PORT is the port your application is listening on.</span></span>

```powershell
Invoke-RestMethod "https://localhost:<PORT>/api/predict" -Method Post -Body (@{Text="This is a very rude movie"} | ConvertTo-Json) -ContentType "application/json"
```

<span data-ttu-id="15ba5-179">如果成功，輸出看起來應該類似下列文字：</span><span class="sxs-lookup"><span data-stu-id="15ba5-179">If successful, the output should look similar to the text below:</span></span>

```powershell
Toxic
```

<span data-ttu-id="15ba5-180">恭喜您！</span><span class="sxs-lookup"><span data-stu-id="15ba5-180">Congratulations!</span></span> <span data-ttu-id="15ba5-181">您已成功提供您的模型，以使用 ASP.NET Core API 在網際網路上進行預測。</span><span class="sxs-lookup"><span data-stu-id="15ba5-181">You have successfully served your model to make predictions over the internet using an ASP.NET Core API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15ba5-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="15ba5-182">Next Steps</span></span>

- [<span data-ttu-id="15ba5-183">部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="15ba5-183">Deploy to Azure</span></span>](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs?view=aspnetcore-2.1#deploy-the-app-to-azure)