# Safari-History-Timestamps
Access Safari History Timestamps by accessing History.db


At first copy History.db from ~/Library/Safari/History.db to any other location, the Terminal doesnt have access to it by default.
Then run the following command to safe it in a csv:

~~~
sqlite3 History.db \
    'SELECT
        datetime(V.visit_time+978307200, "unixepoch", "localtime") AS datetime,
        I.url,
        V.title
 FROM history_visits V
 LEFT JOIN history_items I on V.history_item = I.id
 ORDER BY visit_time DESC
 LIMIT 5000;' -header -csv > safari-history.csv
~~~

Taken from https://apple.stackexchange.com/a/322883/496324
