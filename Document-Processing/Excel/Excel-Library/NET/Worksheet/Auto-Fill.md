---
title: Auto Fill | Syncfusion
description: In this section, you can learn how to use the Auto Fill feature in Excel using C# with the Syncfusion XlsIO library.
platform: document-processing
control: XlsIO
documentation: UG
---

# Auto Fill

 The **Auto Fill** enables users to programmatically populate a range of Excel cells based on defined patterns, sequences, or trends. This helps reduce manual data entry by automatically generating values using built-in logic.

## Types

### Default

The **Default Auto Fill** option automatically determines the most appropriate behavior based on the content, formatting, and pattern in the source range. This option uses default values derived from the source to intelligently populate the destination range.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Assign values to the cells
worksheet["A1"].Number = 2;
worksheet["A2"].Number = 4;
worksheet["A3"].Number = 6;

//Define the source range
IRange source = worksheet["A1:A3"];

//Define the destination range
IRange destinationRange = worksheet["A4:A100"];

//Auto fill using the default option
source.AutoFill(destinationRange, ExcelAutoFillType.FillDefault);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Assign values to the cells
worksheet["A1"].Number = 2;
worksheet["A2"].Number = 4;
worksheet["A3"].Number = 6;

//Define the source range
IRange source = worksheet["A1:A3"];

//Define the destination range
IRange destinationRange = worksheet["A4:A100"];

//Auto fill using the default option
source.AutoFill(destinationRange, ExcelAutoFillType.FillDefault);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Assign values to the cells
worksheet("A1").Number = 2
worksheet("A2").Number = 4
worksheet("A3").Number = 6

'Define the source range
Dim source As IRange = worksheet("A1:A3")

'Define the destination range
Dim destinationRange As IRange = worksheet("A4:A100")

'Auto fill using the default option
source.AutoFill(destinationRange, ExcelAutoFillType.FillDefault)
{% endhighlight %}

{% endtabs %}  

### Copy

The **Copy Auto Fill** option repeats the exact values from the source range without applying any pattern or increment. This option is useful when the same content needs to be duplicated across the destination range while preserving the original data.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Assign values to the cells
worksheet["A1"].Number = 2;
worksheet["A2"].Number = 4;
worksheet["A3"].Number = 6;

//Define the source range
IRange source = worksheet["A1:A3"];

//Define the destination range
IRange destinationRange = worksheet["A4:A100"];

//Auto fill using the copy option
source.AutoFill(destinationRange, ExcelAutoFillType.FillCopy);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Assign values to the cells
worksheet["A1"].Number = 2;
worksheet["A2"].Number = 4;
worksheet["A3"].Number = 6;

//Define the source range
IRange source = worksheet["A1:A3"];

//Define the destination range
IRange destinationRange = worksheet["A4:A100"];

//Auto fill using the copy option
source.AutoFill(destinationRange, ExcelAutoFillType.FillCopy);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Assign values to the cells
worksheet("A1").Number = 2
worksheet("A2").Number = 4
worksheet("A3").Number = 6

'Define the source range
Dim source As IRange = worksheet("A1:A3")

'Define the destination range
Dim destinationRange As IRange = worksheet("A4:A100")

'Auto fill using the copy option
source.AutoFill(destinationRange, ExcelAutoFillType.FillCopy)
{% endhighlight %}

{% endtabs %}  

### Series

The **Series Auto Fill** option populates the destination range with values that follow a defined sequence or step based on the source pattern. It is useful for generating structured data and enables efficient expansion of sequential values.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Assign values to the cells
worksheet["A1"].Number = 2;
worksheet["A2"].Number = 4;
worksheet["A3"].Number = 6;

//Define the source range
IRange source = worksheet["A1:A3"];

//Define the destination range
IRange destinationRange = worksheet["A4:A100"];

//Auto fill using the series option
source.AutoFill(destinationRange, ExcelAutoFillType.FillSeries);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
 //Assign values to the cells
 worksheet["A1"].Number = 2;
 worksheet["A2"].Number = 4;
 worksheet["A3"].Number = 6;

 //Define the source range
 IRange source = worksheet["A1:A3"];

 //Define the destination range
 IRange destinationRange = worksheet["A4:A100"];

 //Auto fill using the series option
 source.AutoFill(destinationRange, ExcelAutoFillType.FillSeries);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Assign values to the cells
