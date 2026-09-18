The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
The petitioner is a software developer who filed Form I-140 in 2019 seeking second-preference immigrant classification based on either an advanced degree or exceptional ability, and requested a national interest waiver of the job-offer requirement. After the initial decision, he appealed and later filed a combined motion to reopen and motion to reconsider.

In support of his motions, the petitioner submitted new evidence including: a letter from his accountant describing how he is paid as a member of an LLC (monthly "guaranteed payments" rather than distributions or dividends), a copy of his U.S. income tax return for 2020, and a new academic credentials evaluation. The accountant’s letter reported annual income figures of R$321,700 for 2018 and R$245,872.30 for 2019 and characterized the guaranteed payments as the petitioner’s method of compensation as an LLC member. The academic evaluation stated the petitioner’s Brazilian Grau de Tecnólogo degree in Computer Science (completed in 2008 after three academic years) together with a Brazilian Lato Sensu Specialization Certificate in Project Management (awarded in 2011 after one and one-half years of graduate study) amount to the equivalent, in time and content, to a U.S. Bachelor of Science in Computer Science with an additional major in Project Management. The petitioner also described a career plan to work on large-scale software development projects and to contribute directly to the field by designing and developing software for companies in need.

As the basis for his requests on motion, the petitioner asserted that he meets the contested salary/remuneration criterion—claiming he has commanded remuneration indicative of exceptional ability—and he reasserted that he qualifies as a member of the professions holding an advanced degree. He asked the adjudicating authority to apply a "more likely than not" burden of proof to the salary issue. He argued that income fluctuations should be viewed in light of an average monthly income over an eight-year period beginning in 2011 (which he reported as R$28,500 per month) compared with monthly figures of R$21,000 for 2018 and R$25,200 for 2019. He also urged that income he receives as a business owner can be combined with his software-developer compensation (citing, by analogy, an attorney who earns income as a business owner connected to legal work). On his earlier appeal, he specifically reasserted satisfaction of the single salary/remuneration criterion and waived pursuing the other eligibility criteria.


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