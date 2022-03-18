# Python操纵Excel

## pandas

### `read_excel()`

```python
import pandas as pd

pd.read_excel?
```

!!!info

    * To read in all sheets, provide `sheet_name=None`
    * To handle NaN values, use a combination of `na_values` and `keep_default_na`

### ExcelFile class

```python
with pd.ExcelFile("xl/stores.xls") as f:
    df1 = pd.read_excel(f, "2019", skiprows=1, usecols="B:F", nrows=2)
    df2 = pd.read_excel(f, "2020", skiprows=1, usecols="B:F", nrows=2)

stores = pd.ExcelFile("xl/stores.xlsx")
stores.sheet_names # 所有的sheet名
```

### `to_excel()`

```python
pd.DataFrame.to_excel?
```

> If you want to write multiple DataFrames to the same or different sheets, you will need to use the ExcelWriter class.

### ExcelWriter class

```python
with pd.ExcelWriter("written_with_pandas2.xlsx") as writer:
    df.to_excel(writer, sheet_name="Sheet1", startrow=1, startcol=1)
    df.to_excel(writer, sheet_name="Sheet1", startrow=10, startcol=1)
```

## openpyxl

```python
import openpyxl
from openpyxl.drawing.image import Image
from openpyxl.chart import BarChart, Reference
from openpyxl.styles import Font, colors
from openpyxl.styles.borders import Border, Side
from openpyxl.styles.alignment import Alignment
from openpyxl.styles.fills import PatternFill

# Instantiate a workbook
book = openpyxl.Workbook()

# Get the first sheet and give it a name
sheet = book.active
sheet.title = "Sheet1"

# Writing individual cells using A1 notation
# and cell indices (1-based)
sheet["A1"].value = "Hello 1"
sheet.cell(row=2, column=1, value="Hello 2")

# Formatting: fill color, alignment, border and font
font_format = Font(color="FF0000", bold=True)
thin = Side(border_style="thin", color="FF0000")
sheet["A3"].value = "Hello 3"
sheet["A3"].font = font_format
sheet["A3"].border = Border(top=thin, left=thin,
                            right=thin, bottom=thin)
sheet["A3"].alignment = Alignment(horizontal="center")
sheet["A3"].fill = PatternFill(fgColor="FFFF00", fill_type="solid")

# Number formatting (using Excel's formatting strings)
sheet["A4"].value = 3.3333
sheet["A4"].number_format = "0.00"

# Date formatting (using Excel's formatting strings)
sheet["A5"].value = dt.date(2016, 10, 13)
sheet["A5"].number_format = "mm/dd/yy"

# Formula: you must use the English name of the formula
# with commas as delimiters
sheet["A6"].value = "=SUM(A4, 2)"

# Image
sheet.add_image(Image("images/python.png"), "C1")

# Two-dimensional list (we're using our excel module)
data = [[None, "North", "South"],
        ["Last Year", 2, 5],
        ["This Year", 3, 6]]

# Chart
chart = BarChart()
chart.type = "col"
chart.title = "Sales Per Region"
chart.x_axis.title = "Regions"
chart.y_axis.title = "Sales"
chart_data = Reference(sheet, min_row=11, min_col=1,
                       max_row=12, max_col=3)
chart_categories = Reference(sheet, min_row=10, min_col=2,
                             max_row=10, max_col=3)
# from_rows interprets the data in the same way
# as if you would add a chart manually in Excel
chart.add_data(chart_data, titles_from_data=True, from_rows=True)
chart.set_categories(chart_categories)
sheet.add_chart(chart, "A15")

# Saving the workbook creates the file on disk
book.save("openpyxl.xlsx")
```

## xlwings

### 安装

```shell
pip install xlwings

conda install -c conda-forge xlwings
```

```python
import xlwings as xw

xw.__version__
```

