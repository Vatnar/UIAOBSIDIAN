Principle:
- Only have on reason for change.
Scenario:
- We have a Student system that originally had a class responsible for storing student details, calculating grades, and managing student report generation.
solution: 
- Student class: stores only the information related to a student (ID< name). This class does not handle responsibilities to grades or reports.
- Grade Calculator Class: this class focuses solely on calculating the students grade. It takes a list of scores as input and provides the grade as output. This class follows SRP by separating the calculation responsibility
- Report Generator, Responsible for generating reports. Takes Student Object as input.
Student class is a pure data class, that we can put in a database (+ getters setters)

1. Reduction in complexity of a code
	A code is based on its functionality. A method holds logic for a single functionality or task.
2. Increased readability, extensibility and maintenance
	As each method has a single functionality
3. Re-usability and reduced error
	As code separates based functionality so if the same functionality uses somewhere else in an application then don't write it again.

