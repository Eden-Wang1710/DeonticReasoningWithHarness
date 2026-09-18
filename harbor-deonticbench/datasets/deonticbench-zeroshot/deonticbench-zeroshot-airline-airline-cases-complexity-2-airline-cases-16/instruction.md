The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
Jennifer is a First Class passenger flying from Austin to Doha with the following items: 1. A backpack: 21 x 12 x 7 inches, 8 lbs; 2. A luggage box: 55 x 32 x 27 inches, 53 lbs; 3. A backpack: 37 x 15 x 12 inches, 53 lbs; 4. A backpack: 37 x 18 x 10 inches, 51 lbs; 5. A luggage box: 42 x 24 x 14 inches, 52 lbs; 6. A luggage box: 48 x 23 x 25 inches, 68 lbs; 7. A luggage box: 35 x 19 x 10 inches, 55 lbs; 8. A backpack: 36 x 14 x 13 inches, 66 lbs; 9. A luggage box: 44 x 26 x 16 inches, 56 lbs; 10. A backpack: 37 x 27 x 13 inches, 52 lbs; 11. A backpack: 35 x 20 x 9 inches, 53 lbs; Jennifer's flight ticket is $1165.


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