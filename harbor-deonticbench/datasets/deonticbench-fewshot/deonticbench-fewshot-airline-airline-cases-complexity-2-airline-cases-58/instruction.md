The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
William is a Business Class passenger flying from Chengdu to Miami with the following items: 1. A backpack: 19 x 11 x 7 inches, 12 lbs; 2. A backpack: 34 x 15 x 14 inches, 55 lbs; 3. A luggage box: 37 x 18 x 17 inches, 81 lbs; 4. A luggage box: 40 x 24 x 14 inches, 64 lbs; 5. A backpack: 38 x 18 x 9 inches, 69 lbs; 6. A luggage box: 37 x 16 x 12 inches, 52 lbs; 7. A luggage box: 35 x 15 x 14 inches, 80 lbs; 8. A luggage box: 50 x 29 x 28 inches, 76 lbs; 9. A backpack: 44 x 28 x 18 inches, 51 lbs; 10. A luggage box: 46 x 28 x 18 inches, 52 lbs; 11. A luggage box: 38 x 20 x 15 inches, 87 lbs; William's flight ticket is $1303.


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