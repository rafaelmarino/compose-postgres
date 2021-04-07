# Notes on Postgres

## Sorting
Based on UTF-8, PostgreSQL sorts characters in this
order:
1. Punctuation marks, including quotes, parentheses, and math
operators
2. Numbers 0 to 9
3. Additional punctuation, including the question mark
4. Capital letters from A to Z
5. More punctuation, including brackets and underscore
6. Lowercase letters a to z
7. Additional punctuation, special characters, and the extended
alphabet

## Pattern Matching

1) The LIKE operator, which is part of the ANSI SQL standard, is case sensitive
2) The ILIKE operator, which is a PostgreSQL-only implementation, is case insensitive
3) Percent sign ( % ) A wildcard matching one or more characters
4) Underscore ( _ ) A wildcard matching just one character