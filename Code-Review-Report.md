| Line | Defect type | Why it is a problem | Proposed solution | Severity |
|------|-------------|---------------------|-------------------|----------|
| 41 (triggered at 119, 108) | Array / buffer overflow | `spawnMonster` never checks `monsterCount < MAX_MONSTERS`. The 6th monster in `main` (and the boss in `readBoss`) writes past the array. | Check `monsterCount < MAX_MONSTERS` before adding; return false or report an error if full. | High |
| 47 | Control flow / logic | `=` assigns instead of comparing. It overwrites every monster's id and always returns the first monster. | Use `==`. | High |
| 54-56 (call at 123) | Null pointer dereference | `findMonster(99)` returns `nullptr` and `m->health` is then dereferenced. | Check `if (!m) return -1;` before use. | High |
| 55-56 | Arithmetic (signed/unsigned) | `m->health - dmg` is unsigned, so it is never `< 0`, and a negative `damage` becomes a huge value. Line 58 also uses `damage` rather than `dmg`. | Use `int` throughout: `if (m->health - damage < 0)`. Validate `damage >= 0`. | High |
| 64 | Loop off-by-one | `i <= monsterCount` reads `monsters[monsterCount]`, an invalid or uninitialized pointer. | Use `i < monsterCount`. | High |
| 70-73 | Function / dangling reference | Returns a reference to the local `label`, which is destroyed on return (undefined behavior). | Return `std::string` by value. | High |
| 71-72 | Null pointer dereference | `m` is not checked before `m->id`. | Check for `nullptr` and return an empty or error label. | Medium |
| 77 | Initialization | `double sum;` is uninitialized, so the result is garbage. | `double sum = 0;` | High |
| 80 | Arithmetic / divide by zero | Divides by `monsterCount`, which can be 0. A `double` result is also truncated to `int`. | Check `monsterCount == 0`; return `double`. | Medium |
| 85-86 | Pointer / use after free | `m` is deleted and then `m->name` is read. The pointer also stays in `monsters[]`, so the destructor deletes it again (double free). | Print before delete, remove the entry from the array and shift or null it, and check `m != nullptr`. | High |
| 91 | Arithmetic | `attack * armorPercent / 100` is integer division, so the fraction is lost (80×25/100 gives 20, but 7×25/100 gives 1, not 1.75). | `return attack * armorPercent / 100.0;` | Medium |
| 94-99 | Control flow / missing return | If `score <= 100`, no value is returned (undefined behavior). `main` calls it with 50. | Add a final `else return 3;` (or a default return). | High |
| 102, 105 | Buffer overflow | `cin >> name` into a 10-byte buffer has no length limit. | Use `std::string name;` with `cin >> name`. | High |
| 109 | Pointer / wrong delete | `new[]` memory is freed with `delete` (undefined behavior). | `delete[] name;`, or avoid it by using `std::string`. | High |
| 121 | Memory leak | `bonus` is allocated with `new` and never deleted. | `delete bonus;` or use a stack object or `unique_ptr`. | Medium |
| 133 | Class / shallow copy | `Game copy = game;` copies the raw pointers. Both objects delete the same monsters (double free). | Add a copy constructor and assignment operator (deep copy), or delete them, or use `std::unique_ptr` or `std::vector`. | High |
| 27, 32 | Initialization | The `monsters[]` pointers are not initialized. | `Monster* monsters[MAX_MONSTERS] = {};` | Low |
| 125 | Logic / output | The stray `file:///C:/...` text inside the string literal prints junk in the output. | Change it to `"Total health: "`. | Low |
