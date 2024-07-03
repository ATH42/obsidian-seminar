```dataview
TABLE
WITHOUT ID
link(Source, dateformat(date(source), "DD.MM.YYYY")) as "",
rows.Details as "Details"
FROM !"Templates"
FLATTEN log as Details
WHERE contains(Details, "REPLACE_THIS_WITH_MATCHER")
GROUP BY file.name as Source
SORT rows.day desc
```