# Notes for Database Management System(Stanford Open Courses)



### Well-formed XML

* What is XML? Extensible Markup Language
* What is the difference from html language? tags describes content instead of formatting
* Stream format? What is the use? used to admit and consume the data
* The use of XML? It is the standard for data representation and exchange over network
* Structure of XML? 
  * Tagged elements, could be nested
  * Attributes
  * Text
* Comparison between relational model and xml?  
  * Structure: tables / Hierarchical trees, graph
  * Schema: fixed in advance / Flexible 'self-describing'
  * Queries: Simple and nice languages / Less so
  * Ordering: None / Implied, ordered in the file or stream
  * Implementation: Native in many systems / add-on, usually translated into the relational implementation
* What is called well-formed xml? It adheres to basic structural requirements
  * Single root element
  * Matched tags, proper nesting
  * Unique attributes within elements
* Displaying xml? How?  Use rule-based language to translate to html, CSS, XSL(extensible stylesheet language): xml -> css/xsl interpreter -> html
* Features of xml? 1. standard for data representation and exchange:  formal specification is enormous

### DTDs, ID, IDref attributes

* valid xml? adheres to basic structural requirements and content-specific specitification;
* Two languages for these specifications? DTD-document type descriptor; XSD-XML Schema;
* DTD? Document type descriptor?  Grammar-like language for specifying elements, attributes, nesting, ordering, # occurence; also special attribute types ID and IDREF(S)(pointers?)
* DTD/XSD versus none(well-formed)
  * pros(benefits of typing): 
    * programs can assume strucutre
    * CSS/XSL, process them into other forms
    * specification-data exchange, use dtd as specification what the xml should look like
    * Documentation
  * cons(benefits of non-typing):
    * flexibility
    * ease of change
    * DTDs can be very messy, irregular documents could behard
    * XDSs could be very messy,

### XML Schema (XSD)

* Extensive language, like DTDs, can specify elements, attiributes, nesting, ordering, #occurrences, also data types, keys, typed pointers, and more, XSD is written in XML
* Demo explained.

### Json Data Introduction

* what is Json? [a new data model, semi-structure, JavaScript Object Notation, Standard for serializing data objects, usually in files, ]
* Feautres? Human-readable, useful for data interchange; Also useful for representation and store semi-structure data; not tied to JavaScript, many parsers for many language
* Basic structure(recursive)?
  * Basic values(number, string, boolean)
  * Objects {} sets of label-value pairs
  * Array [] lists of values
* Comparison between JSON and Relational Model
  * Structure: Tables / Nested{Sets/Arrays}
  * Schema: Fixed in advance / self-describing
  * Queries: Simple and expressive language / widely used, manipulated programatically
  * Ordering: None / Arrays. are ordered, files itself is ordered, 
  * Implementation: Native system/ No standone data base system using JSON , coupled with programming language, 

### Relational Algebra I.

