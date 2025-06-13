---
title: FillSeries in Excel Document | Syncfusion
description: In this section, you can learn how to use FillSeries feature in an Excel using Syncfusion Essential XlsIO.
platform: document-processing
control: XlsIO
documentation: UG
---

# FillSeries in Excel Document

The **FillSeries** feature in the Syncfusion Essential&reg; XlsIO library allows users to programmatically fills a range with a sequence of values based on the specified direction (row or column), series type, step value, and stop value.

## DateTime FillSeries

The following code example illustrates how to fill a date series in a worksheet.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" playgroundButtonLink="https://raw.githubusercontent.com/SyncfusionExamples/XlsIO-Examples/master/Worksheet%20Features/Fill%20Series/.NET/DateTime%20FillSeries/DateTime%20FillSeries/Program.cs,180" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Create(1);
    IWorksheet worksheet = workbook.Worksheets[0];

    //Setting the values to the cells
    worksheet["A1"].DateTime = new DateTime(2025, 1, 1);

    //Define the range
    IRange range = worksheet["A1:A10"];

    //Use FillSeries method to fill the values based on ExcelFillSeries
    range.FillSeries(ExcelSeriesBy.Columns, ExcelFillSeries.Years, 3, new DateTime(2060, 1, 1));

    //Saving the workbook 
    FileStream outputStream = new FileStream(Path.GetFullPath("Output.xlsx"), FileMode.Create, FileAccess.Write);
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

    //Setting the values to the cells
    worksheet["A1"].DateTime = new DateTime(2025, 1, 1);

    //Define the range
    IRange range = worksheet["A1:A10"];

    //Use FillSeries method to fill the values based on ExcelFillSeries
    range.FillSeries(ExcelSeriesBy.Columns, ExcelFillSeries.Years, 3, new DateTime(2060, 1, 1));

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

    'Setting the values to the cells
    worksheet("A1").DateTime = New DateTime(2025, 1, 1)

    'Define the range
    Dim range As IRange = worksheet("A1:A10")

    'Use FillSeries method to fill the values based on ExcelFillSeries
    range.FillSeries(ExcelSeriesBy.Columns, ExcelFillSeries.Years, 3, New DateTime(2060, 1, 1))

    'Saving the workbook
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example of how to fill a date series in a worksheet using C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Fill%20Series/.NET/DateTime%20FillSeries).

## Number FillSeries

The following code example illustrates how to fill a number series in a worksheet.

{% tabs %} 
{% highlight c# tabtitle="C# [Cross-platform]" playgroundButtonLink="https://raw.githubusercontent.com/SyncfusionExamples/XlsIO-Examples/master/Worksheet%20Features/Fill%20Series/.NET/Number%20FillSeries/Number%20FillSeries/Program.cs,180" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Create(1);
    IWorksheet worksheet = workbook.Worksheets[0];

    //Setting the values to the cells
    worksheet["A1"].Number = 1;

    //Define the range
    IRange range = worksheet["A1:A10"];

    //Use FillSeries method to fill the values based on ExcelFillSeries
    range.FillSeries(ExcelSeriesBy.Columns, ExcelFillSeries.Linear, 5, 100);

    //Saving the workbook 
    FileStream outputStream = new FileStream(Path.GetFullPath("Output.xlsx"), FileMode.Create, FileAccess.Write);
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

    //Setting the values to the cells
    worksheet["A1"].Number = 1;

    //Define the range
    IRange range = worksheet["A1:A10"];

    //Use FillSeries method to fill the values based on ExcelFillSeries
    range.FillSeries(ExcelSeriesBy.Columns, ExcelFillSeries.Linear, 5, 100);

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

    'Setting the values to the cells
    worksheet("A1").Number = 1

    'Define the range
    Dim range As IRange = worksheet("A1:A10")

    'Use FillSeries method to fill the values based on ExcelFillSeries
    range.FillSeries(ExcelSeriesBy.Columns, ExcelFillSeries.Linear, 5, 100)

    'Saving the workbook
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example of how to fill a number series in a worksheet using C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Fill%20Series/.NET/Number%20FillSeries).

## FillSeries by Enabling Trend

The following code example illustrates how to fill series by enabling trend.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" playgroundButtonLink="https://raw.githubusercontent.com/SyncfusionExamples/XlsIO-Examples/master/Worksheet%20Features/Fill%20Series/.NET/FillSeries%20by%20Enabling%20Trend/FillSeries%20by%20Enabling%20Trend/Program.cs,180" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Create(1);
    IWorksheet worksheet = workbook.Worksheets[0];

    //Setting the values to the cells
    worksheet["A1"].Number = 1;
    worksheet["A2"].Number = 3;
    worksheet["A3"].Number = 2;

    //Define the range
    IRange range = worksheet["A1:A10"];

    //Use FillSeries method to fill the values by enabling trend
    range.FillSeries(ExcelSeriesBy.Columns, ExcelFillSeries.Linear, true);

    //Saving the workbook 
    FileStream outputStream = new FileStream(Path.GetFullPath("Output.xlsx"), FileMode.Create, FileAccess.Write);
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

    //Setting the values to the cells
    worksheet["A1"].Number = 1;
    worksheet["A2"].Number = 3;
    worksheet["A3"].Number = 2;

    //Define the range
    IRange range = worksheet["A1:A10"];

    //Use FillSeries method to fill the values by enabling trend
    range.FillSeries(ExcelSeriesBy.Columns, ExcelFillSeries.Linear, true);

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

    'Setting the values to the cells
    worksheet("A1").Number = 1
    worksheet("A2").Number = 3
    worksheet("A3").Number = 2

    'Define the range
    Dim range As IRange = worksheet("A1:A10")

    'Use FillSeries method to fill the values by enabling trend
    range.FillSeries(ExcelSeriesBy.Columns, ExcelFillSeries.Linear, True)

    'Saving the workbook
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example of how to fill series by enabling trend in a worksheet using C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Fill%20Series/.NET/FillSeries%20by%20Enabling%20Trend).

