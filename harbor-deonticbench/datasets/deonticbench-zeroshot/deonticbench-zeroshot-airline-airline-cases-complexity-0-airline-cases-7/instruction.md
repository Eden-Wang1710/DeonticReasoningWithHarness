The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
Elizabeth is a First Class passenger flying from Austin to Mumbai with the following items: 1. A backpack: 18 x 14 x 6 inches, 12 lbs; 2. A luggage box: 33 x 23 x 9 inches, 56 lbs; 3. A luggage box: 49 x 27 x 20 inches, 52 lbs; 4. A backpack: 37 x 17 x 10 inches, 58 lbs; 5. A luggage box: 50 x 35 x 30 inches, 53 lbs; Elizabeth's flight ticket is $471.


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