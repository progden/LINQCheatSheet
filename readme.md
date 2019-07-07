**Aggregate**

​ 英文意思是**合計**，但是其實就是循序經過產生共同結果，跟 reduce 的效果類似

```csharp
  var sum = Enumerable.Range(1,10).Aggregate(0, (agg, e) => agg += e);
  Assert.AreEqual(55, sum);
```

**All & Any**

```csharp
  // 建立匿名物件陣列
  var pets = new[] { new { Name="Barley", Age=10 },
      new { Name="Boots", Age=4 },
      new { Name="Babe", Age=6 }};

  // 邏輯處理 All = &&, Any = ||
  Assert.True(pets.All(pet => pet.Name.ToUpper().StartsWith("B")));
  Assert.True(pets.Any(pet => pet.Age > 8));
```

**Prepend & Append**

​ 操作 Enumerable 介面附加項目在前面/後面

**AsEnumerable**

​ 在反組譯的 source code 裡面就只是單純的 return

​ 但是是在其他資料來源(資料庫連線等)，也是利用此介面來建立不同的實作

​ 例如在 Select 才實際執行的機關

```csharp
  public static IEnumerable<TSource> AsEnumerable<TSource>(
    this IEnumerable<TSource> source)
  {
    return source;
  }
```

**Average & Max & Min & Sum**

​ 取平均/最大/最小/總和

**Cast**

**Concat**

**Contains**

**Count**

**DefaultIfEmpty**

**Distinct**

**ElementAt & First & Last & Single**

​ 取得指定位置/第一/最後/取一個且唯一一個

​ 如果沒有東西會拋出例外

​ 另外，Single 取完如果還有其他的也會拋例外

**ElementAtOrDefault & FirstOrDefault & LastOrDefault & SingleOrDefault**

​ 同上但是如果沒有會回傳 default(TSource)

**Empty**

​ 會傳空白的 IEnumerable<TSource>

**Except**

**GroupBy**

**GroupJoin**

**Intersect**

**Join**

**LongCount**

**OfType**

**OrderBy**

**OrderByDescending**

**Range**

**Repeat**

**Reverse**

**Select & SelectMany**

 投射 (projection) 的概念，但是 API 用 Select 大概是把 SQL 的用法考慮進來
 
 應該是在 select 時透過函數做轉換的用法
 
```csharp 
 	Select(Func<int, TResult> selector)
```

 Func\<int, TResult> 是一個 (value) to result 的投射
 
```csharp 
 	Select(Func<int, int, TResult> selector)
```

 Func\<int, int, TResult> 是一個 (value, index) to result 的投射
​ 

```csharp
  var squareSum = Enumerable.Range(1, 10)
  				  			.Select((x) => x*x)
  							.Sum();
  Assert.AreEqual(385, squareSum);
```

**SequenceEqual**

**Skip**

**SkipLast**

**SkipWhile**

**Take**

**TakeLast**

**TakeWhile**

**ThenBy**

**ThenByDescending**

**ToArray**

**ToDictionary**

**ToHashSet**

**ToList**

**ToLookup**

**Union**

**Where**

**Zip**

有點將資料合併起來的意思，也就是zip字面上的拉鍊的感覺

給兩條 IEnumerable<T> 跟一個合併的方法 (first, second) => result

```csharp
// 這個比較有兩個list合併的感覺
var numMapping = Enumerable.Zip(new List<int>{1, 2, 3},								new List<string> { "one", "two", "three", "four"}, //用四個值								(intNum, strNum) => $"{intNum}: {strNum}");Console.WriteLine(numMapping);// 這個 zip 第二個 listvar numMapping2 = Enumerable.Range(1, 5) // 用五個值							.Zip(new List<string> { "one", "two", "three" },								(intNum, strNum) => $"{intNum}: {strNum}");Console.WriteLine(numMapping2);

// 最後zip起來的長度會是以短的為主
Assert.AreEquals(3, numMapping.Count());
Assert.AreEquals(3, numMapping2.Count());


```