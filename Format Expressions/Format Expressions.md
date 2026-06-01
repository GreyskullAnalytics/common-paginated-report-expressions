
## Common Paginated Report Format Expressions

Reference table for frequently used format expressions to control the visual appearance of report elements such as tables, text boxes, and charts.

### Table Row Formatting

| Description | Property | Expression | Notes |
|---|---|---|---|
| Alternating row colours | `BackgroundColor` | `=IIF(RowNumber(Nothing) MOD 2, "Transparent", "LightGrey")` | Apply to all cells in the detail row. Odd rows → Transparent, even rows → LightGrey. Swap colours to invert the pattern. |

### Matrix Row Formatting

`RowNumber()` is unreliable in a Matrix because SSRS evaluates cells independently rather than row by row, so the `IIF(RowNumber(...) MOD 2, ...)` technique used for tables does not work. Instead, use a custom code function that tracks odd/even state via a module-level boolean.

#### Step 1 — Add the custom function

Open **Report Properties → Code** and paste the following:

```vb
Private bOddRow As Boolean
'*************************************************************************
' -- Display colour banding in detail rows
' -- Call from BackGroundColor property of all detail row textboxes
' -- Set Toggle True for first item, False for others.
'*************************************************************************
Function AlternateColour(ByVal OddColour As String, _
         ByVal EvenColour As String, ByVal Toggle As Boolean) As String
    If Toggle Then bOddRow = Not bOddRow
    If bOddRow Then
        Return OddColour
    Else
        Return EvenColour
    End If
End Function
```

#### Step 2 — Set BackgroundColor on detail row cells

| Cell | Property | Expression |
|---|---|---|
| First cell in the detail row | `BackgroundColor` | `=Code.AlternateColour("Transparent", "LightGrey", True)` |
| Every other cell in the detail row | `BackgroundColor` | `=Code.AlternateColour("LightGrey", "Transparent", False)` |

`Toggle=True` on the first cell flips the internal `bOddRow` flag; all subsequent cells in the same row pass `False` to read the current state without flipping it again.

### Notes

- Format expressions are applied to individual cell or row properties (e.g. `BackgroundColor`, `Color`, `FontBold`) in the Properties pane or via Expression editor
- `RowNumber(Nothing)` resets with each new page; use `RowNumber("DataSetName")` to number rows continuously across pages
- Colour values accept named colours (e.g. `"LightGrey"`), hex strings (e.g. `"#D3D3D3"`), or `RGB()` function values (e.g. `RGB(211, 211, 211)`)
- Wrap complex conditions in `IIF(condition, trueValue, falseValue)` or `Switch()` for multiple cases