![オブジェクトの階層構造](https://upload-images.jianshu.io/upload_images/2979196-89d95b50b4a69d4f.png?imageMogr2/auto-orient/strip|imageView2/2/w/804)

### `xw.view()`

> Excel as viewer for tabular data

```python
data = np.random.rand(100, 100)
print(data)

# Open a new book
xw.view(data)

# Reuse an existing sheet(sheets gets cleared with every call)
xw.view(np.random.rand(5, 5), xw.sheets.active)

xw.view(np.random.rand(3, 3), xw.sheets.active)
```

### Book

```python
# 新規ブック
wb1 = xw.Book()
wb1 = xw.books.add()

# 保存されていないブック
wb1 = xw.Book("Book1")
wb1 = xw.books["Book1"]

# （完全な）名前でブックを指定
wb1 = xw.Book(r"C:\Users\XXX\Desktop\Myworkbook.xlsx")
wb1 = xw.books.open(r"C:\Users\XXX\Desktop\Myworkbook.xlsx")
```

### Range

```python
sheet = xw.Book().sheets[0]

# Write Value
sheet.range("A1").value = "hello xlwings!"
# Read value
sheet.range("A1").value
# Write the same value to multiple cells
sheet.range("A3:B4").value = 123
# Excel's numerical format is float
sheet.range("A3").value
# Datetime
sheet.range("A6") = dt.datetime(2020, 12, 25, 22, 22, 22)
sheet.range("A6").value
# Index natation (1-Based like Excel)
sheet.range(1, 1).value = "A1"
sheet.range((1, 1), (3, 3)).value = "C3"
```

!!!info

    インデックスの開始番号は、  
      * 丸括弧()ならExcelと同じく1から
      * 角括弧[]ならPythonと同じく0から（こちらはスライスも可）

```python
# Formula
sheet.range("B1").formula = "=SUM(A3:B4)"
# Named ranges
sheet.range("B1").name = "test"

sheet.range("test").formula

sheet.range("A1:H1").font.name = "微软雅黑"
sheet.range("A1:H1").font.size = 10
sheet.range("A1:H1").font.bold = True
sheet.range("A1:H1").font.color = (255, 255, 255)

foo = sheet.range("test").value
print(foo)

sheet.range("test").value = "Likethis"
# Numpy arrays
sheet.range("A1").value = np.eye(3)
sheet.range("A1").options(convert=np.array, expand="table").value
```

!!!warning

    空のセルは None ではなく nan となります

```python
# Pandas DataFrames
df = pd.DataFrame([1.1, 2.2], [3.3, None], columns=["a", "b"])
sheet.range("A1").value = df
sheet.range("A1:C3").options(pd.DataFrame).value

sheet.range("A5").options(index=False).value = df
sheet.range("A9").options(index=False, header=False).value = df
# Pandas Series
s = pd.Series([1.1, 3.3, 5., np.nan, 6., 8.], name="myseries")

sheet.range("A1").value=s
sheet.range("A1:B7").options(pd.Series).value
```

リストやNumPy arrayやPandas DataFrameをExcelに書き込むには、左上セルを指定するだけで済みます。

例:

```python
sheet.range('A1').value = np.eye(10)
```

### 2D Range

```python
sheet.range("A3:B4").value

# Index notation
sheet.range((3, 1), (4, 2)).value

# Assign a nested list to the top-left corner
sheet.range("A9").value = [["a string", 1, 2, 3],
                           [dt.date(2021, 1, 1), 123.5, None, None]]

# Range expansion: "table", "down", "right"
# Correspond to Ctrl+Shift+Down and/or right
# They return a Range object!
area = sheet.range("A9").expand("table")
area.column_width = 15
area.row_height = 20

# "table" is default
sheet.range("A9").expand.value

# Use .clear to also clear the formatting
sheet.range("A9").expand().clear_contents()
```

### 1D Vector

```python
# Horizontal
sheet.range("A12").value = [1, 2, 3, 4]

# Vertical
sheet.range("A13").options(transpose=True).value = [5, 6, 7, 8]

# this is the same as:
# sheet.range("A13").value = [[5], [6], [7], [8]]
sheet.range("A12").expand("right").value
sheet.range("A12").expand("down").value
```

### ndim

```python
sheet.range("A1").options(ndim=1).value
sheet.range("A12").options(ndim=2, expand="right").value
sheet.range("A12").options(ndim=2, expand="down").value
```

### Autofit

```python
# autofit columns and rows based on a single cell
sheet.range("A3").autofit()

# autofit columns based on range
sheet.range("A1:C3").columns.autofit()

# autofit a whole column
sheet.range("A:A").autofit()
```

### API

```python
import xlwings as xw

app = xw.App(visible=False, add_book=False)
workbook = app.books.open("filepath.xlsx", password="123")
worksheets = workbook.sheets
# api调用
workbook.save()
workbook.close()
app.quit()
```

#### `Protect()`, `Unprotect()`

```python
workbook.api.Protect(Password="123", Structure=True, Windows=True)
```

#### Password

```python
workbook.api.Password = "password"
```

#### Tab.Color

```python
worksheets[0].api.Tab.Color = 255
# Color属性整数值 = R + G * 256 + B * 256 * 256
```

### Background Color

```python
# Assign an RGB value
sheet.range("A1").color = (0, 255, 0)
sheet.range("A1").color
```

### Range indexing/slicing

```python
rng = sheet.range("A1:D5")
print(rng[0, 0])
print(rng[1])
print(rng[:, 3:])
print(rng[1:3, 1:3])
xw.books.active.close()
```

### Full qualification

```python
# Get all available PIDs (Process IDs)
xw.apps.keys()

# This allows us to specify a specific Excel instance
pid = xw.apps.keys()[0] # or xw.apps.active.pid
xw.apps[pid].books[0].sheets[0].range("A1")
xw.apps(pid).books(1).sheets(1).range("A1")

# Instead of indices we can also use names
xw.apps[pid].books["Book1"].sheets["Sheet1"].range("A1")
xw.apps(pid).books("Book1").sheets("Sheet1").range("A1")
```

### Multiple Excel instances

```python
app1 = xw.apps[pid]
app2 = xw.App()

# Open the same workbook twice in different Excel instances
app1.books.open("foo.xlsx")
app2.books.open("foo.xlsx")

# this will throw an error
# xw.Book("foo.xlsx")

# The following syntax is required
# if the same file is opened in more than 1 instance
print(app1.books["foo.xlsm"])
print(app2.books["foo.xlsm"])
print(app1.books["foo.xlsm"].app)
print(app1.books["foo.xlsm"].app)
```

### Active objects

```python
# Active app
xw.apps.active

# active book in active app
xw.books.active

# active sheet in active book in active app
xw.sheets.active

# This is a special shortcut for interactive use only
# It takes the active sheet form the active book
xw.Range("A1").value
app2.kill()
```

### Sheets

```python
xw.sheets[0].name
xw.sheets.count # same as len(xw.sheets)
xw.sheets.add(name="New Sheet By xlwings", after="Sheet1")

sheet = xw.sheets[0]
sheet["A1"]
sheet["A1:B5"]
sheet[0, 1]
sheet[:10, :10]

sheet.delete()

sheet.name = "new name"

sheet.copy(before=sheets[1])

sheet.visible = False

sheet.autofit() # 自动调整工作表的行高和列宽

sheet.max_row

sheet.insert_rows(5, 1)
sheet.insert_cols(5, 1)

sheet.delete_rows(5, 2)
sheet.delete_cols(5, 2)
sheet.freeze_panes = "B2" # 把单元格B2上方的行及左侧的列冻结
```

### Charts

```python
wb = xw.Book()

sheet = wb.sheets[0]
sheet.range("A1").value = [["one", "two"],
                           [1.1, 2.2],
                           [3.3, None]]

chart = sheet.charts.add()
chart.set_source_data(sheet.range("A1").expand())
chart.chart_type = "line"
chart.top = sheet.range("A5").top
chart.chart_type = "area"

xw.constants.chart_types

wb.close()
```

### Matplotlib

```python
% matplotlib inline

from scipy.interpolate import interp1d
import matplotlib as mpl
import matplotlib.pyplot as plt

years = [1, 2, 3, 4, 5, 7, 10, 30]
swap_rate = np.random.rand(8)
years_new = np.linspace(1, 30, num=30)

interpolate = interp1d(years, swap_rate, kind="quadratic")
fig = plt.figure(figsize=(6, 4))
swap_rate_plot = plt.plot(years, swap_rate, "o",
                          years_new, interpolate(years_new),                            "-")
wb = xw.Book()
sheet = wb.sheets[0]
plot = sheet.pictures.add(fig, name="SwapRate", update=True)

width, height = fig.get_size_inches()
dpi = fig.get_dpi()
sheet.pictures.add(fig, name="SwapRate2", update=True,
                   left=sheet.range("A25").left, top=sheet.range("A25"),
                   width=width * dpi / 2, height=height * dpi / 2)
plot.height = plt.height / 2
plot.width = plot.width / 2

wb.close()
```

### Table

```python
wb = xw.Book("foo.xlsx")
sheet = wb.sheets[0]

sheet.range("Table1").value
sheet.range("Table1[Symbol]").value
sheet.range("Table1[#All], [Last]]").value
sheet.range("Table1[[#Headers], [Last]]").value
sheet.range("Table1[[#Totals], [Last]]").value
sheet.range("Table1[[Index]:[Last]]").value

wb.close()
```

### Efficiency

```python
wb = xw.Book()

sheet = wb.sheets[0]
sheet.range("A1").value = np.arange(5 * 30).reshape((30, 5))

wb.close()
```

### Work around for missing features

```python
wb = xw.Book()
sheet = wb.sheets[0]

# On windows, the underlying object is a pywin32 COM object
# On Mac, it is an appscript object
sheet.range("A1").api
if sys.platform.startswith("darwin"):
    sheet.range("A10").api.clear_formats()
elif sys.platform.startswith("win"):
    sheet.range("A10").api.ClearFormats()
```

### UDFs: User Defined Functions(Windows only)

```python
@xw.func
def hello(name):
    return f"Hello {name}"

@xw.func
@xw.arg("x", pd.DataFrame)
def correl2(x):
    retrun x.corr()
```
