The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
The petitioner is a statistics researcher who holds a master’s degree in statistics and is completing a doctorate while teaching statistics and working on his dissertation. He filed an I-140 immigrant petition seeking classification in the EB-2 category and a national interest waiver. His stated proposed endeavor is to develop predictive models—specifically probabilistic and generalized linear models—for predictive analyses. He described applications of this work to defending data and networks against cyber-attacks (including criminal data breaches and distributed denial-of-service attacks), and to a wide range of fields such as finance, life sciences, genetics, medical sciences, meteorology, banking, marketing, anthropology, agriculture, and environmental science (including modeling pesticide and pollutant impacts and informing policymakers about agricultural and food security).

To support his petition, the petitioner submitted multiple letters from academics and experts: a professor in a department of statistical science who described his work as important to studying relationships between predicted and predictive variables with implications for national security and cybersecurity; a professor of mathematical sciences noting citations to his work and utility in ecology and biodiversity (migration and marine movement patterns); a professor of epidemiology describing benefits to AI/ML systems and epidemiology; a professor attesting to potential improvements in farming methods and crop forecasting; and a senior mathematical statistician at the U.S. Department of Health & Human Services commenting on medical diagnostic applications of his machine learning algorithms. He also submitted an article discussing broader societal impacts (including crime reduction, veteran homelessness, and Medicare savings) and cited government use and investment in predictive modeling by agencies such as the Department of Defense, Naval Postgraduate School, EPA, and Department of Energy, including a DOE initiative offering up to $30 million for ML/AI research.

After the Texas Service Center issued an adverse decision on his I-140 petition, the petitioner appealed that denial to the Administrative Appeals Office. On appeal he argued that the adjudicator had focused on an occupational-shortage issue that he had not asserted, reiterated the government and expert support for the national significance of his work, asserted that his proposed endeavor would be more impactful than the comparison case cited by the adjudicator, stated that he intends to pursue the endeavor full time, and asserted that the endeavor would provide him a means for continuous funding.


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