The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
Jennifer is a First Class passenger flying from Chicago to Helsinki with the following items: 1. A backpack: 20 x 12 x 7 inches, 5 lbs; 2. A backpack: 37 x 18 x 17 inches, 64 lbs; 3. A backpack: 33 x 20 x 12 inches, 53 lbs; 4. A backpack: 52 x 28 x 29 inches, 52 lbs; 5. A backpack: 36 x 20 x 9 inches, 52 lbs; 6. A backpack: 51 x 33 x 24 inches, 62 lbs; 7. A luggage box: 50 x 31 x 30 inches, 52 lbs; 8. A backpack: 34 x 16 x 13 inches, 58 lbs; 9. A backpack: 52 x 36 x 27 inches, 52 lbs; 10. A backpack: 36 x 17 x 12 inches, 61 lbs; 11. A luggage box: 33 x 21 x 9 inches, 69 lbs; Jennifer's flight ticket is $204.


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