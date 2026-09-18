The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
Mary is a Business Class passenger flying from Orlando to Los Angeles with the following items: 1. A backpack: 22 x 13 x 7 inches, 7 lbs; 2. A backpack: 41 x 24 x 22 inches, 85 lbs; 3. A backpack: 47 x 33 x 22 inches, 63 lbs; 4. A backpack: 38 x 12 x 14 inches, 57 lbs; 5. A backpack: 35 x 19 x 9 inches, 87 lbs; 6. A luggage box: 33 x 19 x 13 inches, 63 lbs; 7. A backpack: 35 x 19 x 9 inches, 53 lbs; 8. A luggage box: 50 x 32 x 29 inches, 75 lbs; Mary's flight ticket is $291.


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