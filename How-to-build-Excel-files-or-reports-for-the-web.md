# Summary
Often we are asked to make Reports that be sorted or filtered. This can often be done in a flexible way by the system users themselves by providing them an Excel file (i.e., `.xls`, `.xlsx`). This article explains with some examples ways of doing that via a service in a .Net Web project using [EPPlus](https://www.nuget.org/packages/EPPlus).

## Example in Code for Server-Side
One good example of how to make Excel files using .Net is in https://code.cmich.edu/IT-AppDevelopment/Middleware/OcmConnect/blob/master/Api/Services/ExcelService.cs 

### Interface
```c#
using System.Collections.Generic;
using System.IO;
using Cmich.OcmReports.Models;

namespace Cmich.OcmReports.Services
{
    /// <summary>
    /// Service For Generating Excel File
    /// </summary>
    public interface IExcelService
    {
        /// <summary>
        /// Generates Excel for Faculty Content Report
        /// </summary>
        /// <param name="facultyContentReport">List of FacultyContent</param>
        /// <returns>Byte Array</returns>
        byte[] GenerateExcelForNewContentNewFacultyReport(List<FacultyContent> facultyContentReport);
    }
}
```

### Implementation
```c#
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using System.Linq;
using Cmich.OcmReports.Models;
using OfficeOpenXml;
using OfficeOpenXml.Style;

namespace Cmich.OcmReports.Services
{
    /// <inheritdoc />
    public class ExcelService : IExcelService
    {
        /// <inheritdoc />
        public byte[] GenerateExcelForNewContentNewFacultyReport(List<FacultyContent> facultyContentReport)
        {
            var doc = new ExcelPackage();
            var worksheet = doc.Workbook.Worksheets.Add("NewContentNewFaculty");
            worksheet.Cells.LoadFromCollection(facultyContentReport, true);
            worksheet.Cells[1, 1, 1, worksheet.Dimension.End.Column].Style.Font.Bold = true;
            worksheet.Cells[1, 1, 1, worksheet.Dimension.End.Column].Style.Font.Color.SetColor(Color.White);
            worksheet.Cells[1, 1, 1, worksheet.Dimension.End.Column].Style.Fill.PatternType = ExcelFillStyle.Solid;
            worksheet.Cells[1, 1, 1, worksheet.Dimension.End.Column].Style.Fill.BackgroundColor.SetColor(Color.Maroon);
            worksheet.Cells[1, 12, worksheet.Dimension.End.Row, 12].Style.Numberformat.Format = "MM/dd/yyyy";
            worksheet.Cells[1, 15, worksheet.Dimension.End.Row, 15].Style.Numberformat.Format = "MM/dd/yyyy";

            for (var i = 1; i <= worksheet.Dimension.End.Column; i++)
            {
                var cells = worksheet.Cells[worksheet.Dimension.Start.Row, i, worksheet.Dimension.End.Row, i];
                var maxLength = cells.Max(cell =>
                    cell.Value?.ToString().Count(
                        c => char.IsLetterOrDigit(c) || char.IsPunctuation(c))
                );
                worksheet.Column(i).Width = (double)(maxLength + 2);
            }
            return doc.GetAsByteArray();
        }
    }
}
``` 

### Unit tests
```c#
﻿using System;
using System.Collections.Generic;
using Cmich.OcmReports.Models;
using Cmich.OcmReports.Services;
using Microsoft.VisualStudio.TestTools.UnitTesting;

namespace Cmich.OcmReports.Tests.Unit.Services
{
    [TestClass]
    public class ExcelServiceTests
    {
        private ExcelService _excelService;

        [TestInitialize]
        public void Init()
        {
            _excelService = new ExcelService();
        }

        [TestMethod]
        public void ExcelService_GenerateExcelForNewContentNewFacultyReport_ReturnsByteArray()
        {
            //Arrange
            var report = new List<FacultyContent>();
            //Act
            var result = _excelService.GenerateExcelForNewContentNewFacultyReport(report);

            //Assert
            Assert.IsInstanceOfType(result,typeof(byte[]));
        }
    }
}
```

## Example in Code for Client-Side
One good example of how to pull back a .pdf file, which can also be a model for pulling back a .xlsx file, is found in [FinancialAidPortal dashboard component](https://code.cmich.edu/IT-AppDevelopment/CustomApplications/FinancialAidPortal/blob/master/CMich.FinancialAidPortal.Angular/src/app/components/dashboard/dashboard.component.ts#L126)

### Component method to show preview in browser

```ts
getAwardLetter(): void {
    this.printingModal.show();
    this.apiAwardLetter(this.userdto.user.user.globalId, this.userdto.student.user.campusId, this.year).subscribe(
      (pdf) => {
        if (window.navigator && window.navigator.msSaveOrOpenBlob) { // For IE/Edge
          window.navigator.msSaveOrOpenBlob(pdf, "award-letter.pdf");
          this.printingModal.hide();
        } else {
          var url = URL.createObjectURL(pdf);
          window.location.href = url;
        }
      }, (error) => {
        this.ErrorService.add(error.message);
      });
  }
```

### Service method to grab the file as a Blob

```ts
  // this is using Angular 4 
  apiAwardLetter(globalId: string, campusId: string, year: number): Observable<Blob> {
    const awardLetterUrl = this.apiEndpointService.baseUrl + '/v1/reports/awardLetter/' + globalId + '/' + campusId + '/' + year;
    return this.$http
      .get(awardLetterUrl, ({ responseType: ResponseContentType.Blob }) as any)
      .map((response: Response) => {
        return new Blob([response.blob()],
          {
            type:
            'application/pdf'
          });
      });
  }
```

## Tags
[[Excel]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=ExcelTag)
