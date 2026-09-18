The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
Linda is a Business Class passenger flying from Kyoto to Sacramento with the following items: 1. A backpack: 22 x 13 x 9 inches, 6 lbs; 2. A backpack: 41 x 22 x 21 inches, 63 lbs; 3. A luggage box: 47 x 23 x 20 inches, 96 lbs; 4. A backpack: 36 x 20 x 9 inches, 53 lbs; 5. A backpack: 48 x 27 x 23 inches, 69 lbs; 6. A backpack: 38 x 13 x 12 inches, 100 lbs; 7. A backpack: 38 x 11 x 14 inches, 53 lbs; 8. A backpack: 36 x 18 x 11 inches, 68 lbs; 9. A luggage box: 41 x 29 x 18 inches, 90 lbs; 10. A luggage box: 49 x 34 x 29 inches, 91 lbs; 11. A luggage box: 45 x 27 x 20 inches, 73 lbs; Linda's flight ticket is $598.


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