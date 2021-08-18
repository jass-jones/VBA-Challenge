# VBA-Challenge

Sub Homework2()

Dim ws As Worksheet
Dim ticker As String
Dim vol As Integer
Dim year_open As Double
Dim year_close As Double
Dim yearly_change As Double
Dim percent_change As Double
Dim Summary_Table As Long

On Error Resume Next


For Each ws In ThisWorkbook.Worksheets
    ws.Cells(1, 9).Value = "Ticker"
    ws.Cells(1, 10).Value = "Yearly Change"
    ws.Cells(1, 11).Value = "Percent Change"
    ws.Cells(1, 12).Value = "Total Stock Volume"

    Summary_Table = 2
    year_open = ws.Cells(2, 3).Value

For i = 2 To ws.UsedRange.Rows.Count
    If ws.Cells(i + 1, 1).Value <> ws.Cells(i, 1).Value Then
            
            ticker = ws.Cells(i, 1).Value
    
            year_close = ws.Cells(i, 6).Value

            yearly_change = year_close - year_open
            
            If year_open <> 0 Then
                percent_change = (yearly_change / year_open)
                
            End If
            
            vol = vol + ws.Cells(i, 7).Value
            ws.Range("I" & Summary_Table).Value = ticker
            ws.Range("J" & Summary_Table).Value = yearly_change
        
            If (yearly_change > 0) Then
                ws.Range("J" & Summary_Table).Interior.Color = vbRed
                
            ElseIf (yearly_change <= 0) Then
                ws.Range("J" & Summary_Table).Interior.Color = vbGreen
                
            End If
            
            ws.Range("K" & Summary_Table).Value = (CStr(percent_change) & "%")
            
            ws.Range("L" & Summary_Table).Value = vol
            
            open_year = ws.Cells(i + 1, 3).Value
            
            ws.Cells(Summary_Table, 9).Value = ticker
            ws.Cells(Summary_Table, 10).Value = yearly_change
            ws.Cells(Summary_Table, 11).Value = percent_change
            ws.Cells(Summary_Table, 12).Value = vol
            Summary_Table = Summary_Table + 1

    
        
            vol = 0
            percent_change = 0
    

    vol = vol + ws.Cells(i, 7).Value
    
End If

    Next i
Next ws
