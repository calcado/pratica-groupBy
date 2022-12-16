# pratica-groupBy
Resultado do log dos exercicios conforme meu progresso:


alcado@calcado-System-Product-Name:~/Downloads/linkedrivenv2/linkedriven$ bash connect-database
Checando status do postgres...
psql (12.12 (Ubuntu 12.12-0ubuntu0.20.04.1))
Type "help" for help.

linkedrivenv2=# SELECT COUNT(id), experiences."endDate" AS "currentExperiences" FROM experiences WHERE "currentExperiences" IS NOT NULL;
ERROR:  column "currentExperiences" does not exist
LINE 1: ...e" AS "currentExperiences" FROM experiences WHERE "currentEx...
                                                             ^
linkedrivenv2=# SELECT COUNT(id), experiences."endDate" AS "currentExperiences" FROM experiences WHERE experiences."endDate" IS NOT NULL;
ERROR:  column "experiences.endDate" must appear in the GROUP BY clause or be used in an aggregate function
LINE 1: SELECT COUNT(id), experiences."endDate" AS "currentExperienc...
                          ^
linkedrivenv2=# SELECT COUNT(id), experiences."endDate" AS "currentExperiences" FROM experiences GROUP BY experiences."endDate" WHERE experiences."endDate" IS NOT NULL;
ERROR:  syntax error at or near "WHERE"
LINE 1: ..." FROM experiences GROUP BY experiences."endDate" WHERE expe...
                                                             ^
linkedrivenv2=# SELECT COUNT(id), experiences."endDate" AS "currentExperiences" FROM experiences GROUP BY experiences."endDate" WHERE "endDate" IS NOT NULL;
ERROR:  syntax error at or near "WHERE"
LINE 1: ..." FROM experiences GROUP BY experiences."endDate" WHERE "end...
                                                             ^
linkedrivenv2=# SELECT COUNT(id), experiences."endDate" AS "currentExperiences" FROM experiences GROUP BY experiences."endDate" IS NOT NULL;
ERROR:  column "experiences.endDate" must appear in the GROUP BY clause or be used in an aggregate function
LINE 1: SELECT COUNT(id), experiences."endDate" AS "currentExperienc...
                          ^
linkedrivenv2=# SELECT COUNT(id), experiences."endDate" AS "currentExperiences" FROM experiences GROUP BY experiences."endDate" WHERE "endDate" IS NOT NULL;
ERROR:  syntax error at or near "WHERE"
LINE 1: ..." FROM experiences GROUP BY experiences."endDate" WHERE "end...
                                                             ^
linkedrivenv2=# SELECT COUNT(id), "endDate" AS "currentExperiences" FROM experiences GROUP BY id WHERE "endDate" IS NOT NULL;
ERROR:  syntax error at or near "WHERE"
LINE 1: ..."currentExperiences" FROM experiences GROUP BY id WHERE "end...
                                                             ^
linkedrivenv2=# 
Session terminated, killing shell... ...killed.

calcado@calcado-System-Product-Name:~/Downloads/linkedrivenv2/linkedriven$ sudo -i -u postgres
[sudo] password for calcado: 
postgres@calcado-System-Product-Name:~$ \l
l: command not found
postgres@calcado-System-Product-Name:~$ pqsl

Command 'pqsl' not found, did you mean:

  command 'aqsl' from deb aqsis (1.8.2-12build2)
  command 'psl' from deb psl (0.21.0-1ubuntu1)
  command 'tqsl' from deb trustedqsl (2.5.1-1build1)
  command 'psql' from deb postgresql-client-common (214ubuntu0.1)

Try: apt install <deb name>

postgres@calcado-System-Product-Name:~$ psql
psql (12.12 (Ubuntu 12.12-0ubuntu0.20.04.1))
Type "help" for help.

postgres=# \l
postgres=# \c linkedrivenv2
You are now connected to database "linkedrivenv2" as user "postgres".
linkedrivenv2=# SELECT COUNT(id), "endDate" AS "currentExperiences" FROM experiences  WHERE "endDate" IS NOT NULL GROUP BY id;
linkedrivenv2=# SELECT COUNT(id), "endDate" AS "currentExperiences" FROM experiences  WHERE "endDate" IS NOT NULL GROUP BY id;
linkedrivenv2=# SELECT id, COUNT("endDate") AS "currentExperiences" FROM experiences  GROUP BY id;
linkedrivenv2=# SELECT id, COUNT("endDate") AS "currentExperiences" FROM experiences  GROUP BY "endDate";
ERROR:  column "experiences.id" must appear in the GROUP BY clause or be used in an aggregate function
LINE 1: SELECT id, COUNT("endDate") AS "currentExperiences" FROM exp...
               ^
