The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
William is a Business Class passenger flying from New Orleans to Boston with the following items: 1. A backpack: 19 x 13 x 6 inches, 11 lbs; 2. A luggage box: 50 x 37 x 27 inches, 75 lbs; 3. A backpack: 37 x 15 x 13 inches, 58 lbs; 4. A backpack: 46 x 26 x 23 inches, 87 lbs; 5. A backpack: 36 x 19 x 9 inches, 72 lbs; 6. A backpack: 41 x 28 x 20 inches, 54 lbs; 7. A luggage box: 38 x 26 x 14 inches, 79 lbs; 8. A backpack: 48 x 28 x 24 inches, 52 lbs; William's flight ticket is $269.


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