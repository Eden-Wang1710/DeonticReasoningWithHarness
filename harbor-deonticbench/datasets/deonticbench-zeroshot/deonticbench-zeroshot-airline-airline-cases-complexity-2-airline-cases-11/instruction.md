The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
Charles is a First Class passenger flying from Berlin to Seattle with the following items: 1. A backpack: 18 x 12 x 6 inches, 12 lbs; 2. A luggage box: 47 x 29 x 24 inches, 51 lbs; 3. A luggage box: 45 x 20 x 22 inches, 51 lbs; 4. A backpack: 37 x 18 x 10 inches, 60 lbs; 5. A backpack: 39 x 25 x 18 inches, 59 lbs; 6. A luggage box: 37 x 13 x 14 inches, 56 lbs; 7. A backpack: 45 x 27 x 23 inches, 53 lbs; 8. A luggage box: 45 x 23 x 16 inches, 63 lbs; 9. A luggage box: 37 x 15 x 12 inches, 61 lbs; 10. A luggage box: 44 x 20 x 18 inches, 57 lbs; 11. A backpack: 36 x 19 x 17 inches, 55 lbs; Charles's flight ticket is $516.


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