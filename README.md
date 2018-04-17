# Q-Basic-Practice
Using QB64 for Windows 10

Hi, my name is Jake and I have been having trouble with this one particular exercise for coding in QB64 or QBasic. I can't seem to figure out what exactly is making the code not output every single DATA input, it only outputs a few when I run it. I'll post the code below. If anyone could help that would be much appreciated! Thanks! Also code will not look right unless you open to commit on this readme.


' ****************************** CIS - 130 - W1 *****************************
' Jacob Kurbis
' 4/12/18
' Homework: 6_4
' Purpose: A program using control breaks to produce a sales summary for
' charter hours booked for yachts.
' Variables Used:
' Type$ = Type of Yacht
' Size = Size of yacht
' Rate = Rate per hour
' ChrtHrs = Charter Hours
' Revenue = Revenue of Charter Hours * Rate
' SubTotalHrs = Subtotal of the Charter Hours for the type of yacht
' SubTotalRev = Subtotal of the Revenue for the type of yacht
' TotalHrs = Total of all the Charter Hours booked from each yacht
' TotalRev = Total of all Revenue made from each yacht
' LineCt = Line Count
' PageCt = Page Count
' MaxLines = Maximum number of lines per page
' T1$, H1$, H2$, D1$, TL$ = Print Headings
'
' ********* Program Mainline *********
'
CLS
GOSUB InitializeVariables
GOSUB PrintHeadings
GOSUB ProcessDetail
GOSUB PrintTotals
END
'
' ********* Initialize Variables *********
InitializeVariables:
T1$ = "                    SALES SUMMARY  PAGE##"
H1$ = "YACHT TYPE          SIZE   RATE     CHARTER       REVENUE"
D1$ = "\              \     ##    ###.##     ##.##     $##,###.##"
H2$ = "\              \  SUBTOTAL            ##.##     $##,###.##"
TL$ = "               REPORT TOTAL        ###,###.##   $###,###.##"
MaxLines = 30
Return
'
' ********* Print Headings *********
PrintHeadings:
PageCt = PageCt + 1
Print CHR$(12);
Print Using T1$; PageCt
Print
Print
Print H1$
Print
Print
LineCt = 0
Return
'
' ********** Process Detail *********
ProcessDetail:
GOSUB ReadData
TypeSave$ = Type$
DO UNTIL Type$ = "Last Type"
    GOSUB CalculateSubTotal
    IF LineCt >= MaxLines THEN
        GOSUB PrintHeadings
    END IF
    GOSUB PrintDetail
    GOSUB ReadData
    IF TypeSave$ <> Type$ THEN
        GOSUB PrintSubtotals
    END IF
LOOP
Return
'
' ********* Read Data Input *********
ReadData:
READ Type$, Size, Rate, ChrtHrs
DATA RANGER,22,95.00,24
DATA RANGER,22,69.00,12
DATA WAVELENGTH,24,69.00,6
DATA WAVELENGTH,24,89.00,12
DATA CATALINA,27,160.00,24
DATA CATALINA,27,99.00,6
DATA CATALINA,30,190.00,12
DATA CATALINA,30,225.00,24
DATA CORONADO,32,230.00,24
DATA HOBIE,33,192.00,33
DATA HOBIE,33,235.00,24
DATA HOBIE,33,137.00,6
DATA HOBIE,33,235.00,24
DATA C & C,34,290.00,24
DATA C & C,34,175.00,6
DATA CATALINA,36,185.00,6
DATA CATALINA,36,320.00,24
DATA HANS CHRISTIAN,38,400.00,24
DATA HANS CHRISTIAN,38,250.00,6
DATA EXCALIBER,45,550.00,24
DATA EXCALIBER,45,295.00,6
DATA "Last Type",00,00,00
Return
'
' ********* Calculate Subtotal *********
CalculateSubTotal:
Revenue = RATE * CHRTHRS
SubTotalHrs = SubTotalHrs + CHRTHRS
SubTotalRev = SubTotalRev + Revenue
Return
'
' ********* Print Detail *********
PrintDetail:
Print Using D1$; Type$, Size, Rate, ChrtHrs, Revenue
LineCt = LineCt + 1
Return
'
' ********* Print Subtotals *********
PrintSubtotals:
Print
Print Using H2$;TypeSave$, SubTotalHrs, SubTotalRev
Print
TotalHrs = TotalHrs + SubTotalHrs
TotalRev = TotalRev + SubTotalRev
SubTotalHrs = 0
SubTotalRev = 0
LineCt = LineCt + 3
TypeSave$ = Type$
Return
'
' ********* Print Totals *********
PrintTotals:
Print
Print Using TL$; TotalHrs, TotalRev
Print
Return
'
' ***************************** End of Program *****************************
