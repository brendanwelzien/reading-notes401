# Class 2 Notes

## Refactoring and Unit Tests (TEST-DRIVEN-DEVELOPMENT)

- unit tests are pieces of code to exercise input, output, and behavior of code
    - test-driven development is a way to write tests first
    - this makes it more dynamic for code to run

- when creating tests we should separate them from *module*

Follow this order for structure...
- Arrange, Act, and Assert

1. Arrange - organize data needed to execute that piece of code input
2. Act - execute code being tested (behavior)
3. Assert - After executing, check result (output) and whether it is same as you were expecting

    - this flows into the `cycle`
    - the `cycle` is...
        1. Write a unit test and make it fail
        2. Write a feature and make the test pass
        3. Refactor the code

    - craft the sofware design first.. when a change occurs you can run tests and everything will flow more easily


## Recursion
- The process in which a function calls itself and the corresponding function is called as *recursive function*

approach 1 - simply adding by one by one
```bash
f(n) = 1 + 2 + 3..... + n
```
approach 2 - Recursive adding
```bash
f(n) = 1     n = 1
f(n) = n + f(n-1) n>1
```
- represent a problem in terms of one or more smaller problems and add more base conditions that stop recursion.
[<-- Back](README.md)