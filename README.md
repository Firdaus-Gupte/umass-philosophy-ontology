# UMass Philosophy Course Ontology
This project is an applied ontology project of the UMass Philosophy Course curriculum over the last five years. It models philosophy courses, course offerings, academic terms, course levels, and distribution requirements. It is built on top of Basic Formal Ontology (BFO) and Common Core Ontology (CCO).

I made this project as a way to learn more about applied ontology. I practiced modeling domains with competency questions, RDF/OWL and Protege, using Cellfie and ROBOT to import data into Protege, and writing SPARQL queries.

## Competency Questions
See the .xlsx file labeled "UMass Ontology Planning and Data" for more details.

I started this project with the goal that the finished project should be able to answer certain domain-specific questions (DSQs).

1) Which philosophy courses are being offered in a specified term at UMass Amherst?
2) Which philosophy courses satisfy major distribution requirements?
3) What kind of teaching experience do instructors have?
4) Are there enough courses being offered in Fall 2026, and of all the right kinds?

I broke those questions down into the following, more specific competency questions:

1) Which philosophy courses are being offered in a specified term at UMass Amherst?
   - Which Philosophy courses are offered in Fall 2026?
   - Which Philosophy courses offered in Fall 2026 are online?
   - Which Philosophy courses offered in Fall 2026 are in person?
2) Which philosophy courses satisfy major distribution requirements?
   - Which courses offered in a specified academic term satisfy the value-theory requirement?
   - Which courses offered in a specified academic term satisfy the logic requirement?
   - Which courses offered in a specified academic term satisfy the ancient and medieval history requirement?
   - Which courses offered in a specified academic term satisfy the 17th and 18th century history requirement?
   - Which courses offered in a specified academic term satisfy the metaphysics and epistemology requirement?
   - Which courses in a specified semester are upper-division courses?
   - Which courses in a specified semester are lower-division courses?
3) What kind of teaching experience do instructors have?
   - Which instructors have taught philosophy courses?
   - Which instructors have taught logic courses, and how many?
   - Which instructors have taught ancient and medieval history courses, and how many?
   - Which instructors have taught 17th and 18th-century history courses, and how many?
   - Which instructors have taught metaphysics and epistemology courses, and how many?
   - Which instructors have taught upper-division courses, and how many?
   - Which instructors have taught lower-division courses, and how many?'
   - How many experienced instructors do we have at UMass?
4) Are there enough courses being offered in Fall 2026, and of all the right kinds?
   - Does each major distribution requirement area have at least one course offered in a specified academic term?
   - Which distribution requirement area has no Fall 2026 course offerings?
   - How many Fall 2026 course offerings satisfy each major distribution area?

I then brainstormed potential classes and relations that would need to be created when building the ontology on top of BFO. These included:
- Course
- CourseOffering
- Course Requirement
- taughtBy
- satisfiesCourseDistributionRequirement

I also brainstormed the BFO/CCO classes that I could categorize these classes under.
See the .xlsx file labeled "UMass Ontology Planning and Data", tab "Competency Questions", for more details.

## Modeling Decisions
Next, I started adding classes in Protege.

I distinguished between a Course (like "Introduction to Ethics") and a particular Course Offering (like Section 01 of Introduction to Ethics taught by Kornblith in Fall 2026). I categorized Course as a Generically Dependent Continuant because its existence depends on (potentially multiple copies) of a particular course offering. On the other hand, I categorized Course Offering as a process, because it is something that unfolds over time. More specifically, it is an act of educational training instruction. Within the class Course, I created subclasses like Upper Division Course and Lower Division Course, Metaphysics and Epistemology Course, Value Theory Course, and so on.

I added a few other relevant classes, like AcademicTerm, which I placed as a subclass of Temporal Interval, and InstructorPerson, which I placed as a subclass of Person.

Then, I categorized Course Requirement as a Prescriptive Information Content Entity since it is an informational content entity that requires students to enroll in courses of certain kinds. I added axioms so that if a course satisfied a specific Course Requirement (say, the Logic Requirement), it would automatically be added to the appropriate class (e.g. Logic Course). 

I added a few object properties, like satisfiesCourseDistributionRequirement and isOfferedInTerm. I created the property isTaughtBy, with the domain CourseOffering and range InstructorPerson, and its inverse teaches. Finally, I created the object property isOfferingOf as a subproperty of concretizes. I also created some relevant data properties, like hasCourseNumber. I added axioms that would sort courses into upper- and lower-division based on their course number.

## Getting and Importing the Data


Then, I scraped the UMass Philosophy course website for data on Course Codes, Course Titles, Academic Terms, and Course IDs.
See the .xlsx file labeled "UMass Ontology Planning and Data", tab "Merged Data", for the entire data set. 

I then organized and cleaned the data. I had to assign Instructor IDs to the instructors (e.g., Instructor 001) because many of the instructors had names with special characters that might cause problems in Protege. Similarly, I created IDs for courses, created names for course offerings, and sorted the courses into in-person and online.

Then, I used the [Cellfie](https://github.com/protegeproject/cellfie-plugin) plugin and [ROBOT](https://robot.obolibrary.org/) to import the data into Protege.

## Querying the data using SPARQL

Finally, I wrote SPARQL queries to ask questions about the data, to answer the competency questions above. I wrote 16 SPARQL queries, which you can find in the folder named "SPARQL queries". Here is a list of questions I asked of the data:

- CQ1: Which Philosophy courses are offered in Fall 2026?
- CQ2: Which Philosophy courses are online in Fall 2026?
- CQ3: Which Philosophy courses are in person in Fall 2026?
- CQ4: Which Philosophy courses in Spring 2025 satisfied the Logic requirement?
- CQ5: Which Philosophy courses offered in Fall 2024 satisfied the Value Theory requirement?
- CQ6: Which Philosophy courses offered in Fall 2026 satisfy the Ancient and Medieval History requirement?
- CQ7: Which Philosophy courses offered in the last two years satisfy the 17th and 18th Century History requirement? Which terms were they offered in?
- CQ8: Which Philosophy courses in the last two years satisfied the metaphysics and epistemology requirement?
- CQ9: How many total Philosophy course offerings in the last two years satisfied the metaphysics and epistemology requirement?
- CQ10: Which courses in Fall 2026 are upper- and lower-division courses?
- CQ11: How many course offerings has each instructor taught over the last 2 years?
- CQ12: Which instructors have lots of teaching experience over the last 2 years? (Which instructors have taught at least 4 Philosophy courses over the last 2 years? How many courses did they teach?)
- CQ13: How many experienced instructors do we have at UMass? (How many instructors at UMass have taught at least 4 course offerings over the last 2 years, from Fall 2024 to Summer 2026?)
- CQ14: Which instructors have taught upper-division courses over the last two years, from Fall 2024 to Summer 2026?
- CQ15: Which instructors have no upper-division teaching experience over the last 2 years? (Which instructors have taught a Philosophy course, but ONLY taught lower-division Philosophy courses, over the last two years, from Fall 2024 to Summer 2026?)
- CQ16: Do we have enough course variety in Fall 2026? (How many course offerings are there in Fall 2026 of each major distribution requirement?)

