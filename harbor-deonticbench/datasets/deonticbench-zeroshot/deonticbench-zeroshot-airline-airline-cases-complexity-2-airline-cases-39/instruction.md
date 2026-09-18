The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
Michael is a Business Class passenger flying from New Orleans to Orlando with the following items: 1. A backpack: 19 x 12 x 8 inches, 11 lbs; 2. A backpack: 34 x 22 x 9 inches, 56 lbs; 3. A luggage box: 35 x 19 x 11 inches, 53 lbs; 4. A luggage box: 43 x 20 x 19 inches, 64 lbs; 5. A backpack: 35 x 17 x 12 inches, 51 lbs; 6. A luggage box: 40 x 24 x 14 inches, 73 lbs; 7. A backpack: 49 x 32 x 29 inches, 51 lbs; 8. A luggage box: 46 x 23 x 19 inches, 69 lbs; 9. A backpack: 49 x 32 x 28 inches, 99 lbs; 10. A luggage box: 33 x 17 x 14 inches, 51 lbs; 11. A backpack: 46 x 26 x 22 inches, 61 lbs; Michael's flight ticket is $294.


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