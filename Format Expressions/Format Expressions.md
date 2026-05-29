
## Common Paginated Report Format Expressions

Reference table for frequently used format expressions to control the visual appearance of report elements such as tables, text boxes, and charts.

### Table Row Formatting

| Description | Property | Expression | Notes |
|---|---|---|---|
| Alternating row colours | `BackgroundColor` | `=IIF(RowNumber(Nothing) MOD 2, "White", "AliceBlue")` | Apply to all cells in the detail row. Odd rows → White, even rows → AliceBlue. Swap colours to invert the pattern. |

### Notes

- Format expressions are applied to individual cell or row properties (e.g. `BackgroundColor`, `Color`, `FontBold`) in the Properties pane or via Expression editor
- `RowNumber(Nothing)` resets with each new page; use `RowNumber("DataSetName")` to number rows continuously across pages
- Colour values accept named colours (e.g. `"AliceBlue"`), hex strings (e.g. `"#F0F8FF"`), or `RGB()` function values (e.g. `RGB(240, 248, 255)`)
- Wrap complex conditions in `IIF(condition, trueValue, falseValue)` or `Switch()` for multiple cases
