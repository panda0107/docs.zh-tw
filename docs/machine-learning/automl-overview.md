---
title: ML.NET 的自動化機器學習
description: 自動模型選取和定型概觀
author: natke
ms.date: 05/01/2019
ms.topic: overview
ms.custom: mvc
ms.author: nakersha
ms.openlocfilehash: e6654718f174c9d8b628b05d85d74952c222eb66
ms.sourcegitcommit: 4c10802ad003374641a2c2373b8a92e3c88babc8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2019
ms.locfileid: "65452716"
---
# <a name="automated-machine-learning-with-mlnet"></a><span data-ttu-id="574ef-103">ML.NET 的自動化機器學習</span><span class="sxs-lookup"><span data-stu-id="574ef-103">Automated machine learning with ML.NET</span></span>

<span data-ttu-id="574ef-104">自動化機器學習是 ML.NET 的一項功能，可執行自動模型選取和定型。</span><span class="sxs-lookup"><span data-stu-id="574ef-104">Automated machine learning is a feature of ML.NET that performs automatic model selection and training.</span></span> <span data-ttu-id="574ef-105">您可以指定機器學習工作並提供資料集，而自動化 ML 會選擇具有最佳計量的模型。</span><span class="sxs-lookup"><span data-stu-id="574ef-105">You specify the machine learning task and supply a dataset, and automated ML chooses the model with the best metrics.</span></span> <span data-ttu-id="574ef-106">它會輸出：</span><span class="sxs-lookup"><span data-stu-id="574ef-106">It outputs:</span></span>
- <span data-ttu-id="574ef-107">可載入預測應用程式的模型檔案</span><span class="sxs-lookup"><span data-stu-id="574ef-107">a model file that can be loaded into your prediction application</span></span>
- <span data-ttu-id="574ef-108">進行預測的應用程式程式碼</span><span class="sxs-lookup"><span data-stu-id="574ef-108">application code to make predictions</span></span>
- <span data-ttu-id="574ef-109">用於特徵選取和模型定型 (以了解模型) 的原始程式碼</span><span class="sxs-lookup"><span data-stu-id="574ef-109">the source code used for feature selection and model training (to understand the model)</span></span>

> [!NOTE]
> <span data-ttu-id="574ef-110">這項功能目前處於預覽狀態，資料可能會有變更。</span><span class="sxs-lookup"><span data-stu-id="574ef-110">This feature is currently in Preview, and material may be subject to change.</span></span> 

<span data-ttu-id="574ef-111">自動化 ML 目前僅限於二元分類、多元分類和迴歸的機器學習[工作](resources/tasks.md)。</span><span class="sxs-lookup"><span data-stu-id="574ef-111">Automated ML is currently limited to the machine learning [tasks](resources/tasks.md) of binary classification, multiclass classification, and regression.</span></span> <span data-ttu-id="574ef-112">未來版本將支援其他機器學習工作。</span><span class="sxs-lookup"><span data-stu-id="574ef-112">The other machine learning tasks will be supported in future releases.</span></span>

<span data-ttu-id="574ef-113">使用自動化 ML 的方法三種：</span><span class="sxs-lookup"><span data-stu-id="574ef-113">There are three ways to use automated ML:</span></span>
1. <span data-ttu-id="574ef-114">在命令列上，使用 [ML.NET CLI](automate-training-with-cli.md)</span><span class="sxs-lookup"><span data-stu-id="574ef-114">On the command line, with the [ML.NET CLI](automate-training-with-cli.md)</span></span>
1. <span data-ttu-id="574ef-115">透過應用程式，使用[自動化 ML API](how-to-guides/how-to-use-the-automl-api.md)</span><span class="sxs-lookup"><span data-stu-id="574ef-115">Via an application, with the [automated ML API](how-to-guides/how-to-use-the-automl-api.md)</span></span>
1. <span data-ttu-id="574ef-116">透過圖形化使用者介面，使用 ML.NET 模型產生器</span><span class="sxs-lookup"><span data-stu-id="574ef-116">With a graphical user interface, with the the ML.NET Model Builder</span></span>