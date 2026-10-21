| # | Category | Result | Where |
|---|----------|--------|-------|
| 1 | Initialization | Issue | `sum` uninitialized (77); `monsters[]` never initialized (27) |
| 2 | Pointers (null/delete) | Issue | Null dereference (54-56, 71-72); use after delete (85-86); `delete` vs `delete[]` (109); leak (121) |
| 3 | Arrays / buffers | Issue | No bounds check (41, 119); `cin >> name` overflows a 10-char buffer (102, 105) |
| 4 | Loops | Issue | `i <= monsterCount` reads past the end (64) |
| 5 | Arithmetic | Issue | Unsigned subtraction (55-56); integer division (91); truncation and divide by zero (80) |
| 6 | Control flow | Issue | `=` instead of `==` (47); missing return path (94-99) |
| 7 | Function call | Issue | `findMonster` result never checked (54, 71, 84); returns reference to a local (70-73) |
| 8 | Classes | Issue | Shallow copy and no copy constructor or assignment operator (133, 35-38) |
