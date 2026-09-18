The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
Susan is a Business Class passenger flying from Chicago to Hong Kong with the following items: 1. A backpack: 21 x 13 x 6 inches, 12 lbs; 2. A luggage box: 37 x 15 x 12 inches, 66 lbs; 3. A luggage box: 46 x 29 x 27 inches, 51 lbs; 4. A backpack: 38 x 20 x 13 inches, 53 lbs; 5. A luggage box: 40 x 23 x 20 inches, 62 lbs; 6. A luggage box: 33 x 20 x 12 inches, 63 lbs; 7. A backpack: 53 x 34 x 27 inches, 53 lbs; 8. A luggage box: 46 x 30 x 25 inches, 65 lbs; Susan's flight ticket is $1055.


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