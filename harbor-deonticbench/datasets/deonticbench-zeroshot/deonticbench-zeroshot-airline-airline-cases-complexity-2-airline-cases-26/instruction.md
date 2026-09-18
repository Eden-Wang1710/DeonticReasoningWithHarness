The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
Emily is a First Class passenger flying from Austin to Shanghai with the following items: 1. A backpack: 18 x 13 x 6 inches, 6 lbs; 2. A backpack: 42 x 24 x 14 inches, 89 lbs; 3. A backpack: 50 x 28 x 24 inches, 95 lbs; 4. A backpack: 35 x 17 x 11 inches, 52 lbs; 5. A backpack: 51 x 36 x 27 inches, 64 lbs; 6. A luggage box: 50 x 36 x 25 inches, 53 lbs; 7. A backpack: 33 x 23 x 9 inches, 66 lbs; 8. A luggage box: 37 x 19 x 9 inches, 81 lbs; 9. A luggage box: 38 x 14 x 11 inches, 64 lbs; 10. A luggage box: 38 x 16 x 9 inches, 52 lbs; 11. A luggage box: 40 x 26 x 15 inches, 78 lbs; Emily's flight ticket is $858.


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