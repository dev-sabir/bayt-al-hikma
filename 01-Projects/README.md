# Projects

Active work with a clear finish line.

```dataview
TABLE status, file.mtime as "Last Updated"
FROM "01-Projects"
WHERE type = "project"
SORT file.mtime DESC
```
