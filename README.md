﻿#excel for golang

read and write excel files in golang.

go语言读写excel文件.

#dependency

[github.com/go-ole/go-ole][ole]

#install

go get github.com/aswjh/excel

#example
``` go
package main

import (
	"time"
	"github.com/aswjh/excel"
)

func main() {
	option := excel.Option{"Visible": true, "DisplayAlerts": true}
	xl, _ := excel.New(option)      //xl, _ := excel.Open("test_excel.xls", option)
	defer xl.Quit()

	sheet, _ := xl.Sheet(1)         //xl.Sheet("sheet1")
	sheet.Cells(1, 1, "hello")
	sheet.PutCell(1, 2, 2006)
	sheet.MustCells(1, 3, 3.14159)
	urc := sheet.MustGet("UsedRange", "Rows", "Count").(int32)
	println("str:"+sheet.MustCells(1, 2), sheet.MustGetCell(1, 2).(float64), urc)

	cell := sheet.MustCell(5, 6)
	cell.Put("go")
	cell.Put("font", map[string]interface{}{"name": "Arial", "size": 26, "bold": true})
	cell.Put("interior", "colorindex", 6)

	sheet.PutRange("a3:c3", []string {"@1", "@2", "@3"})
	sheet.Range("d3:f3").Put([]string {"~4", "~5", "~6"})

	time.Sleep(3000000000)
	xl.SaveAs("test_excel.xls")    //xl.SaveAs("test_excel", "html")
}

```

#license

The [BSD 3-Clause license][bsd]

[ole]: http://github.com/go-ole/go-ole
[bsd]: http://opensource.org/licenses/BSD-3-Clause