linkedrivenv2=# SELECT COUNT("endDate") AS "currentExperiences" FROM experiences  GROUP BY "endDate";
linkedrivenv2=# SELECT COUNT("endDate") AS "currentExperiences" FROM experiences  GROUP BY "currentExperiences";
ERROR:  aggregate functions are not allowed in GROUP BY
LINE 1: SELECT COUNT("endDate") AS "currentExperiences" FROM experie...
               ^
linkedrivenv2=# SELECT COUNT("endDate") AS "currentExperiences" FROM experiences  GROUP BY "endDate";
linkedrivenv2=# SELECT COUNT("endDate") AS "currentExperiences" FROM experiences;
 currentExperiences 
--------------------
                 80
(1 row)

linkedrivenv2=# SELECT users.id, COUNT(educations.id) AS "educations", FROM users JOIN educations ON users.id = educations."userId" GROUP BY educations.id;
ERROR:  syntax error at or near "FROM"
LINE 1: ...T users.id, COUNT(educations.id) AS "educations", FROM users...
                                                             ^
linkedrivenv2=# SELECT users.id, COUNT(educations.id) AS "educations", FROM users JOIN educations ON users.id = educations."userId" GROUP BY educations.id;
ERROR:  syntax error at or near "FROM"
LINE 1: ...T users.id, COUNT(educations.id) AS "educations", FROM users...
                                                             ^
linkedrivenv2=# SELECT users.id, COUNT(educations.id) AS "educations", FROM users JOIN educations ON users.id = educations."userId";
ERROR:  syntax error at or near "FROM"
LINE 1: ...T users.id, COUNT(educations.id) AS "educations", FROM users...
                                                             ^
linkedrivenv2=# SELECT users.id, COUNT(educations.id) AS "educations" FROM users JOIN educations ON users.id = educations."userId";
ERROR:  column "users.id" must appear in the GROUP BY clause or be used in an aggregate function
LINE 1: SELECT users.id, COUNT(educations.id) AS "educations" FROM u...
               ^
linkedrivenv2=# SELECT users.id, COUNT(educations.id) AS "educations" FROM users JOIN educations ON users.id = educations."userId" GROUP BY educations.id;
ERROR:  column "users.id" must appear in the GROUP BY clause or be used in an aggregate function
LINE 1: SELECT users.id, COUNT(educations.id) AS "educations" FROM u...
               ^
linkedrivenv2=# SELECT users.id, COUNT(educations.id) AS "educations" FROM users JOIN educations ON users.id = educations."userId" GROUP BY users.id;
linkedrivenv2=# SELECT "userId", COUNT(id) AS "educations" FROM educations  GROUP BY "userId";
linkedrivenv2=# SELECT "userId", COUNT(id) AS "educations" FROM educations  GROUP BY "id";
linkedrivenv2=# SELECT "userId", COUNT(id) AS "educations" FROM educations ASC GROUP BY "id";
ERROR:  syntax error at or near "ASC"
LINE 1: ...serId", COUNT(id) AS "educations" FROM educations ASC GROUP ...
                                                             ^
linkedrivenv2=# SELECT "userId", COUNT(id) AS "educations" FROM educations GROUP BY "id" ASC;
ERROR:  syntax error at or near "ASC"
LINE 1: ...COUNT(id) AS "educations" FROM educations GROUP BY "id" ASC;
                                                                   ^
linkedrivenv2=# SELECT "userId", COUNT(id) AS "educations" FROM educations GROUP BY "id";
linkedrivenv2=# SELECT "userId" ASC, COUNT(id) AS "educations" FROM educations GROUP BY "id";
ERROR:  syntax error at or near "ASC"
LINE 1: SELECT "userId" ASC, COUNT(id) AS "educations" FROM educatio...
                        ^
