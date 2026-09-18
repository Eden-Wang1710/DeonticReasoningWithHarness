The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
The petitioner is a citizen of El Salvador who unlawfully crossed the U.S. border in June 2012 and was apprehended the next day. She was placed in expedited removal but temporarily released under an order of supervision and reported to Immigration and Customs Enforcement several times in 2012 and 2013. In late 2013 she failed to report for removal as required, and the order of supervision was revoked. She remains in the United States and filed Form I-212 seeking conditional permission to reapply for admission before departing; she does not contest that she will be inadmissible upon departure because she was previously ordered removed.

Family and personal background: the petitioner married a U.S. citizen in 2018 and had a child with him in 2019. She has two daughters from a prior marriage, born abroad in 2001 and 2007. At the time she filed, her spouse worked as a restaurant manager and had been offered a job with 12-hour shifts that would limit his availability for child care. The petitioner and her spouse stated that she provides emotional support and performs important household activities, including child care, and that her spouse would be severely distressed if she were required to return to El Salvador. The petitioner submitted letters from various individuals attesting to her moral character and a U.S. Department of State travel advisory about crime in El Salvador.

Employment and records: third-party letters dated 2019 indicate the petitioner had been employed for at least six years while in the United States, including time at the same restaurant that employed her spouse and at a second employer; she did not submit evidence of employment authorization, and her and her spouse’s statements did not describe that employment. She submitted a 2018 tax return showing reported income. She has no criminal record and asserted she “has not attempted to infringe any other immigration laws.”

Reason for appealing: the petitioner appealed the field office denial of her Form I-212 on the ground that the director did not give sufficient weight to her favorable factors (her asserted good moral character, family ties in the U.S., employment and tax payments, and the risks of returning to El Salvador) and gave excessive adverse weight to her immigration violations—particularly her failure to comply with the removal order. She also argued the director failed to properly adjudicate her positive equities and invoked prior decisions in support of how those equities should be considered.


**Question:**
Should this case be accepted or dismissed?

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

The answer is exactly "Accepted" or "Dismissed". E.g., `Answer: Accepted`

The task is complete once `swipl -q -f /app/solution.pl` runs without errors and prints the `Answer:` line.