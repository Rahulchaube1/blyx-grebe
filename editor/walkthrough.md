## Resume a keyset page from its last emitted key

Returns [first index, exclusive end, resume key, has more]. On an empty result the input cursor is retained. Supply stable unique numeric keys from a consistent snapshot. Invalid arguments and nonfinite results return an empty vector.

1. Open an empty file named `grebe-demo.blyx`.
2. Type `blyx-grebe-demo` and select **Grebe — runnable example**. You can also use **Snippets: Fill File with Snippet**.
3. Choose **Blyx: Run File** from the command palette. Change an argument near the end of `fn main()` to try another input.

Expected output

```text
1
3
30
1
```

[Work through the example in the browser](https://www.blyx-lang.space/play?example=package-grebe)
