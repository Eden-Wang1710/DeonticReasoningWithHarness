The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
John is a Business Class passenger flying from Guangzhou to Salt Lake City with the following items: 1. A backpack: 21 x 11 x 8 inches, 11 lbs; 2. A backpack: 34 x 18 x 11 inches, 52 lbs; 3. A luggage box: 36 x 16 x 13 inches, 53 lbs; 4. A backpack: 37 x 18 x 9 inches, 51 lbs; 5. A backpack: 34 x 21 x 9 inches, 52 lbs; 6. A backpack: 39 x 18 x 11 inches, 52 lbs; 7. A luggage box: 46 x 24 x 22 inches, 59 lbs; 8. A backpack: 44 x 28 x 24 inches, 53 lbs; 9. A luggage box: 35 x 18 x 11 inches, 63 lbs; 10. A luggage box: 43 x 19 x 20 inches, 70 lbs; 11. A backpack: 38 x 18 x 9 inches, 62 lbs; John's flight ticket is $1182.


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