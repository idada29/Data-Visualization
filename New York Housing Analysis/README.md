


![Final Viz1024_1](https://user-images.githubusercontent.com/22597020/220607414-e76d89bf-cc69-484a-a002-8a761aa305f6.png)


let.


    Source = Csv.Document(File.Contents("C:\Users\dadai\Documents\All Projects\Power BI Project\Housing Project - New Y\nyc-rolling-sales.csv\New York Housing Sales.csv"),[Delimiter=",", Columns=22, Encoding=1252, QuoteStyle=QuoteStyle.Csv]),
    #"Promoted Headers" = Table.PromoteHeaders(Source, [PromoteAllScalars=true]),
    #"Changed Type" = Table.TransformColumnTypes(#"Promoted Headers",{{"BOROUGH#(lf)", Int64.Type}, {"NEIGHBORHOOD#(lf)", type text}, {"BUILDING CLASS CATEGORY#(lf)", type text}, {"TAX CLASS AS OF FINAL ROLL 17/18", type text}, {"BLOCK#(lf)", Int64.Type}, {"LOT#(lf)", Int64.Type}, {"EASE-MENT#(lf)", type text}, {"BUILDING CLASS AS OF FINAL ROLL 17/18", type text}, {"ADDRESS#(lf)", type text}, {"APARTMENT NUMBER#(lf)", type text}, {"ZIP CODE#(lf)", Int64.Type}, {"RESIDENTIAL UNITS#(lf)", Int64.Type}, {"COMMERCIAL UNITS#(lf)", Int64.Type}, {"TOTAL UNITS#(lf)", Int64.Type}, {"LAND SQUARE FEET#(lf)", Int64.Type}, {"GROSS SQUARE FEET#(lf)", Int64.Type}, {"Year Built", Int64.Type}, {"TAX CLASS AT TIME OF SALE#(lf)", Int64.Type}, {"BUILDING CLASS AT TIME OF SALE#(lf)", type text}, {"Sale Price#(lf)", Int64.Type}, {"Date#(lf)", type date}, {"Borough Name", type text}}),
    #"Removed Columns" = Table.RemoveColumns(#"Changed Type",{"NEIGHBORHOOD#(lf)", "BUILDING CLASS CATEGORY#(lf)", "TAX CLASS AS OF FINAL ROLL 17/18", "BLOCK#(lf)", "LOT#(lf)", "EASE-MENT#(lf)", "BUILDING CLASS AS OF FINAL ROLL 17/18", "ADDRESS#(lf)", "APARTMENT NUMBER#(lf)", "ZIP CODE#(lf)", "RESIDENTIAL UNITS#(lf)", "COMMERCIAL UNITS#(lf)", "TOTAL UNITS#(lf)", "LAND SQUARE FEET#(lf)", "GROSS SQUARE FEET#(lf)", "TAX CLASS AT TIME OF SALE#(lf)", "BUILDING CLASS AT TIME OF SALE#(lf)", "BOROUGH#(lf)", "Year Built"}),
    #"Reordered Columns" = Table.ReorderColumns(#"Removed Columns",{"Date#(lf)", "Borough Name", "Sale Price#(lf)"}),
    #"Removed Columns1" = Table.RemoveColumns(#"Reordered Columns",{"Sale Price#(lf)", "Borough Name"}),
    #"Removed Duplicates" = Table.Distinct(#"Removed Columns1"),
    #"Duplicated Column" = Table.DuplicateColumn(#"Removed Duplicates", "Date#(lf)", "Date#(lf) - Copy"),
    #"Extracted Day" = Table.TransformColumns(#"Duplicated Column",{{"Date#(lf) - Copy", Date.Day, Int64.Type}}),
    #"Renamed Columns" = Table.RenameColumns(#"Extracted Day",{{"Date#(lf) - Copy", "Day of Month"}}),
    #"Duplicated Column1" = Table.DuplicateColumn(#"Renamed Columns", "Date#(lf)", "Date#(lf) - Copy"),
    #"Extracted Day Name" = Table.TransformColumns(#"Duplicated Column1", {{"Date#(lf) - Copy", each Date.DayOfWeekName(_), type text}}),
    #"Renamed Columns1" = Table.RenameColumns(#"Extracted Day Name",{{"Date#(lf) - Copy", "Day of Week Name"}}),
    #"Duplicated Column2" = Table.DuplicateColumn(#"Renamed Columns1", "Day of Week Name", "Day of Week Name - Copy"),
    #"Extracted First Characters" = Table.TransformColumns(#"Duplicated Column2", {{"Day of Week Name - Copy", each Text.Start(_, 1), type text}}),
    #"Renamed Columns2" = Table.RenameColumns(#"Extracted First Characters",{{"Day of Week Name - Copy", "Day of Week Initial"}}),
    #"Duplicated Column3" = Table.DuplicateColumn(#"Renamed Columns2", "Date#(lf)", "Date#(lf) - Copy"),
    #"Calculated Day of Week" = Table.TransformColumns(#"Duplicated Column3",{{"Date#(lf) - Copy", Date.DayOfWeek, Int64.Type}}),
    #"Renamed Columns3" = Table.RenameColumns(#"Calculated Day of Week",{{"Date#(lf) - Copy", "Day of Week Number"}}),
    #"Duplicated Column4" = Table.DuplicateColumn(#"Renamed Columns3", "Date#(lf)", "Date#(lf) - Copy"),
    #"Renamed Columns4" = Table.RenameColumns(#"Duplicated Column4",{{"Date#(lf) - Copy", "Month"}}),
    #"Extracted Month" = Table.TransformColumns(#"Renamed Columns4",{{"Month", Date.Month, Int64.Type}}),
    #"Duplicated Column5" = Table.DuplicateColumn(#"Extracted Month", "Date#(lf)", "Date#(lf) - Copy"),
    #"Renamed Columns5" = Table.RenameColumns(#"Duplicated Column5",{{"Date#(lf) - Copy", "Month Name"}}),
    #"Extracted Month Name" = Table.TransformColumns(#"Renamed Columns5", {{"Month Name", each Date.MonthName(_), type text}}),
    #"Duplicated Column6" = Table.DuplicateColumn(#"Extracted Month Name", "Date#(lf)", "Date#(lf) - Copy"),
    #"Duplicated Column7" = Table.DuplicateColumn(#"Duplicated Column6", "Date#(lf) - Copy", "Date#(lf) - Copy - Copy"),
    #"Extracted Last Characters" = Table.TransformColumns(#"Duplicated Column7", {{"Date#(lf) - Copy", each Text.End(Text.From(_, "en-GB"), 4), type text}}),
    #"Extracted Text Range" = Table.TransformColumns(#"Extracted Last Characters", {{"Date#(lf) - Copy - Copy", each Text.Middle(Text.From(_, "en-GB"), 3, 2), type text}}),
    #"Added Custom" = Table.AddColumn(#"Extracted Text Range", "MonthnYear", each [#"Date#(lf) - Copy"]&[#"Date#(lf) - Copy - Copy"]),
    #"Removed Columns2" = Table.RemoveColumns(#"Added Custom",{"Date#(lf) - Copy", "Date#(lf) - Copy - Copy"}),
    #"Changed Type1" = Table.TransformColumnTypes(#"Removed Columns2",{{"MonthnYear", Int64.Type}}),
    #"Duplicated Column8" = Table.DuplicateColumn(#"Changed Type1", "Date#(lf)", "Date#(lf) - Copy"),
    #"Inserted Quarter" = Table.AddColumn(#"Duplicated Column8", "Quarter", each Date.QuarterOfYear([#"Date#(lf) - Copy"]), Int64.Type),
    #"Renamed Columns6" = Table.RenameColumns(#"Inserted Quarter",{{"Quarter", "Quarter Number"}}),
    #"Inserted Week of Year" = Table.AddColumn(#"Renamed Columns6", "Week of Year", each Date.WeekOfYear([#"Date#(lf) - Copy"]), Int64.Type),
    #"Renamed Columns7" = Table.RenameColumns(#"Inserted Week of Year",{{"Week of Year", "Week Number"}}),
    #"Removed Columns3" = Table.RemoveColumns(#"Renamed Columns7",{"Date#(lf) - Copy"}),
    #"Duplicated Column9" = Table.DuplicateColumn(#"Removed Columns3", "Date#(lf)", "Date#(lf) - Copy"),
    #"Extracted Month1" = Table.TransformColumns(#"Duplicated Column9",{{"Date#(lf) - Copy", Date.Month, Int64.Type}}),
    #"Renamed Columns8" = Table.RenameColumns(#"Extracted Month1",{{"Date#(lf) - Copy", "Month Number"}})
in
    #"Renamed Columns8"