worksheet("A1").Number = 2
worksheet("A2").Number = 4
worksheet("A3").Number = 6

'Define the source range
Dim source As IRange = worksheet("A1:A3")

'Define the destination range
Dim destinationRange As IRange = worksheet("A4:A100")

'Auto fill using the series option
source.AutoFill(destinationRange, ExcelAutoFillType.FillSeries)
{% endhighlight %}

{% endtabs %}  

### Formats

The **Formats Auto Fill** option copies only the formatting from the source range to the destination range without affecting the existing values. It is useful for maintaining a uniform appearance and enables efficient application of styles across large data ranges.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Assign values and format cells
worksheet["A1"].Number = 2;
worksheet["A1"].NumberFormat = "$.00";  
worksheet["A1"].CellStyle.ColorIndex = ExcelKnownColors.Blue;

worksheet["A2"].Number = 4;
worksheet["A2"].NumberFormat = "$.00";           
worksheet["A2"].CellStyle.ColorIndex = ExcelKnownColors.Red;

worksheet["A3"].Number = 6;
worksheet["A3"].NumberFormat = "$.00";       
worksheet["A3"].CellStyle.ColorIndex = ExcelKnownColors.Green;

//Define the source range
IRange source = worksheet["A1:A3"];

//Define the destination range
IRange destinationRange = worksheet["A4:A100"];

//Auto fill using the formats option
source.AutoFill(destinationRange, ExcelAutoFillType.FillFormats);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Assign values and format cells
worksheet["A1"].Number = 2;
worksheet["A1"].NumberFormat = "$.00";
worksheet["A1"].CellStyle.ColorIndex = ExcelKnownColors.Blue;

worksheet["A2"].Number = 4;
worksheet["A2"].NumberFormat = "$.00";
worksheet["A2"].CellStyle.ColorIndex = ExcelKnownColors.Red;

worksheet["A3"].Number = 6;
worksheet["A3"].NumberFormat = "$.00";
worksheet["A3"].CellStyle.ColorIndex = ExcelKnownColors.Green;

//Define the source range
IRange source = worksheet["A1:A3"];

//Define the destination range
IRange destinationRange = worksheet["A4:A100"];

//Auto fill using the formats option
source.AutoFill(destinationRange, ExcelAutoFillType.FillFormats);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Assign values and format cells
worksheet("A1").Number = 2
worksheet("A1").NumberFormat = "$.00"
worksheet("A1").CellStyle.ColorIndex = ExcelKnownColors.Blue

worksheet("A2").Number = 4
worksheet("A2").NumberFormat = "$.00"
worksheet("A2").CellStyle.ColorIndex = ExcelKnownColors.Red

worksheet("A3").Number = 6
worksheet("A3").NumberFormat = "$.00"
worksheet("A3").CellStyle.ColorIndex = ExcelKnownColors.Green

'Define the source range
Dim source As IRange = worksheet("A1:A3")

'Define the destination range
Dim destinationRange As IRange = worksheet("A4:A100")

'Auto fill using the formats option
source.AutoFill(destinationRange, ExcelAutoFillType.FillFormats)
{% endhighlight %}

{% endtabs %}  

### Values

The **Values Auto Fill** option copies only the values from the source range to the destination range without carrying over any formatting. It is useful for preserving raw data while applying it consistently across cells, enabling efficient duplication of content without altering the existing cell styles.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Assign values to the cells
worksheet["A1"].Number = 2;
worksheet["A2"].Number = 4;
worksheet["A3"].Number = 6;

//Define the source range
IRange source = worksheet["A1:A3"];

//Define the destination range
IRange destinationRange = worksheet["A4:A100"];

//Auto fill using the values option
source.AutoFill(destinationRange, ExcelAutoFillType.FillValues);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Assign values to the cells
worksheet["A1"].Number = 2;
worksheet["A2"].Number = 4;
worksheet["A3"].Number = 6;

//Define the source range
IRange source = worksheet["A1:A3"];

//Define the destination range
IRange destinationRange = worksheet["A4:A100"];

//Auto fill using the values option
source.AutoFill(destinationRange, ExcelAutoFillType.FillValues);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Assign values to the cells
worksheet("A1").Number = 2
worksheet("A2").Number = 4
worksheet("A3").Number = 6

