The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
Karen is a First Class passenger flying from Madrid to Denver with the following items: 1. A backpack: 21 x 11 x 8 inches, 6 lbs; 2. A luggage box: 34 x 17 x 14 inches, 64 lbs; 3. A luggage box: 33 x 21 x 11 inches, 60 lbs; 4. A backpack: 34 x 16 x 13 inches, 53 lbs; 5. A luggage box: 54 x 31 x 26 inches, 69 lbs; 6. A luggage box: 46 x 22 x 21 inches, 58 lbs; 7. A luggage box: 43 x 21 x 17 inches, 56 lbs; 8. A luggage box: 45 x 25 x 20 inches, 54 lbs; 9. A backpack: 33 x 20 x 11 inches, 52 lbs; 10. A backpack: 34 x 16 x 14 inches, 53 lbs; 11. A backpack: 47 x 29 x 22 inches, 67 lbs; Karen's flight ticket is $265.


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