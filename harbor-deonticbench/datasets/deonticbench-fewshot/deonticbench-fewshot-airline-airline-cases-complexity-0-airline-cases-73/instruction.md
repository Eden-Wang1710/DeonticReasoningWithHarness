The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
Daniel is a Business Class passenger flying from Brussels to Philadelphia with the following items: 1. A backpack: 19 x 13 x 6 inches, 11 lbs; 2. A luggage box: 36 x 17 x 12 inches, 64 lbs; 3. A backpack: 37 x 22 x 12 inches, 51 lbs; 4. A backpack: 40 x 21 x 20 inches, 51 lbs; 5. A backpack: 33 x 21 x 10 inches, 65 lbs; Daniel's flight ticket is $519.


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