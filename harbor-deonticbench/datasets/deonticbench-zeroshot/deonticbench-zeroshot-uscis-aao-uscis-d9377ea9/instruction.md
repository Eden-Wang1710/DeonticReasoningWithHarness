The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
The Petitioner filed Form I-918 seeking U-1 nonimmigrant classification as a victim of qualifying criminal activity in June 2015. The Nebraska Service Center denied the petition, and the Petitioner appealed that denial to the Administrative Appeals Office and later filed motions to reopen and reconsider.

As part of the record, the Petitioner submitted three Form I-918 Supplement B certifications: one signed in July 2014, one signed in October 2019, and one signed in June 2020 by an individual identified as C‑R‑. On motion, the Petitioner provided a letter from the certifying agency stating that C‑R‑ was a designated certifying official at the time she signed the June 2020 Supplement B. The Petitioner’s asserted basis for the appeal and for seeking reopening/reconsideration was that the June 2020 Supplement B was properly signed and executed by a properly designated certifying official, and therefore the prior denial and dismissal were erroneous.


**Question:**
Should this case be accepted or dismissed?

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

The answer is exactly "Accepted" or "Dismissed". E.g., `Answer: Accepted`

The task is complete once `swipl -q -f /app/solution.pl` runs without errors and prints the `Answer:` line.