---
type: daily
date: <% tp.file.title %>
---
# <% tp.file.title %> - Daily Note
> **Previous Day::** [[<% tp.date.now("YYYY-MM-DD", -1, tp.file.title, "YYYY-MM-DD") %>]]
> **Next Day::** [[<% tp.date.now("YYYY-MM-DD", +1, tp.file.title, "YYYY-MM-DD") %>]]
> **Parent::** [[<% tp.date.now("YYYY-MM", 0, tp.file.title, "YYYY-MM-DD") %>]], [[<% tp.date.now("YYYY-[W]ww", 0, tp.file.title, "YYYY-MM-DD") %>]]
> ---
### New Tasks

## Logs
> [! orbit]- Daily Logs
> 
> 

## Good Morning, Now say it back.
> [! sun]- Morning Review
>  ### Log morning
> log_sleep_hours:: 0
> log_sleep_rating:: 0
> log_wake_time:: 0
> log_weight:: 0
>
> log_morning_review::  #on/morningReview
>  
>> [! bird]- acumulated tasks 
>> ####  ✅ Acumulated Tasks:
>> ```dataview
>> TASK 
>> FROM "Journal"
>> WHERE !completed and !task.title
>> GROUP BY file.link
> 
> ___ 
> 
>>[! todo]  Urgent and Today:
>>```dataview
>> TASK 
>> FROM "Journal"
>> WHERE !completed and contains(text, "⏫")
>> GROUP BY file.link 

## Pictures
 ### <% tp.file.title %> 
> [! image] Pictures
>
>  
>
>

## Tracking
> [! scroll]- Overall Tracking
> ### 🏃 Exercise
> - log_cycling:: 0
> - log_stretching:: 0
> - log_meditation:: 0
>- log_strength:: 0
> 
> ### 🍜 Consumable
> + log_water:: 0
> + log_coffee:: 0
> + log_food:: 
> + healthy_eating:: 0
>  
> ### 🃏 Habits
> - reading_habit:: 0
> - gamedev_habit:: 0
> 
> ### ⌛ Time Tracking
> - Creative_time:: 0
> - Distraction_time:: 0 
> - Maintenance_time:: 0 
> - Personal_development_time:: 0
> - Relationship_time:: 0
> - Play_time:: 0
> - Wellness_time:: 0
> - Work_time:: 0

## Evening Review
> [! bed]- Before Bed
> - log_day_review:: The Day that i... #on/dayReview
> - log_day_rating:: 0
>
>  ### Songs of the day
>  log_song::   #on/dailySong
>
## Files
> [! files]- Files Created and Updated
>> ### 🗃️ which files we created this day
>> ``` dataview
>> LIST
>> FROM !"Templates"
>> WHERE file.cday =  this.file.day
>> SORT file.ctime desc
>
>> ### 🗄️ which files were last modified this day
>> ``` dataview
>> list
>> FROM !"Templates" and !"MOC"
>> where file.mday = this.file.day
>> sort file.mtime desc
> 

