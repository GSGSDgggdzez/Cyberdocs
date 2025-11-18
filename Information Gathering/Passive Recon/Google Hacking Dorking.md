# Google Hacking Dorking

- https://www.exploit-db.com/google-hacking-database/
- https://www.google.com/advanced_search
- https://archive.org/web/
- https://tineye.com/

PDF documents in a specific site or domain can be searched

```c
site:example.com filetype:pdf
```

References to email addresses of a specific domain, excluding the domain's site

```c
"@example" -site:example.com
```

Administrative sites with the word admin in the title or the URL in
example.com 

```c
intitle:admin OR inurl:admin site:example.com
```


You can also look for a specific error message indicating a possible SQL injection
vulnerability

```c
"SQL Server Driver][SQL Server]Line 1: Incorrect syntax near"
 site:example.com
```

Find results with an exact search phrase

```c
"search phrase"
```

Search for files of type `PDF` related to a certain term.

```c
OSINT filetype:pdf
```

Limit search results to a specific site

```c
salary site:blog.tryhackme.com
```

Exclude a specific site from results

```c
pentest -site:example.com
```

Search for pages with a specific term in the page title.

```c
walkthrough intitle:TryHackMe
```

Search in a title

```c
intitle:"index of" "parent directory"
```

