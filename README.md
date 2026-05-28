
## Common Paginated Report Date Expressions

Reference table for frequently used date expressions to set default parameter values and dynamic date ranges.

### Current Period - Start Dates

| Description | Expression | Output Example |
|---|---|---|
| Today | `=Today()` | 5/28/2026 12:00:00 AM |
| Yesterday | `=DateAdd("d", -1, Today())` | 5/27/2026 12:00:00 AM |
| Tomorrow | `=DateAdd("d", 1, Today())` | 5/29/2026 12:00:00 AM |
| First day of this week | `=DateAdd("d", -DatePart(DateInterval.WeekDay, Today(), 0, 0) + 1, Today())` | 5/25/2026 12:00:00 AM |
| First day of last week | `=DateAdd("ww", -1, DateAdd("d", -DatePart(DateInterval.WeekDay, Today(), 0, 0) + 1, Today()))` | 5/18/2026 12:00:00 AM |
| First day of this month | `=DateAdd("d", -(Day(Today()) - 1), Today())` | 5/1/2026 12:00:00 AM |
| First day of last month | `=DateAdd("m", -1, DateAdd("d", -(Day(Today()) - 1), Today()))` | 4/1/2026 12:00:00 AM |
| First day of this year | `=DateAdd("d", -DatePart(DateInterval.DayOfYear, Today(), 0, 0) + 1, Today())` | 1/1/2026 12:00:00 AM |
| First day of last year | `=DateAdd("yyyy", -1, DateAdd("d", -DatePart(DateInterval.DayOfYear, Today(), 0, 0) + 1, Today()))` | 1/1/2025 12:00:00 AM |

### Current Period - End Dates

| Description | Expression | Output Example |
|---|---|---|
| End of today | `=DateAdd("d", 1, Today()) - 0.00000001` | 5/28/2026 11:59:59 PM |
| End of this week | `=DateAdd("d", 7 - DatePart(DateInterval.WeekDay, Today(), 0, 0), Today())` | 5/31/2026 11:59:59 PM |
| End of last week | `=DateAdd("d", -DatePart(DateInterval.WeekDay, Today(), 0, 0) - 1, Today())` | 5/24/2026 11:59:59 PM |
| End of this month | `=DateAdd("d", -Day(DateAdd("m", 1, Today())), DateAdd("m", 1, Today()))` | 5/31/2026 11:59:59 PM |
| End of last month | `=DateAdd("d", -Day(Today()), Today())` | 4/30/2026 11:59:59 PM |
| End of this year | `=DateAdd("d", 365 - DatePart(DateInterval.DayOfYear, Today(), 0, 0), Today())` | 12/31/2026 11:59:59 PM |
| End of last year | `=DateAdd("yyyy", -1, DateAdd("d", 365 - DatePart(DateInterval.DayOfYear, Today(), 0, 0) + 1, Today())) - 0.00000001` | 12/31/2025 11:59:59 PM |

### Period-over-Period Comparisons

| Description | Expression | Output Example |
|---|---|---|
| Same day last week | `=DateAdd("d", -7, Today())` | 5/21/2026 12:00:00 AM |
| Same day last month | `=DateAdd("m", -1, Today())` | 4/28/2026 12:00:00 AM |
| Same day last year | `=DateAdd("yyyy", -1, Today())` | 5/28/2025 12:00:00 AM |
| Week-over-week | `=DateAdd("ww", -1, Today())` | 5/21/2026 12:00:00 AM |
| Month-over-month | `=DateAdd("m", -1, Today())` | 4/28/2026 12:00:00 AM |
| Year-over-year | `=DateAdd("yyyy", -1, Today())` | 5/28/2025 12:00:00 AM |

### Rolling Periods

| Description | Expression | Output Example |
|---|---|---|
| Last 7 days | `=DateAdd("d", -7, Today())` | 5/21/2026 12:00:00 AM |
| Last 30 days | `=DateAdd("d", -30, Today())` | 4/28/2026 12:00:00 AM |
| Last 90 days | `=DateAdd("d", -90, Today())` | 2/28/2026 12:00:00 AM |
| Last 365 days | `=DateAdd("d", -365, Today())` | 5/28/2025 12:00:00 AM |
| Last 12 months | `=DateAdd("m", -12, Today())` | 5/28/2025 12:00:00 AM |

### Fiscal Year (assuming July 1 start)

| Description | Expression | Output Example |
|---|---|---|
| First day of current fiscal year | `=iif(Month(Today()) >= 7, DateSerial(Year(Today()), 7, 1), DateSerial(Year(Today()) - 1, 7, 1))` | 7/1/2025 12:00:00 AM |
| First day of last fiscal year | `=iif(Month(Today()) >= 7, DateSerial(Year(Today()) - 1, 7, 1), DateSerial(Year(Today()) - 2, 7, 1))` | 7/1/2024 12:00:00 AM |

### Formatting & Helper Expressions

| Description | Expression | Output Example |
|---|---|---|
| Current month name | `=MonthName(Month(Today()))` | May |
| Current day name | `=WeekdayName(Weekday(Today()))` | Wednesday |
| Format date (MM/dd/yyyy) | `=Format(Today(), "MM/dd/yyyy")` | 05/28/2026 |
| Format date (MMMM d, yyyy) | `=Format(Today(), "MMMM d, yyyy")` | May 28, 2026 |

### Notes

- Replace `Today()` with `Parameters!DateParameter.Value` to use parameter values instead
- Use `DateAdd()` with these interval types: "d" (day), "ww" (week), "m" (month), "yyyy" (year), "q" (quarter), "h" (hour), "n" (minute), "s" (second)
- For end-of-day timestamps, subtract a small value (0.00000001) to stay within the same day
- DateInterval enumeration can also use: `DateInterval.Day`, `DateInterval.Month`, `DateInterval.Year`, `DateInterval.WeekDay`, `DateInterval.DayOfYear`
- Test expressions in parameter default values or text boxes before using in filters

