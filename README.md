<!--
author:  André Dietrich

version: 0.0.1

logo:    img/logo.png

comment: This is a LiaScript template for **JSSpreadsheet**, a lightweight,
          Excel‑like spreadsheet component for the web.  
          It shows how to embed editable spreadsheets into any LiaScript course.

script:  https://bossanova.uk/jspreadsheet/v5/jspreadsheet.js
         https://jsuites.net/v5/jsuites.js
        
link:    https://bossanova.uk/jspreadsheet/v5/jspreadsheet.css
         https://jsuites.net/v5/jsuites.css

@spreadsheet: @spreadsheet_(@uid,```@0```)

@spreadsheet_
<div id="spreadsheet_@0"></div>
<script>
const spreadsheet = document.getElementById('spreadsheet_@0')

if (spreadsheet.innerHTML.length == 0) {
    // jspreadsheet.destroy(spreadsheet)
    jspreadsheet(spreadsheet, @1);
    spreadsheet.addEventListener('keydown', function(e) {
       if ([37, 38, 39, 40].indexOf(e.keyCode) > -1) {
           // Arrow key codes
           e.stopPropagation();
       }
    });
}


"LIA: stop"
</script>
@end
-->

# JSSpreadsheet – LiaScript Template

                 --{{0}}--
This template lets you drop a fully‑featured spreadsheet into any LiaScript document with a single macro.
Powered by **[JSSpreadsheet](https://bossanova.uk/jspreadsheet)**, learners can sort, filter, validate and style data right inside the slide.

**Try it now** → \
https://liascript.github.io/course/?https://raw.githubusercontent.com/LiaTemplates/SpreadSheet/refs/heads/main/README.md

GitHub repo → \
https://github.com/LiaTemplates/SpreadSheet

Official docs → \
https://bossanova.uk/jspreadsheet/v5


                 --{{1}}--
Like every LiaTemplate, you have three ways to integrate it, the quickest being
copy‑and‑paste of the definition from *Sec. Implementation*.

                   {{1}}
1. **Import the latest** (may change without notice) \
   `import: https://raw.githubusercontent.com/LiaTemplates/SpreadSheet/refs/heads/main/README.md`

   or lock to **version 0.0.1** \
   `import: https://raw.githubusercontent.com/LiaTemplates/SpreadSheet/refs/tags/0.0.1/README.md`

2. **Copy the definitions** into your own project.

3. **Fork / clone** this repository on GitHub.

## `@spreadsheet`

                 --{{0}}--
`@spreadsheet` embeds one or more worksheets.
The fenced code block after the macro must contain the JSON configuration that [JSSpreadsheet](https://bossanova.uk/jspreadsheet) expects.

````markdown
```json @spreadsheet
{
  "worksheets": [{
    "data": [
      ["Task", "Owner", "Done?"],
      ["Template", "You", true]
    ],
    "columns": [
      { "type": "text",      "title": "Task",  "width": 200 },
      { "type": "dropdown",  "title": "Owner", "source": ["You","Me"]},
      { "type": "checkbox",  "title": "Done?" }
    ]
  } ]
}
```
````

Result:

```json @spreadsheet
{
  "worksheets": [{
    data: [
      ["Task", "Owner", "Done?"],
      ["Template", "You", true]
    ],
    columns: [
      { "type": "text",      "title": "Task",  "width": 200 },
      { "type": "dropdown",  "title": "Owner", "source": ["You","Me"]},
      { "type": "checkbox",  "title": "Done?" }
    ]
  } ]
}
```

### Multiple worksheets

           --{{0}}--
Simply provide an array of worksheet objects:

````markdown
```json @spreadsheet
{
  "worksheets": [
    { "minDimensions": [8, 12], "worksheetName": "Expenses" },
    { "minDimensions": [5,  8], "worksheetName": "Income"   }
  ]
}
```
````

```json @spreadsheet
{
  "worksheets": [
    { "minDimensions": [8, 12], "worksheetName": "Expenses" },
    { "minDimensions": [5,  8], "worksheetName": "Income"   }
  ]
}
```

### Calculations

```json @spreadsheet
{
  "worksheets": [
    {
      "data": [
        ["Region", "Q1", "Q2", "Q3", "Q4", "Total"],
        ["North", 245000, 267000, 301000, 352000, "=SUM(B2:E2)"],
        ["South", 312000, 298000, 286000, 329000, "=SUM(B3:E3)"],
        ["East", 198000, 237000, 246000, 268000, "=SUM(B4:E4)"],
        ["West", 342000, 356000, 401000, 443000, "=SUM(B5:E5)"],
        ["Total", "=SUM(B2:B5)", "=SUM(C2:C5)", "=SUM(D2:D5)", "=SUM(E2:E5)", "=SUM(F2:F5)"]
      ],
      "columns": [
        { "type": "text", "title": "Region", "width": 100 },
        { "type": "numeric", "title": "Q1", "width": 100, "mask": "$ #,##0", "decimal": "." },
        { "type": "numeric", "title": "Q2", "width": 100, "mask": "$ #,##0", "decimal": "." },
        { "type": "numeric", "title": "Q3", "width": 100, "mask": "$ #,##0", "decimal": "." },
        { "type": "numeric", "title": "Q4", "width": 100, "mask": "$ #,##0", "decimal": "." },
        { "type": "numeric", "title": "Total", "width": 120, "mask": "$ #,##0", "decimal": "." }
      ],
      "worksheetName": "Sales Overview",
      "style": {
        "A1:F1": "background-color: #2c3e50; color: white; font-weight: bold",
        "A6:F6": "background-color: #f1c40f; font-weight: bold",
        "F2:F5": "background-color: #ecf0f1; font-weight: bold"
      }
    },
    {
      "data": [
        ["Date", "Product", "Region", "Sales Rep", "Units", "Price", "Revenue"],
        ["2025-04-01", "Product A", "North", "John Smith", 12, 99.99, "=E2*F2"],
        ["2025-04-03", "Product B", "South", "Maria Garcia", 8, 149.99, "=E3*F3"],
        ["2025-04-05", "Product C", "East", "Robert Chen", 15, 59.99, "=E4*F4"],
        ["2025-04-08", "Product A", "West", "Lisa Wong", 10, 99.99, "=E5*F5"],
        ["2025-04-10", "Product D", "North", "James Brown", 5, 199.99, "=E6*F6"],
        ["2025-04-12", "Product B", "South", "Sarah Johnson", 7, 149.99, "=E7*F7"],
        ["2025-04-15", "Product E", "West", "Michael Lee", 20, 24.99, "=E8*F8"]
      ],
      "columns": [
        { "type": "calendar", "title": "Date", "width": 100, "format": "YYYY-MM-DD" },
        { "type": "dropdown", "title": "Product", "width": 100, "source": ["Product A", "Product B", "Product C", "Product D", "Product E"] },
        { "type": "dropdown", "title": "Region", "width": 100, "source": ["North", "South", "East", "West"] },
        { "type": "text", "title": "Sales Rep", "width": 120 },
        { "type": "numeric", "title": "Units", "width": 80 },
        { "type": "numeric", "title": "Price", "width": 100, "mask": "$ #,##0.00", "decimal": "." },
        { "type": "numeric", "title": "Revenue", "width": 120, "mask": "$ #,##0.00", "decimal": "." }
      ],
      "worksheetName": "Sales Transactions",
      "options": {
        "search": true,
        "columnSorting": true
      }
    },
    {
      "data": [
        ["Product", "Q1 Units", "Q2 Units", "Q3 Units", "Q4 Units", "Total Units", "Avg Price", "Total Revenue"],
        ["Product A", 145, 156, 187, 203, "=SUM(B2:E2)", 99.99, "=F2*G2"],
        ["Product B", 98, 112, 124, 131, "=SUM(B3:E3)", 149.99, "=F3*G3"],
        ["Product C", 205, 187, 201, 234, "=SUM(B4:E4)", 59.99, "=F4*G4"],
        ["Product D", 56, 68, 77, 85, "=SUM(B5:E5)", 199.99, "=F5*G5"],
        ["Product E", 312, 345, 367, 401, "=SUM(B6:E6)", 24.99, "=F6*G6"]
      ],
      "columns": [
        { "type": "text", "title": "Product", "width": 100 },
        { "type": "numeric", "title": "Q1 Units", "width": 80 },
        { "type": "numeric", "title": "Q2 Units", "width": 80 },
        { "type": "numeric", "title": "Q3 Units", "width": 80 },
        { "type": "numeric", "title": "Q4 Units", "width": 80 },
        { "type": "numeric", "title": "Total Units", "width": 100 },
        { "type": "numeric", "title": "Avg Price", "width": 100, "mask": "$ #,##0.00", "decimal": "." },
        { "type": "numeric", "title": "Total Revenue", "width": 120, "mask": "$ #,##0.00", "decimal": "." }
      ],
      "worksheetName": "Product Analysis"
    }
  ]
}
```

---

```` markdown
```json @spreadsheet
{
  "worksheets": [
    {
      "data": [
        ["Region", "Q1", "Q2", "Q3", "Q4", "Total"],
        ["North", 245000, 267000, 301000, 352000, "=SUM(B2:E2)"],
        ["South", 312000, 298000, 286000, 329000, "=SUM(B3:E3)"],
        ["East", 198000, 237000, 246000, 268000, "=SUM(B4:E4)"],
        ["West", 342000, 356000, 401000, 443000, "=SUM(B5:E5)"],
        ["Total", "=SUM(B2:B5)", "=SUM(C2:C5)", "=SUM(D2:D5)", "=SUM(E2:E5)", "=SUM(F2:F5)"]
      ],
      "columns": [
        { "type": "text", "title": "Region", "width": 100 },
        { "type": "numeric", "title": "Q1", "width": 100, "mask": "$ #,##0", "decimal": "." },
        { "type": "numeric", "title": "Q2", "width": 100, "mask": "$ #,##0", "decimal": "." },
        { "type": "numeric", "title": "Q3", "width": 100, "mask": "$ #,##0", "decimal": "." },
        { "type": "numeric", "title": "Q4", "width": 100, "mask": "$ #,##0", "decimal": "." },
        { "type": "numeric", "title": "Total", "width": 120, "mask": "$ #,##0", "decimal": "." }
      ],
      "worksheetName": "Sales Overview",
      "style": {
        "A1:F1": "background-color: #2c3e50; color: white; font-weight: bold",
        "A6:F6": "background-color: #f1c40f; font-weight: bold",
        "F2:F5": "background-color: #ecf0f1; font-weight: bold"
      }
    },
    {
      "data": [
        ["Date", "Product", "Region", "Sales Rep", "Units", "Price", "Revenue"],
        ["2025-04-01", "Product A", "North", "John Smith", 12, 99.99, "=E2*F2"],
        ["2025-04-03", "Product B", "South", "Maria Garcia", 8, 149.99, "=E3*F3"],
        ["2025-04-05", "Product C", "East", "Robert Chen", 15, 59.99, "=E4*F4"],
        ["2025-04-08", "Product A", "West", "Lisa Wong", 10, 99.99, "=E5*F5"],
        ["2025-04-10", "Product D", "North", "James Brown", 5, 199.99, "=E6*F6"],
        ["2025-04-12", "Product B", "South", "Sarah Johnson", 7, 149.99, "=E7*F7"],
        ["2025-04-15", "Product E", "West", "Michael Lee", 20, 24.99, "=E8*F8"]
      ],
      "columns": [
        { "type": "calendar", "title": "Date", "width": 100, "format": "YYYY-MM-DD" },
        { "type": "dropdown", "title": "Product", "width": 100, "source": ["Product A", "Product B", "Product C", "Product D", "Product E"] },
        { "type": "dropdown", "title": "Region", "width": 100, "source": ["North", "South", "East", "West"] },
        { "type": "text", "title": "Sales Rep", "width": 120 },
        { "type": "numeric", "title": "Units", "width": 80 },
        { "type": "numeric", "title": "Price", "width": 100, "mask": "$ #,##0.00", "decimal": "." },
        { "type": "numeric", "title": "Revenue", "width": 120, "mask": "$ #,##0.00", "decimal": "." }
      ],
      "worksheetName": "Sales Transactions",
      "options": {
        "search": true,
        "columnSorting": true
      }
    },
    {
      "data": [
        ["Product", "Q1 Units", "Q2 Units", "Q3 Units", "Q4 Units", "Total Units", "Avg Price", "Total Revenue"],
        ["Product A", 145, 156, 187, 203, "=SUM(B2:E2)", 99.99, "=F2*G2"],
        ["Product B", 98, 112, 124, 131, "=SUM(B3:E3)", 149.99, "=F3*G3"],
        ["Product C", 205, 187, 201, 234, "=SUM(B4:E4)", 59.99, "=F4*G4"],
        ["Product D", 56, 68, 77, 85, "=SUM(B5:E5)", 199.99, "=F5*G5"],
        ["Product E", 312, 345, 367, 401, "=SUM(B6:E6)", 24.99, "=F6*G6"]
      ],
      "columns": [
        { "type": "text", "title": "Product", "width": 100 },
        { "type": "numeric", "title": "Q1 Units", "width": 80 },
        { "type": "numeric", "title": "Q2 Units", "width": 80 },
        { "type": "numeric", "title": "Q3 Units", "width": 80 },
        { "type": "numeric", "title": "Q4 Units", "width": 80 },
        { "type": "numeric", "title": "Total Units", "width": 100 },
        { "type": "numeric", "title": "Avg Price", "width": 100, "mask": "$ #,##0.00", "decimal": "." },
        { "type": "numeric", "title": "Total Revenue", "width": 120, "mask": "$ #,##0.00", "decimal": "." }
      ],
      "worksheetName": "Product Analysis"
    }
  ]
}
```
````

### Persistence

              --{{0}}--
If you want to make the data persistent during the course, add the `persistent` property to the slide.
This way the table will be generated only once and not destroyed when the slide is left.

```` markdown
# slide
<!--
persistent: true
-->

```json @spreadsheet
{
  "worksheets": [
    { "minDimensions": [8, 12], "worksheetName": "Expenses" },
    { "minDimensions": [5,  8], "worksheetName": "Income"   }
  ]
}
```
````

### Columns

           --{{0}}--
The `columns` property is an array of objects, where each object defines a column in the spreadsheet.
Each object can have the following properties:

- `type`: The type of the column (e.g., `text`, `numeric`, `dropdown`, etc.).
- `title`: The title of the column.
- `width`: The width of the column (in pixels).
- `source`: The source for dropdown columns (an array of values).
- `mask`: A mask for formatting the input (e.g., `€ #.##0,00`).
- `decimal`: The decimal separator (e.g., `','`).
- `multiple`: Whether the dropdown allows multiple selections (for `dropdown` type).
- `readonly`: Whether the column is read-only (for `text` type).
- `render`: The rendering method for the column (e.g., `square` for color picker).

```json
{
  "columns": [
    { "type": "text",      "title": "Task",  "width": 200 },
    { "type": "dropdown",  "title": "Owner", "source": ["You","Me"]},
    { "type": "checkbox",  "title": "Done?" }
  ]
}
```

---

__Column types at a glance__

| Type       | Description                  | Extras (examples)                       |
| ---------- | ---------------------------- | --------------------------------------- |
| `text`     | Free text                    | `readonly:true`, `mask:'AA‑999'`        |
| `numeric`  | Numbers with mask / decimals | `mask:'€ #.##0,00'`, `decimal:','`      |
| `dropdown` | Select from list             | `source:["A","B","C"]`, `multiple:true` |
| `checkbox` | Boolean                      | –                                       |
| `calendar` | Date picker                  | `format:'DD/MM/YYYY'`                   |
| `image`    | Image URL                    | –                                       |
| `color`    | Color picker                 | `render:'square'`                       |

For the full API see the [JSSpreadsheet documentation](https://bossanova.uk/jspreadsheet/v5/pro).

## Implementation

                 --{{0}}--
Everything above runs on this tiny macro.
Copy it once and you can spawn spreadsheets anywhere in your course.

````html
script:  https://bossanova.uk/jspreadsheet/v5/jspreadsheet.js
         https://jsuites.net/v5/jsuites.js
        
link:    https://bossanova.uk/jspreadsheet/v5/jspreadsheet.css
         https://jsuites.net/v5/jsuites.css

@spreadsheet: @spreadsheet_(@uid,```@0```)

@spreadsheet_
<div id="spreadsheet_@0"></div>
<script>
const spreadsheet = document.getElementById('spreadsheet_@0')

if (spreadsheet.innerHTML.length > 0) {
    jspreadsheet.destroy(spreadsheet)
}

jspreadsheet(spreadsheet, @1);

"LIA: stop"
</script>
@end
````

          --{{1}}--
With that in place, your learners get an interactive, resizable Excel‑like experience—no plugins, no server, just pure client‑side JavaScript.
