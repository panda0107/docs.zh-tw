---
title: C# 8.0 的新功能 - C# 指南
description: 大致了解 C# 8.0 中可用的新功能。 此文章為適用於預覽 2 的最新資訊。
ms.date: 02/12/2019
ms.openlocfilehash: 1aa5a200f84b35fda3c33a900655249d07000e8e
ms.sourcegitcommit: bd28ff1e312eaba9718c4f7ea272c2d4781a7cac
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/26/2019
ms.locfileid: "56835430"
---
# <a name="whats-new-in-c-80"></a><span data-ttu-id="5bbd8-104">C# 8.0 的新功能</span><span class="sxs-lookup"><span data-stu-id="5bbd8-104">What's new in C# 8.0</span></span>

<span data-ttu-id="5bbd8-105">有許多 C# 語言的增強功能，您已經可透過預覽 2 來試用。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-105">There are many enhancements to the C# language that you can try out already with preview 2.</span></span> <span data-ttu-id="5bbd8-106">在預覽 2 中新增的功能為：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-106">The new features added in preview 2 are:</span></span>

- <span data-ttu-id="5bbd8-107">[模式比對增強功能](#more-patterns-in-more-places)：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-107">[Pattern matching enhancements](#more-patterns-in-more-places):</span></span>
  * [<span data-ttu-id="5bbd8-108">Switch 運算式</span><span class="sxs-lookup"><span data-stu-id="5bbd8-108">Switch expressions</span></span>](#switch-expressions)
  * [<span data-ttu-id="5bbd8-109">屬性模式</span><span class="sxs-lookup"><span data-stu-id="5bbd8-109">Property patterns</span></span>](#property-patterns)
  * [<span data-ttu-id="5bbd8-110">Tuple 模式</span><span class="sxs-lookup"><span data-stu-id="5bbd8-110">Tuple patterns</span></span>](#tuple-patterns)
  * [<span data-ttu-id="5bbd8-111">位置模式</span><span class="sxs-lookup"><span data-stu-id="5bbd8-111">Positional patterns</span></span>](#positional-patterns)
- [<span data-ttu-id="5bbd8-112">Using 宣告</span><span class="sxs-lookup"><span data-stu-id="5bbd8-112">Using declarations</span></span>](#using-declarations)
- [<span data-ttu-id="5bbd8-113">靜態區域函式</span><span class="sxs-lookup"><span data-stu-id="5bbd8-113">Static local functions</span></span>](#static-local-functions)
- [<span data-ttu-id="5bbd8-114">可處置的 ref struct</span><span class="sxs-lookup"><span data-stu-id="5bbd8-114">Disposable ref structs</span></span>](#disposable-ref-structs)

<span data-ttu-id="5bbd8-115">下列語言功能首次出現於 C# 8.0 預覽 1 中：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-115">The following language features first appeared in C# 8.0 preview 1:</span></span>

- [<span data-ttu-id="5bbd8-116">可為 Null 的參考類型</span><span class="sxs-lookup"><span data-stu-id="5bbd8-116">Nullable reference types</span></span>](#nullable-reference-types)
- [<span data-ttu-id="5bbd8-117">非同步資料流</span><span class="sxs-lookup"><span data-stu-id="5bbd8-117">Asynchronous streams</span></span>](#asynchronous-streams)
- [<span data-ttu-id="5bbd8-118">索引和範圍</span><span class="sxs-lookup"><span data-stu-id="5bbd8-118">Indices and ranges</span></span>](#indices-and-ranges)

> [!NOTE]
> <span data-ttu-id="5bbd8-119">此文章內容為 C# 8.0 預覽 2 的最新更新。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-119">This article was last updated for C# 8.0 preview 2.</span></span>

<span data-ttu-id="5bbd8-120">此文章的其餘部分會簡短說明這些功能。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-120">The remainder of this article briefly describes these features.</span></span> <span data-ttu-id="5bbd8-121">提供教學課程及概觀的連結，其中包含深入詳盡的文章。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-121">Where in-depth articles are available, links to those tutorials and overviews are provided.</span></span>

## <a name="more-patterns-in-more-places"></a><span data-ttu-id="5bbd8-122">在更多位置使用更多的模式</span><span class="sxs-lookup"><span data-stu-id="5bbd8-122">More patterns in more places</span></span>

<span data-ttu-id="5bbd8-123">**模式比對**讓您能夠使用提供相關但不同種類資料間圖形相依功能的工具。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-123">**Pattern matching** gives tools to provide shape-dependent functionality across related but different kinds of data.</span></span> <span data-ttu-id="5bbd8-124">C# 7.0 透過使用 [`is`](../language-reference/keywords/is.md) 運算式及 [`switch`](../language-reference/keywords/switch.md) 陳述式，推出了類型模式及常數模式的語法。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-124">C# 7.0 introduced syntax for type patterns and constant patterns by using the [`is`](../language-reference/keywords/is.md) expression and the [`switch`](../language-reference/keywords/switch.md) statement.</span></span> <span data-ttu-id="5bbd8-125">這些功能代表達成支援程式設計範例 (資料及功能分開) 的暫訂步驟。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-125">These features represented the first tentative steps toward supporting programming paradigms where data and functionality live apart.</span></span> <span data-ttu-id="5bbd8-126">隨著業界趨勢轉向微服務及其他雲端式架構，也產生其他語言工具的需求。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-126">As the industry moves toward more microservices and other cloud-based architectures, other language tools are needed.</span></span>

<span data-ttu-id="5bbd8-127">C# 8.0 可展開此詞彙，讓您能夠在程式碼中的更多位置，使用更多的模式運算式。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-127">C# 8.0 expands this vocabulary so you can use more pattern expressions in more places in your code.</span></span> <span data-ttu-id="5bbd8-128">當您的資料與功能分開時，請考慮使用這些功能。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-128">Consider these features when your data and functionality are separate.</span></span> <span data-ttu-id="5bbd8-129">當您的演算法取決於物件執行階段類型外的事實時，請考慮使用模式比對。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-129">Consider pattern matching when your algorithms depend on a fact other than the runtime type of an object.</span></span> <span data-ttu-id="5bbd8-130">這些技術提供表達設計的另一種方式。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-130">These techniques provide another way to express designs.</span></span>

<span data-ttu-id="5bbd8-131">除了在新位置的新模式之外，C# 8.0 還新增了**遞迴模式**。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-131">In addition to new patterns in new places, C# 8.0 adds **recursive patterns**.</span></span> <span data-ttu-id="5bbd8-132">任何模式運算式的結果皆是運算式。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-132">The result of any pattern expression is an expression.</span></span> <span data-ttu-id="5bbd8-133">遞迴模式僅為套用到其他模式運算式輸出的模式運算式。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-133">A recursive pattern is simply a pattern expression applied to the output of another pattern expression.</span></span>

### <a name="switch-expressions"></a><span data-ttu-id="5bbd8-134">switch 運算式</span><span class="sxs-lookup"><span data-stu-id="5bbd8-134">switch expressions</span></span>

<span data-ttu-id="5bbd8-135">通常，[`switch`](../language-reference/keywords/switch.md) 陳述式會在其各個 `case` 區塊中產生值。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-135">Often, a [`switch`](../language-reference/keywords/switch.md) statement produces a value in each of its `case` blocks.</span></span> <span data-ttu-id="5bbd8-136">**Switch 運算式**讓您能夠使用更精簡的運算式語法。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-136">**Switch expressions** enable you to use more concise expression syntax.</span></span> <span data-ttu-id="5bbd8-137">重複的 `case` 及 `break` 關鍵字和大括號都減少了。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-137">There are fewer repetitive `case` and `break` keywords, and fewer curly braces.</span></span>  <span data-ttu-id="5bbd8-138">例如，請考慮以下列出彩虹色彩的列舉：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-138">As an example, consider the following enum that lists the colors of the rainbow:</span></span>

```csharp
public enum Rainbow
{
    Red,
    Orange,
    Yellow,
    Blue,
    Indigo,
    Violet
}
```

<span data-ttu-id="5bbd8-139">您可使用以下包含 switch 運算式的方法，將 `Rainbow` 值轉換為其 RGB 值：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-139">You could convert a `Rainbow` value to its RGB values using the following method containing a switch expression:</span></span>

```csharp
public static RGBColor FromRainbow(Rainbow colorBand) =>
    colorBand switch
    {
        Rainbow.Red    => new RGBColor(0xFF, 0x00, 0x00),
        Rainbow.Orange => new RGBColor(0xFF, 0x7F, 0x00),
        Rainbow.Yellow => new RGBColor(0xFF, 0xFF, 0x00),
        Rainbow.Blue   => new RGBColor(0x00, 0x00, 0xFF),
        Rainbow.Indigo => new RGBColor(0x4B, 0x00, 0x82),
        Rainbow.Violet => new RGBColor(0x94, 0x00, 0xD3),
        _              => throw new ArgumentException(message: "invalid enum value", paramName: nameof(colorBand)),
    };
```

<span data-ttu-id="5bbd8-140">幾項語法改進如下：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-140">There are several syntax improvements here:</span></span>

- <span data-ttu-id="5bbd8-141">變數挪到了 `switch` 關鍵字前。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-141">The variable comes before the `switch` keyword.</span></span> <span data-ttu-id="5bbd8-142">不同的順序讓您可輕鬆區分出 switch 運算式及 switch 陳述式。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-142">The different order makes it visually easy to distinguish the switch expression from the switch statement.</span></span>
- <span data-ttu-id="5bbd8-143">`case` 及 `:` 元素取代為 `=>`。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-143">The `case` and `:` elements are replaced with `=>`.</span></span> <span data-ttu-id="5bbd8-144">這更加精簡而且符合直覺。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-144">It's more concise and intuitive.</span></span>
- <span data-ttu-id="5bbd8-145">`default` 案例取代為 `_` 捨棄。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-145">The `default` case is replaced with a `_` discard.</span></span>
- <span data-ttu-id="5bbd8-146">主體為運算式，而非陳述式。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-146">The bodies are expressions, not statements.</span></span>

<span data-ttu-id="5bbd8-147">對比該語法與使用傳統 `switch` 陳述式的對等程式碼：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-147">Contrast that with the equivalent code using the classic `switch` statement:</span></span>

```csharp
public static RGBColor fromRainbowClassic(Rainbow colorBand)
{
    switch (colorBand)
    {
        case Rainbow.Red:
            return new RGBColor(0xFF, 0x00, 0x00);
        case Rainbow.Orange:
            return new RGBColor(0xFF, 0x7F, 0x00);
        case Rainbow.Yellow:
            return new RGBColor(0xFF, 0xFF, 0x00);
        case Rainbow.Blue:
            return new RGBColor(0x00, 0x00, 0xFF);
        case Rainbow.Indigo:
            return new RGBColor(0x4B, 0x00, 0x82);
        case Rainbow.Violet:
            return new RGBColor(0x94, 0x00, 0xD3);
        default:
            throw new ArgumentException(message: "invalid enum value", paramName: nameof(colorBand));
    };
}
```

### <a name="property-patterns"></a><span data-ttu-id="5bbd8-148">屬性模式</span><span class="sxs-lookup"><span data-stu-id="5bbd8-148">Property patterns</span></span>

<span data-ttu-id="5bbd8-149">**屬性模式**使您得以比對所檢查物件的屬性。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-149">The **property pattern** enables you to match on properties of the object examined.</span></span> <span data-ttu-id="5bbd8-150">試想必須根據購買者地址計算營業稅的電子商務網站。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-150">Consider an eCommerce site that must compute sales tax based on the buyer's address.</span></span> <span data-ttu-id="5bbd8-151">`Address` 類別的核心功能並非負責進行該計算。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-151">That computation is not a core responsibility of an `Address` class.</span></span> <span data-ttu-id="5bbd8-152">這項計算會隨著時間變更，而且可能比地址格式的變更更加頻繁。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-152">It will change over time, likely more often than address format changes.</span></span> <span data-ttu-id="5bbd8-153">營業稅額取決於地址的 `State` 屬性。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-153">The amount of sales tax depends on the `State` property of the address.</span></span> <span data-ttu-id="5bbd8-154">下列方法會使用屬性模式，從地址及價格計算營業稅：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-154">The following method uses the property pattern to compute the sales tax from the address and the price:</span></span>

```csharp
public static decimal ComputeSalesTax(Address location, decimal salePrice) =>
    location switch
    {
        { State: "WA" } => salePrice * 0.06M,
        { State: "MN" } => salePrice * 0.75M,
        { State: "MI" } => salePrice * 0.05M,
        // other cases removed for brevity...
        _ => 0M
    };
```

<span data-ttu-id="5bbd8-155">模式比對會建立簡潔的語法以表示此演算法。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-155">Pattern matching creates a concise syntax for expressing this algorithm.</span></span>

### <a name="tuple-patterns"></a><span data-ttu-id="5bbd8-156">Tuple 模式</span><span class="sxs-lookup"><span data-stu-id="5bbd8-156">Tuple patterns</span></span>

<span data-ttu-id="5bbd8-157">某些演算法需仰賴數個輸入。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-157">Some algorithms depend on multiple inputs.</span></span> <span data-ttu-id="5bbd8-158">**Tuple 模式**可讓您根據以 [tuple](../tuples.md) 形式表示的多個值進行切換。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-158">**Tuple patterns** allow you to switch based on multiple values expressed as a [tuple](../tuples.md).</span></span>  <span data-ttu-id="5bbd8-159">下列範例示範「剪刀、石頭、布」遊戲的 switch 運算式：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-159">The following code shows a switch expression for the game *rock, paper, scissors*:</span></span>

```csharp
public static string RockPaperScissors(string first, string second)
    => (first, second) switch
    {
        ("rock", "paper") => "rock is covered by paper. Paper wins.",
        ("rock", "scissors") => "rock breaks scissors. Rock wins.",
        ("paper", "rock") => "paper covers rock. Paper wins.",
        ("paper", "scissors") => "paper is cut by scissors. Scissors wins.",
        ("scissors", "rock") => "scissors is broken by rock. Rock wins.",
        ("scissors", "paper") => "scissors cuts paper. Scissors wins.",
        (_, _) => "tie"
    };
```

<span data-ttu-id="5bbd8-160">訊息會指出優勝者。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-160">The messages indicate the winner.</span></span> <span data-ttu-id="5bbd8-161">捨棄案例代表平手的三個組合，或其他文字輸入。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-161">The discard case represents the three combinations for ties, or other text inputs.</span></span>

### <a name="positional-patterns"></a><span data-ttu-id="5bbd8-162">位置模式</span><span class="sxs-lookup"><span data-stu-id="5bbd8-162">Positional patterns</span></span>

<span data-ttu-id="5bbd8-163">某些類型會包含 `Deconstruct` 方法，其能將自己的屬性解構成離散變數。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-163">Some types include a `Deconstruct` method that deconstructs its properties into discrete variables.</span></span> <span data-ttu-id="5bbd8-164">可存取 `Deconstruct` 方法時，您可以使用**位置模式**來檢查物件的屬性，然後將那些屬性用於某個模式。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-164">When a `Deconstruct` method is accessible, you can use **positional patterns** to inspect properties of the object and use those properties for a pattern.</span></span>  <span data-ttu-id="5bbd8-165">請考慮下列 `Point` 類別，其包含 `Deconstruct` 方法來針對 `X` 和 `Y` 建立離散變數：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-165">Consider the following `Point` class that includes a `Deconstruct` method to create discrete variables for `X` and `Y`:</span></span>

```csharp
public class Point
{
    public int X { get; }
    public int Y { get; }

    public Point(int x, int y) => (X, Y) = (x, y);

    public void Deconstruct(out int x, out int y) =>
        (x, y) = (X, Y);
}
```

<span data-ttu-id="5bbd8-166">下列方法會使用**位置模式**擷取 `x` 及 `y` 的值。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-166">The following method uses the **positional pattern** to extract the values of `x` and `y`.</span></span> <span data-ttu-id="5bbd8-167">接著，其使用 `when` 子句判斷點的象限：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-167">Then, it uses a `when` clause to determine the quadrant of the point:</span></span>

```csharp
static string Quadrant(Point p) => p switch
{
    (0, 0) => "origin",
    (var x, var y) when x > 0 && y > 0 => "Quadrant 1",
    (var x, var y) when x < 0 && y > 0 => "Quadrant 2",
    (var x, var y) when x < 0 && y < 0 => "Quadrant 3",
    (var x, var y) when x > 0 && y < 0 => "Quadrant 4",
    (var x, var y) => "on a border",
    _ => "unknown"
};
```

<span data-ttu-id="5bbd8-168">當 `x` 或 `y` (非兩者) 為 0 時，上述 switch 中的捨棄模式就會符合。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-168">The discard pattern in the preceding switch matches when either `x` or `y`, but not both, is 0.</span></span> <span data-ttu-id="5bbd8-169">switch 運算式必須產生值或者擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-169">A switch expression must either produce a value or throw an exception.</span></span> <span data-ttu-id="5bbd8-170">若沒有任何案例符合，則 switch 運算式會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-170">If none of the cases match, the switch expression throws an exception.</span></span> <span data-ttu-id="5bbd8-171">若您未在 switch 運算式中涵蓋所有可能的案例，則編譯器會對您產生警告。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-171">The compiler generates a warning for you if you do not cover all possible cases in your switch expression.</span></span>

## <a name="using-declarations"></a><span data-ttu-id="5bbd8-172">using 宣告</span><span class="sxs-lookup"><span data-stu-id="5bbd8-172">using declarations</span></span>

<span data-ttu-id="5bbd8-173">**using 宣告**為以 `using` 關鍵字開頭的變數宣告。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-173">A **using declaration** is a variable declaration preceded by the `using` keyword.</span></span> <span data-ttu-id="5bbd8-174">其會告知編譯器，應在括住的範圍結尾處置所宣告的變數。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-174">It tells the compiler that the variable being declared should be disposed at the end of the enclosing scope.</span></span> <span data-ttu-id="5bbd8-175">例如，試想下列寫入文字檔的程式碼：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-175">For example, consider the following code that writes a text file:</span></span>

```csharp
static void WriteLinesToFile(IEnumerable<string> lines)
{
    using var file = new System.IO.StreamWriter("WriteLines2.txt");
    foreach (string line in lines)
    {
        // If the line doesn't contain the word 'Second', write the line to the file.
        if (!line.Contains("Second"))
        {
            file.WriteLine(line);
        }
    }
// file is disposed here
}
```

<span data-ttu-id="5bbd8-176">在上述範例中，到達方法的右大括號時，就會處置檔案。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-176">In the preceding example, the file is disposed when the closing brace for the method is reached.</span></span> <span data-ttu-id="5bbd8-177">這是宣告 `file` 之範圍的結尾。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-177">That's the end of the scope in which `file` is declared.</span></span> <span data-ttu-id="5bbd8-178">上述程式碼與下列使用傳統 [using 陳述式](../language-reference/keywords/using-statement.md)的程式碼相等：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-178">The preceding code is equivalent to the following code using the classic [using statements](../language-reference/keywords/using-statement.md) statement:</span></span>


```csharp
static void WriteLinesToFile(IEnumerable<string> lines)
{
    using (var file = new System.IO.StreamWriter("WriteLines2.txt"))
    {
        foreach (string line in lines)
        {
            // If the line doesn't contain the word 'Second', write the line to the file.
            if (!line.Contains("Second"))
            {
                file.WriteLine(line);
            }
        }
    } // file is disposed here
}
```

<span data-ttu-id="5bbd8-179">在上述範例中，到達與 `using` 陳述式相關的結尾右大括號時，就會處置檔案。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-179">In the preceding example, the file is disposed when the closing brace associated with the `using` statement is reached.</span></span>

<span data-ttu-id="5bbd8-180">在這兩個案例中，編譯器皆會產生對 `Dispose()` 的呼叫。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-180">In both cases, the compiler generates the call to `Dispose()`.</span></span> <span data-ttu-id="5bbd8-181">若無法處置 using 陳述式中的運算式，則編譯器會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-181">The compiler generates an error if the expression in the using statement is not disposable.</span></span>

## <a name="static-local-functions"></a><span data-ttu-id="5bbd8-182">靜態區域函式</span><span class="sxs-lookup"><span data-stu-id="5bbd8-182">Static local functions</span></span>

<span data-ttu-id="5bbd8-183">您現可將 `static` 修飾詞新增至區域函式，以確保區域函式不會從括住的範圍擷取 (參考) 任何變數。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-183">You can now add the `static` modifier to local functions to ensure that local function doesn't capture (reference) any variables from the enclosing scope.</span></span> <span data-ttu-id="5bbd8-184">這樣會產生 `CS8421`「靜態區域函式不可包含對 <variable> 的參考。」。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-184">Doing so generates `CS8421`, "A static local function can't contain a reference to <variable>."</span></span> 

<span data-ttu-id="5bbd8-185">請考慮下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-185">Consider the following code.</span></span> <span data-ttu-id="5bbd8-186">區域函式 `LocalFunction` 會存取在所括住範圍 (方法 `M`) 中宣告的變數 `y`。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-186">The local function `LocalFunction` accesses the variable `y`, declared in the enclosing scope (the method `M`).</span></span> <span data-ttu-id="5bbd8-187">因此，無法使用 `static` 修飾詞宣告 `LocalFunction`：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-187">Therefore, `LocalFunction` can't be declared with the `static` modifier:</span></span>

```csharp
int M()
{
    int y;
    LocalFunction();
    return y;

    void LocalFunction() => y = 0;
}
```

<span data-ttu-id="5bbd8-188">下列程式碼包含靜態區域函式。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-188">The following code contains a static local function.</span></span> <span data-ttu-id="5bbd8-189">因為其不會存取所括住範圍中的任何變數，所以可以為靜態：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-189">It can be static because it doesn't access any variables in the enclosing scope:</span></span>

```csharp
int M()
{
    int y = 5;
    int x = 7;
    return Add(x, y);

    static int Add(int left, int right) => left + right;
}
```

## <a name="disposable-ref-structs"></a><span data-ttu-id="5bbd8-190">可處置的 ref struct</span><span class="sxs-lookup"><span data-stu-id="5bbd8-190">Disposable ref structs</span></span>

<span data-ttu-id="5bbd8-191">使用 `ref` 修飾詞宣告的 `struct` 不會實作任何介面，故無法實作 <xref:System.IDisposable>。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-191">A `struct` declared with the `ref` modifier may not implement any interfaces and so cannot implement <xref:System.IDisposable>.</span></span> <span data-ttu-id="5bbd8-192">因此，若要讓 `ref struct` 可處置，其必須具有可存取的 `void Dispose()` 方法。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-192">Therefore, to enable a `ref struct` to be disposed, it must have an accessible `void Dispose()` method.</span></span> <span data-ttu-id="5bbd8-193">這也適用於 `readonly ref struct` 宣告。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-193">This also applies to `readonly ref struct` declarations.</span></span>

## <a name="nullable-reference-types"></a><span data-ttu-id="5bbd8-194">可為 Null 的參考型別</span><span class="sxs-lookup"><span data-stu-id="5bbd8-194">Nullable reference types</span></span>

<span data-ttu-id="5bbd8-195">在可為 Null 的註解內容中，參考型別的任何變數皆視為**不可為 Null 的參考型別**。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-195">Inside a nullable annotation context, any variable of a reference type is considered to be a **nonnullable reference type**.</span></span> <span data-ttu-id="5bbd8-196">若您要表示變數可能為 Null，則必須使用 `?` 來附加類型名稱，以將變數宣告為**可為 Null 的參考型別**。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-196">If you want to indicate that a variable may be null, you must append the type name with the `?` to declare the variable as a **nullable reference type**.</span></span>

<span data-ttu-id="5bbd8-197">對於不可為 Null 的參考型別，編譯器會使用流程分析來確保將區域變數在宣告時，初始化為非 Null 的值。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-197">For nonnullable reference types, the compiler uses flow analysis to ensure that local variables are initialized to a non-null value when declared.</span></span> <span data-ttu-id="5bbd8-198">必須在建構期間將欄位初始化。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-198">Fields must be initialized during construction.</span></span> <span data-ttu-id="5bbd8-199">若變數不是由對任何可用建構函式的呼叫，或是初始設定式所設定，則編譯器會產生警告。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-199">The compiler generates a warning if the variable is not set by a call to any of the available constructors or by an initializer.</span></span> <span data-ttu-id="5bbd8-200">此外，也不能對不可為 Null 的參考型別指派可為 Null 的值。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-200">Furthermore, nonnullable reference types can't be assigned a value that could be null.</span></span>

<span data-ttu-id="5bbd8-201">系統不會檢查可為 Null 的參考型別，來確保其不會指派或初始化為 Null。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-201">Nullable reference types aren't checked to ensure they aren't assigned or initialized to null.</span></span> <span data-ttu-id="5bbd8-202">不過，編譯器會在將變數存取或指派至不可為 Null 的參考型別之前，使用流程分析來確保已對可為 Null 參考型別的所有變數檢查可 Null 性。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-202">However, the compiler uses flow analysis to ensure that any variable of a nullable reference type is checked against null before it's accessed or assigned to a nonnullable reference type.</span></span>

<span data-ttu-id="5bbd8-203">您可在[可為 Null 的參考型別](../nullable-references.md)概觀中深入了解功能。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-203">You can learn more about the feature in the overview of [nullable reference types](../nullable-references.md).</span></span> <span data-ttu-id="5bbd8-204">在此[可為 Null 的參考型別教學課程](../tutorials/nullable-reference-types.md)中，親自在新的應用程式內試用。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-204">Try it yourself in a new application in this [nullable reference types tutorial](../tutorials/nullable-reference-types.md).</span></span> <span data-ttu-id="5bbd8-205">在[移轉應用程式以使用可為 Null 的參考型別教學課程](../tutorials/upgrade-to-nullable-references.md)中，了解移轉現有程式碼基底的步驟，進而利用可為 Null 的參考型別。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-205">Learn about the steps to migrate an existing codebase to make use of nullable reference types in the [migrating an application to use nullable reference types tutorial](../tutorials/upgrade-to-nullable-references.md).</span></span>

## <a name="asynchronous-streams"></a><span data-ttu-id="5bbd8-206">非同步資料流</span><span class="sxs-lookup"><span data-stu-id="5bbd8-206">Asynchronous streams</span></span>

<span data-ttu-id="5bbd8-207">自 C# 8.0 起，您可非同步地建立及取用資料流。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-207">Starting with C# 8.0, you can create and consume streams asynchronously.</span></span> <span data-ttu-id="5bbd8-208">傳回非同步資料流的方法具有三個屬性：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-208">A method that returns an asynchronous stream has three properties:</span></span>

1. <span data-ttu-id="5bbd8-209">使用 `async` 修飾詞來宣告。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-209">It was declared with the `async` modifier.</span></span>
1. <span data-ttu-id="5bbd8-210">其會傳回 <xref:System.Collections.Generic.IAsyncEnumerable%601>。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-210">It returns an <xref:System.Collections.Generic.IAsyncEnumerable%601>.</span></span>
1. <span data-ttu-id="5bbd8-211">方法會包含 `yield return` 陳述式以傳回非同步資料流中的後續元素。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-211">The method contains `yield return` statements to return successive elements in the asynchronous stream.</span></span>

<span data-ttu-id="5bbd8-212">當您列舉資料流的元素時，必須在 `foreach` 關鍵字前新增 `await` 關鍵字，才可取用非同步資料流。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-212">Consuming an asynchronous stream requires you to add the `await` keyword before the `foreach` keyword when you enumerate the elements of the stream.</span></span> <span data-ttu-id="5bbd8-213">需要方法才可新增 `await` 關鍵字，而且該方法列舉要使用 `async` 修飾詞宣告的非同步資料流，並傳回 `async` 方法允許的類型。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-213">Adding the `await` keyword requires the method that enumerates the asynchronous stream to be declared with the `async` modifier and to return a type allowed for an `async` method.</span></span> <span data-ttu-id="5bbd8-214">通常這代表傳回 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601>。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-214">Typically that means returning a <xref:System.Threading.Tasks.Task> or <xref:System.Threading.Tasks.Task%601>.</span></span> <span data-ttu-id="5bbd8-215">也可以是 <xref:System.Threading.Tasks.ValueTask> 或 <xref:System.Threading.Tasks.ValueTask%601>。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-215">It can also be a <xref:System.Threading.Tasks.ValueTask> or <xref:System.Threading.Tasks.ValueTask%601>.</span></span> <span data-ttu-id="5bbd8-216">方法可同時取用及產生非同步資料流，這代表其會傳回 <xref:System.Collections.Generic.IAsyncEnumerable%601>。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-216">A method can both consume and produce an asynchronous stream, which means it would return an <xref:System.Collections.Generic.IAsyncEnumerable%601>.</span></span> <span data-ttu-id="5bbd8-217">下列程式碼會產生 1 到 20 的序列，產生每個號碼需等待 100 毫秒的間隔：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-217">The following code generates a sequence from 1 to 20, waiting 100 ms between generating each number:</span></span>

```csharp
public static async System.Collections.Generic.IAsyncEnumerable<int> GenerateSequence()
{
    for (int i = 0; i < 20; i++)
    {
        await Task.Delay(100);
        yield return i;
    }
}
```

<span data-ttu-id="5bbd8-218">您應使用 `await foreach` 陳述式列舉序列：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-218">You would enumerate the sequence using the `await foreach` statement:</span></span>

```csharp
await foreach (var number in GenerateSequence())
{
    Console.WriteLine(number);
}
```

<span data-ttu-id="5bbd8-219">您可在我們有關[建立及取用非同步資料流](../tutorials/generate-consume-asynchronous-stream.md)的教學課程中，親自試用非同步資料流。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-219">You can try asynchronous streams yourself in our tutorial on [creating and consuming async streams](../tutorials/generate-consume-asynchronous-stream.md).</span></span>

## <a name="indices-and-ranges"></a><span data-ttu-id="5bbd8-220">索引和範圍</span><span class="sxs-lookup"><span data-stu-id="5bbd8-220">Indices and ranges</span></span>

<span data-ttu-id="5bbd8-221">範圍及索引可提供用來指定陣列中子範圍的簡潔語法，<xref:System.Span%601> 或 <xref:System.ReadOnlySpan%601>。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-221">Ranges and indices provide a succinct syntax for specifying subranges in an array, <xref:System.Span%601>, or <xref:System.ReadOnlySpan%601>.</span></span>

<span data-ttu-id="5bbd8-222">您可**從結尾**指定索引。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-222">You can specify an index **from the end**.</span></span> <span data-ttu-id="5bbd8-223">您可使用 `^` 運算子指定**從結尾**。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-223">You specify **from the end** using the `^` operator.</span></span> <span data-ttu-id="5bbd8-224">您已熟悉 `array[2]` 表示「從開頭起算 2 個」元素。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-224">You are familiar with `array[2]` meaning the element "2 from the start".</span></span> <span data-ttu-id="5bbd8-225">現在，`array[^2]` 表示「從結尾起算 2 個」元素。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-225">Now, `array[^2]` means the element "2 from the end".</span></span> <span data-ttu-id="5bbd8-226">索引 `^0` 表示「結尾」，或最後一個元素後接續的索引。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-226">The index `^0` means "the end", or the index that follows the last element.</span></span>

<span data-ttu-id="5bbd8-227">您可使用**範圍運算子**指定**範圍**：`..`。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-227">You can specify a **range** with the **range operator**: `..`.</span></span> <span data-ttu-id="5bbd8-228">例如，`0..^0` 會指定陣列的整個範圍：從開頭起算由 0 開始，從結尾起算則不包含 0。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-228">For example, `0..^0` specifies the entire range of the array: 0 from the start up to, but not including 0 from the end.</span></span> <span data-ttu-id="5bbd8-229">運算元各可以使用「從開頭」或「從結尾」。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-229">Either operand may use "from the start" or "from the end".</span></span> <span data-ttu-id="5bbd8-230">此外，也可省略各運算元。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-230">Furthermore, either operand may be omitted.</span></span> <span data-ttu-id="5bbd8-231">預設是開始索引為 `0`，結尾索引為 `^0`。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-231">The defaults are `0` for the start index, and `^0` for the end index.</span></span>

<span data-ttu-id="5bbd8-232">讓我們來看以下幾個範例。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-232">Let's look at a few examples.</span></span> <span data-ttu-id="5bbd8-233">試想下列使用其索引從開頭或從結尾標註的陣列：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-233">Consider the following array, annotated with its index from the start and from the end:</span></span>

```csharp
var words = new string[]
{
                // index from start    index from end
    "The",      // 0                   ^9
    "quick",    // 1                   ^8
    "brown",    // 2                   ^7
    "fox",      // 3                   ^6
    "jumped",   // 4                   ^5
    "over",     // 5                   ^4
    "the",      // 6                   ^3
    "lazy",     // 7                   ^2
    "dog"       // 8                   ^1
};
```

<span data-ttu-id="5bbd8-234">各元素的索引會強調「從開頭」及「從結尾」的概念，而且該範圍專屬於範圍的結尾。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-234">The index of each element reinforces the concept of "from the start", and "from the end", and that ranges are exclusive of the end of the range.</span></span> <span data-ttu-id="5bbd8-235">整個陣列的「開頭」是第一個元素。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-235">The "start" of the entire array is the first element.</span></span> <span data-ttu-id="5bbd8-236">整個陣列的「結尾」則「結束在」最後一個元素。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-236">The "end" of the entire array is *past* the last element.</span></span>

<span data-ttu-id="5bbd8-237">您可使用 `^1` 索引擷取最後一個字組：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-237">You can retrieve the last word with the `^1` index:</span></span>

```csharp
Console.WriteLine($"The last word is {words[^1]}");
// writes "dog"
```

<span data-ttu-id="5bbd8-238">下列程式碼會建立具有 "quick"、"brown" 和 "fox" 字組的子範圍。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-238">The following code creates a subrange with the words "quick", "brown", and "fox".</span></span> <span data-ttu-id="5bbd8-239">其會包含 `words[1]` 到 `words[3]`。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-239">It includes `words[1]` through `words[3]`.</span></span> <span data-ttu-id="5bbd8-240">元素 `words[4]` 則不在範圍內。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-240">The element `words[4]` is not in the range.</span></span>

```csharp
var brownFox = words[1..4];
```

<span data-ttu-id="5bbd8-241">下列程式碼會建立具有 "lazy" 和 "dog" 的子範圍。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-241">The following code creates a subrange with "lazy" and "dog".</span></span> <span data-ttu-id="5bbd8-242">其包含 `words[^2]` 及 `words[^1]`。</span><span class="sxs-lookup"><span data-stu-id="5bbd8-242">It includes `words[^2]` and `words[^1]`.</span></span> <span data-ttu-id="5bbd8-243">不包含結束索引 `words[^0]`：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-243">The end index `words[^0]` is not included:</span></span>

```csharp
var lazyDog = words[^2..^0];
```

<span data-ttu-id="5bbd8-244">下列範例會建立不限定開始、結束或兩者的範圍：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-244">The following examples create ranges that are open ended for the start, end, or both:</span></span>

```csharp
var allWords = words[..]; // contains "The" through "dog".
var firstPhrase = words[..4]; // contains "The" through "fox"
var lastPhrase = words[6..]; // contains "the, "lazy" and "dog"
```

<span data-ttu-id="5bbd8-245">您也可將範圍宣告為變數：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-245">You can also declare ranges as variables:</span></span>

```csharp
Range phrase = 1..4;
```

<span data-ttu-id="5bbd8-246">接著範圍可用於 `[` 及 `]` 字元中：</span><span class="sxs-lookup"><span data-stu-id="5bbd8-246">The range can then be used inside the `[` and `]` characters:</span></span>

```csharp
var text = words[phrase];
```