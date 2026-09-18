The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
David is a Business Class passenger flying from Salt Lake City to Atlanta with the following items: 1. A backpack: 18 x 14 x 7 inches, 12 lbs; 2. A backpack: 33 x 20 x 10 inches, 51 lbs; 3. A backpack: 43 x 19 x 19 inches, 66 lbs; 4. A backpack: 49 x 26 x 27 inches, 68 lbs; 5. A backpack: 46 x 22 x 20 inches, 53 lbs; 6. A luggage box: 47 x 26 x 26 inches, 58 lbs; 7. A backpack: 35 x 19 x 11 inches, 53 lbs; 8. A backpack: 51 x 31 x 26 inches, 100 lbs; 9. A backpack: 34 x 20 x 9 inches, 81 lbs; 10. A luggage box: 38 x 16 x 11 inches, 66 lbs; 11. A backpack: 41 x 18 x 14 inches, 59 lbs; David's flight ticket is $194.


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