linkedrivenv2=# SELECT "userId", COUNT(course.id) AS "educations" FROM educations GROUP BY "userId";
ERROR:  missing FROM-clause entry for table "course"
LINE 1: SELECT "userId", COUNT(course.id) AS "educations" FROM educa...
                               ^
linkedrivenv2=# SELECT "userId", COUNT("courseId") AS "educations" FROM educations GROUP BY "userId";
linkedrivenv2=# SELECT "userId", COUNT("courseId") AS "educations" FROM educations GROUP BY "userId" ORDER BY "userId" DESC;
linkedrivenv2=# SELECT "userId" AS id, COUNT("courseId") AS educations FROM educations GROUP BY "userId" ORDER by educations DESC;
linkedrivenv2=# SELECT "userId", COUNT("courseId") AS "educations" FROM educations GROUP BY "userId" ORDER BY "userId" ASC;
linkedrivenv2=# SELECT "userId", COUNT("courseId") AS "educations" FROM educations GROUP BY "userId" ORDER BY "educations" ASC;
linkedrivenv2=# SELECT "userId", COUNT("courseId") AS "educations" FROM educations GROUP BY "userId" ORDER BY "educations" DESC;
linkedrivenv2=# SELECT testimonials."writerId" AS "testimonialCount", 
linkedrivenv2-# COUNT(id),users.name AS "writer" 
linkedrivenv2-# FROM testimonials  
linkedrivenv2-# JOIN users 
linkedrivenv2-# ON users.id = testimonials."writerId" 
linkedrivenv2-# GROUP BY "writerId" 
linkedrivenv2-# WHERE "writerId" = 435;
ERROR:  syntax error at or near "WHERE"
LINE 7: WHERE "writerId" = 435;
        ^
linkedrivenv2=# SELECT testimonials."writerId" AS "testimonialCount", 
linkedrivenv2-# COUNT(id),users.name AS "writer" 
linkedrivenv2-# FROM testimonials  
linkedrivenv2-# JOIN users 
linkedrivenv2-# ON users.id = testimonials."writerId" 
linkedrivenv2-# GROUP BY "writerId" 
linkedrivenv2-# WHERE users.id = 435;
ERROR:  syntax error at or near "WHERE"
LINE 7: WHERE users.id = 435;
        ^
linkedrivenv2=# SELECT testimonials."writerId" AS "testimonialCount", 
linkedrivenv2-# COUNT(id),users.name AS "writer" 
linkedrivenv2-# FROM testimonials  
linkedrivenv2-# JOIN users 
linkedrivenv2-# ON users.id = testimonials."writerId"
linkedrivenv2-# WHERE users.id = 435 
linkedrivenv2-# GROUP BY "writerId" ;
ERROR:  column reference "id" is ambiguous
LINE 2: COUNT(id),users.name AS "writer" 
              ^
linkedrivenv2=# SELECT testimonials."writerId" AS "testimonialCount", 
linkedrivenv2-# COUNT(testimonial.id),users.name AS "writer" 
linkedrivenv2-# FROM testimonials  
linkedrivenv2-# JOIN users 
linkedrivenv2-# ON users.id = testimonials."writerId"
linkedrivenv2-# WHERE users.id = 435 
linkedrivenv2-# GROUP BY "writerId" ;
ERROR:  missing FROM-clause entry for table "testimonial"
LINE 2: COUNT(testimonial.id),users.name AS "writer" 
              ^
linkedrivenv2=# SELECT testimonials."writerId" AS "testimonialCount", 
linkedrivenv2-# COUNT(testimonials.id),users.name AS "writer" 
linkedrivenv2-# FROM testimonials  
linkedrivenv2-# JOIN users 
linkedrivenv2-# ON users.id = testimonials."writerId"
linkedrivenv2-# WHERE users.id = 435 
linkedrivenv2-# GROUP BY "writerId" ;
ERROR:  column "users.name" must appear in the GROUP BY clause or be used in an aggregate function
LINE 2: COUNT(testimonials.id),users.name AS "writer" 
                               ^
