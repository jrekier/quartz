---
tags: [Podcast]
# date: {{Date}}
---
![]({{ImageURL}})
## Description:
{{Description}}
-> [Podcast Link]({{PodcastURL}})

# Literature note(s)
```dataview
TABLE without ID 
	file.link AS "Literature Note(s)", 
	file.cday AS "Date",
	file.mday AS "Last modified"
FROM "2 Literature notes" AND [[🎙️ {{Title}}]]
sort date ASCENDING
```

