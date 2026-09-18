The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
Patricia is a Main Cabin Class passenger flying from San Francisco to Melbourne with the following items: 1. A backpack: 18 x 13 x 8 inches, 5 lbs; 2. A backpack: 40 x 25 x 14 inches, 57 lbs; 3. A luggage box: 33 x 21 x 10 inches, 66 lbs; 4. A luggage box: 38 x 13 x 12 inches, 52 lbs; 5. A luggage box: 43 x 20 x 18 inches, 52 lbs; 6. A backpack: 52 x 26 x 28 inches, 52 lbs; 7. A luggage box: 36 x 16 x 13 inches, 53 lbs; 8. A backpack: 38 x 15 x 12 inches, 67 lbs; 9. A backpack: 39 x 21 x 13 inches, 51 lbs; 10. A luggage box: 49 x 28 x 28 inches, 55 lbs; 11. A backpack: 48 x 33 x 28 inches, 68 lbs; Patricia's flight ticket is $744.


**Question:**
What is the total cost (including the flight ticket fee, checked bag fees, cost of special needs) according to the policies for the passenger?

Review the examples in `/app/examples.txt` to understand the expected Prolog structure,
then write a complete, runnable SWI-Prolog program at `/app/solution.pl` that:
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