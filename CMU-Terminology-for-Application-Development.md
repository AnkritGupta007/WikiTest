# special note: this is like a James Joyce novel, just a stream of conciousness so there is no particular order to the items.

## SAP
SAP is an Enterprise Resource Planning platform that seeks to provide horizontal and vertical application support to businesses in many industries. Horizontal features may be application programming and delivery models; Vertical features are like higher education-specific components like academic catalogs, student records, etc. CMU uses components from several modules (as organized by SAP): Human Resources (HR), Finance (FI), Controller (CO), Materials Management (MM), Plant Management (PM), Campus Management (CM, also branded as Student Lifecycle Management, or SLCM).  Most of our custom application work and data integrations focus on SLCM.

Term (and synonyms)   | Description
------ | ------
SLCM, CM, SIS   | Student Lifecycle Management (SLCM), Campus Management (CM), and Student Information system (SIS) are acronyms related to the main system of record for our academic records.
Program | This is a very loose term and the use of it may be somewhat dependent on the sub-system you are currently associating it with. Roughly, it represents an academic collection of work intended to correlate together for a purpose. Usually that purpose is the awarding of a degree (i.e. Bachelor's or Master's degree with associated major(s) and/or minor(s)) or certificate (i.e. undergraduate or graduate certificate) or, sometimes, non-degree programs. In CMU's system of record (SAP) there are varied objects that can be applied toward this concept. It is important to understand what is meant when your project seeks to use this term.
Academic Term, Academic Period, Academic Semester | I haven't seen a lot of coalescing around some of these. Each has been used in various manners. The most I can see is that TERM is more often used to represent the sub-components of a typical semester (e.g. Fall I, Fall II) but these are really Global Campus concepts and these don't exist in the system of record (SAP). Some specific codes that are present: 300 (Fall), 500 (Spring), 700 (Summer). Note that historically there were several codes for actual breakdowns in summer (like 710 and 720) and that sometimes we have some EXTERNAL organization (for the purpose of transfer courses) have different values, yet, in the 800s, and represent some concepts like quarters.
Academic Year | This has various concepts but is, generally, the Fall, Spring, and Summer semesters (with Fall starting the year). It is expressed either in two year components (e.g. 2020-2021 or 20-21) but sometimes (particularly in SAP) as the end year of the pair only. So 2021300 represents the Fall semester of the calendar year 2020 (i.e. Fall 2020 or Fall 2020-2021).
Fiscal Year | Many of our financial systems follow a fiscal year. This does not align directly with Academic Year or Calendar Year. It is 7/1 through 6/30 of the following year.
Degree | at the simplest, it is the type of credential you earn by completing a degree-seeking program. Bachelor of Arts, Bachelor of Science, Master of Science, PhD. In some usages it represents a version of those items that ties to our academic catalog. For instance, a Bachelor of Science is represented in a number of different ways at CMU, sometimes like "Bachelor of Business Administration" and sometimes like Bachelor of Science (BS:MC as an alternate code) and Bachelor of Science (BS:GC). Both of the latter two provide the same academic credential (i.e. what is printed on a diploma or transcript) and only differ by which majors they tie to. This is an element of a time when main campus and global campus were clearly separate. I think this is no longer necessary (or even was necessary when it was contrived).
Modality | How is the course offered? Classroom, Lab, Hybrid, Online are all examples. This is typically expressed by virtue of the event type, which means, for all intents and purposes, that a section may have more than one modality.
Campus ID, CMID, SLCM ID, Chip ID, Student Number, Employee Number | this is the SAP object of type ST, but a P for employee. For employees, we have a separate (but the same digits) record of type P (person). Thus an employee who is also a student has a ST record and a P record.  The caveat is that HR systems most often use a 8 character number vs. the 10 character padded number of SLCM so the padding of zeroes at the front is different.


