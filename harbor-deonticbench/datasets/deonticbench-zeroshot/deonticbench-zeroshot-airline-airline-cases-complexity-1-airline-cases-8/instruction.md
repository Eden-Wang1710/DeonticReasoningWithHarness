The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
William is a First Class passenger flying from Hong Kong to Las Vegas with the following items: 1. A backpack: 20 x 11 x 8 inches, 8 lbs; 2. A backpack: 38 x 14 x 13 inches, 51 lbs; 3. A luggage box: 49 x 27 x 25 inches, 70 lbs; 4. A backpack: 45 x 30 x 22 inches, 83 lbs; 5. A backpack: 37 x 13 x 13 inches, 53 lbs; 6. A backpack: 47 x 28 x 22 inches, 56 lbs; 7. A backpack: 35 x 17 x 11 inches, 64 lbs; 8. A backpack: 33 x 20 x 12 inches, 53 lbs; William's flight ticket is $1413.


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