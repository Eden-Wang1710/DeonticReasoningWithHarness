The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
James is a Business Class passenger flying from Lima to Denver with the following items: 1. A backpack: 20 x 14 x 7 inches, 11 lbs; 2. A backpack: 34 x 20 x 10 inches, 51 lbs; 3. A backpack: 49 x 33 x 27 inches, 88 lbs; 4. A luggage box: 37 x 17 x 9 inches, 61 lbs; 5. A luggage box: 43 x 29 x 20 inches, 53 lbs; 6. A backpack: 33 x 20 x 12 inches, 52 lbs; 7. A luggage box: 35 x 20 x 9 inches, 56 lbs; 8. A backpack: 36 x 17 x 10 inches, 87 lbs; 9. A luggage box: 51 x 32 x 29 inches, 53 lbs; 10. A luggage box: 34 x 18 x 12 inches, 94 lbs; 11. A backpack: 54 x 32 x 27 inches, 57 lbs; James's flight ticket is $533.


**Question:**
What is the total cost (including the flight ticket fee, checked bag fees, cost of special needs) according to the policies for the passenger?

Write a complete, runnable SWI-Prolog program at `/app/solution.pl` that:
1. Encodes the relevant rules from the statute as Prolog clauses
2. Encodes the case facts as Prolog facts
3. Derives the answer to the question
4. Prints the answer on a single line in exactly this format: `Answer: <value>`
5. Calls `:- halt.`

**Use `swipl` to verify your program as you go:**
```
swipl -q -f /app/solution.pl
```
Check the output for syntax errors or warnings. If any errors appear, fix them and re-run until the program executes cleanly and prints the expected `Answer:` line.

The answer is a whole number (total cost in dollars, no $ sign). E.g., `Answer: 1166`

The task is complete once `swipl -q -f /app/solution.pl` runs without errors and prints the `Answer:` line.