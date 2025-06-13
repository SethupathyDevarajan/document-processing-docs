---
title: AutoFill in Excel Document | Syncfusion
description: In this section, you can learn how to use AutoFill feature in an Excel using Syncfusion Essential XlsIO.
platform: document-processing
control: XlsIO
documentation: UG
---

# AutoFill in Excel Document

The **AutoFill** feature in the Syncfusion Essential&reg; XlsIO library enables users to populate a destination range based on patterns or values defined in a source range, simulating Excel’s built-in AutoFill behavior for series, formatting, and more.

## AutoFill Based On Excel AutoFill Type

The following code example illustrates how to autofill a series in a worksheet.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" playgroundButtonLink="https://raw.githubusercontent.com/SyncfusionExamples/XlsIO-Examples/master/Worksheet%20Features/AutoFill/.NET/AutoFill%20Using%20ExcelAutoFillType/AutoFill%20Using%20ExcelAutoFillType/Program.cs,180" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Create(1);
    IWorksheet worksheet = workbook.Worksheets[0];

    //Setting the values to the cells
    worksheet["A1"].Number = 1;
    worksheet["A2"].Number = 3;
    worksheet["A3"].Number = 5;

    //Define the source range
    IRange source = worksheet["A1:A3"];

    //Define the destination range
    IRange destinationRange = worksheet["A4:A10"];

    //Use AutoFill method to fill the values based on ExcelAutoFillType
    source.AutoFill(destinationRange, ExcelAutoFillType.FillSeries);

    //Saving the workbook as stream
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
    worksheet["A3"].Number = 5;

    //Define the source range
    IRange source = worksheet["A1:A3"];

    //Define the destination range
    IRange destinationRange = worksheet["A4:A10"];

    //Use AutoFill method to fill the values based on ExcelAutoFillType
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

    'Setting the values to the cells
    worksheet("A1").Number = 1
    worksheet("A2").Number = 3
    worksheet("A3").Number = 5

    'Define the source range
    Dim source As IRange = worksheet("A1:A3")

    'Define the destination range
    Dim destinationRange As IRange = worksheet("A4:A10")

    'Use AutoFill method to fill the values based on ExcelAutoFillType
    source.AutoFill(destinationRange, ExcelAutoFillType.FillSeries)

    'Saving the workbook
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example of how to autofill a series in a worksheet using C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/AutoFill/.NET/AutoFill%20Using%20ExcelAutoFillType).
