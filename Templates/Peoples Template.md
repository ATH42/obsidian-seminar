---
name: <% tp.file.title %>
aliases: 
date-created: <% tp.date.tomorrow %>
location: 
---
# <% tp.file.title %>
> [! ]
>  
> **Links**
> []()
> 
> **Relationships**
>  


```dataview
TABLE
rows.Details as "Details"
WHERE contains(log, this.file.name)
FLATTEN log as Details
WHERE contains(Details, this.file.name)
GROUP BY file.link as Source
SORT rows.file.day desc
```