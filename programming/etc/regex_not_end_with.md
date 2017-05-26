## Regex not end with

Solution: `/.*(?<!SomeText)$/`

Example:

`/John.*(?<!html)$/`

- **Johnnash**
- Good**Johngrate**
- GoodJohn.html

Reference: http://stackoverflow.com/questions/3178795/how-to-match-a-string-that-does-not-end-in-a-certain-substring
