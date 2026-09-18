The relevant statute is available at `/app/statute.txt`.


**Case Facts:**
The petitioner is a citizen of El Salvador who filed a U petition in January 2018 with a Supplement B certified by a Victim Advocate from the Florida State Attorney’s Office; the certifying official identified the crime under investigation as murder and referred to a police report for a description of the criminal activity and any injuries. The police report included information about the petitioner’s mother and sister and had portions of the witness section redacted. The petitioner submitted biographical documents including a Georgia driver’s license dated May 2017 and other identity documents.

In a sworn affidavit, the petitioner stated that his mother and sister were murdered in his mother’s home in 2017. He described calling his mother and, when she did not answer, contacting his former sister‑in‑law, who went to the house and found many police officers present. When the petitioner arrived, he saw the bodies of his mother and sister and learned that neighbors had alerted police after seeing the petitioner’s sister’s two‑year‑old daughter—who had been present during the shootings—covered in blood. The petitioner also submitted a mental health evaluation reporting severe anxiety and depression since the incident. The record notes the petitioner’s age as 36 at the time of the incident and that he was not at his mother’s house at the moment the murders occurred.

On appeal, the petitioner argues he qualifies as a victim because he lived with his mother in Florida at the time of her murder, suffered substantial and lasting harm from the loss, and assisted law enforcement by providing information about unanswered calls that helped establish the timeframe of the murders and clarify his sister’s relationship with the alleged perpetrator. To support his claim of residence and connection to his mother’s household, he submitted additional evidence including an updated personal affidavit, a 2010 insurance bill, 2009 tax documentation, a Florida driver’s license issued in 2007, a 2016 statement of financial assistance, and an affidavit from a neighbor and family friend.


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