* Select operator? select students; Student with GPA > 3.7 ($\sigma_{GPA > 3.7}\text{Student}$); Student with GPA > 3.7  and HS < 1000 ($\sigma_{GPA > 3.7\ join S < 1000}\text{Student}$): $\sigma_{cond}\text{Relation}$
* Project operator? ID and decisionsolumns, $\Pi_{sID, dec}\text{Apply}$, results in two columns containing ID and decisions
* To pick both columns and rows. ID and name of students with GPA > 3.7: $\Pi_{sID, sName}(\sigma_{GPA>3.7}\text{Student})$ 
* Duplicates: lists of application majors and decisions, $\Pi_{major, dec}\text{Apply}$ only results in duplicates eliminated result,
* Difference between SQL and R.A. ? SQL: Multisets, R.A: Sets
* Cross-product?  $\text{Student} X \text{Apply}$  results in 8(# Student) * 9(# Apply) tuples in product.
* Student * Apply usage? $\sigma_{student.sId = Apply.sID\wedge HS>1000\wedge major=‘CS’ \wedge dec='R' }(Student * Applay)$
* Natural Join? Enforce equality on all attr with same name; eliminate one copy of duplicate attr.
  *  Names and gpas of students with HS>10000 who applied to cs and were rejected. $\Pi_{sName, GPA}\sigma_{HS>1000 \wedge major = 'CS\wedge dec='R'}(\text{Stduent}\bowtie \text{Apply})$;
  *  exp1$\bowtie$exp2 $=$ $\Pi_{schema(e1)\cup schema(e2)}(\sigma_{e1.a1 = e2.a2 \wedge e1.a2=e2.a2 ...}(e1 \times e2)) $;
* Theta join? $\bowtie_{\theta}$, exp1 $\bowtie_{\theta}$ epx2 = $\sigma_{\theta}(exp1\times exp2)$, "join" = "theta join"

### Relational Algebra II.

* Union?  lists of college and student names, vertically as list, $\Pi_{cName}\text{college} \cup \Pi_{sName}\text{Student}$ 
* Difference? Ids of students who didnt apply anywhere, $\Pi_{sID}\text{Stdudent} - \Pi_{sID}\text{Apply}$
* Intersection? Names that are both college name and student name: $\Pi_{cName}\text{college} \cap \Pi_{sName}\text{Student}$, $E1\bowtie E2 = E1 \cap E2$
* Rename operator? 
  * $\rho_{R(A1, A2, ..., An)}(E)$
  * $\rho_R(E)$
  * $\rho_{A_1, A_2, A_3...}(E)$
  * Goal: to unify schemas for set oeprators, like list of college and student names. Since $\Pi_{cName}\text{College} \cup \Pi_{sName}\text{Student}$ is not allowed. We have to do sth like $\rho_{c(name)}\Pi_{cName}\text{College} \cup \rho_{c(name)}\Pi_{sName}\text{Student}$
  * Pairs of colleges in the same state? cross, rename
* Alternate notation : assignment operator and expression trees. 

### Introduction to SQL

* sql standardized? yes
* How to use it? GUI or prompt or embedded in programs
* What is declarative ? based on relational algebra , query optimizer
* What is in DDL(data definition language)? create/drop
* What is DML(data manipulation language)? select/insert/delete/update
* Select?  select A1, A2 from R1, R2, where condition = $\Pi_{A1, A2, A3....}(\sigma_{condition}(R1\times R2 \times R3....))$

### Select statement

* select A1, A2, A3... from R1, R2, R3... where condition
* Example:
  * select sID, sName, GPA from Student where GPA>3.6
  * select sName, major from Student, Apply where Student.sID = Apply.sID may result in duplicates.
  * select distinct ... may get rid of duplicates
  * select sName, GPA, decision from Student, Apply wehre Student.sID = Apply.sID and sizeHS < 1000 and major = 'cs'
  * ordered by GPA desc/asc
  * like: whre major like '%bio%'
  * select * from 
  * select ..., GPA * 100as scale GPA

### Table Variables and Set Operators

* Table variables? R1, R2, R3

* Set operators? $\cup, \cap, \bar{}$

* Example

  * ```sql
    select S1.sID, S1.sName, S1.GPA, S2.sID, S2.sName, S2.GPA
    from Student S1, Student S2
    where S1.GPA = S2.GPA and S1.sID < S2.sID
    ```

  * ```sql
    select cName as name from College
    union (all) will gets the duplicated
    select sName as name from Student; // This will result in non-duplicated entries
    ```

  * ```sql
    select sID from Applay where major = 'cs'
    intersect
    select sID from Apply where major = 'ee'
    ```

  * ```sql
    select distinct A1.sID
    from Applay A1, Apply A2
    where A1.sID = A2.sID and A1.major = 'cs' and A2.major = 'ee'
    ```

  * ```sql
    select sID from APply where major = 'cs'
    except 
    select sID from Apply where major = 'ee'
    ```

  * ```sql
    select A1.sID
    from Apply A1, Apply A2
    where A1.sID = A2.sID and A1.major = 'cs' and A2.major <> 'ee' # different result from above one
    ```

### Sub-queries in WHERE

* Examples:

  * ```sql
    select sID, sName
    from Student
    where sID in (select sID from Apply where major = 'cs')
    ```

  * ```sql
    select sName
    from Student
    where sID in (select sID from Apply where major = 'cs')
    ```

  * ```sql
    without except
    select sID, sName
    from Student
    where sID in (select sID from Apply where major = 'cs') and sID not in (select sID from Apply where major = 'ee')
    ```

  * ```sql
    select cName, state
    from College C1
    where exists(select * from College C2
                where C2.state = C1.state and C1.cName <> C2.cName)
    ```

  * ```sql
    select sName
    from Student S1
    where not exist(select * from Stduent S2 
                   where S2.GPA > S1.GPA)
    ```

  * ```sql
    select S1.Name, S1.GPA
    from Student S1, Student S2
    where S1.GPA > S2.GPA; // select complimentary set to lowest gpa studentql
    ```

  * ```sql
    select sName, GPA 
    from Student
    where GPA >= all(select GPA from Student)
    ```

  * ```sql
    select sName
    from Student S1 
    where GPA > all(select GPA from Student S2 where S2.sID <> S1.sID) // Zero result
    ```

  * ```sql
    select cName
    from College S1
    where not enrollment <= any(select enrollment from College S1 where S2.cName <> S1.cName)
    ```

### Sub-queries in FROM and SELECT

* Examples:

  * ```sql
    select *
    from (select sID, sName, GPA, GPA*(sizeHS/10000.0) as scaledGPA
    from Student) G
    where abs(scaledGPA - GPA) > 1.0
    ```

  * ```sql
    Colleges paired with highest gpa of other applicants
    select distinct College.cName, state, GPA
    from College, Apply, Student
    where College.cName = Apply.cName
    and Apply.sID = Student.sID
    and GPA >= all
    (select GPA from Student, Apply
    where Student.sID= Apply.sID
    and Apply.cName = College.cName)
    ```

  * ```sql
    the same as above;
    select cName, state
    (select distinct GPA
    from College, Apply, Student
    where College.cName = Apply.cName
    and Apply.sID = Student.sID
    and GPA >= all
    (select GPA from Student, Apply
    where Student.sID= Apply.sID
    and Apply.cName = College.cName)) as GPA
    from College
    ```

  * subquery should return exactly one value every time.

### Aggregations

* Examples

  * aggregation function over values in multiple rows: min, max, sum, avg, count

  * Group by columns / Having condition

  * ```sql
    select avg(GPA)
    from Student
    ```

  * ```sql
    select min(GPA)
    from Student, Apply
    where Student.sID = Apply.sID and major = 'cs' wrong, multiple counts
    ```

  * ```sql
    select * 
    from Student
    where sID in (select sID from Apply where major = 'cs')
    ```

  * ```sql
    select count(distinct sID)
    from APply 
    where cName = 'Cornell'
    ```

  * ```sql
    select cName, count(*)
    from Apply
    group by cName; // partition the database by college name
    ```

  * ```sql
    select cName, major, min(GPA), max(GPA)
    from Student , Apply
    where Student.sID = Apply.sID
    group by cName, major;
    ```

  * ```sql
    find out the students applying for nothing
    select Student.sID, count(distinc cName)
    from Student, Apply
    where Student.sID = Apply.sID
    group by Student.sID
    union 
    select sID, 0======> this fill the second column with zero
    from Student
    where sID not in (select sID from Apply); 
    ```

  * ```sql
    select cName
    from Apply
    group by cName
    having coutn(*) < 5;
    ```

  * ```sql
    same as above
    select cName
    from Apply A1
    where 5 > (select count(*) from Apply A2 where A2.cName = A1.cName)
    ```

  * ```sql
    same as above
    select cName
    from Apply A1
    where 5 > (select count(distinct sID) from Apply A2 where A2.cName = A1.cName)
    ```

### Null Value 

* Examples

  * ``` sql
    select sID, sName, GPA
    from Student
    where GPA > 3.5 or GPA <= 3.5  // or GPA is null ----> this will result in students with gpa available/ all students
    ```

  * ```sql
    select sID, sName, sizeHS
    from Student
    where GPA > 3.5 or sizeHS < 16000 or sizeHS >= 16000
    ```

  * ```sql
    select count(distinct GPA)
    from Student
    where GPA is not null; // count(distinct) will not count NULL as a possibility, but select distinc would do that
    ```

### Data Modification Statements

* Examples

  * ```sql
    insert into talbel value(a1, a2, a3, a4)
    insert into table select-statement
    ```

  * ```sql
    delete from table where condition
    ```

  * ```sql
    update table
    set attr = expression
    where condition
    ```

  * ```sql
    Update table
    set a1 = exp1, a2 = exp2, a3 = exp3, a4 = exp4
    where condition
    ```

  * ```sql
    construction
    insert into Apply (
    select sID, 'carnegie mello', 'cs', null
    from Student
    where sID not in (select sID from Apply))

    ```

  * ```sql
    delete from Student 
    where sID in (
    select sID from Apply group by sID having count(distinct major) > 2)
    ```

### Join Statement

* join family for operators: inner join (theta join, cross join with condition), natural join, inner join using(attr, explicitly list attr you want to squated), outer join(left, right, full,  null value while not satisfying theta condition) ;


* Examples:

  * ```sql
    select distinct sName, major
    from Student inner join Apply
    on Student.sID = Apply.sID
    ```

  * ```sql
    where ? on? seperate attr for where, on for that specific student.sID = apply.sID
    ```

  * ```sql
    select distinc sName, major 
    from Student natural join Apply;
    ```

  * ```sql
    select sName, GPA
    from Student join Apply using (sID)// better software engeering practice , than natural join
    where sizeHS < 1000 and major = 'cs' and cName = 'Stanford'
    ```

  * ```sql
    OUTTER JOIN  => most interesting
    select sName, sID, cName, major
    from Student left outer join Apply using(sID) .left on the join side will induce null for non-existing tuple 
    ​````
    ```

  * ```sql
    select sName, Student
    from Student natural left outer join Apply
    ​````
    ```

  * ```sql
    right outer join 
    from Student natural right outer join Apply, find in the left relation matching for Apply
    ```

  * ```sql
    select sName, sID, cName, major
    from Student full outer join Apply using(sID);
    ==
    select sName, sID, cName, major
    from Stdent left outer join Apply using(sID)
    union
    select sName, sID, cName, major
    from Student right outer join APply using(sID)
    ​````
    ```

  * Think about the outer join when you do multiple ones, since they are not associative, may give the system a hint how to improve performance;

### Relational Design Overview

*  Design by decomposition:

*  mega realtions + properties of the data
   * system decomposese based on properties
   * final set of relations satifisfty normal form, no anomalies, no list info
   * functional dependencies => Boyce-Codd Normal Form
   * Multivalued dependencies => Fourth Normal Form

*  How ? Auto? 

   * Mega relations + properties of the data
   * system decomposes based on properties
   * final set of relations satisfy normal form, no anomalies and no lost information

*  BCNF > 4NF? 

*  WHat is functional dependency? SSN->sName, ssn determines the student name. Example: Apply(ssn, sName, cName), shows ssn-sName pair should only store once for each college, but we store multiple times.

*  BCNF: if a->b, a should be a key ==> decomposition: student (ssn, sname), apply(ssn, cName)

*  4NF: Apply(ssn, cName, HS)

   * redundancy : update delete anomalies;
   * mutliplicaticve effect: c college, h high schools c*H tuples
   * Not addressed by CVNF: no functional dependency

   ssn ->> cName

   * given ssn has every combinationsof cName with HS
   * should store each cName and each HS for an SSN once

   if A->>B, then a is a key

### Functional Dependencies

* concept? Data storage-compression, Reasoning about queries - optimization

* example: college application info. 

  * Student(SSN, sName, address, HScode, HSname, HScity, GPA, priority)
  * Apply(SSN, cName, state, date, major)

  GPA > 3.8 => priority = 1

  GPA > 3.3 and GPA < 3.8 => priority = 2

  otherwise priority = 3

* $A1, A2, A3...An \rightarrow B1, B2, B3, ... Bn$: $\bar{A}\rightarrow \bar{B}$

* Features of functional dependency? 

  * Based on knowledge of real worldd
  * All instances of relation must adhere

* Examples(Student (SSN, sName, address, HScode, HSname, HScity, GPA, priority)):

  * $SSN\rightarrow sName$
  * $SSN\rightarrow address$
  * $HScode\rightarrow HSname, HScity$
  * $HSname, HScity \rightarrow HScode$
  * $SSN\rightarrow GPA$
  * $GPA\rightarrow priority$
  * $SSN\rightarrow priority$

* Example(Apply(SSN, cName, state, date, major)):

  * $cName\rightarrow date$
  * $SSn, cName\rightarrow major$

  driven by real world relationship 

* Functional Dependencies and Keys

  * Relation with no duplicates $R(\bar A, \bar B)$
  * Suppose $\bar A\rightarrow \text{all attributes}​$

  so $\bar A$ is the key

* Trivial Functional dependency: $\bar A \rightarrow \bar B, if \bar B\subseteq \bar A $

* Non-trivial FD: $\bar A \rightarrow \bar B, if \bar B\subset\bar A$

* completley non-trivial: $\bar A \rightarrow \bar B , \bar A\cap \bar B = \emptyset$, this is the most interesting one we will look for

* Rules: 

  * Splitting rule:$\bar A\rightarrow B1, B2, B3....$ = $\bar A \rightarrow B1, \bar A\rightarrow B2$

  * Tirvial-dependency rules: $\bar A\rightarrow \bar B$ then $\bar A\rightarrow \bar A \cup \bar B$

  * Transitive rule: $\bar A\rightarrow \bar B, \bar B\rightarrow \bar C$  then $\bar A \rightarrow \bar C$

  * Closure of attributes:  Given relation, FDs, set of attributes $\bar A$, find all B s.t. $\bar A\rightarrow B$

     algo:

    ​      start with {A1, A2, A3, A4...}

    ​      repeat until no change(iterate each element):

    ​              if $\bar A\rightarrow \bar B$ and $\bar A $ in set add $\bar B$ to set

* Closure and keys:

  * Is $\bar A$ a key for R? compute $\bar A^+ $ if all attr then $\bar A$ is a key

  * How can we find all keys given a set of FDs? 

      consider every subset of attrs as $\bar A$ if $\bar A $ is a key then it is a key.

* Specify FDs for a relation

  * S1 and S2 sets of FDs

  * S2 "follows from " S1 if every relation instance satisfying S1, also satisfy S2

  * How to test? 

      problem: does $\bar A \rightarrow \bar B$ follows S

      closure: compute $\bar A^+$ based on S check if $\bar B $ in set $\bar A^+$????

  * Armstrong's Axioms:

* Goal of doing all of these things: minimal set of completely nontrivial FDs st all FDs that hold on the relation follow from the dependencies in this set

### Boyce-Codd Normal Form(need more time to consume)

* decomposition of a relational schema:  

  ​    R(A1, A2, A3...)($\bar A$) -> R1(B1, B2, B3...) $\bar B$and R2(C1, C2, C3...)$\bar C$

  ​    $\bar B\cup \bar C = \bar A$ , $R_1\bowtie R_2 = R$

* Good decompositions only? reassembly or lostless join property, need algo to do automatically figure out

* Into good relations BCNF

* BCNF:   

     Relation R with FDs is in BCNF if:

  ​       for each $\bar A\rightarrow B$ $\bar A$ is(contains) a key(superkey- super set of key)

### Multivalued Dependencies

* stronger than BCNF $A\twoheadrightarrow B$


### Relational Database Design(Chapter 8 in _Database System Concepts_) 

* Goal of relational database design is to:

  * generate a set of relation schemas that allows us to store information without unnecessary redundancy, 
  * yet also allows us to retrieve information easily. 
  * This is always achieved by designing schemas that are in an appropriate _normal form_

* Example of the real world enterprise: ![](http://i.imgur.com/UgXouUm.png)

   

* A few concepts clarification:

  * A superkey means a set of one or more attributes that , taken collectively, allow us to identify uniquely a tuple in the relation. 
  * A preimary key to denote a candidate key that is chosedn by the databse designer as the principal means of identifying tuples within a relation.  
    * a primary key should be chosen s.t. its attribute values are never, or very rearely , changed. 
  * Foreign key: primary key from other relation but also appear in this relation's attributes set. 
  * Functional Dependency: from real world constraints, we designer should keep in mind some rules, like: each specific value of dep_name should corresponds to at most one budget. No matter if _dep_name_ is primary key or not. In other words, functional dependency denotes the real world constraints. 
  * a domain is atomic: elements of this domain is not divisible , we say that a realtion schema R is in first normal form , but if the ID is like "CS111", "EE929", then with those id as an attributes in the relation, it is not in first norm.dont try to put more meaning in one string, if do so, then it is not in first norm. 
  * Relation Schema: a set of attributes, denoted as: r(R)
  * Superkey denoted as K is a superkey of r(R)
  * legal instance of r(R) means instance of r(R) satisfying all of the real-world constraints. 
  * Superkey another definition in terms of functional dependencies: $K\rightarrow R$ holds on r(R). 
  * Functional dependencies set is denoted as F, then all of the functional dependencies inferred from F can be forming a closure of set F, denoted as $F^+$
  * Boyce-Codd normal form: any functional dependency in $F^+$ in the form of $\alpha\rightarrow \beta$ holds at least:
    * $\alpha\rightarrow \beta$ is trivial
    * $\alpha$ is a superkey of schema R
  * How to decompose non-BCNF into BCNF smaller schemas: 
    * $\alpha\rightarrow \beta$ is not trivial and $\alpha$ is not a superkey
    * ($\alpha\cup\beta$)
    * (R - ($\beta - \alpha $))
  * What is the goal of decomposition? Eliminate the redundancy. So the thing is insertion(no null required insertion may prevent someone from insertion), update(twice), delete(all other information. )

* Decomposition using multivalued dependencies

  *  Stronger than BCNF

  * Example: r2(ID, departmentName, street, city), one instructor could have two homes, so ID$\rightarrow$ dName is not correct and vice versa.(__people can associate with different departments__) , so no function dependencies exist in this example. so still lots of redundancies. 

  * $\alpha \twoheadrightarrow \beta$:![](http://i.imgur.com/7rRfYlh.png)

    which actually means in each schema, you have to make this right, to hold. 

  * A little bit intuition about MVD(multi-valued dependencies): like name -> has several cell phone numbers, several home addresses, so phone number has no correlation with home address, so it is for sure they can be combined in any way possible(__i.e., name$\twoheadrightarrow$phone number, home address__), if we change the __cell phone__ to __home phone__, then __phone number__ will have correlation with __home address__, which doesnt lead to multi-valued dependencies.  

  * what is the goal of 4NF?