linkedrivenv2=# SELECT testimonials."writerId" AS "testimonialCount", 
linkedrivenv2-# COUNT(testimonials.id),users.name AS "writer" 
linkedrivenv2-# FROM testimonials  
linkedrivenv2-# JOIN users 
linkedrivenv2-# ON users.id = testimonials."writerId"
linkedrivenv2-# WHERE users.id = 435 
linkedrivenv2-# GROUP BY "users.name" ;
ERROR:  column "users.name" does not exist
LINE 7: GROUP BY "users.name" ;
                 ^
linkedrivenv2=# SELECT COUNT(testimonials."writerId") AS "testimonialCount", 
linkedrivenv2-# ,users.name AS writer
linkedrivenv2-# FROM testimonials  
linkedrivenv2-# JOIN users 
linkedrivenv2-# ON users.id = testimonials."writerId"
linkedrivenv2-# WHERE users.id = 435 
linkedrivenv2-# GROUP BY "users.name" ;
ERROR:  syntax error at or near ","
LINE 2: ,users.name AS writer
        ^
linkedrivenv2=# SELECT COUNT(testimonials."writerId") AS "testimonialCount", 
linkedrivenv2-# users.name AS writer
linkedrivenv2-# FROM testimonials  
linkedrivenv2-# JOIN users 
linkedrivenv2-# ON users.id = testimonials."writerId"
linkedrivenv2-# WHERE users.id = 435 
linkedrivenv2-# GROUP BY "users.name" ;
ERROR:  column "users.name" does not exist
LINE 7: GROUP BY "users.name" ;
                 ^
linkedrivenv2=# 
linkedrivenv2=# SELECT COUNT(testimonials."writerId") AS "testimonialCount", 
linkedrivenv2-# users.name AS writer
linkedrivenv2-# FROM testimonials  
linkedrivenv2-# JOIN users 
linkedrivenv2-# ON users.id = testimonials."writerId"
linkedrivenv2-# WHERE users.id = 435 
linkedrivenv2-# GROUP BY writer ;
 testimonialCount | writer 
------------------+--------
                3 | Jesus
(1 row)

linkedrivenv2=# SELECT users.name AS writer, 
linkedrivenv2-# COUNT(testimonials."writerId")AS "testimonialCount" 
linkedrivenv2-# FROM testimonials  
linkedrivenv2-# JOIN users 
linkedrivenv2-# ON users.id = testimonials."writerId"
linkedrivenv2-# WHERE users.id = 435 
linkedrivenv2-# GROUP BY writer ;
 writer | testimonialCount 
--------+------------------
 Jesus  |                3
(1 row)

linkedrivenv2=# SELECT  MAX(salary) AS "maximumSalary", 
linkedrivenv2-# role.name AS role  
linkedrivenv2-# FROM jobs 
linkedrivenv2-# JOIN roles 
linkedrivenv2-# ON jobs."roleId" = roles.id
linkedrivenv2-# GROUP BY roles ORDER BY "maximumSalary"  ASC;
ERROR:  missing FROM-clause entry for table "role"
LINE 2: role.name AS role  
        ^
linkedrivenv2=# SELECT  MAX(salary) AS "maximumSalary", 
linkedrivenv2-# roles.name AS role  
linkedrivenv2-# FROM jobs 
linkedrivenv2-# JOIN roles 
linkedrivenv2-# ON jobs."roleId" = roles.id
linkedrivenv2-# GROUP BY roles ORDER BY "maximumSalary"  ASC;
ERROR:  column "roles.name" must appear in the GROUP BY clause or be used in an aggregate function
LINE 2: roles.name AS role  
        ^
linkedrivenv2=# SELECT  MAX(salary) AS "maximumSalary", 
linkedrivenv2-# roles.name AS role  
linkedrivenv2-# FROM jobs 
linkedrivenv2-# JOIN roles 
linkedrivenv2-# ON jobs."roleId" = roles.id
linkedrivenv2-# GROUP BY role ORDER BY "maximumSalary"  ASC;
 maximumSalary |           role           
---------------+--------------------------
        107981 | Junior Software Engineer
        153208 | Front-end developer
        183405 | Software Engineer
        215640 | QA Analyst
        229468 | Data Analyst
        246764 | Scrum Master
        256310 | Tech Lead
        257172 | Product Manager
        261307 | DevOps Analyst
        265869 | Senior Software Engineer
        267886 | Back-end developer
       3040208 | VP of Technology
    1000000000 | CTO
(13 rows)

linkedrivenv2=# 

