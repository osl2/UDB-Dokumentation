# u<sup>db</sup>

> #### This page only explains what the tool is. If you're only looking for deployment instructions, go [here](./deployment.md).

u<sup>db</sup>, meant as "You to the power of databases", sometimes also written as upowdb,
is a tool for teaching and learning the usage of relational databases.
It does not include any content, it will not explain databases,
or otherwise perform the role of a teacher. Instead, it tries to provide an interface for students,
where they can learn with content uploaded by teachers, in the form of courses and worksheets,
experiment with sample databases and solve tasks provided in the worksheets.
u<sup>db</sup> has some abilities to check whether the solutions by the students are correct,
but they are not thorough enough to replace manual checks by a teacher.

### Courses
Teachers can create courses and fill them with worksheets. These worksheets are made up from tasks,
which have an associated sample database, and a list of subtasks.
Teachers can set the visibility of worksheets and separately of solutions to subtasks.
Even when the solution to a subtask is not visible, the teacher can allow students to check whether
a solution is correct using the solution stored on the server.

When given a link by the teacher, students can join a course. Joining a course is a completely local action,
the server does (on purpose) not keep track who has joined a course. Once inside the course,
students will see worksheets provided by the teacher (given that they are set to be visible),
and can then start to work on them.

### Tasks
There are 3 types of tasks:
 - **SQL:**             Here, students are given an instruction and a field in which they should enter an SQL statement.
                        Optionally there is a graphic interface where students can craft SQL statements visually using a
                        [scratch](https://scratch.mit.edu/)-like interface based on
                        Google's [blockly](https://developers.google.com/blockly/).
                        For courses with more advanced learners, teachers can disable this
                        interface to challenge students more.

 - **Text:**            Here, students are asked a question, which they are supposed to answer in their own words.

 - **Multiple Choice:** Here, students are asked a question, which they should answer by selecting one (or more) options
                        from a predefined set of answers.

### Sandbox Mode
Outside of courses, there is also a sandbox mode, where users can manipulate and query databases directly, without tasks attached.
This also includes usage of the visual SQL editor.