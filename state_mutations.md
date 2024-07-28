# Topic

State mutations (e.g. usage of `let` in typescript). To what degree is it acceptable?
 
## Opinion

My background is in Functional Programming, so i have a heavy bias against it. These are the reasons, why I’m very averse to any state mutation:

1. Maintenance over time is hard. Especially if a variable undergoes a 2nd mutation. It’s hard to follow what’s happening

2. Testing is hard. If you have an array and you manipulate its state across different functions, it’s much harder to unit test those functions.

3. Refactoring is incredibly hard. It’s super annoying and a pain to refactor code that has a variable being changed in multiple places.

Some pros of state mutation are the following:

1. It’s quick. For example, this code - There’s just one state change and it’s faster and easier to do it this way:

```ts
  let chartLeftMargin = 10;
  if (chartData && chartData.length > 0) {
    chartLeftMargin = getMaxLabelWidthFromLabels(
      chartData.flatMap((d) => [numFormatter.format(d.range[0]), numFormatter.format(d.range[1])])
    );
  }
```

 The FP equivalent would be to use a lambda or break it into a helper:

```ts
function getMargin(defaultLeftMargin: number = 10) {
  if (chartData && chartData.length > 0) {
    return getMaxLabelWidthFromLabels(
      chartData.flatMap((d) => [numFormatter.format(d.range[0]), numFormatter.format(d.range[1])])
    );
  }
  
  return defaultLeftMargin;
}
```

2. Performance - I think this is irrelevant for us because this is hardly a factor into perforance in our use cases and premature optimization anyway is a bad idea.
