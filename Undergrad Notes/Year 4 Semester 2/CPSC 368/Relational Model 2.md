**Relational Model 2:**
 
Entities: Student (sid) ,  
VisitingStudent (sid),  
Section (sec#, year, course#, dept),  
Course (course#, dept), Instructor(name)
 
Relationships: Student-Enrolled-Section ((sid), (sec#, year, course#, dept)),  
Instructor-Teach-Section((name), (sec#, year, course#, dept)),  
Section-Offering-Course (sec#, year, course#, dept),  
Course-Prerequisite(course#, dept),  
Student-ISA-VisitingStudent (sid)
 
Student(sid, name, address, phone, major)  
VisitingStudent(**sid**, HomeInst, StartDate)  
Instructor(name, degree)  
SectionOffering(sec#, year, **course#**, **dept**)  
Course(course#, dept, title, credits)
 
Teach(**name**, **sec#**, **year**, **course#**, **dept**)  
Enrolled(**sid**, **sec#**, **year**, **course#**, **dept**, mark)  
Prerequisite(**course#**, **courseDept**, **preDept**, **pre#**)