'Define the source range
Dim source As IRange = worksheet("A1:A3")

'Define the destination range
Dim destinationRange As IRange = worksheet("A4:A100")

'Auto fill using the values option
source.AutoFill(destinationRange, ExcelAutoFillType.FillValues)
{% endhighlight %}

{% endtabs %}  

### DateTime

The **Days, Weekdays, Months, and Years Auto Fill** options populate the destination range with date values by incrementing the corresponding part of the date from the source range. These options allow you to extend dates by individual days, skip weekends (weekdays), or increment by months or years. They are useful for generating timelines, schedules, or date-based reports with consistent and structured date progression.

#### Days

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Assign date values to the cells
worksheet.Range["A1"].NumberFormat = "m/d/yyyy";
worksheet.Range["A1"].DateTime = new DateTime(2025, 1, 1);
worksheet.Range["A2"].NumberFormat = "m/d/yyyy";
worksheet.Range["A2"].DateTime = new DateTime(2025, 1, 2);
worksheet.Range["A3"].NumberFormat = "m/d/yyyy";
worksheet.Range["A3"].DateTime = new DateTime(2025, 1, 3);

//Define the source range
IRange source = worksheet["A1:A3"];

//Define the destination range
IRange destinationRange = worksheet["A4:A100"];

//Auto fill using the days option
source.AutoFill(destinationRange, ExcelAutoFillType.FillDays);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Assign date values to the cells
worksheet.Range["A1"].NumberFormat = "m/d/yyyy";
worksheet.Range["A1"].DateTime = new DateTime(2025, 1, 1);
worksheet.Range["A2"].NumberFormat = "m/d/yyyy";
worksheet.Range["A2"].DateTime = new DateTime(2025, 1, 2);
worksheet.Range["A3"].NumberFormat = "m/d/yyyy";
worksheet.Range["A3"].DateTime = new DateTime(2025, 1, 3);

//Define the source range
IRange source = worksheet["A1:A3"];

//Define the destination range
IRange destinationRange = worksheet["A4:A100"];

//Auto fill using the days option
source.AutoFill(destinationRange, ExcelAutoFillType.FillDays);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Assign date values to the cells
worksheet.Range("A1").NumberFormat = "m/d/yyyy"
worksheet.Range("A1").DateTime = New DateTime(2025, 1, 1)
worksheet.Range("A2").NumberFormat = "m/d/yyyy"
worksheet.Range("A2").DateTime = New DateTime(2025, 1, 2)
worksheet.Range("A3").NumberFormat = "m/d/yyyy"
worksheet.Range("A3").DateTime = New DateTime(2025, 1, 3)

'Define the source range
Dim source As IRange = worksheet("A1:A3")

'Define the destination range
Dim destinationRange As IRange = worksheet("A4:A100")

'Auto fill using the days option
source.AutoFill(destinationRange, ExcelAutoFillType.FillDays)
{% endhighlight %}

{% endtabs %}  

Like this, you can use the **FillWeekdays, FillMonths, and FillYears** options to populate the destination range by incrementing only the weekday, month, or year part of the date, respectively. These options are useful for generating workday schedules, monthly plans, or yearly summaries while maintaining a consistent date progression pattern. The usage remains the same as shown in the FillDays example, only the ExcelAutoFillType value needs to be changed.

### Linear Trend

The **Linear Trend Auto Fill** option fills the destination range by calculating and applying a constant difference between values in the source range. It is useful for generating values that follow a straight-line progression and enables efficient creation of forecast or analytical data series.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Assign values to the cells
worksheet["A1"].Number = 2;
worksheet["A2"].Number = 4;
worksheet["A3"].Number = 6;

//Define the source range
IRange source = worksheet["A1:A3"];

//Define the destination range
IRange destinationRange = worksheet["A4:A100"];

//Auto fill using the linear trend option
source.AutoFill(destinationRange, ExcelAutoFillType.LinearTrend);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Assign values to the cells
worksheet["A1"].Number = 2;
worksheet["A2"].Number = 4;
worksheet["A3"].Number = 6;

//Define the source range
IRange source = worksheet["A1:A3"];

//Define the destination range
IRange destinationRange = worksheet["A4:A100"];

