The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
The petitioner is a company that provides cable, Internet, and telephone service and that operates a free, ad-supported streaming television (FAST) platform built into several smart television brands and available as an app on others. The petitioner employs the beneficiary as a vice president in charge of that streaming service. The beneficiary earned a Master of Business Administration in Japan in 2008 and previously worked in various positions at a related company from 2000 to 2014. He became chief operating officer of another related entity in 2014 soon after its founding, and when the petitioner acquired the streaming platform in 2020 he began serving as the petitioner’s vice president. The beneficiary is present in the United States on an O-1 nonimmigrant visa for individuals with extraordinary ability.

The record describes the beneficiary’s duties as leading and overseeing business development for the streaming platform and managing all facets of contract development, negotiation, and closeout with over 150 content partners. The petitioner submitted contracts and license agreements that the beneficiary signed on the platform’s behalf, letters from industry executives crediting him as “a key figure” in creating and maintaining content relationships, and statements from the platform’s president and chief financial officer asserting that the beneficiary was essential to the platform’s success and future growth. A former chief executive officer (now a senior vice president) described the beneficiary as one of the leading core executives since the platform’s initial conception and as the driving force behind many partnerships with major smart television brands. The record also includes company plans and forecasts and documentation of the beneficiary’s ongoing efforts to secure content and broaden distribution. The platform and its products are shown in the record to have won national industry awards in 2018 and 2020 and to reach more than 20 million monthly active users.

The petitioner appealed the Nebraska Service Center director’s denial of the Form I-140 petition. The director denied the petition on the basis that the record did not establish that the beneficiary’s proposed work met the director’s standards for national significance and related criteria, and had previously stated in a request for evidence that the petitioner had not described the importance of the beneficiary’s role as the platform’s vice president. On appeal, the petitioner contends the director did not fully consider or explain the evidence submitted and challenges the director’s stated deficiencies in the record.


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