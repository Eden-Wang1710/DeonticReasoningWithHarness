The relevant statute is available at `/app/statute.txt`.
Example Prolog solutions for similar problems are available at `/app/examples.txt`.


**Case Facts:**
The Petitioner is a dentist who seeks classification in the advanced-degree professional category and requests a national interest waiver of the job-offer requirement associated with that immigrant classification. The Director of the Texas Service Center denied the petition, and the matter was then brought on appeal. During adjudication, the Director issued a request for evidence seeking a detailed description of the Petitioner's proposed endeavor. The Petitioner states that she worked as a dental surgeon and clinic owner in Brazil. In a business plan submitted with the petition, she stated that she intended to create a dental services organization to support dentists and dental clinics by providing infrastructure and services such as equipment maintenance, business management, marketing and branding, tax services, information technology, financial and capital management, human-resources management, and courses and training. That plan projected hiring 1 employee in the first year and 18 employees by the fifth year, with payroll increasing from $60,000 to $516,000, and it also projected $4 million in tax revenue and net income of $261,411 by the fifth year. The record includes academic credentials, letters of support and recommendation, testimonial letters, and industry articles and reports, including materials about lack of affordable dental care in the United States, dental-care trends, and the importance of oral health. The Director stated that the Petitioner's evidence did not provide specific insight into what she intended to do in the United States and did not show prospective impact, significant potential to employ U.S. workers, or other substantial positive economic effects. On appeal, the Petitioner submitted a brief emphasizing her qualifications, maintained that the record showed the national importance of her proposed endeavor and that she met all three Dhanasar prongs, and submitted a revised business plan that she said corrected problems in the initial plan.


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