//Auto fill using the linear trend option
source.AutoFill(destinationRange, ExcelAutoFillType.LinearTrend);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Assign values to the cells
worksheet("A1").Number = 2
worksheet("A2").Number = 4
worksheet("A3").Number = 6

'Define the source range
Dim source As IRange = worksheet("A1:A3")

'Define the destination range
Dim destinationRange As IRange = worksheet("A4:A100")

'Auto fill using the linear trend option
source.AutoFill(destinationRange, ExcelAutoFillType.LinearTrend)
{% endhighlight %}

{% endtabs %}  

### Growth Trend

The **Growth Trend Auto Fill** option fills the destination range by applying a constant multiplication factor between values in the source range. It is useful for generating values that follow an exponential progression and enables efficient creation of growth-based forecasts or analytical data series.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Assign values to the cells
worksheet["A1"].Number = 2;
worksheet["A2"].Number = 4;
worksheet["A3"].Number = 6;

//Define the source range
IRange source = worksheet["A1:A3"];

//Define the destination range
IRange destinationRange = worksheet["A4:A100"];

//Auto fill using the growth trend option
source.AutoFill(destinationRange, ExcelAutoFillType.GrowthTrend);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Assign values to the cells
worksheet["A1"].Number = 2;
worksheet["A2"].Number = 4;
worksheet["A3"].Number = 6;

//Define the source range
IRange source = worksheet["A1:A3"];

//Define the destination range
IRange destinationRange = worksheet["A4:A100"];

//Auto fill using the growth trend option
source.AutoFill(destinationRange, ExcelAutoFillType.GrowthTrend);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Assign values to the cells
worksheet("A1").Number = 2
worksheet("A2").Number = 4
worksheet("A3").Number = 6

'Define the source range
Dim source As IRange = worksheet("A1:A3")

'Define the destination range
Dim destinationRange As IRange = worksheet("A4:A100")

'Auto fill using the growth trend option
source.AutoFill(destinationRange, ExcelAutoFillType.GrowthTrend)
{% endhighlight %}

{% endtabs %}  

The following code example illustrates how to auto fill using **FillSeries** in a worksheet.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" playgroundButtonLink="https://raw.githubusercontent.com/SyncfusionExamples/XlsIO-Examples/master/Worksheet%20Features/Auto%20Fill/.NET/AutoFillUsingFillSeries/AutoFillUsingFillSeries/Program.cs,180" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Create(1);
    IWorksheet worksheet = workbook.Worksheets[0];

    //Assign values to the cells
    worksheet["A1"].Number = 2;
    worksheet["A2"].Number = 4;
    worksheet["A3"].Number = 6;

    //Define the source range
    IRange source = worksheet["A1:A3"];

    //Define the destination range
    IRange destinationRange = worksheet["A4:A100"];

    //Auto fill using the series option
    source.AutoFill(destinationRange, ExcelAutoFillType.FillSeries);

    //Saving the workbook 
    FileStream outputStream = new FileStream(Path.GetFullPath("Output/Output.xlsx"), FileMode.Create, FileAccess.Write);
    workbook.SaveAs(outputStream);

    //Dispose streams
    outputStream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Create(1);
    IWorksheet worksheet = workbook.Worksheets[0];

    //Assign values to the cells
    worksheet["A1"].Number = 2;
    worksheet["A2"].Number = 4;
    worksheet["A3"].Number = 6;

    //Define the source range
    IRange source = worksheet["A1:A3"];

    //Define the destination range
    IRange destinationRange = worksheet["A4:A100"];

    //Auto fill using the series option
    source.AutoFill(destinationRange, ExcelAutoFillType.FillSeries);

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Create(1)
    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    'Assign values to the cells
    worksheet("A1").Number = 2
    worksheet("A2").Number = 4
    worksheet("A3").Number = 6

    'Define the source range
    Dim source As IRange = worksheet("A1:A3")

    'Define the destination range
    Dim destinationRange As IRange = worksheet("A4:A100")

    'Auto fill using the series option
    source.AutoFill(destinationRange, ExcelAutoFillType.FillSeries)

    'Saving the workbook
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example of how to auto fill using **FillSeries** in a worksheet using C# is present on <a href="https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Auto%20Fill/.NET/AutoFillUsingFillSeries">this GitHub page</a>.