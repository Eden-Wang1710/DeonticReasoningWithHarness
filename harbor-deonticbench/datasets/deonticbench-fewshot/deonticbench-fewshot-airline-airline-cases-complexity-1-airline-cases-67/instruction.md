The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
Joseph is a First Class passenger flying from Minneapolis to Phoenix with the following items: 1. A backpack: 19 x 11 x 7 inches, 7 lbs; 2. A backpack: 34 x 18 x 11 inches, 70 lbs; 3. A backpack: 48 x 35 x 24 inches, 63 lbs; 4. A luggage box: 33 x 20 x 11 inches, 81 lbs; 5. A luggage box: 44 x 20 x 19 inches, 68 lbs; 6. A backpack: 41 x 30 x 17 inches, 97 lbs; 7. A backpack: 54 x 32 x 27 inches, 60 lbs; 8. A backpack: 46 x 31 x 20 inches, 52 lbs; Joseph's flight ticket is $77.


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