---
title: "🦆 DuckDB may be the tool you didn't know you were missing"
date: "2024-07-13T09:31:37-05:00"
url: "/2024/07/13/duckdb-may-be-the-tool/"
type: "post"
feed_id: "http://webology.micro.blog/2024/07/13/duckdb-may-be-the-tool/"
categories: ["Python"]
aliases: ["/2024/07/12/duckdb-may-be.html"]
---

🤔 I haven't fully figured out [DuckDB](https://duckdb.org) yet, but it's worth trying out if you are a Python dev who likes to work on data projects or gets frequently tasked with data import projects. 

DuckDB is a fast database engine that lets you read CSV, Parquet, and JSON files and query them using SQL. Instead of importing data into your database, DuckDB enables you to write SQL and run it against these file types. 

I have a YouTube to frontmatter project that can read a YouTube playlist and write out each video to a markdown file. I modified the export script to save the raw JSON output to disk. 

I used DuckDB to read a bunch of JSON files using the following script:

```python
import duckdb

def main():
    result = duckdb.sql("SELECT id,snippet FROM read_json('data/*.json')").fetchall()

    for row in result:
        id, snippet = row
        print(f"{id=}")
        print(snippet["channelTitle"])
        print(snippet["title"])
        print(snippet["publishedAt"])
        print(snippet["description"])
        print()


if __name__ == "__main__":
    main()
```

This script accomplishes several things:

- It reads over 650 JSON files in about one second.
- It uses SQL to query the JSON data directly.
- It extracts specific fields (id and snippet) from each JSON file. 

## Performance and Ease of Use

The speed at which DuckDB processes these files is remarkable. In traditional setups, reading and parsing this many JSON files could take significantly longer and require more complex code.

## When to Use DuckDB

DuckDB shines in scenarios where you need to:

- Quickly analyze data in files without a formal import process.
- Perform SQL queries on semi-structured data (like JSON)
- Process large datasets efficiently on a single machine.

## Conclusion

DuckDB is worth trying out in your data projects. If you have a lot of data and you need help with what to do with it, being able to write SQL against hundreds of files is powerful and flexible.