## SAP Terminology
SAP Name | Description
-------- | -----------
Notification Status, Application Status | this is a 4 char code to describe different steps. It is on the Applications tab in the Student File portion of SAP. Two important values are ACCP (accepted), RGST (ready to allow registration). 
Registration, Program | On the Registration tab there is a dropdown showing the programs a student has as well as a list of registrations (representing semesters for which the student was enrolled in the program). All that have ever been associated with the student are in the drop down.
SC, Program | The object type for the main degree program/certificate. Has a short text and long text as well as bulletin descriptions, etc.
CS, Study ID | The object type that identifies a relationship between a student and a SC (program/degree). This is unique to the student and a new CS is created if a student changes degrees (i.e. for relationship with new degree) but is continued to be used if the student changes back to the degree again (i.e. after changing then changing back to original).
CG, Module Group | very many uses in the academic structure. Hierarchical so recursion is necessary to ascend and descend because it is variable depth. Our top-most module groups of the hierarchy are typically majors/minors/programs, otherwise called specializations in SAP. Many of our graduate programs have a 1:1 relationship between an SC and a CG, so this can make it a bit confusing. Ideally, these are used for different concentrations (under the same SC) like many majors can be taken with the same degree.
F, Location | These are ny locations for the system. Some are for academic locaitons, but others are not.
SM, Module | Colloquially called a course by some, though module has certainly leaked to the vernacular, this represents the main template for a course (e.g. BIO 100). This is not what the student has the relationship to. A student registers for a section (a.k.a. event package).
SE, Event Package | This is what represents the course a student will register for. It can be composed of one or more events (type E), one for each combination of day of week/time of day and modality of the course.
E, Event or Course | The day of week/time of day combination. This can have a lot of details associated with it like room, schedule, capacity, prices, etc.
EL, Time-independent Event | much like an E, but no day of week/time of day associated with it.
EO, External Organization | in the academic arena, other universities and colleges and high schools are EOs, though I don't think it is limited to these types of organizations.
CQ, Internal Qualification | this is what is awarded upon program completion (i.e. bachelor's degree, certificate, etc.) and details which type of degree (e.g. "Bachelor of Science" )
O, Org Unit | Departments and divisions of the university are identified as org units. These have a hierarchy and the depth is variable on any given path, so recursion may be needed to climb or descend this tree.
H, External person | examples can be CMU employees of special natures (i.e. work outside USA) or instructors of courses, often military science, where the relationship is non-standard. These users do have a Global ID, but they lack a Campus ID.
P, Person | this is the internal representation of a person (student, faculty, or staff)
ST, Student | this represents the student. These are created at the time of application (i.e. prior to an admission decision) so not all of our student records have enrolled at CMU.
S, Position | this represents the position into which a person is hired. Most security is driven by this and facilitates smooth transition of application rights when used for this purpose (as you gain rights when assigned to the position and lose them when you vacate the position by leaving university employment or changing to a new position).

## SAP relationships
Most objects have relationships to other objects to build links between programs and the respective available majors/minors/etc. or students and the courses they are registered for, etc. Typically, these are between the object types (i.e. ST linked to SE when a student enrolls in a section).
There are a few that are used for purposes that may be helpful to understand. These are bi-directional with the parent being on the "A" side of the relationship and the child on the "B" side. These have start and end dates.

Relationship | Purpose
------------ | -------
Y08 | Important for grading and class list/roster security on the web. A position (S) has a relationship to the org unit (O) for which the employee in the position would have rights. So, an accounting department secretary position will have a Y08 relationship with the accounting department. This aggregates for most of our usages of Y08 (i.e. a relationship with an org unit grants you authority over those descending org units, even without an explicit Y08 relationship with subordinate org units).
Y12 | Cross-listed course. PSY 000 may be cross-listed with REL 000. Cross-listed courses are equivalent and most impact what shows on a transcript and distribution of tuition dollars. This relationship is between SMs.
Y13 | I call them variants, regardless, the end result is that they are equivalent courses. Used for suffixes attached to SMs (i.e. REL 100 vs. REL 100WI). The relationship is between SMs.
Y21 | Used for relating a SM to another SM but in the context of the "B" side of the relationship is the lab for a particular course and this impacts auto-inclusion of lab courses with requirements, if desired, in Degree Progress. There is a placeholder SM to represent the concept that a single SM might count for both lecture and lab.



## SAP Time Limits
There are two calendars where you can look up some of these Time Limit types: **CMU** and **CMED**. Note that CMED does not have a summer semester.

Time Limit | Purpose
---------- | -------
"0100" | General Date range of a semester where the start date is the first day of the semester
"0200" | Date range of Fall and Spring semesters where the startDate is the first day that courses start. The dates for Summer vary every year.  No breaks for holidays because OffCampus has classes sometimes when OnCampus does not.
"ZGON" | (for fall and spring OnCampus) grading
"ZH01" | for the first half of summer grading
"ZH02" | for the second half of summer grading
"ZGOF" | for OffCampus grading
"ZCH1" | General Date range for On-Campus Grad and Undergrad Registration (for general, non-credit-level-specific dates use **Window** of `Z000`)
"ZRG1" | General Date range for On-Campus Grad and Undergrad Registration
"ZCHU" | General Date range for Off-Campus Undergrad Registration (for general, non-credit-level-specific dates use **Window** of `Z000`)
"ZRG3" | General Date range for Off-Campus Undergrad Registration

