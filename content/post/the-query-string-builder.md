---
date: 2014-03-19
title: "The Query String Builder"
tags: [ "dotnet", "code" ]
categories: [ "development" ]
---

I was after a query string builder to support a `System.Net.HttpClient` that I was building tonight and it was surprising hard to find something that met my needs.

After some digging through the Uri source code I decided to knock one up based on the NameValueCollection.

```csharp
public class QueryStringBuilder : NameValueCollection
{
    public QueryStringBuilder()
        : base(StringComparer.InvariantCultureIgnoreCase) { }

    public QueryStringBuilder(NameValueCollection collection)
        : base(StringComparer.InvariantCultureIgnoreCase)
    {
        Add(collection);
    }

    public QueryStringBuilder(object items)
        : base(StringComparer.InvariantCultureIgnoreCase)
    {
        if (items != null)
        {
            foreach (var propertyInfo in items.GetType().GetProperties())
            {
                base.Add(
                  propertyInfo.Name,
                    (propertyInfo.GetValue(items, null) ?? "").ToString());
            }
        }
    }

    public override string ToString()
    {
        var builder = new StringBuilder();

        var first = true;
        foreach (var item in AllKeys)
        {
            builder.AppendFormat("{0}{1}={2}",
                first ? "?" : "&",
                Uri.EscapeUriString(item),
                Uri.EscapeUriString(this[item]));

            first = false;
        }

        return builder.ToString();
    }
}
```
