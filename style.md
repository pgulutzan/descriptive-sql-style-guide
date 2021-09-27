<!DOCTYPE html>
<html>

<head>
</head>

<body>

<h1>Descriptive SQL Style Guide</h1>

<p>Copyright (c) 2020 by Peter Gulutzan. All rights reserved.</p>

<p>This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; version 2 of the License.</p>

<p>This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.</p>

<p>You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA 02110-1301  USA</p>

<p>All references to "this program" or "software" mean "this guide", the Descriptive SQL Style Guide.
The copy of the GNU General Public License is the final section of this guide.</p>

<p>Version 0.1.0 2020-04-30</p>

<p>This is a descriptive style guide, like a dictionary that tells you what is common usage, with citations.
To find common usage I looked at vendor manuals, expert blogs, and prescriptive style guides
(guides that tell you what you should do). Status = alpha.</p>

<p>I think that anyone might use this to decide what code conventions are best for their own organizations,
based on orthodoxy, logic, style used for another language's style guide, and chosen DBMS vendor.</p>

<p>
The prescriptive style guides are the ones on github, in English, that have more than 100 stars at time of writing:<br>
Konstantin Taranov,
<a href="https://github.com/ktaranov/sqlserver-kit/blob/master/SQL%20Server%20Name%20Convention%20and%20T-SQL%20Programming%20Style.md">
SQL Server Name Convention and T-SQL Programming Style</a>,
841 stars.<br>
Simon Holywell,
<a href="https://github.com/treffynnon/sqlstyle.guide">
SQL Style guide</a>.
811 stars. Partly based on the book "Joe Celko's SQL Programming Style".<br>
Matt Mazur,
<a href="https://github.com/mattm/sql-style-guide">
Mazur's SQL Style Guide</a>.
441 stars. Mr Mazur says his guide is "opinionated".<br>
Fred Benenson,
<a href="https://gist.github.com/fredbenenson/7bb92718e19138c20591">
KickStarter, SQL Style Guide</a>
240 stars. Some PostgreSQL emphasis.<br>
Philipp Salvisberg,
<a href="https://github.com/Trivadis/plsql-and-sql-coding-guidelines">
"Trivadis PL/SQL &amp; SQL Coding Guidelines"</a>
62 stars + favourable reviews for example by Steven Feuerstein.
Also available as
<a href="https://trivadis.github.io/plsql-and-sql-coding-guidelines/v3.5/9-appendix/PLSQL-and-SQL-Coding-Guidelines.pdf">
pdf</a>. Oracle emphasis.<br>
Mark Donnelly,
<a href="https://github.com/meadmaker/sql-style-guide">
SQL Style guide</a>.
119 stars. Last updated in 2013.<br>

<p></p>

<p>For the "Names" sections I also consult these non-github web pages because they have details about specific object types:<br>
Tim Hall,
<a href="https://oracle-base.com/articles/misc/naming-conventions">
Oracle naming conventions</a>.<br>
Peter Gulutzan,
<a href="http://www.dbazine.com/db2/db2-disarticles/gulutzan5/">
"SQL Naming Conventions"</a>.<br>
Sehrope Sarkuni,
<a href="https://launchbylunch.com/posts/2014/Feb/16/sql-naming-conventions/">
"How I Write SQL, Part 1: Naming Conventions"</a>.<br>
Craig Mullins,
<a href="https://www.datavail.com/blog/on-db2-naming-conventions/">
"On DB2 Naming Conventions"</a>.
Also at
<a href="https://www.datavail.com/blog/on-db2-naming-conventions/">
datavail.com</a>
and
<a href="https://db2portal.blogspot.com/2006/11/on-db2-naming-conventions.html">
db2portal</a>.<br>
Jeffrey Keller,
<a href="https://www.vertabelo.com/blog/an-unemotional-logical-look-at-sql-server-naming-conventions/">
"An Unemotional Logical Look at SQL Server Naming Conventions"</a>.<br>
</p>

<p>For the "Format" sections I also consult this book chapter:<br>
Phil Factor.
<a href="http://assets.red-gate.com/community/books/redgate-guide-sql-server-development.pdf">
"SQL Server Team-Based Development. Chapter 1: Writing Readable SQL"</a>.
Section = Code Layout.</p>

<p>
The vendor manuals are:<br>
<a href="https://docs.oracle.com/en/database/oracle/oracle-database/20/sqlrf/">
Oracle Release 20 or 19 SQL Language Reference</a>.<br>
<a href="https://www.ibm.com/support/knowledgecenter/da/SSEPGG_11.5.0/com.ibm.db2.luw.sql.ref.doc/doc/r0011049.html">
DB2 manual 11.5</a>.<br>
<a href="https://docs.microsoft.com/en-us/sql/t-sql/statements/statements?view=sql-server-ver15">
SQL Server: 2019</a>. <br>
<a href="https://dev.mysql.com/doc/refman/8.0/en/create-table.html">
MySQL: 8.0</a>.<br>
<a href="https://mariadb.com/kb/en/create-table/">
MariaDB 10</a>.</br>
<a href="https://www.tarantool.io/en/doc/2.3/reference/reference_sql/sql/">
Tarantool 2.3</a>.<br>
Although I am a former or current employee of some of these companies,
I am only using information that is publicly available.</p>

<p>
For SQL Developer's
<a href="https://en.wikipedia.org/wiki/Oracle_SQL_Developer">
"code editor"</a> also called "worksheet"
I rely on
<a href="https://www.thatjeffsmith.com">www.thatjeffsmith.com</a>
and
<a href="http://totierne.blogspot.com/2013/07/text-version-of-plsql-formatter-options.html">
totierne.blogspot.com</a>.</p>

<p>Finally, I will sometimes quote the ANSI/ISO SQL standard,
and many bloggers whom I will identify as they come up.</p>

<p>Inconsistency happens so I try to look for multiple examples.</p>

<p>In following sections I will identify style guides by the author's surname,
and identify vendor manuals by the product's name.</p>

<p>My definition of SQL style is:
consistently choosing words or formats that do not affect what the DBMS returns,
often describable as a list of rules that formalize what words or formats to choose,
for example saying INTEGER rather than int.
Or, more simply: what to say when there are two ways to say (almost) exactly the same thing.</p>

<p>I do not bother with rules that only affect one vendor.</p>

<p>I begin most sections with the word Choice: followed by settings that you can pick.
Then I describe what the choices mean, then what prescriptive guides say,
what I happen to have seen in vendor manuals (warning: sampling may be affected by chance),
and what some bloggers or other sources might have said if I happened to notice them.</p>

<p>I want to avoid looking biased for one style or one vendor,
so I do not use a consistent style in examples.</p>

<H3 id="contents">Contents</H3><HR>

<p>
<a href="#choices">Choices</a><br>
<a href="#keywords-and-letter-case">Keywords and letter case</a><br>
<a href="#semicolons">Semicolons</a><br>
<a href="#not-equal-operators">Not-equal operator</a><br>
<a href="#unnecessary-keywords-and-operators">Unnecessary keywords and operators</a><br>
<a href="#select-star">SELECT *</a><br>
<a href="#order-by-ordinal">ORDER BY ordinal</a><br>
<a href="#comments">Comments</a><br>
<a href="#multiple-line-comments">Multiple-line comments</a><br>
<a href="#new-or-old-style-inner-join">New or old style inner join</a><br>
<a href="#data-types">Data types</a><br>
<a href="#literals">Literals</a><br>
<a href="#long-literals">Long literals</a><br>
<a href="#names-meaning">Names (meaning)</a><br>
<a href="#names-letter-case">Names (letter case)</a><br>
<a href="#names-legal-characters">Names (legal characters</a><br>
<a href="#names-length">Names (length)</a><br>
<a href="#names-delimiter">Names (delimiter)</a><br>
<a href="#names-qualifier">Names (qualifier)</a><br>
<a href="#names-prefix-or-suffix">Names (prefix or suffix)</a><br>
<a href="#names-of-tables">Names of tables</a><br>
<a href="#names-of-temporary-tables">Names of temporary tables</a><br>
<a href="#names-of-views">Names of views</a><br>
<a href="#names-of-columns">Names of columns</a><br>
<a href="#names-of-aliases-and-range-variables">Names of aliases and range variables</a><br>
<a href="#names-of-constraints">Names of constraints</a><br>
<a href="#names-of-indexes">Names of indexes</a><br>
<a href="#names-of-triggers">Names of triggers</a><br>
<a href="#names-of-sequences">Names of sequences</a><br>
<a href="#names-of-functions">Names of functions (or: names of routines)</a><br>
<a href="#names-of-savepoints">Names of savepoints</a><br>
<a href="#names-of-collations">Names of collations</a><br>
<a href="#names-of-variables-or-parameters">Names of variables or parameters</a><br>
<a href="#dynamic-sql">Dynamic SQL</a><br>
<a href="#format-terminology">Format terminology</a><br>
<a href="#format-choices-terminology">Format choices terminology</a><br>
<a href="#format-symbols">Format symbols</a><br>
<a href="#format-parentheses">Format parentheses</a><br>
<a href="#format-comments">Format comments</a><br>
<a href="#format-line-length">Format line length</a><br>
<a href="#indenting-units">Indenting units</a><br>
<a href="#indenting">Indenting</a><br>
<a href="#format-clauses-deciding-what-is-a-clause">Format clauses deciding what is a clause</a><br>
<a href="#format-clauses-by-indenting">Format clauses by indenting</a><br>
<a href="#format-clauses-by-right-aligning-keywords">Format clauses by right-aligning keywords</a><br>
<a href="#format-clauses-by-aligning-contents">Format clauses by aligning contents</a><br>
<a href="#format-lists">Format lists</a><br>
<a href="#format-conditions">Format conditions</a><br>
<a href="#format-subqueries">Format subqueries</a><br>
<a href="#format-with">Format WITH</a><br>
<a href="#format-joins">Format joins</a><br>
<a href="#format-insert">Format INSERT</a><br>
<a href="#format-update">Format UPDATE</a><br>
<a href="#format-create-table">Format CREATE TABLE</a><br>
<a href="#format-create-view">Format CREATE VIEW</a><br>
<a href="#format-create-procedure-or-create-function">Format CREATE PROCEDURE or CREATE FUNCTION</a><br>
<a href="#format-create-trigger">Format CREATE TRIGGER</a><br>
<a href="#format-case-expression">Format CASE expression</a><br>
<a href="#format-blocks-the-usual-way">Format blocks the usual way</a><br>
<a href="#format-blocks-with-analogies-to-other-guides-and-choices">Format blocks with analogies to other guides and choices</a><br>
<a href="#format-declare">Format DECLARE</a><br>
<a href="#format-overflow">Format overflow</a><br>
<a href="#formatters-or-pretty-printers">Formatters or pretty printers</a><br>
<a href="#contributors">Contributors</a><br>
<a href="#gpl-version-2-license">GPL Version 2 License</a><br></p>

<H3 id="choices">Choices</H3><HR>

<p>Choice: worry about style?</p>

<p>I will put "Choice: ...?" questions in most sections.</p>

<p>You do not need to care if ...<br>
You have a good-enough tool that does the job for you.<br>
You only work with SQL occasionally, and mostly for yourself.<br>
You see that fussing about appearance should be low priority.<br>
You have read one of the prescriptive guides and are satisfied.<br>
If any of those things apply to you, good, you are in the
majority and now you can go off and find better things to do.</p>

<p>You only need to care if ...<br>
You want to come up with a better tool.<br>
You are in a team whose boss insists on consistency.<br>
You would like to know what, if anything, justifies the rules.<br>
If any of those things apply to you, too bad,
now you will have to check "worry about style = yes"
and make similar checks for all the "Choice:" matters
that follow.</p>

<p>Choices are not inheritable because I do not classify well.</p>

<h2>Keywords and letter case</h2><HR>

<p>Choice: Keywords upper case or lower case?</p>

<p>Google Ngrams shows relative popularity of words and phrases in books, and it distinguishes upper versus lower case.
I used it for terms that are likely to appear only in database books:<br>
<a href="https://books.google.com/ngrams/graph?content=CREATE+TABLE%2Ccreate+table&year_start=1800&year_end=2008&corpus=15&smoothing=3&share=&direct_url=t1%3B%2CCREATE%20TABLE%3B%2Cc0%3B.t1%3B%2Ccreate%20table%3B%2Cc0">CREATE TABLE is more popular than create table</a>.<br>
<a href="https://books.google.com/ngrams/graph?content=SELECT+DISTINCT%2Cselect+distinct&year_start=1800&year_end=2008&corpus=15&smoothing=3&share=&direct_url=t1%3B%2CSELECT%20DISTINCT%3B%2Cc0%3B.t1%3B%2Cselect%20distinct%3B%2Cc0">SELECT DISTINCT is more popular than select distinct</a>.<br>
<a href="https://books.google.com/ngrams/graph?content=TO+SAVEPOINT%2Cto+savepoint&year_start=1800&year_end=2008&corpus=15&smoothing=3&share=&direct_url=t1%3B%2CTO%20SAVEPOINT%3B%2Cc0%3B.t1%3B%2Cto%20savepoint%3B%2Cc0">TO SAVEPOINT is more popular than to savepoint</a>.<br>
<a href="https://books.google.com/ngrams/graph?content=EXECUTE+IMMEDIATE%2Cexecute+immediate&year_start=1800&year_end=2008&corpus=15&smoothing=3&share=&direct_url=t1%3B%2CEXECUTE%20IMMEDIATE%3B%2Cc0%3B.t1%3B%2Cexecute%20immediate%3B%2Cc0">EXECUTE IMMEDIATE is more popular than execute immediate</a>.<br>
<a href="https://books.google.com/ngrams/graph?content=integer+primary+key%2CINTEGER+PRIMARY+KEY&year_start=1800&year_end=2008&corpus=15&smoothing=3&share=&direct_url=t1%3B%2Cinteger%20primary%20key%3B%2Cc0%3B.t1%3B%2CINTEGER%20PRIMARY%20KEY%3B%2Cc0">INTEGER PRIMARY KEY is more popular than integer primary key</a>.<br>
So saying "in general keywords are upper case" has some evidence.</p>

<p>Similarly, a poll by Lukas Eder resulted in
<a href="https://twitter.com/lukaseder/status/1052809813447593986?ref_src=twsrc%5Etfw%7Ctwcamp%5Etweetembed%7Ctwterm%5E1052809813447593986&ref_url=https%3A%2F%2Fblog.jooq.org%2F2019%2F10%2F29%2Fa-guide-to-sql-naming-conventions%2F">
a majority for SELECT in upper case</a>.</p>

<p>Exception #1: when a keyword is not being used as a keyword.
For example, IMMEDIATE is in the SQL standard's "non-reserved word" list, so I can use it as a column name.
I have trouble believing that the guides which say "capitalize keywords" mean that I should capitalize IMMEDIATE
in that circumstance. I think they really meant
"capitalize words that are not identifiers", which coincidentally excludes reserved words.</p>

<p>Exception #2: when trying to avoid SHOUTING or when trying to be like most other languages.
This might be reasonable when entering statements with a client that highlights properly.
See <a href="https://stackoverflow.com/questions/292026/is-there-a-good-reason-to-use-upper-case-for-sql-keywords">
this argument on stackoverflow</a>.</p>

<p>Exception #3: data type names. See later section = <a href="#data-types">Data types</a>.</p>

<p>Prescriptive guides:</p>

<p>Benenson, Donnelly, Holywell, Salvisberg say: upper case.<br>
Taranov says: upper case, except for data types.<br>
Mazur says: lower case ("It's just as readable as uppercase SQL and you will not have to constantly be holding down a shift key.")</p>

<p>Vendor manual examples:</p>

<p>MySQL, MariaDB, Oracle, SQL Server, Tarantool: upper case for keywords.<br>
DB2: upper case for all words, whether or not they are keywords.<br>
Oracle SQL Developer has an option "Case change" with choices "UPPER", "lower", "keep unchanged", and "Init cap"
(which presumably is intended for identifiers more than keywords).</p>

<p>Bloggers:</p>

<p>The <a href="https://www.drupal.org/docs/develop/standards/sql-coding-conventions">Drupal manual</a> says:
"Make SQL reserved words UPPERCASE. This is not a suggestion.
Drupal db abstraction commands will fail if this convention is not followed."</p>

<p>Ian Hellström in <a href="https://oracle.readthedocs.io/en/latest/sql/plans/">"Execution Plans"</a>
notes that Oracle uses a hash of the statement text to see whether it is in the
library cache. Thus even a tiny difference between two statements
can cause a cache miss and affect performance.</p>

<p>According to <a href="http://www.dba-oracle.com/t_library_cache_hash_value.htm">Don Burleson</a>
capitalization of keywords does not matter, but
according to <a href="https://books.google.ca/books?id=XUPXAQAAQBAJ&pg=PA29&lpg=PA29&dq=oracle+hash+statement+text+capitalize&source=bl&ots=ZNbcQhS-se&sig=ACfU3U3m6FCnCJLEvd66ASFSnR-KSjduKg&hl=en&sa=X&ved=2ahUKEwivx4-tpcroAhXR854KHfEMCzIQ6AEwAHoECAwQKQ#v=onepage&q=oracle%20hash%20statement%20text%20capitalize&f=false">
Morton and Osborne and Sands</a>
it does matter. Probably they're looking at different versions.
Anyway, that means that maybe sometimes in theory inconsistency will affect performance.</p>

<p>A <a href="http://www.tpc.org/tpc_documents_current_versions/pdf/tpc-h_v2.18.0.pdf">TPC-H example</a> has all lower case.</p>

<H3 id="semicolons">Semicolons</H3><HR>

<p>Choice: End all statements with semicolons?</p>

<p>In standard SQL ";" is not part of a statement, it is a signal that the statement is over,
so it is required for direct SQL (such as SQL typed to a client program) and within BEGIN ... END,
but not dynamic SQL (such as execute immediate, or SQLExecDirect in the call level interface).
Thus if a JDBC driver rejects a semicolon-terminated statement with
"SQLSyntaxErrorException: ORA-00911: invalid character",
which has been known to happen, it is within its rights.
Also see <a href="https://xkcd.com/327/">this cartoon</a>.</p>

<p>But all the vendor manuals either show that ";" is an optional part of a statement
(as in <a href="https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-database-transact-sql?view=sql-server-ver15">
this SQL Server bnf</a>), or show it in examples.
The key problems are: <br>
(1) if you do not know when statements end, you cannot run a script containing multiple statements <br>
(2) it is hard to know when statements end, for example "SELECT 5 BEGIN" is a valid single statement
    (in a certain dialect where BEGIN is not a reserved word and [AS] is not required),
    but simple parsers could easily think it is more than one.</p>

<p>Of course, a client
might get confused and think that &lt;semicolon&gt; &lt;newline&gt; is end-of-statement
(this has happened with Toad [] within comments,
and with other clients within BEGIN ... END blocks).
However, vendors have options for changing what the client thinks is the
terminator --
<a href="https://www.ibm.com/support/knowledgecenter/SS8PJ7_9.1.0/com.ibm.datatools.sqlxeditor.doc/topics/tchngstmtterm.html">SET TERMINATOR for DB2</a>,
<a href="https://mariadb.com/kb/en/delimiters/">DELIMITER for MySQL/MariaDB</a>,
<a href="https://asktom.oracle.com/pls/apex/asktom.search?tag=escape-semicolon">SET SQLTERMINATOR for Oracle</a>,
<a href="https://github.com/tarantool/test-run/issues/178">\set delimiter</a> for Tarantool.
Of course, I like to emphasize that there is a cleaner solution --
use a client with a
recognizer that supports
<a href="http://ocelot.ca/blog/blog/2016/03/20/client-side-predictive-parsing-of-mysqlmariadb-grammar/">
client-side predictive parsing</a>.</p>

<p>It is not true that Microsoft has deprecated the feature
"Not ending Transact-SQL statements with a semicolon".
Read the fine print of Microsoft's
<a href="https://docs.microsoft.com/en-us/sql/database-engine/deprecated-database-engine-features-in-sql-server-2016?redirectedfrom=MSDN&view=sql-server-ver15">
Deprecated Notice</a>.
It says that the feature will be "supported in the next version"
although it "will be deprecated in a later version", which they have been saying 
for
<a href="https://social.msdn.microsoft.com/Forums/sqlserver/en-US/a6201cf8-a7ca-45ec-918e-18646aa02f37/best-practice-use-of-semicolon-to-terminate-statements?forum=transactsql">
over a decade</a>
and lack of ; has been known to
<a href="https://www.dbdelta.com/always-use-semicolon-statement-terminators/">cause an error</a>,
but they probably are holding back because there is so much installed code.</p>

<p>Prescriptive guides: Taranov says end with ";". Factor says "generally speaking" end with ";"</p>

<p>Vendor manuals:</p>

<p>Usually ";" is not in the BNFs or railroad diagrams
(although Oracle does show it and Microsoft does show it as [;] i.e. optional);
however, most manuals' examples end with semicolons (except DB2's).</p>

<p>Bloggers:</p>

<p><a href="http://www.dbdelta.com/always-use-semicolon-statement-terminators/">Dan Guzman</a> says end with ";".<br>
<a href="http://www.dba-oracle.com/oracle_news/2005_2_2_do_semicolons_sql_expose_database_injection_attacks.htm">Don Burleson</a> says it depends.<br>
<a href="https://www.thatjeffsmith.com/archive/2012/12/sql-developer-why-do-you-require-semicolons-when-executing-sql-in-the-worksheet/">Jeff Smith</a> says it depends.<br>
Factor says "Use the semicolon to aid the reading of code, even where SQL syntax states that it is only optional."</p>

<p>The best explanation of SQL Server anomalies that I have seen is in
<a href="https://solutioncenter.apexsql.com/rules-of-sql-formatting-terminating-sql-statements-with-semicolons/">
"Rules of SQL formatting – Terminating SQL statements with semicolons"</a>.</p>

<H3 id="not-equal-operator">Not-equal operator</H3><HR>

<p>Choice: Not-Equal Operator: &lt;&gt; or != or ^= or &not;=?</p>

<p>The main variants are != and &lt;&gt; which are accepted by all major vendors.</p>

<p>DB2 and Oracle also support ^= and &not;=.
&not; is the Unicode standard symbol U+00AC "NOT SIGN" but since it is not in 7-bit ASCII.
it will not be recognized if you have the wrong code page.
Accordingly Oracle
<a href="https://docs.oracle.com/database/121/SQLRF/conditions002.htm#SQLRF52105">
says</a>
"Some forms of the inequality condition may be unavailable on some platforms"
and IBM
<a href="https://www.ibm.com/support/knowledgecenter/SSEPEK_10.0.0/sqlref/src/tpc/db2z_basicpredicate.html#db2z_basicpredicate__fnocop">
says</a>
"A logical not sign (&not;) can cause parsing errors in statements passed from one DBMS to another."</p>

<p>!= is found in C, Java, Perl, Python and the like.
The Python manual used to accept &lt;&gt; along with the warning
<a href="https://docs.python.org/2/reference/expressions.html">
"The &lt;&gt; spelling is considered obsolescent."</a>
... now it does not mention &lt;&gt; at all.
The idea is that ! is a "not sign" (if you know C and do not know Unicode) and
= is an equals sign, so this should be easy reading,</p>

<p>&lt;&gt; is found in Access, BASIC, Pascal, and Rexx (remember them?).
The idea is that &lt;= means "less than or equal", so in a consistent world &lt;&gt; means "less than or greater than".</p>

<p>&lt;&gt; is standard but != is more common in Oracle examples that I have seen.</p>

<p>That reminds me that once upon a time someone reported a case where
!= was faster than &lt;&gt; and
<a href="https://web.archive.org/web/20150909223016/http://www.freelists.org/post/oracle-l/Performance-Difference-Between-and">
spawned many answers</a>.</p>

<p>Prescriptive guides:</p>

<p>Mazur says: Use != over &lt;&gt; ... Simply because != reads like "not equal" which is closer to how we'd say it out loud."<br>
Benenson uses != in an example.</p>

<p>Vendor manuals:</p>

<p>Oracle's <a href="https://docs.oracle.com/en/database/oracle/oracle-database/20/sqlrf/Comparison-Conditions.html#GUID-828576BF-E606-4EA6-B94B-BFF48B67F927">inequality test example</a> uses !=<br>
MySQL's <a href="https://dev.mysql.com/doc/refman/8.0/en/comparison-operators.html">example</a> uses both != and &lt;&gt;<br>
SQL Server <a href="https://dev.mysql.com/doc/refman/8.0/en/comparison-operators.html">example</a> uses both != and &lt;&gt;<br>
DB2's <a href="https://www.ibm.com/support/knowledgecenter/SSEPEK_10.0.0/sqlref/src/tpc/db2z_basicpredicate.html#db2z_basicpredicate__fnocop">example</a> uses &lt;&gt; </p>

<p>Bloggers:</p>

<p><a href="https://books.google.ca/books?id=ivaaDgAAQBAJ&pg=PT20&lpg=PT20&dq=%22As+an+example+of+when+to+choose+the+standard+form%22+operator&source=bl&ots=srJAINy0bC&sig=ACfU3U3dVfoJYT2QfUygabpOi1lzg6eZWg&hl=en&sa=X&ved=2ahUKEwiJucvIrZ_oAhULv54KHd6AB60Q6AEwAHoECAkQAQ#v=onepage&q=%22As%20an%20example%20of%20when%20to%20choose%20the%20standard%20form%22%20operator&f=false">
Itzik Ben-Gan</a> says "This case should be a nobrainer: go for the standard one!"</p>

<p>An <a href="http://ibatis.10938.n7.nabble.com/How-to-define-not-equal-lt-gt-in-SQL-statement-td3118.html">iBATIS thread</a> shows a
user getting into trouble because XML complains about an SQL statement that contains &lt;&gt;
and seeing two proposed solutions: use cdata, or switch to !=.</p>

<H3 id="unnecessary-keywords-and-operators">Unnecessary keywords and operators</H3><HR>

<p>Choice: Add unnecessary keyword INNER in INNER JOIN?<br>
Choice: Add unnecessary keyword OUTER in LEFT OUTER JOIN?<br>
Choice: Add unnecessary keyword INTO in INSERT INTO?<br>
Choice: Add unnecessary parentheses around low-precedence expressions?<br>
Choice: Add unnecessary keyword COLUMN for ALTER TABLE ADD?</p>

<p>This is pleonasm, which <a href="https://dictionary.cambridge.org/dictionary/english/pleonasm">Cambridge</a>
defines as
"the use of more words than are needed to express a meaning, done either unintentionally or for emphasis;"
According to <a href="https://www.merriam-webster.com/dictionary/pleonasm">Merriam-Webster</a>
pleonasm means "the use of more words than those necessary to denote mere sense"
and "Pleonasm is commonly considered a fault of style, but it can also serve a useful function."</p>

<p>That is perhaps the reason that I can not find prescriptive guides or vendor examples
that advocate SELECT ALL, or UNION DISTINCT or ORDER BY x ASC.</p>

<p>But saying Add unnecessary keywords and operators = yes
should have these three effects, which are activated in at least one prescriptive guide or blog:</p>

<p>[INNER] before JOIN<br>
Mazur says: "Include inner for inner joins", probably the reasoning again is that it makes something easier to read.
Examples in vendor manuals seem to show INNER more often than not.</p>

<p>[INTO] after INSERT<br>
The word INTO is optional in MySQL/MariaDB and SQL Server, 
but compulsory in DB2, Oracle, and the SQL standard.
Holywell says:
"Why you would willingly choose a proprietary solution when a standard SQL method already exists is beyond me."</p>

<p>Parentheses around OR conditions<br>
That is, x OR y becomes (x OR y).
The reasoning is that, if there is an AND in the vicinity,
it will take precedence -- but who remembers precedence rules?
As the
<a href="https://www.oracle.com/technetwork/java/codeconventions-150003.pdf">Java style guide</a> says:
(regarding mixed operators)
"you should not assume that other programmers know precedence as well as you do".</p>

<p>But add-unnecessary-keywords-and-operators = yes does not mean:<br>
[TRANSACTION] or [TRAN] or [WORK] after COMMIT.<br>
This is the opposite of the INSERT INTO phenomenon --
in this case not every vendor supports the unnecessary word.
So, naturally, you will not see the same usage of these keywords in all vendor manuals.</p>

<p>Prescriptive guides:</p>

<p>Salvisberg says: "Never initialize variables with NULL. ... Variables are initialized to NULL by default."
(but probably he does not mean DEFAULT NULL).</p>

<p>Holywell says:
"Keep code succinct and devoid of
redundant SQL—such as unnecessary quoting or parentheses or WHERE clauses that can otherwise be derived."</p>

<p>Vendor manual examples:</p>

<p>Oracle: <a href="https://docs.oracle.com/cloud/latest/big-data-discovery-cloud/BDDEQ/ceql_statement_join.htm#BDDEQ-concept_C34DE81F378945A68B88025E29D5CE58">does not allow LEFT JOIN with OUTER</a><br>
MariaDB, MySQL: show LEFT JOIN without OUTER</p>

<p>Bloggers:</p>

<p><a href="https://gist.github.com/mattmc3/38a85e6a4ca1093816c08d4815fbebfb">
"Modern SQL Style Guide"</a>,
explaining why "left outer join" is bad, says: "`outer` is an unnecessary optional keyword".</p>

<p><a href="https://czep.net/15/pedantic-sql.html">Scott Czepiel</a> says:
Omit the “outer” when doing a left join ... Likewise omit “inner” from inner joins</p>

<H3 id="select-star">SELECT *</H3><HR>

<p>Choice: Allow SELECT *?</p>

<p>The main complaint about SELECT * is that the definition of the table might change.
However, that is true even if we select with column names, if ALTER can be used to
change a column definition.</p>

<p>To be consistent, Allow SELECT * = no should also affect other syntax
that is based on assumptions about stable table structures, such as
INSERT without INTO, or NATURAL JOIN.</p>

<p>And maybe it is not truly pleonastic to specify column names,
if there is a chance that table definition will change someday.
So maybe SELECT * can be replaced by<br>
SELECT column-name [, column-name ...]<br>
and maybe INSERT INTO table-name can be replaced by<br>
INSERT INTO table-name (column-name [, column-name ...]).</p>

<p>Vendor manual examples:</p>

<p>Since I expect that SELECT * will be used for examples, I did not check.</p>

<p>Bloggers:</p>

<p>Factor <a href="https://www.red-gate.com/hub/product-learning/sql-prompt/finding-code-smells-using-sql-prompt-asterisk-select-list">
says</a>: use SELECT * for "ad-hoc" work, not "production" work.</p>

<H3 id="order-by-ordinal">ORDER BY ordinal</H3><HR>

<p>Choice: Allow ORDER BY ordinal?</p>

<p>"SELECT ... ORDER BY 1;" was once legal in standard SQL but became illegal in the 1999 version.
However, all major vendors still support it.</p>

<p>MySQL and Tarantool and
DB2 with
<a href="https://www.ibm.com/support/producthub/db2/docs/content/SSEPGG_11.5.0/com.ibm.db2.luw.apdv.porting.doc/doc/r_sql_compat_group_by_column.html">
NPS-mode</a> even support "GROUP BY 1".</p>

<p>"ORDER BY ordinal" would be convenient for<br>
SELECT very_long_expression, very_long_expression FROM ... ORDER BY 2;<br>
However, all major vendors support aliases too.</p>

<p>ORDER BY ordinal" would be convenient for<br>
VALUES ('b', 'c') UNION ALL VALUES ('x', 'y') ORDER BY 2;<br>
However, not all vendors support ORDER BY in such contexts.</p>

<p>Prescriptive guides:</p>

<p>Taranov, Salvisberg say: specify columns.</p>

<p>Salvisberg says: "Always specify column names instead of positional references in ORDER BY clauses."</p>

<p>Vendor manuals:</p>

<p>Oracle: <a href="https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/SELECT.html#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6">
shows</a> ORDER BY position as well as ORDER BY name</p>

<p>DB2: <a href="https://www.ibm.com/support/producthub/db2/docs/content/SSEPGG_11.5.0/com.ibm.db2.luw.sql.ref.doc/doc/r0059211.html">
has</a> examples of ORDER BY name only.</p>

<p>SQL Server: <a href="https://docs.microsoft.com/en-us/sql/t-sql/queries/select-order-by-clause-transact-sql?redirectedfrom=MSDN&view=sql-server-ver15">
says</a> "Avoid specifying integers in the ORDER BY clause as positional representations of the columns in the select list."</p>

<p>Bloggers:</p>

<p>Claire Carroll
<a href="https://blog.getdbt.com/write-better-sql-a-defense-of-group-by-1/">posted</a>
"Write better SQL: In defense of group by 1"
... the <a href="https://about.gitlab.com/handbook/business-ops/data-team/sql-style-guide/">gitlab</a> folks would probably approve.</p>

<H3 id="comments">Comments</H3><HR>

<p>Choice: /* comment */ or --comment?</p>

<p>The main variants of comments are:<br>
bracketed (start with /* and end with */) also called multi-line or block or C-style or slash star,<br>
simple (start with -- and end with newline) also called single-line or line or double-dash.<br>
MySQL allows replacing -- with # for simple comments but that is rare.</p>

<p>Although the SQL standard said that simple comments are mandatory and bracketed comments are optional,
nowadays all vendors support both types.
Oddly, there are cases where bracketed comments are legal but simple comments are illegal,
for example with DB2's <a href="https://www.idug.org/p/bl/et/blogaid=943">DSNTIAUL</a>
and in standard PREPARE texts (General Rule 6 = 
"If P [the contents of the SQL statement variable]
does not conform to the Format, Syntax Rules, and Access Rules of a &lt;preparable statement&gt;,
or if P contains a &lt;simple comment&gt; then ... an exception condition is raised: syntax error or access rule violation.").
I do not know why.
Maybe it has something to do with the fact that some types of SQL injection attack
depend on simple comments, as
described on <a href="https://www.netsparker.com/blog/web-security/sql-injection-cheat-sheet/">netsparker.com</a>.
Or maybe it has something to do with caching, as a
<a href="https://books.google.ca/books?id=UfjHAgAAQBAJ&pg=PA329&lpg=PA329&dq=bracketed+comment+sql&source=bl&ots=Jq3NhpfFzG&sig=ACfU3U11aqTgiXffIIeZYSwP5_5BgS7vpA&hl=en&sa=X&ved=2ahUKEwjz29-84vznAhURIjQIHcCVB4YQ6AEwA3oECAYQAQ#v=onepage&q=bracketed%20comment%20sql&f=false">
DB2 document</a> hints that only
statements with bracketed comments will get into the dynamic cache.</p>

<p>There are <a href="https://en.wikipedia.org/wiki/Comparison_of_documentation_generators">
documentation generators</a>
that have SQL support and that require a particular comment style, often starting with /**.</p>

<p>The other style question is: where to put comments?</p>

<p><a href="https://solutioncenter.apexsql.com/rules-of-sql-formatting-sql-code-commenting/">ApexSQL</a> has advice for where to put bracketed comments inside stored procedures.
but I did not find specific advice about location in other documents (except Don Burleson's blog).
Vendor manual examples show comments preceding the statement (on a separate line),
or comments following a clause (on the same line, at the end of the line),
but I found none that show comments following the statement or comments within a line.</p>

<p>Prescriptive guides:</p>

<p>Taranov says "Always use multi-line comment".<br>
Holywell says "Use the C style opening /* and closing */ where possible" and
"Avoid nesting comments" (with an example of a bracketed comment inside a simple comment).<br>
Salvisberg says: "Inside a program unit only use the line commenting technique --".</p>

<p>Vendor manuals: show both styles, no apparent preference.</p>

<p>Oracle SQL Developer has an option "Put -- comments between /* ... */" but not the other way around,
which I guess is a hint about where their sentiments lie.</p>

<p>Bloggers:</p>

<p><a href="http://www.dba-oracle.com/t_plsql_comments_best_practice_standards.htm">Don Burleson</a>
says: use simple comments except inside 3GL programs that use the Oracle Precompilers.</p>

<H3 id="multiple-line-comments">Multiple-line comments</H3><HR>

<p>Choice: multiple-line comment style 1, or 2, or 3, or 4, or 5?<br>
Choice: precede multiple-line comment with a blank line?<br>
Choice: follow multiple-line comment with a blank line?</p>

<p>Bracketed /* ... */ comments can take up multiple lines.
Usually they precede what they are commenting on.
It may be hard to reformat them so it is good if each line is short.</p>

<p>I have seen or read about five styles.
Usually they are preceded or followed by newlines.</p>
<pre>
/*
  This comment is Style 1: Align start and end.
*/

/*
 * This comment is Style 2: Align asterisks.
 */

/*
** This comment is Style 3: Lines start with **.
*/

/**
 * This comment is Style 4: Comment starts with **.
 */

/*
This comment is style 5: Comment ends on line end. */
</pre></p>

<p>Style 3 is recommended (but not followed) by <a href="https://docs.microsoft.com/en-us/sql/t-sql/language-elements/slash-star-comment-transact-sql?view=sql-server-ver15">the SQL Server manual</a>.<br>
Style 4 is a signal to tools like <a href="http://www.doxygen.nl/manual/docblocks.html">Doxygen</a> that this is for documentation as mentioned earlier.</p>

<p>Vendor examples:</p>

<p>Oracle: <a href="https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/Comments.html#GUID-5C84C344-CEB3-4DBF-B748-337DE11CCE2A">style 5</a>.<br>
DB2: <a href="https://www.ibm.com/support/knowledgecenter/SSEPEK_10.0.0/sqlref/src/tpc/db2z_sqlcomments.html">style 2</a>.<br>
SQL Server: style 1.<br>
MySQL: <a href="https://dev.mysql.com/doc/refman/8.0/en/comments.html">style 1</a>.<br>
MariaDB: <a href="https://mariadb.com/kb/en/comment-syntax/">style 5</a>.</p>

<p>Bloggers:</p>

<p><a href="https://solutioncenter.apexsql.com/rules-of-sql-formatting-sql-code-commenting/">Apex SQL</a>
has recommendations for what should be in the comment, and options for inserting empty lines before/after
the comment.</p>

<H3 id="new-or-old-style-inner-join">New or old style inner join</H3><HR>

<p>Choice: join syntax: old-style or new-style?</p>

<p>"FROM a, b [WHERE join-condition etc.]" is old style, also called FROM-join.<br>
"FROM a ... JOIN b ON join-condition" is new style, also called ANSI or ISO or SQL92 join.</p>

<p>Back in 2005 Doug Burns <a href="http://oracledoug.com/serendipity/index.php?/archives/933-ANSI-Join-Syntax.html">described</a>
his pro-and-con thoughts, which I hereby distort:<br>
Pro: changing to an OUTER join is easy because it has almost the same syntax<br>
Pro: it is more unlikely that you will miss a condition and go Cartesian<br>
Pro: mixing up the join-condition with other conditions in the WHERE clause might mislead,<br>
Con: new style is more verbose<br>
Con: old style has a long-established base.</p>

<p>Some bloggers give the wrong impression that Microsoft has deprecated old style joins and/or they are non-standard.
In fact Microsoft only deprecated old style outer joins
(see 
<a href="https://www.red-gate.com/hub/product-learning/sql-prompt/finding-code-smells-using-sql-prompt-old-style-join-syntax-st001">
this red-gate post</a>
and
<a href="https://blogs.technet.microsoft.com/wardpond/2008/09/13/deprecation-of-old-style-join-syntax-only-a-partial-thing/">
this Microsoft post</a>).
In fact the syntax "FROM table_name1 , table_name2" is legal according to the ISO/IEC ("ANSI")
SQL:2016 rules for &lt;table reference list&gt;
and Microsoft
<a href="https://docs.microsoft.com/en-us/previous-versions/sql/sql-server-2008-r2/ms190014(v=sql.105)?redirectedfrom=MSDN">
is aware of that</a>.</p>

<p>Prescriptive guides:</p>

<p>Benenson, Salvisberg, Taranov say: use new style.</p>

<p>Vendor manuals:</p>

<p>DB2: the
<a href="https://www.ibm.com/support/knowledgecenter/SSEPEK_11.0.0/intro/src/tpc/db2z_innerjoin.html">"Inner join"</a>
examples mix old and new style without recommendations.</p>

<p>Oracle: the
<a href="https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/SELECT.html#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6__I2066611">
"Using Join Queries: Examples"</a> show only old style.
Remember that we're only talking about inner joins here --
for outer joins, Oracle recommends
<a href="https://docs.oracle.com/cd/B19306_01/server.102/b14200/queries006.htm">against</a>
using the old style and its Oracle-specific join operator.</p>

<p>MariaDB: recommends <a href="https://mariadb.com/kb/en/comma-vs-join/">new style</a>.</p>

<p>SQL Server: says new style is
<a href="https://docs.microsoft.com/en-us/sql/relational-databases/performance/joins?view=sql-server-ver15">"recommended"</a>.</p>

<p>Tarantool: has an introductory section using only old style.</p>

<p>Bloggers:</p>

<p><a href="https://developer.salesforce.com/forums/?id=906F00000005K22IAE">Salesforce</a>
apparently is in the group that thinks that old style is
<a href="https://salesforce.stackexchange.com/questions/195461/marketing-cloud-query-doesnt-allow-two-tables-in-from">
not standard</a>.</p>

<p><a href="https://www.sqlservercentral.com/forums/topic/non-ansi-equal-join-sql-2012">Joe Celko</a> says:<br>
"But what I found is that people who use the traditional notation think in sets,
while those who use the infix notation are stuck with a procedural linear mindset."<br>
He <a href="https://www.sqlteam.com/forums/topic.asp?TOPIC_ID=162162">also</a> says:<br>
"Weaker SQL programmers use INNER JOIN, since it is sequential and a familiar, procedural infix binary operator.
Stronger SQL programmers use the WHERE syntax because it is set-oriented, obeys the law of proximity and is an n-ary operator."</p>

<H3 id="data-types">Data types</H3><HR>

<p>Choice: abbreviated data type names?<br>
Choice: upper case or lower case data type names?</p>

<p>In standard SQL you can create a column with data type int,
but in information_schema it will show up as INTEGER --
the canonical form is always the unabbreviated word in upper case.
Unfortunately not every vendor converts canonically but this
shows that for the standard INTEGER is a better word.</p>

<p>However, <a href="https://www.sentryone.com/blog/aaronbertrand/backtobasics-lower-case-data-types">Aaron Bertrand</a>
(who wrote a series of blog posts touching on SQL style) switched to int,
because of a SQL Server quirk.
In SQL Server, if you are querying a system table, it makes a difference
what collation you used when you originally defined the whole database.
It can mean that you will not find columns defined as 'int' when you search for columns defined as 'INT' or 'INTEGER'.
(In SQL Server built-in data type names are not
<a href="https://docs.microsoft.com/en-us/sql/t-sql/language-elements/reserved-keywords-transact-sql?view=sql-server-ver15">
not reserved words</a>.)</p>

<p>For another indicator, again using Ngrams ...<br>
<a href="https://books.google.com/ngrams/graph?content=integer+primary+key%2CINTEGER+PRIMARY+KEY%2Cint+primary+key%2CINT+PRIMARY+KEY%2Cint+PRIMARY+KEY&year_start=1800&year_end=2008&corpus=15&smoothing=3&share=&direct_url=t1%3B%2Cinteger%20primary%20key%3B%2Cc0%3B.t1%3B%2CINTEGER%20PRIMARY%20KEY%3B%2Cc0%3B.t1%3B%2Cint%20primary%20key%3B%2Cc0%3B.t1%3B%2CINT%20PRIMARY%20KEY%3B%2Cc0%3B.t1%3B%2Cint%20PRIMARY%20KEY%3B%2Cc0#t1%3B%2Cinteger%20primary%20key%3B%2Cc0%3B.t1%3B%2CINTEGER%20PRIMARY%20KEY%3B%2Cc0%3B.t1%3B%2Cint%20primary%20key%3B%2Cc0%3B.t1%3B%2CINT%20PRIMARY%20KEY%3B%2Cc0%3B.t1%3B%2Cint%20PRIMARY%20KEY%3B%2Cc0">INTEGER PRIMARY KEY is more popular than INT PRIMARY KEY</a><br>
<a href="https://books.google.com/ngrams/graph?content=varchar%2CVARCHAR%2Ccharacter+varying%2CCHARACTER+VARYING&year_start=1800&year_end=2008&corpus=15&smoothing=3&share=&direct_url=t1%3B%2Cvarchar%3B%2Cc0%3B.t1%3B%2CVARCHAR%3B%2Cc0%3B.t1%3B%2Ccharacter%20varying%3B%2Cc0%3B.t1%3B%2CCHARACTER%20VARYING%3B%2Cc0">
but varchar is more popular than VARCHAR or CHARACTER VARYING</a>.</p>

<p>Although the INT-versus-INTEGER questions are not settled, there is no question
that CHAR(n) is preferred instead of CHARACTER(n).
By the way, if you did not know how to pronounce CHAR, see
<a href="https://ocelot.ca/blog/blog/2016/11/30/pronouncing-database-terms/">this blog post</a>.
For the other data type abbreviation -- DEC versus DECIMAL -- I found no guidance.</p>

<p>Sometimes I have seen that the length, and/or precision and scale, is skipped when it is default.
This is probably related to the Pleonasm question -- should unnecessary words be skipped?</p>

<p>Prescriptive guides:</p>

<p>Salvisberg says: "Avoid declaring NUMBER variables, constants or subtypes with no precision."<br>
Holywell says: "It is best to avoid the abbreviated keywords and use the full length ones where available"
(but he is not talking about data types)<br>
Taranov says: "Always specify a length to any text-based data type such as varchar, nvarchar, char, nchar:"</p>

<p>Vendor Manuals:</p>

<p>I just looked at the data types that were used in the manuals' CREATE TABLE examples.</p>

<p>DB2: CHAR(n), CHAR (n), CLOB, CLOB(n), DATE, DECIMAL(n,n), DOUBLE, INTEGER, SMALLINT, TIMESTAMP, VARCHAR(n)
(I thought it was interesting tht DOUBLE was used although DOUBLE PRECISION is standard)</p>

<p>Oracle: BLOB, CHAR(n), CLOB, DATE, NUMBER,, NUMBER(n), NUMBER(n,n), number(n), NCLOB, VARCHAR2(n), varchar2(n)
(I thought it was interesting that CHAR(n) was used when n &lt;= 2 and NVARCHAR(n) was used when n &gt; 2 but doubt that is a rule)</p>

<p>SQL Server: char(n), DATETIME, datetime, float, INT, int, money, nvarchar(n), smallint, VARBINARY, VARCHAR(n)</p>

<p>MySQL: BLOB, CHAR(n), DATE, DATETIME, INT, VARCHAR(n)</p>

<p>MariaDB: bigint, BLOB, CHAR(n), DATETIME INT, int, varchar(n)</p>

<p>Tarantool: INT, INTEGER, SCALAR, STRING</p>

<p>... Summary: vendors do not follow style guides in this area.</p>

<p>Oracle SQL Developer has an option "Case change", and if you pick "UPPER"
then VARCHAR2 is upper case, that is, it is a keyword like any other.</p>

<p>This <a href="https://forum.red-gate.com/discussion/11420/auto-completion-insertion-keys-behaviour">redgate forum post</a>
shows that there are different options for keywords UPPERCASE and data types lowercase.</p>

<H3 id="literals">Literals</H3><HR>

<p>Choice: allow non-standard literal formats?</p>

<p>In standard SQL the format of a literal determines its type:<br>
inside '' -- CHAR<br>
inside X'' -- BINARY or VARBINARY<br>
inside DATE '' -- DATE<br>
exponential notation -- DOUBLE or REAL or FLOAT<br>
[sign]digits[[period][digits]] INTEGER or SMALLINT or DECIMAL or NUMERIC<br>
and so on.<br>
But vendors vary, and due to implicit casting the format does not really indicate much.</p>

<p>What then should we do if we want to put ' within ''?<br>
MySQL/MariaDB and SQL Server sometimes let us say "...'..." (they have to use something else for delimiting identifiers).<br>
Some DBMSs let us escape by saying '...\'...'.<br>
Some JDBC APIs let us escape by saying {escape 'escape character'}<br>
Oracle lets us change what the character string delimiter is with q'{...'...}'<br>
Perhaps all DBMSs let us say '...''...'.</p>

<p>Prescriptive guides:</p>

<p>Nobody says anything.</p>

<p>Vendor manuals:</p>

<p>Examples usually show '...''...' as it is the only standard unless the DBMS supports Unicode escaping.</p>

<p>Blogs:</p>

<p><a href="https://www.red-gate.com/simple-talk/blogs/how-to-and-not-to-escape-a-string-in-tsql/">Louis Davidson</a>
suggests functions quotename() and concat() for putting strings together.</p>

<H3 id="long-literals">Long literals</H3><HR>

<p>Choice: use standard syntax, or use a continuation character, or use ||</p>

<p>This situation comes up with both character and binary strings:<br>
the string is too long (presumably that means "Maximum line length" is exceeded).<br>
The string has to be broken up and placed on multiple lines.</p>

<p>"use standard syntax" means: depend on the fact that in
standard SQL 'A' /* whitespace */ 'B' is interpreted as 'AB'. So<pre>
SELECT 'video meliora proboque, '
       'deteriora sequor.' ...</pre>
But, alas, some vendors do not allow it.<br>
And even one that does -- MySQL/MariaDB -- does not allow X'41' '42'.</p>

<p>"use a continuation character" means depend on the client
(or possibly the server) to see a line-continuation signal. So<pre>
SELECT 'video meliora proboque, '\
       'deteriora sequor.' ...</pre>
But, alas, some vendors use different continuation characters.</p>

<p>"use ||" means depend on support of || for concatenation. So<br><pre>
SELECT 'video meliora proboque, ' ||
       'deteriora sequor.' ...</pre>
This is the best bet for vendor support; even MySQL/MariaDB
can be forced to accept || for concatenation sometimes.<br>
The problem is not that || might make a performance difference.
The problem is that we have to specify a special format rule
regarding placement of the operator (see section <a href="#format-symbols">Format symbols</a>).</p>

<p>Prescriptive guides:</p>

<p>I have no information from any prescriptive guide.</p>

<p>Vendor manuals:</p>

<p>Oracle: In SQL/Plus, the continuation character is a hyphen.</p>

<p>DB2: line continuation is possible with \ but this is in the client</p>

<p>SQL Server: line continuation is possible with \ and
<a href="https://sqlquantumleap.com/2017/10/27/line-continuation-in-t-sql/">this</a> says that is part of T-SQL not the client</p>

<H3 id="names-meaning">Names (meaning)</H3><HR>

<p>Choice: Names should mean something?</p>

<p>We all know the setting should be 'yes' but 
if you are trying to make a point about syntax,
then a <a href="https://en.wikipedia.org/wiki/Metasyntactic_variable">placeholder name</a>
has all the meaning that you need, because the referent could be anything at all.
So in a document like this I use names like
TABLE_NAME or Column1 but expect that people
would be more specific when representing something specific.</p>

As far as I can tell the
<a href="https://en.wikipedia.org/wiki/Foobar">foobar</a> placeholders,
known in other languages, are not frequent in SQL contexts.
Perhaps we have fewer reasons to swear.

<p>Prescriptive guides:</p>

<p>No need to quote. Everybody would agree.</p>

<H3 id="names-letter-case">Names (letter case)</H3><HR>

<p>Choice: Names UPPER CASE or lower case or snake_case or PascalCase or camelCase?</p>

<p>Terminology:<br>
camelCase = (all words except the first start with a capital letter)<br>
PascalCase = (all words start with a capital letter) sometimes called upper camel case<br>
SNAKE_CASE  = all words all capital letters, underscore separator)<br>
snake_case = all words all lower case letters, underscore separator)<br>
...<br>
Inevitably, in the following Names sections, I am going to have to
give examples which use a particular case.
This does not mean I recommend a particular case, I leave recommendations to prescriptive guides.</p>

<p>One argument against lower case is that it does not reflect what the
standard information_schema name will look like, since the standard
rule is that the name will be folded to upper case before being stored.
PostgreSQL ignores the SQL standard
(see the blog post
<a href="https://ocelot.ca/blog/blog/2013/09/30/sometimes-mysql-is-more-standards-compliant-than-postgresql/">
"Sometimes MySQL is more standards-compliant than PostgreSQL"</a>), but some other DBMSs do not.</p>

<p>One argument against snake_case is the academic conference presentation by
David Binkley and Marcia Davis and Dawn Lawrie and Christopher Morrell,
<a href="https://www.researchgate.net/publication/221219628_To_camelcase_or_under-score">
"To camelcase or under-score"</a>
which concluded:<br>
"... it be-comes evident that the camel
case style leads to better allaround performance once a subject is trained on this style."
But their experimenting was not in an SQL situation
where names are distinguished by indentation or by having all non-identifiers in upper case.
And anyway there is another study by
Bonita Sharif and Jonathan I. Maletic,
"An Eye Tracking Study on camelCase and under_score Identifier Styles",
which concluded:<br>
"While results indicate no difference in accuracy between the two styles,
subjects recognize identifiers in the underscore style more quickly."
(I have only read the abstract.)</p>

<p>Prescriptive guides:</p>

<p>Holywell says: "Use underscores where you would naturally include a space in the name" ...
"Avoid ... CamelCase—it is difficult to scan quickly." (Apparently this is a reference to what I have called PascalCase.)</p>

<p>Salvisberg says: "write all names in lower case"</p>

<p>Benenson gives an example of snake_case: "SELECT COUNT(*) AS backers_count"
and says "Variable names should be underscore separated:"
(I consider "underscore separated" to be a synonym of "snake_case").</p>

<p>Sarkuni says: snake_case</p>

<p>Mullins says: SNAKE_CASE</p>

<p>Taranov says: PascalCase for everything except database, schema, and synonym.</p>

<p>Factor says: "Schema objects are, I believe, better capitalized." (example) "This_Is_Capitalized"</p>

<p>Vendor manual examples:</p>

<p>MariaDB, MySQL, Oracle, Tarantool: usually snake_case<br>
SQL Server: usually PascalCase<br>
DB2: usually SNAKE_CASE<br>
SQL Standard: SNAKE_CASE</p>

<p>For example these are extracts from the manuals' CREATE TABLE pages.<br>
CREATE TABLE employees_demo ... (Oracle)<br>
CREATE TABLE EMPLOYEE_SALARY ... (DB2)<br>
CREATE TABLE CREATE TABLE dbo.PurchaseOrderDetail ... (SQL Server)<br>
CREATE TABLE client_firms ... (MySQL)<br>
CREATE TABLE table_name ... (MariaDB)<br>
CREATE TABLE modules ... (Tarantool)</p>

<H3 id="names-legal-characters">Names (legal characters)</H3><HR>

<p>Choice: Names can include $?<br>
Choice: Names can include letters other than A-Z?</p>

<p>What characters should be legal for regular identifiers of most objects?
In standard SQL, the answer is _ or digit or any Unicode character that is considered to be a letter, so Cyrillic / Japanese kana / Chinese / etc. are all okay
But in practice the answers vary widely, as one can see by looking at the vendor documentation of
<a href="https://www.ibm.com/support/knowledgecenter/SSEPGG_11.1.0/com.ibm.db2.luw.admin.cmd.doc/doc/r0002141.html">DB2</a>,
<a href="https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/Database-Object-Names-and-Qualifiers.html#GU">Oracle</a>,
<a href="https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers?view=sql-server-ver15">SQL Server</a>,
<a href="https://mariadb.com/kb/en/identifier-names">MariaDB</a>,
<a href="https://www.tarantool.io/en/doc/2.3/reference/reference_sql/sql/">Tarantool (see "Identifiers")</a>.
The minimum common denominator is A-z, a-z, 0-9, _ and -- for some reason I have never understood -- $.
The maximum is any Unicode letter, digit, _, $, and sometimes # or @.</p>

<p>I used to expect that (say) Russian developers would regard Latin-alphabet names as inferior to Cyrillic-alphabet names.
But evidence for that expectation is totally lacking.
Possibly one thing that holds people back is the fear that some client or driver will
misplace the character set and show garbage?
Improve your vocabulary: the word for such misplacement is <a href="https://en.wikipedia.org/wiki/Mojibake">mojibake</a>.</p>

<p>Prescriptive guides:</p>

<p>Holywell says: "Only use letters, numbers and underscores in names."
Taranov says: "use only Latin symbols [A-z] and numeric [0-9]."</p>

<p>Vendor manuals:</p>

<p><a href="https://www.ibm.com/support/knowledgecenter/SSEPGG_11.1.0/com.ibm.db2.luw.admin.cmd.doc/doc/r0002141.html">DB2 "Naming conventions"</a>.</p>

<p>DB2's
<a href="https://www.ibm.com/support/pages/some-odbc-applications-may-not-be-able-handle-special-characters-tablecolumn-names">
"Some ODBC Applications May Not Be Able to Handle Special Characters in Table/Column Names"</a>
warning is that there are problems with drivers with some special characters.</p>

<H3 id="names-length">Names (length)</H3><HR>

<p>Choice: maximum length: 18 or 30 or 64 or 128?</p>

<p>There is a vendor-dependent maximum length.
Usually it is 128 (DB2, Oracle, SQL Server), or 64 (MySQL/MariaDB), or more than 20000 (Tarantool).
Shorter names were required in olden times and may still be required for a few objects.</p>

<p>But the desirable column-name length will be less than the maximum if column names are used as headers
in reports. Here I am assuming that the name will inevitably be the label, although
<a href="https://docs.oracle.com/javase/8/docs/api/java/sql/ResultSetMetaData.html#getColumnLabel-int-">JDBC</a>
thinks otherwise.</p>

<p>Length considerations might induce people to use abbreviations,
and that must be okay because the SQL standard uses abbreviations too.</p>

<p>Prescriptive guides:</p>

<p>Mullins says:  recommended maximum length = 128<br>
Holywell says: "Keep the length to a maximum of 30 bytes"<br>
Taranov says: 128 for most things<br>
Salvisberg says:
"Avoid using abbreviations unless the full name is excessively long.
Avoid long abbreviations. Abbreviations should be shorter than 5 characters.
Any abbreviations must be widely known and accepted.
Create a glossary with all accepted abbreviations."</p>

<p>Vendor examples:</p>

<p>Microsoft's
<a href="https://docs.microsoft.com/en-us/sql/odbc/microsoft/column-name-limitations?view=sql-server-ver15">
"Column name limitations"</a>
warning is that there are problems with drivers with long names and special characters.</p>

<p>Bloggers:</p>

<p>Northwestern University
<a href="https://www.it.northwestern.edu/bin/docs/BI_Database_Naming_Standards.pdf">
"Data base object naming standards: Abbreviations"</a>
is a huge list prefaced by the words
"In general, abbreviations should be used only when length restrictions prevent use of fully spelled-out words in object names."</p>

<H3 id="names-delimiter">Names (delimiter)</H3><HR>

<p>Choice: Should identifiers be delimited?</p>

<p>If possible this means enclosing "..."s as in standard SQL, but may mean enclosing `...`s or enclosing [...]s.</p>

<p>Again, there might be some reason for explanatory names for reporting requirements,
but for programming requirements the only possible reasons would be:<br>
() You are using more than one SQL dialect and you want to maintain the same names in both dialects<br>
() You prefer case sensitive names and your SQL dialect follows the SQL standard requirement for delimited identifiers.</p>

<p>Re [...]: Microsoft's rules for
<a href="https://docs.microsoft.com/en-us/sql/t-sql/statements/set-quoted-identifier-transact-sql?view=sql-server-ver15">
SET QUOTED_IDENTIFIER</a>
are so complicated that nobody can be blamed for using []s instead.</p>

<p>Re `...`: Although people call them backticks when used for delimiting, the real (Unicode) name is U+0060 "grave accent".
If you have a French keyboard where a grave accent is a
<a href="https://en.wikipedia.org/wiki/Dead_key">"dead key"</a>,
it might be troublesome.</p>

<p>Prescriptive guides:</p>

<p>Sarkuni says: "Avoid quotes."<br>
Donnelly says: "Named objects should not be surrounded by backticks"<br>
Salvisberg says: "avoid double quoted identifiers" ... "Never use quoted identifiers."<br>
Holywell says: "Avoid ... Quoted identifiers -- if you must use them then stick to SQL92 double quotes for portability".</p>

<p>Bloggers:</p>

<p>Apex's
<a href="https://solutioncenter.apexsql.com/rules-of-sql-formatting-regular-and-delimited-t-sql-identifiers/">
 "Rules of SQL formatting"</a> say:
Adding square brackets around all identifiers can be visually distracting.
but they have an option named "Remove unnecessary brackets".</p>

<p>Cloudera's
<a href="https://docs.cloudera.com/documentation/enterprise/5-8-x/topics/impala_identifiers.html">
Impala Guide</a> recommends:
"consider adopting coding conventions (especially for any automated scripts or in packaged applications)
to always quote all identifiers with backticks."</p>

<H3 id="names-qualifier">Names (qualifier)</H3><HR>

<p>Choice: Should names be qualified?</p>

<p>Saying "SELECT employees.id FROM employees;" looks like pleonasm.<br>
Saying "SELECT employees.id FROM employees, departments;" looks like pleonasm but maybe serves a "useful function".<br>
Saying "SELECT id FROM schema_name.table_name;" looks like a necessity if there is no default schema.</p>

<p>I have rarely seen the four-level catalog_name.schema_name.table_name.column_name.
At MySQL we played with it for a while for information_schema but in my opinion we
should have reserved the top level for the server source, which is something that
I think SQL Server has approached.
People who get deep in qualifier mires might be tempted to add aliases.</p>

<p>Prescriptive guides:</p>

<p>Sarkuni says: "All field names in non-trivial SQL statements (i.e. those with more than one table) should be explicitly qualified and prefixing as a form of namespacing field names is a bad idea."<br>
Mazur says: "Include the table when there is a join, but omit it otherwise" (i.e. qualify if there is a join).</p>

<p>Blogs:</p>

<p>Tim Hall passes on advice about
<a href="https://oracle-base.com/blog/2015/11/25/preventing-plsql-name-clashes-you-learn-something-new-every-day/">
avoiding name clashes</a> in PL/SQL.</p>

<p>Aaron Bertrand
<a href="https://www.sentryone.com/blog/aaronbertrand/best-practices-referencing-columns">
says</a> that leaving out a schema name can have side effects.</p>

<p>Steven Feuerstein
<a href="https://mafiadoc.com/best-practices-for-writing-sql-in-pl-sql-steven-toad-world_5a0bd1d11723dd78fd2e7266.html">
says</a> "Qualify every identifier in SQL statements."</p>

<H3 id="names-prefix-or-suffix">Names (prefix or suffix)</H3><HR>

<p>Choice: Should any object name have any prefix or suffix?</p>

<p>Some say that an object's name should indicate its type, and some say otherwise.
I will just note here what the otherwise-sayers say in prescriptive guides.
Sarkuni says: "Object names should not include the object type in them."
Mullins says: "it is a bad idea to embed specialized meaning into database object names"
(he gives an example of a suffix that means unique, and asks what if it is also a foreign key).
Salvisberg says: "Avoid adding redundant or meaningless prefixes and suffixes to identifiers. Example: CREATE TABLE emp_table."
Holywell says: "Avoid ... Descriptive prefixes or Hungarian notation such as sp_ or tbl."</p>

<p>Improve your vocabulary again ...
Factor
<a href="https://www.red-gate.com/simple-talk/sql/t-sql-programming/laying-out-sql-code/">says</a>:
"The habit most resistant to eradication is "Tibbling," the use of reverse Hungarian notation,
a habit endemic among those who started out with Microsoft Access.
A tibbler will prefix the name of a table with "tbl," thereby making it difficult to pronounce."</p>

<p>Keller says: "Avoid prefixes and suffixes for tables and views, such as tblTable.
Hungarian notation (which was always intended to identify variable usage)
slipped into common SQL Server naming conventions, but it is widely derided.
Object identifiers should describe what is contained within, not the object itself."</p>

<p>But other prescriptive guides say: go for it.</p>

<p>So in later sections I will repeat the advice of people who advocate prefixes and suffixes,
but those sections all have an implicit caveat: others disagree with all such paraphernalia.</p>

<p>If you decide "Should any object name have any prefix or suffix=no", then
ignore any prefix/suffix Choices in following sections.</p>

<H3 id="names-of-tables">Names of tables</H3><HR>

<p>Choice: Should table names be plural?</p>

<p>Sometimes no. In English and many other languages pluralizing can be confusing
or inconsistent. Some tables by definition have exactly one row so demanding
plurals everywhere can be excessive. And of course sometimes noted authorities
say use singular, so just go along to get along.</p>

<p>One authority that is sometimes brought in is Codd.
He used singular for relations.
But
<a href="http://www.dbdebunk.com/2019/05/naming-relations-singular-or-plural.html">
Fabian Pascal</a> says
"In other words, there is no relational (i.e., formal theoretical) reason for preferring one over the other -- Codd's
reference to the "Supplier relation" should not be taken to mean imposition of the singular."</p>

<p>One authority that is sometimes brought in is
<a href="https://en.wikipedia.org/wiki/ISO/IEC_11179">ISO 11179</a>.
But I have been unable to find where that states that singular names are better,
and it seems that
<a href="https://social.msdn.microsoft.com/Forums/en-US/d5f2faf3-3c85-413d-bc09-ce1d477b31e8/iso-111795-and-table-names?forum=transactsql">
other people</a>
have also been unable.</p>

<p>Prescriptive guides:</p>

<p>Hall says: All table names should be plural. If the table name contains several words, only the last one should be plural.
Example: APPLICATION_FUNCTION_ROLES</p>

<p>Sarkuni says: "Tables, views, and other relations that hold data should have singular names, not plural.
Rather than going into the relational algebra explanation of why this is correct I will give a few practical reasons.
They're Consistent. It's possible to have a relation that holds a single row. Is it still plural?
They're unambiguous. Using only singular names means you do not need to determine how to pluralize nouns.
Ex: Does a "Person" object go into a "Persons" relation or a "People" one? How about an "Octopus" object? Octopuses? Octopi? Octopodes?
Straightforward 4GL Translation. Singular names allow you to directly translate from 4GL objects to database relations. You may need to remove some underscores and switch to camel case but the name translation will always be straight forward.
Ex: team_member unambigously becomes the class TeamMember in Java or the variable team_member in Python."</p>

<p>Keller says: "At first glance, it’s natural to think of a collection of objects in the plural. A group of several individuals or companies would be Customers. Therefore, a table (being a collection of objects) should be named in the plural. An individual row in that table would be a single customer.
The ISO/IEC naming principles, while dated, recommend pluralized table names and singular column names.
Most SQL Server system tables use plural names (sysnotifications, sysoperators), but this is inconsistent. Why sysproxylogin and not sysproxylogins?"
... "Because pluralization of words can vary in so many ways (customers, mice, moose, children,
crises, syllabi, aircraft), non-native speakers have additional challenges.
Sticking with singular object names avoids this problem entirely."</p>

<p>Salvisberg says: "Plural name of what is contained in the table (unless the table is designed to always hold one row only – then you should use a singular name)."
and "A jar containing beans is labeled "beans"."</p>

<p>Mazur says: "Table names should be a plural snake case of the noun"</p>

<p>Holywell says: "Avoid ... Plurals—use the more natural collective term where possible instead. For example staff instead of employees or people instead of individuals.
          ... "Use a collective name or, less ideally, a plural form. For example (in order of preference) staff and employees."</p>

<p>Taranov says: not plural.</p>

<p>In some SQL standard examples, there are plurals when contents can be plural, singular when contents can only be singular</p>

<p>Bloggers:</p>

<p>Peter Gulutzan (also known as "I") said long ago in 
<a href="http://www.dbazine.com/db2/db2-disarticles/gulutzan5/">"SQL Naming Conventions"</a>:
Example: SELECT * FROM beans; not SELECT * FROM bean;</p>
	
<p>Ben Brumm says in <a href='https://www.databasestar.com/sql-best-practices/'>SQL Best Practices and Style Guide</a> that singular table names are preferred, but it's important to be consistent with your team and the existing database.</p>

<H3 id="names-of-temporary-tables">Names of temporary tables</H3><HR>

<p>Choice: temporary table name prefix = # or tmp or temp or nothing?</p>

<p>With some DBMSs, it is possible to create a table named A <i>and</i> a temporary table named A.
References to A will only find the temporary table, and the result is occasional confusion.
So it might be okay to recommend, or force, people to distinguish temporary table names.</p>

<p>Prescriptive guides:</p>

<p>Salvisberg says temporary tables can have an optional suffix _tmp.</p>

<p>Vendor manuals:</p>

<p>In
<a href="https://docs.microsoft.com/en-us/sql/t-sql/statements/create-table-transact-sql?view=sql-server-ver15">
SQL Server</a>
a prefix # or ## is compulsory. (The Unicode name for the # symbol is "number sign", not
"hash mark" and, alas, not the lovely word
<a href="https://www.merriam-webster.com/dictionary/octothorpe)">"octothorpe"</a>).</p>

<p>Bloggers:</p>

<p>Stephen Faroult and Pascal l'Hermite in
<a href="https://books.google.ca/books?id=ua7lCQAAQBAJ&pg=PA44&lpg=PA44&dq=sql+Table+names+which+are+temporary+may+have+the+suffix+_tmp&source=bl&ots=7aywb7Pfb_&sig=ACfU3U3jCUN7c2l6_HXWEkaCCzbBL9PUGw&hl=en&sa=X&ved=2ahUKEwjwyc-b4sfoAhU1On0KHccyCC0Q6AEwCnoECA0QKQ#v=onepage&q=sql%20Table%20names%20which%20are%20temporary%20may%20have%20the%20suffix%20_tmp&f=false">
 "Refactoring SQL Applications"</a>
suggest that it is common for temporary tables to
have a prefix or suffix of TMP or TEMP.</p>

<H3 id="names-of-views">Names of views</H3><HR>

<p>Choice: view name prefix = v_ or vi_ or vw_ or nothing?<br>
Choice: view name suffix = _v or _vi or _vw or nothing?</p>

<p>View names are table names and are not distinguished from base table names.</p>

<p>Views are tables so the Choices in the previous section are applicable.
However, sometimes people want to distinguish them with a prefix or suffix.
In particular, I have seen a suggestion that,
if a view is of a single base table, its name may be
the base table name plus the suffix _v.</p>

<p>Keller says: view suffix = _v.
Taranov says:  View prefix = VI_
Salvisberg says: optionally add _v</p>

<p>Bloggers:</p>

<p>Joe Celko
<a href="https://www.red-gate.com/simple-talk/sql/learn-sql-server/sql-view-basics/">
says</a>
"VIEWs are often named incorrectly. A VIEW is a table, so it is named just like any other table.
The name tells us what set of things it represents in the data model.
The most common offender is the “Volkswagen” coder who prefixes or suffixes
the VIEW name with “vw_” or “VIEW_” in violation of ISO-11179 rules.
We do not mix data and meta data in a name.
This is as silly as prefixing every noun in a novel with “n_” so the reader will
know that  the word is a noun in English grammar."</p>

<p>(That reminds me that once upon a time writers
<a href="https://english.stackexchange.com/questions/10522/capitalisation-of-nouns-in-english-in-the-17th-and-18th-centuries">
did distinguish nouns by capitalizing them</a>. Germans still do.)</p>

<p>Sharad Maheshwari and Ruchin Jain,
<a href="https://books.google.ca/books?id=nt-T0cfaWPoC&pg=PA458&lpg=PA458&dq=%22create+view%22+%22vw%22+prefix&source=bl&ots=ZHvX9BhM43&sig=ACfU3U0VGvR758Gfo0MqzNBm69MzxbWZbQ&hl=en&sa=X&ved=2ahUKEwibn5in_eXoAhVfJzQIHTBUBCgQ6AEwAHoECAsQKQ#v=onepage&q=%22create%20view%22%20%22vw%22%20prefix&f=false">
"DBMS – Complete Practical Approach"</a>, say: "All view names must begin with of the following prefixes: vw, VW, v, or V."</p>

<p>Mullins says: "avoid embedding a 'T', or any other character, into table names to indicate that the object is a table.
Likewise, indicator characters should be avoided for any other table-like object (i.e. aliases, synonyms, and views)."</p>

<p>isbe.net
<a href="https://www.isbe.net/Documents/SQL_server_standards.pdf">
"Naming conventions"</a> says: prefix with vw.</p>

<H3 id="names-of-columns">Names of columns</H3><HR>

<p>Choice: Should column name include table name or abbreviated table name?</p>

<p>Column names are singular, although I suppose that columns with an array or multiset data type might not be
(the only guide that suggests such an exception is Salvisberg).</p>

<p>The name "id",
which is an abbreviation of
<a href="https://dictionary.cambridge.org/dictionary/english/id">identification</a>,
usually for a unique-key column with a numeric data type, is popular.
But opinions vary whether a column should be named id or have a suffix _id.
If you join two tables, and they both have a column named id, then you are forced to qualify.
But if you avoid that by putting the table name in the column name,
for example the employees table has employee_id and the departments table has department_id,
then you are being redundant because you already know what tables the columns are in.
An advantage of naming all primary keys id is: you know what it is without looking it up.</p>

<p>Names in other computer languages have hints about types, for example is_fat is probably a boolean.
But opinions vary whether this should occur in SQL.</p>

<p>Prescriptive guides:</p>

<p>Hall says: do not include table name or alias.</p>

<p>Sarkuni says: name = id is okay ("This means that when you're writing SQL you don't have to remember the names of the fields to join on")
and a column referencing it should have referenced-table-name and suffix _id.</p>

<p>But Keller says: if there is a column referencing it, then name = CustomerID is better than Customer.ID.</p>

<p>Holywell says: name = id is not okay ("avoid").</p>

<p>Mazur says: 
"Boolean fields should be prefixed with is_, has_, or does_. For example, is_customer, has_unsubscribed, etc."</p>

<p>Vendor manuals:</p>

<p>I checked what column names were in examples for the CREATE TABLE statement.</p>

<p>MariaDB: a, b, expires, x<br>
MySQL: id, name, a, b, adate, s1, s2<br>
Oracle: employee_id, first_name, last_name, email, phone_number, hire_date, job_id, salary, commission_pct,
manager_id, department_id, dn, id, col1, col2, title, author, department_id, department_name, etc.<br>
DB2: DEPTNO, DEPTNAME, MGRNO, ADMRDEPT, PROJNO, PROJNAME, RESPEMP, PRSTAFF, PRSTDATE, EMPNO, SALARY, ID, NAME, LIVING_DIST,
SSN, VOICE, PHOTO, HIREDATE, COMM, ACTNO, EMPTiME, etc.<br>
SQL Server: col1, x, EmployeeID, PurchaseOrderID, LineNumber, ProductID, UnitPrice, OrderQty,
ReceivedQty, RejectedQty, DueDate, rowguid, LineTotal, StockedQty, LName, FName, GUID, low, high, etc.<br>
Tarantool: s1, s2<br>
... Notice the frequency of _id or NO suffix, DB2's love of abbreviations, and
how both MySQL and Tarantool use s1 and s2 (you can blame me for that, s stands for Spalte which is the German word for column).
Notice that SQL Server does capitalize when there is only one word, but probably this is not a rule.</p>

<p>Blogs:</p>

<p>Lukas Eder
<a href="https://blog.jooq.org/author/lukaseder/">
points out</a> that qualifying id in SQL statements is not good enough
if you also have to distinguish in a Java client.</p>

<p>Power BI 
(apparently thinking about things like report headings) 
<a href="https://www.sqlbi.com/articles/data-import-best-practices-in-power-bi/">says</a>:
"For example, you should use “Sales Amount” instead of “SalesAmt” or “SalesAmount”.
You can use space and special characters in column names of a view.
The goal is to simplify the life to the user,
and not to simplify the life to a programmer who has to type a column name in the keyboard."</p>

<H3 id="names-of-aliases-and-range-variables">Names of aliases and range variables</H3><HR>

<p>Choice: Should aliases / range variables be abbreviations?</p>

<p>In a select list a column can be named with [AS] alias-name.
Aliases can be used in ORDER BY, and in MySQL/MariaDB can be used in GROUP BY,
and with
(rarely supported)
<a href="https://aws.amazon.com/about-aws/whats-new/2018/08/amazon-redshift-announces-support-for-lateral-column-alias-reference/">
"lateral column aliasing"</a> they can even be used later in the select list,
but the main purpose is just so that the result name can be short and legal.
Vendors might invent names for expressions but they can vary and can be odd.</p>

<p>Also in FROM etc. an [AS] name clause can appear.
Often the name is called an alias but in standard SQL terms
like "correlation name" and "range variable" are preferred.
One main purpose is to avoid repeating long qualified names.</p>

<p>For columns the common idea is to be comprehensible,
for tables the common idea is to be short.</p>

<p>Prescriptive guides:</p>

<p>Holywell, Mazur, and Taranov say: Always be explicit and say AS name. Pleonasm does not apply.<br>
Donnelly says: Always be explicit and say AS name -- for columns. "Column aliases should always use the keyword AS"<br>
Donnelly says: "Tiny names for table aliases can sometimes work as abbreviations."<br>
Holywell says: maybe, alias name should be first letter of each word in a table name<br>
Mazur says: "Avoid aliasing table names most of the time"<br>
Benenson says: "Always rename all columns when selecting with table aliases"<br>
Salvisberg says: "Always use table aliases when your SQL statement involves more than one source."</p>

<p>Vendor manuals:</p>

<p>Oracle: "AVG(salary) AS avgsal"</p>

<p>SQL Server: "AVG(UnitPrice) AS [Average Price]" ... 
an
<a href="https://docs.microsoft.com/en-us/previous-versions/sql/sql-server-2008-r2/ms179300(v=sql.105)?redirectedfrom=MSDN">
old version of the manual</a>
says: "The AS clause ... is the preferred syntax to use in SQL Server 2005."
Perhaps one could interpret that as meaning the word AS should be explicit, but I prefer to
believe that it means: stop using the
<a href="https://www.red-gate.com/hub/product-learning/sql-prompt/sql-prompt-code-analysis-avoid-non-standard-column-aliases">
deprecated alternative</a>, an equal sign</p>

<p>MySQL: "CONCAT(last_name,', ',first_name) AS full_name", "id AS 'Customer identity'" (very non-standard) ...
"it is good practice to be in the habit of using AS explicitly when specifying column aliases"</p>

<p>Blogs:</p>

<p><a href="https://solutioncenter.apexsql.com/how-to-improve-sql-code-layout-and-presentation/">
ApexSQL</a>
has an option named "Use first three letters for alias" and an example "HumanResources.EmployeeDepartmentHistory edh".</p>

<p>Aaron Bertrand says: one to three letters, but no random single letters please.</p>

<H3 id="names-of-constraints">Names of constraints</H3><HR>

<p>Choice: Use automatically generated names where possible?<br>
Choice: Constraint (Primary Key) Suffix =  _pk or _PK or nothing<br>
Choice: Constraint (Primary Key) Prefix =  pk or PK or pk_ or PK_ or nothing<br>
Choice: Constraint (Unique Key) Suffix =  uq or UQ or _uq or _UQ or _uk or _UK or nothing<br>
Choice: Constraint (Unique Key) Prefix =  uq or UQ or uq_ or UQ_ or uk_ or UK_ or nothing<br>
Choice: Constraint (Foreign Key) Suffix =  fk or FK or _fk or _FK or nothing<br>
Choice: Constraint (Foreign Key) Prefix =  fk or FK or fk_ or FK_ or nothing<br>
Choice: Constraint (Check) Suffix =  ck or CK or ck_ or CK_ or nothing<br>
Choice: Constraint (Check) Prefix =  ck or CK or _ck or _CK or nothing </p>

<p>Sometimes constraint names are decided by the vendor, for example when the
word UNIQUE is used in a CREATE TABLE statement. This is fine if you
intend to use the vendor's style, but usually it looks machine-generated.
For example if you say CREATE TABLE m (... s1 INTEGER UNIQUE);
for Tarantool it is named unique_unnamed_M_1 (type + name + table-name + integer),
for DB2 it is a timestamp,
for MySQL/MariaDB it is the column name.
If you think that as a human you can do better, you will want to
override the DBMS, always, by specifying with your own system.
And there is no reason that the name of a constraint should differ wildly from the name of an index that it depends on.</p>

<p>Typically a constraint name will include a table name (sometimes abbreviated or aliased),
a column name if applicable, and a suffix indicating the constraint type.
Some suggesters,
for example <a href="https://bugs.mysql.com/bug.php?id=66051">this bugs.mysql.com issue#66051</a>
and cakephp's <a href="https://book.cakephp.org/3/en/intro/conventions.html">"Database Conventions"</a>,
say that for foreign keys the table-name part should be singular, for example if
the table name is orders then the table-name part of the foreign key name should be order.</p>

<p>Prescriptive guides:</p>

<p>Holywell says: depend on the vendor name (generally it is "sufficiently intelligible"), otherwise make a custom name<br>
Keller says: prefix PK or CK or FK or UQ "sometimes"<br>
Hall says: table + _PK or _FK or _CK. For foreign key: referencing-table + referenced-table + _FK. For check: something + _CHK.<br>
Taranov says: PK_ or CK_ or FK_<br>
Salvisberg says:
  For primary key: table + _pk.
  For unique key: table + _uk.
  For check: table + column-or-role + _ck + optional number
  For foreign key: referencing-table + referenced-table + _fk + optional number<br>
Mullins asks: what if a constraint is both foreign-key and unique, what do the suffix-lovers do? I have seen no answers.</p>

<p>Vendor manuals:</p>

<p>Oracle: (for foreign key) fk_deptno, fk_empid_hiredate,
        (for check) check_divname, check_office, 
        (for not null) nn_qty, emp_salary_nn_demo
        (for unique) promo_id_u, wh_unq, emp_email_uk_demo
        (for primary key) loc_id_pk, sales_pk.</p>

<p>DB2: (for check) phoneno_length, YEARSAL,
     (for unique) EMP_ACT_UNIQ,
     (for foreign key) EMP_ACT_PROJ</p>

<p>SQL Server: (for check) CK_emp_id
            (for default) DF_PurchaseOrderDetail_ModifiedDate
            (for primary key) PK_PurchaseOrderDetail_PurchaseOrderID_LineNumber, Guid_PK</p>

<p>MySQL: (for check) c1_nonzero, c2_positive
       (for foreign key) child_ibfk_1</p>

<p>MariaDB: (for check) a_greater</p>

<p>Bloggers:</p>

<p>Microsoft's
<a href="https://docs.microsoft.com/en-us/sql/analysis-services/specify-naming-conventions-schema-generation-analysis-services-multidimensional-data?view=sql-server-2014">
"Schema Generation Wizard"</a>
has options for prefixes of names of primary-key columns and foreign-key columns: PK and FK.</p>

<p>Shane O’Neill has arguments for
<a href="https://nocolumnname.blog/2016/05/25/temporary-tables-naming-constraints/">
why all constraints should have names</a>.</p>

<H3 id="names-of-indexes">Names of indexes</H3><HR>

<p>Choice: Include table name in index name?<br>
Choice: Index name prefix = idx or ix or nothing?<br>
Choice: Index name suffix = i or idx or ix or nothing?<br></p>

<p>Often an index will be associated with a constraint, and so the rules
for "Names of constraints" will apply to indexes. Otherwise, the
components of an index name are:
maybe a prefix, maybe the table name, maybe one or more column names,
maybe a suffix, maybe an ordinal.</p>

<p>For the typical index that is a result of something like<br>
CREATE INDEX index-name ON table-name (column-name [, column-name ...])<br>
the index is in the table's namespace, so there is no problem
having an index named I for one table and another index named I for another table.
Therefore it is redundant to include table-name in index-name, but
it happens anyway.</p>

<p>Prescriptive guides:</p>

<p>Sarkuni says: "Indexes should be explicitly named and include both the table name and the column name(s) indexed.
Including the column names make it much easier to read through SQL explain plans."<br>
Keller says: prefix = IX.<br>
Hall says: name = table + column(s) + _I<br>
Salvisberg says: name = table + column(s)-or-purposes + _idx.</p>

<p>Vendor manual examples:</p>

<p>Oracle: "cust_eff_ix ON customers", "ord_customer_ix ON orders", "idx_personnel ON CLUSTER personnel",
        "area_index ON xwarehouses", "upper_ix ON employees (UPPER(last_name))", 
        "income_ix ON employees(salary + (salary*commission_pct))", "cust_last_name_ix ON customers (cust_last_name)" etc.</p>

<p>DB2: "UNIQUE_NAM ON PROJECT(PROJNAME)", "JOB_BY_DPT ON EMPLOYEE (WORKDEPT, JOB)", "IDX1 ON TAB1 (col1)",
     "MYDOCSIDX ON MYDOCS(DOC)" etc.</p>

<p>SQL Server: "i1 ON t1 (col1)", "IX_VendorID ON ProductVendor (VendorID)"
            "AK_UnitMeasure_Name ON Production.UnitMeasure(Name)", "IX_INDEX_1 ON T1 (C2)" etc.</p>

<p>MySQL: "part_of_name ON customer (name(10))", "idx1 ON t1 ((col1 + col2))", "id_index ON lookup (id)"</p>

<p>MariaDB: "HomePhone ON Employees(Home_Phone)", "xi ON xx5 (x)"</p>

<p>... None of the manuals have a consistent style, but we do see some index names that have prefixes/suffixes,
table names, column names, or function names.</p>

<H3 id="names-of-triggers">Names of triggers</H3><HR>

<p>Choice: Trigger name suffix = _trg or _TRG or _tr or or _TR or nothing?<br>
Choice: Trigger name prefix = _tr or TR_ or nothing?</p>

<p>If a trigger involves an action on a table, everyone seems to agree
that the trigger name should say something about the action and the table.
Not everyone agrees which comes first,
and not everyone agrees what "something" is. It could be the verb as a suffix
(for example _insert) or it could be an abbreviation (for example I or ins)
or it could merely be a "suggestion" of the verb (for example new_).</p>

<p>If for column names you decide "do not include the table name",
why for trigger names should you decide "do include the table name"?
Here is a possible excuse: columns are parts of tables, but
triggers are independent objects, so this is a different matter.
In PostgreSQL a trigger is
<a href="https://www.postgresql.org/docs/current/infoschema-triggers.html">"local" to a table</a>
(a departure from standard SQL) so I do not know whether the usual rules should apply there.</p>

<p>Prescriptive guides:</p>

<p>Hall says: "Trigger names should be made up of the table name, an acronym representing the triggering action and the suffix "_TRG"."
      Example: APPLICATION_BIS_TRG where BIS stands for BEFORE INSERT STATEMENT-LEVEL"<br>
Taranov says: TR_ prefix and _DML or _DDL suffix<br>
Salvisberg says:
either object-name + b or io (for before-row or instead of) i or u or d (for insert or update or delete) without _trg suffix,
or object-name + suggestion-of-the-verb + _trg.</p>

<p>Vendor manuals:</p>

<p>I looked at examples in the CREATE TRIGGER pages and sub-pages.</p>

<p>Oracle: t, "order_info_insert INSTEAD OF INSERT ON order info", dept_emplist_tr
         , "maintain_employee_salaries FOR UPDATE OF salary ON employees</p>

<p>DB2: "NEW_HIRED AFTER INSERT ON EMPLOYEE", "RAISE_LIMIT AFTER UPDATE OF SALARY ON EMPLOYEE"
     "NEWPROD NO CASCADE BEFORE INSERT ON PRODUCT"</p>

<p>SQL Server: reminder1, "Purchasing.LowCredit ON Purchasing.PurchaseOrderHeader AFTER INSERT"
            "connection_limit_trigger ON ALL SERVER WITH EXECUTE AS 'login_test' FOR LOGON"</p>

<p>MySQL: "ins_sum BEFORE INSERT ON account", "ins_transaction BEFORE INSERT ON account",
       "upd_check BEFORE UPDATE ON account"</p>

<p>MariaDB: "increment_animal AFTER INSERT ON animals"</p>

<p>Tarantool: "stores_before_insert BEFORE INSERT ON stores"</p>

<H3 id="names-of-sequences">Names of sequences</H3><HR>

<p>Choice: Sequence name suffix = _seq or nothing?
Choice: Sequence name prefix = sq_ or nothing?</p>

<p>If a sequence is associated with a single other object, such as a table
or the primary-key column of a table, then there is agreement that
the sequence name should say something about that object.
There is no agreement, as I said earlier, to have a prefix or suffix to
indicate object type. </p>

<p>Prescriptive guides:</p>

<p>Salvisberg says: if the sequence is for a table's primary-key generation: table-name-or-abbreviation + _seq<br>
Taranov says: sq_ prefix</p>

<p>Vendor manuals:</p>

<p>Oracle: customers_seq</p>

<p>SQL Server: Test.CountBy1, Test.CountByNeg1, ID_Seq, TestSequence, SmallSeq, DecSeq
            (apparently they're naming based on increment-value and on data type, as well as object-name + suffix)</p>

<p>DB2: ORDER_SEQ</p>

<p>MariaDB: s, s2, s3</p>

<p>Here is
<a href="https://docs.oracle.com/cd/E63231_01/doc/BIAET/GUID-AF634C2B-93D1-4338-A375-30ED1504E741.htm#BIASA24516">
an Oracle document</a> saying _SEQ.
Here is
Oracle's
<a href="https://docs.oracle.com/en/database/oracle/oracle-database/19/tdddg/2-day-developers-guide.pdf">
"2-Day Developer's Guide"</a> saying
"Tip:
When you plan to use a sequence to populate the primary key of a table,
give the sequence a name that reflects this purpose. (This topic uses the naming convention table_name_SEQ.)"</p>

<p>Bloggers:</p>

<p><a href="https://richardfoote.wordpress.com/category/scalable-sequences/">Richard Foote</a> and
<a href="https://mandysandhu.com/2018/03/16/oracle-18c-scalable-sequences/">Mandeep K Sandhu</a> and
<a href="https://www.foxinfotech.in/2018/08/5-oracle-create-sequence-examples.html">Vinish Kapoor</a>
uses _seq.</p>

<p>The <a href="https://knowledgebase.progress.com/articles/Article/P13076?popup=true">
progress.com manual</a> says:
Do not define ORACLE sequences with names ending in _SEQ unless the dataserver manual instructs you to do so.
The DataServer uses ORACLE sequences whose names end in _SEQ for internal purposes.</p>

<p>The
<a href="http://www.sqlquery.com/plsql_style_guide.html">
PL/SQL Style Guide</a>
says all sequence names should end in _seq</p>

<p><a href="https://portal.suncom.myflorida.com/wiki/doku.php?id=oracle_naming_conventions">
SunCom</a> says: add _SEQ</p>

<H3 id="names-of-routines">Names of routines</H3><HR>

<p>Choice: Use prefix or suffix for function or procedure name?</p>

<p>Function names show what the returned value is, and optionally how it was obtained.
Some people
<a href="https://twitter.com/sfonplsql/status/1034879083073556480?lang=en">
wonder</a> whether a "get_" prefix is necessary.<br>
Example: first_initial_of_name<br>
Example: name_in_upper_case_according_to_german_collation</p>

<p>Built-in function names are upper case.
They are not keywords and not reserved (at least not always),
and they are like ordinary functions,
so if we put them in upper case it is not because we are following a general rule that only keywords are
upper case.
However, it is popular to put them in upper case, as some
vendors' manuals show.
Example: SELECT ABS(1); not SELECT abs(1);</p>

<p>Prescriptive guides:</p>

<p>Salvisberg says: (re function)
Name is built from a verb followed by a noun in general. Nevertheless, it is not sensible to call a function get_... as a function always gets something.
The name of the function should answer the question “What is the outcome of the function?”
Optionally prefixed by a project abbreviation.</p>

<p>Salvisberg says: (re procedure)
Name is built from a verb followed by a noun. The name of the procedure should answer the question “What is done?” 
e.g. calculate_salary</p>

<p>Bloggers:</p>

<p>ApexSQL's
<a href="https://solutioncenter.apexsql.com/rules-of-sql-formatting-sql-naming-conventions-and-capitalization-rules/">
Rules of SQL formatting – SQL naming conventions and capitalization rules</a> says:
"Also, the prefix in the name of the stored procedure should not be sp_".</p>

<H3 id="names-of-savepoints">Names of savepoints</H3><HR>

<p>Savepoint names may contain a hint of what went before,
for example after inserting the name could be: inserting.
However, there is no common practice, so there is no need for a "Choice: ..." here.</p>

<p>Vendor manual examples:</p>

<p><a href="https://docs.oracle.com/en/database/oracle/oracle-database/19/lnpls/static-sql.html#GUID-68924CF6-130E-497B-9DA8-7B3E4D510FA6">
Oracle:</a> do_insert my_savepoint</p>

<p><a href="https://www.ibm.com/support/knowledgecenter/SSEPGG_10.1.0/com.ibm.db2.luw.sql.ref.doc/doc/r0003271.html">
DB2:</a> SAVEPOINT1, SAVEPOINT2, SAVEPOINT3</p>

<p><a href="https://docs.microsoft.com/en-us/sql/t-sql/language-elements/save-transaction-transact-sql?view=sql-server-ver15">
SQL Server:</a> ProcedureSave</p>

<p>Tarantool: x</p>

<H3 id="names-of-collations">Names of collations</H3><HR>

<p>Choices: Collation names: BCP style or Microsoft style or roll-your-own?</p>

<p>This would apply only for vendors which allow users to create collations, which are rare.</p>

<p>BCP style is what I call the use of the
Unicode Locale Data Markup Language (LDML), for example
"da-u-ks-level1" where da = language tag for Danish,
u stands for BCP 47's <a href="https://www.ietf.org/rfc/rfc6067.txt">locale extension</a>,
ks is the key for strength
from the
<a href="http://unicode.org/reports/tr35/tr35-collation.html#Collation_Settings">
Collation Settings</a> table
and level1 means level1. No character set or code page.</p>

<p>Microsoft style is what I call the
<a href="https://docs.microsoft.com/en-us/sql/relational-databases/collations/collation-and-unicode-support?view=sql-server-ver15">
suffixes</a>
 and Microsoft's
<a href="https://docs.microsoft.com/en-us/sql/t-sql/statements/sql-server-collation-name-transact-sql?view=sql-server-ver15">
fixed rules</a>:
The suffix _ai ("accent insensitive") and the suffix _ci ("case insensitive").
Although _ci_ai might sometimes be very very roughly equivalent to a standard level1 collation,
level1 really should also mean things like "ignore Japanese katakana/hiragana differences"
and "ignore differences between S and Sharp S"
and much else that has absolutely nothing to do with accents and cases.</p>

<p>The roll-your-own choice would be something more descriptive but less "standard"
than the other choices, for example GermanPhoneBook.</p>

<p>Prescriptive style guides and vendor manual examples: none.</p>

<H3 id="names-of-variables-or-parameters">Names of variables or parameters</H3><HR>

<p>Choice: input-parameter prefix: i_ or in_ or nothing<br>
Choice: output-parameter prefix: out_ or nothing<br>
Choice: local-variable prefix: l_ or v_ or nothing<br>
Choice: parameter names: UPPER CASE or snake_case or PascalCase or camelCase</p>

<p>There is an incentive to use a prefix. Consider a MySQL procedure:<pre>
CREATE TABLE employees (thing INTEGER);
INSERT INTO employees VALUES (0);
CREATE PROCEDURE select_thing()
BEGIN
 DECLARE thing INTEGER DEFAULT 1;
 SELECT thing FROM employees;
END;</pre>
Will it select 0 or 1?
Yes there is a rule -- <a href="https://bugs.mysql.com/bug.php?id=5967">MySQL bug 5967</a>
where Konstantin Osipov improves our vocabulary again by mentioning "name shadowing" --
but it is easy to forget it.
So if there was a convention that always distinguished column names
from variable names, this particular confusion could be avoided.</p>

<p>Standard SQL allows for qualifying variable names with the block label,
but not all vendors allow that.</p>

<p>Prescriptive guides:</p>

<p>Hall says: "PL/SQL variables are prefixed with a single letter, if possible, to indicate their type or usage."
      e.g. l_ + local variable name, i_ for input parameter name</p>

<p>Salvisberg says: in_ prefix for input parameter, out_ prefix for output parameter, l_ prefix for local variable</p>

<p>Taranov says: "Parameters name should be in camelCase"</p>

<p>Vendor manual examples:</p>

<p>I only looked at DECLARE examples:</p>

<p><a href="https://docs.oracle.com/en/database/oracle/oracle-database/19/lnpls/plsql-language-fundamentals.html#GUID-EDB2297F-A80D-48B3-8EF1-5437BF981CC2">
Oracle:</a> no suffixes or prefixes, snake_case</p>

<p><a href="https://www.ibm.com/support/knowledgecenter/SSEPGG_11.5.0/com.ibm.db2.luw.apdv.sqlpl.doc/doc/c0020497.html">
DB2:</a> Prefix v_ then camelCase, for example v_rowsChanged</p>

<p><a href="https://docs.microsoft.com/en-us/sql/t-sql/language-elements/declare-local-variable-transact-sql?view=sql-server-ver15">
SQL Server:</a> Variable names always start with @, after that the case examples are inconsistent.</p>

<p>Bloggers:</p>

<p>Malcolm Coxall,
<a href="https://books.google.ca/books?id=itSi0r6mXoAC&pg=PT77&lpg=PT77&dq=Parameters+names+must+begin+with+p_&source=bl&ots=zt5HiFW67o&sig=ACfU3U056o-XjFZL58GcESVzWZMnnUUNtw&hl=en&sa=X&ved=2ahUKEwiix5HkhuboAhVoCTQIHTjvC-UQ6AEwCnoECAwQKQ#v=onepage&q=Parameters%20names%20must%20begin%20with%20p_&f=false">
"Oracle Quick Guides"</a>, says
"Parameters names must begin with p_. Variable names must begin with v_ ...
IN parameter can be named _in" OUT parameter can be named _out ...
INOUT parameter can be named _inout".</p>

<H3 id="dynamic-sql">Dynamic SQL</H3><HR>

<p>Choice: Use host language's multiple quoting?<br>
Choice: Put SQL statement text in variables?</p>

<p>This applies for EXECUTE IMMEDIATE but also for non-SQL programs that call SQL.
The problem is always that execute("sql-statement") will not look nice if
sql-statement contains "s, forcing escapes. Escapes -- usually \s --
make a statement less easy to read.</p>

<p>Languages such as Lua support
<a href="https://en.wikipedia.org/wiki/String_literal">multiple quoting</a>,
so the Tarantool manual suggests things like<br>
execute([[SELECT 'string-literal' FROM "delimited-table-name";]])<br>
instead of<br>
execute("SELECT 'string-literal' FROM \"delimited-table-name\";")</p>

<p>But maybe you should not pass string literals, you should instead
assign the literals to variables and pass variables.
It is common in other languages to use a variable or a macro for
any constant that might be re-used, and the same could apply
for SQL.</p>

<p>Prescriptive guides:</p>

<p>Salvisberg says: "Always use a character variable to execute dynamic SQL."</p>

<p>Examples from vendor manuals:</p>

<p><a href="https://docs.oracle.com/en/database/oracle/oracle-database/19/lnpls/dynamic-sql.html#GUID-30ADFC05-8DFB-4C8A-831D-426C2E97F217">
Oracle</a> shows an EXECUTE IMMEDIATE statement with a character variable.</p>

<p><a href="https://www.ibm.com/support/knowledgecenter/SSEPEK_11.0.0/apsg/src/tpc/db2z_includedynamicvaryinglistselect.html">
DB2</a> shows an embedded-SQL example with a character variable.</p>

<p>Blogs:</p>

<p><a href="https://books.google.ca/books?id=XUPXAQAAQBAJ&pg=PA29&lpg=PA29&dq=oracle+hash+statement+text+capitalize&source=bl&ots=ZNbcQhS-se&sig=ACfU3U3m6FCnCJLEvd66ASFSnR-KSjduKg&hl=en&sa=X&ved=2ahUKEwivx4-tpcroAhXR854KHfEMCzIQ6AEwAHoECAwQKQ#v=onepage&q=oracle%20hash%20statement%20text%20capitalize&f=false">
"Pro Oracle SQL"</a> says that using bind variables may decrease parsing overhead.</p>

<H3 id="format-terminology">Format terminology</H3><HR>

<p>Choice: format?</p>

<p>Formatting, also called layout, involves
adding or removing white space (spaces or tabs or newlines).
Effects include indenting and aligning.</p>

<p>Choosing format = no means: leave the text as is.</p>

<p>Choosing format = yes means: remove white space that is already in the text,
except in comments or literals or delimited identifiers.
Then add white space according to Choices described in following Format sections.</p>

<p><b>Indenting</b> means: adding
<a href="https://www.lexico.com/definition/indent"> fixed amounts</a>
("units") of whitespace at the start of a line. 
For example one can say that the indent amount is "4 spaces".
Then in this statement the second line is indented:<pre>
TEXT AT LEFT MARGIN, ALSO CALLED THE ZERO POINT
    TEXT INDENTED BY ONE UNIT</pre>
The implication is that the second line is "within", "subsidiary to", "a level below", the first line.</p>

<p>If there is a third line which is subsidiary to the second line, then that is a multi-level indent.<pre>
TEXT AT LEFT MARGIN, ALSO CALLED THE ZERO POINT
    TEXT INDENTED BY ONE UNIT (AT LEVEL ONE)
        TEXT INDENTED BY TWO UNITS (AT LEVEL TWO)
    TEXT INDENTED BY ONE UNIT (AT LEVEL ONE AGAIN)</pre>
I say the first line is at "indent zero", the second line is "indent +1",
and the third line is also at "indent +1" (because "+" will mean "relative to the previous line").
It is not necessary to show "indent -1" because text end is obvious, it is before the next text starts.</p>

<p><b>Aligning</b>, also called lining up, means: placing
non-white-space text underneath non-white-space text on an earlier line.
Left-align is the same as "indent at same level" (i.e. "indent +0 levels"), it
means the first characters align, for example<pre>
TEXT AT LEFT MARGIN
A BIT OF TEXT</pre>
Right-align-of-first-word means the last characters of
the first word align, for example<pre>
TEXT AT LEFT MARGIN
   A BIT OF TEXT</pre>
Right-align-of-last-word means the last characters of the last
word align, for example<pre>
TEXT AT LEFT MARGIN
      A BIT OF TEXT</pre>
Right-aligning may involve shifting earlier shorter strings
to match the longest string, for example<pre>
      TEXT AT LEFT MARGIN
            A BIT OF TEXT
A MUCH LONGER BIT OF TEXT</pre></p>

<p>Phrase means: an uninterrupted series of keywords. Phrases may be treated as units,
and people avoid putting newlines in phrases. Examples:
CREATE OR REPLACE TRIGGER, DROP VIEW IF EXISTS, ROLLBACK TO SAVEPOINT, LEFT OUTER JOIN.
Also I call &gt;= ALL a phrase, though I acknowledge it does not fit my definition exactly.</p>

<p>Clause start means: a word or phrase that begins a clause.
When discussing indenting or aligning, a statement start may be treated as a clause start.</p>

<p>Blogs:</p>

<p><a href="https://www.thatjeffsmith.com/archive/2018/09/can-you-format-my-code-this-way/">
Jeff Smith</a> has examples of formatting with slightly different choices of words.</p>

<H3 id="format-choices-terminology">Format choices terminology</H3><HR>

<p>Format choices are often expressible as:</p>

<p>Change &lt;word-or-phrase&gt; to [&lt;whitespace&gt; +] &lt;word-or-phrase&gt; [+ &lt;whitespace&gt;].</p>

<p>For example, instead of expressing a choice as<br>
Choice: Add spaces around arithmetic operators?<br>
I say<br>
Choice: Replace arithmetic operator with space + arithmetic operator + space?<br>
For one Choice, that does not look simpler.<br>
But for 30 Choices, it is much simpler because all Choices have the same "BNF".</p>

<p>Whitespace is zero or more<br>
"space"       U+0020<br>
"tab"         U+0009 rarely needed if indent units are expressed as spaces<br>
"newline"     go to start of next line, i.e. this is carriage return + line feed. also called line break.<br>
"line feed"   go to same position on next line, rarely needed<br>
"+1 indent"   adding one level of indentation<br>
"-1 indent"   removing one level of indentation, rarely needed<br>
"+0 indent"   to the same level, but this would always be assumed after newline<br>
"0 indent"    to level 0, which is the left margin</p>

<p>There are two default assumptions which are not Choices because they are universal defaults:<br>
"Where K is keyword or literal, Change K + K to K + space + K"<br>
"Change whitespace + newline to newline".</p>

<p>Choices are not cumulative. Once a Choice has been applied for a token, go to the next token.</p>

<p>The initial general assumption is:
All text is changed so that all tokens are separated by a single space.
As we will see in later sections, that assumption can be overridden,
especially when there are comments and parentheses.</p>

<p>So most formatting choices can be phrased as:<br>
Choice: [For a particular situation]<br>
          [before] add N newlines, indent N levels or left-align or right-align<br>
          [after] add N newlines<br>
Example = "Choice: change FROM to 1 newline + indent+1 + FROM + [nothing]<br>
          "Choice: change WHERE to 1 newline + indent+0 + WHERE + [nothing]<br>
          "Choice: change AND to 1 newline + right-align + AND + [nothing]<br><pre>
SELECT skill
    FROM employees
    WHERE 0 = 0
      AND 1 = 1;</pre></p>

<H3 id="format-symbols">Format symbols</H3><HR>

<p>Choice: change arithmetic operator to space + arithmetic operator + space?<br>
Choice: change comparison operator to space + comparison operator + space?<br>
Choice: && and || meaning OR are equivalent to AND and OR?<br>
Choice: change . to space + . + space, or to .?<br>
Choice: change || meaning concatenate to || + newline?<br>
Choice: change semicolon to space + semicolon?<br>
Choice: change comma to comma + space?</p>

<p>In this context a symbol is a token which is made up of non-alphabetic
characters, such as = or &lt;&gt;.
SQL does not require that symbols must be separated by white space,
for example ('x'||'y'='z'AND-1="5") and ( 'x' || 'y' = 'z' AND -1 = "5" ) are the same.
Therefore there are Choices for symbols but not for other tokens.</p>

<p>A binary operator is a symbol that separates two operands.
The operation may be arithmetic, concatenation, bitwise, comparison, or assignment.
Generally it does not matter -- all binary operators except . have the same rule,
and the unanimous opinion of prescriptive guides is that that rule should be:
change binary operator to space + binary operator + space = yes.
But there are three possible exceptions: for &amp;&amp; and || meaning OR, for ., and for || meaning concatenate.</p>

<p>By the way the SQL standard term is "dyadic operator" but
<a href="https://books.google.com/ngrams/graph?content=binary+operator%2C+dyadic+operator&year_start=1800&year_end=2008&corpus=15&smoothing=3&share=&direct_url=t1%3B%2Cbinary%20operator%3B%2Cc0%3B.t1%3B%2Cdyadic%20operator%3B%2Cc0">
according to Google Ngrams</a> the term "binary operator" is much more common.</p>

<p>"&amp;&amp; and || are equivalent to AND and OR: yes" would only apply for
MYSQL/MariaDB. See "Format AND / OR". There is no guidance for this setting.</p>

<p>"change . to space + . + space" means that qualified identifiers
look like "table_name.column_name" instead of "table_name&nbsp;.&nbsp;column_name".
It is clear from vendor examples that "table_name.column_name" is the
preference, but I have seen exceptions.</p>

<p>"change || meaning concatenate to || + newline"
is a Choice because there is a formatter that has special options for ||.
I suspect that this choice exists for the sake of long literals.
See section <a href="#long-literals">Long literals</a>.</p>

<p>Another, more general, exception is: operators can be aligned if they
are in lists.
See section <a href="#format-lists">Format lists"</a>.</p>

<p>There is no Choice for other (monadic) operators such as unary minus
or ~ for negation. They are always: space + operator, with no space before the next token.</p>

<p>There is no choice for : when it is used with a label in SQL/PSM.
It is always : + space, with no space before the previous token.</p>

<p>"change semicolon to space + semicolon" is an uncommon choice but I have seen "&nbsp;;"
<a href="https://docs.microsoft.com/en-us/sql/t-sql/statements/create-view-transact-sql?view=sql-server-ver15">
in the Microsoft manual</a>
and I have read that in eclipse it is
<a href="https://bugs.eclipse.org/bugs/show_bug.cgi?id=485495">
considered a bug</a>
if the formatter always removes space before semicolon.</p>

<p>"change comma to comma space" is applicable only for commas
that are not in a list (see <a href="#format-lists">Format lists</a>).
So the Choice affects function arguments like substring(1,2)
or declarations like DECIMAL(5,3).
Style guides for C, such as 
<a href="http://www.cs.umd.edu/~nelson/classes/resources/cstyleguide/">this one at umd.edu</a>, say
"Leave one space after a comma", but are probably not applicable.</p>

<p>Prescriptive guides:</p>

<p>Taranov gives an example where + instead of || is used for concatenation.
Holywell says: "Although not exhaustive always include spaces: before and after equals (=) after commas (,) surrounding apostrophes (') where not within parentheses or with a trailing comma or semicolon."</p>

<p>Vendor Manuals:</p>

<p>In the MariaDB manual there is sometimes no spacing around = or before *.</p>

<p>Some Oracle examples are
<a href="https://docs.oracle.com/cd/B19306_01/server.102/b14200/operators002.htm">
here</a>.</p>

<p>Oracle SQL Developer has three options:
"Spaces around operators (= &lt; &gt; + - * /)", "Spaces around commas", "Spaces around brackets [i.e. parentheses]"</p>

<p>Bloggers:</p>

<p>ApexSQL: there is an option for "add space inside parentheses"</p>

<p>Toad has a single option for "Plus-Minus-Mul-Div-Concat".</p>

<H3 id="format-parentheses">Format parentheses</H3><HR>

<p>Choice: change table-name + ( to table-name + space + (?<br>
Choice: change built-in-routine-name + ( to built-in-routine-name + space + (?<br>
Choice: change user-defined-routine-name + ( to user-defined-routine-name + space + (?<br>
Choice: change data-type + ( to data-type + space + (?<br>
Choice: change ( to ( + space?<br>
Choice: change ) to space + )?</p>

<p>Choice: align ) with statement start?</p>

<p>"change table-name + ( to table-name + space + (?"
affects things like
table-name(column-name) as in CREATE TABLE table-name(column-name),
INSERT INTO table-name(column-name), CREATE INDEX index-name ON table-name(column-name).
The most common setting is: yes.</p>

<p>"change built-in-routine-name + ( to built-in-routine-name + space + (?"
is the decision whether to say UPPER(...) or UPPER&nbsp;(...).
"change user-defined-routine-name + ( to user-defined-routine-name + space + (?"
is the decision whether to say user_function(...) or user_function&nbsp;(...)
Often the setting is No for both.
But sometimes there are recommendations to say Yes for one and No for the other,
so that it will be clear from the syntax what kind of routine you are calling.
I am guessing that this happened because of C guidelines,
for example <a href="https://users.ece.cmu.edu/~eno/coding/CCodingStandard.html">this one at cmu.edu</a>, that say
"Do not put parens next to keywords. Put a space between.
Do put parens next to function names. 
Keywords are not functions. By putting parens next to keywords keywords and function names are made to look alike."
The
<a href="https://www.oracle.com/technetwork/java/codeconventions-150003.pdf">
Java Code Conventions</a> are similar.
But if that is the reasoning, it is an example of how C/Java rules get applied to SQL unnecessarily.</p>

<p>"change data-type + ( to data-type + space + ("
is the decision to say VARCHAR&nbsp;(10) instead of VARCHAR(10).
Really, nobody does. But I state it as a choice because it seems to be the
only case where reserved-word + ( does not become reserved-word + space + (.
Think of "IF (", "IN (", "WHILE (", "&gt;= ALL (", "SELECT (", "VALUES (".</p>

<p>"change ( to ( + space" and "change ) to space + )"
is rare, but I have seen a recommendation for it.
Notice that this would change <code>(((...)))</code> to <code>(&nbsp;(&nbsp;(&nbsp;...&nbsp;)&nbsp;)&nbsp;)</code>.</p>

<p>For operator (expression) see <a href="#format-symbolss">Format symbols</a>.</p>

<p>For (expression list) or (column list) see <a href="#format-lists">Format lists</a>.</p>

<p>Prescriptive guides:</p>

<p>Mazur says:  "Avoid spaces inside of parenthesis".</p>

<p>Vendor manuals:</p>

<p>In all vendor manuals, I was able to find parentheses in conditional expressions
which did not contain a space after ( or a space before ).</p>

<p>The SQL standard document uses <code>(&nbsp;(&nbsp;(</code> consistently.</p>

<p>Bloggers:</p>

<p>Michael Kruckenberg and Jay Pipes, in
<a href="https://books.google.ca/books?id=FAbmW1WdUWkC&pg=PA383&lpg=PA383&dq=sql+%22style+guide%22+%22create+function%22&source=bl&ots=e1-8p4Pmp4&sig=ACfU3U3XoY0W10ArLjlpAWBE8oQfZyYNHQ&hl=en&sa=X&ved=2ahUKEwj0-MHMxOboAhWMsZ4KHTeNAFEQ6AEwAnoECAwQKQ#v=onepage&q=sql%20%22style%20guide%22%20%22create%20function%22&f=false">
"pro SQL"</a>, say:
"you may want to have your style guide
require that SQL statements always include a space after the function name
when using stored functions." This tip might depend on the proper setting
of sql_mode=ignore_spaces in MySQL or MariaDB.</p>

<p>"Choice: Change ( to ( + newline + indent+1" in combination with
"Choice: align ) with statement start = yes" is something I have
only seen for<br>
CREATE TABLE ... ( (Holywell)<br>
ALTER TABLE ...( (Taranov)<br>
and WITH ... (. (Taranov, Mazur, Benenson).<br>
That is, the effect is<pre>
VERB name-or-expression (
)</pre></p>

<p><a href="https://blog.jooq.org/2020/03/03/better-understand-sql-by-adding-optional-parentheses/">
Lukas Eder</a>
has some recommendations about when parentheses are good, and when they are not.</p>

<H3 id="format-comments">Format comments</H3><HR>

<p>Choice: change simple comment to simple comment + 1 newline?</p>

<p>This is not really a choice, because nothing else makes sense.
I cannot think of another time in SQL where &lt;newline&gt; cannot be eliminated or replaced by some other white space.
Therefore it might be handy to put -- at the end of a line, to prevent a formatter program from removing the newline.</p>

<p>Choice: Put bracketed comment with following keyword.<br>
Choice: Put bracketed comment after comma in a list.<br>
Choice: Put bracketed comment on separate line, left-align?</p>

<p>Given<br>
SELECT skill /* per test */ FROM employees;<br>
only a human could know whether the comment is about the
column or about the FROM clause. Therefore, the human
who writes the statement should signal.
One way is to stick to the advice in section <a href="#comments">Comments</a>
and always put bracketed comments before their subjects.
Another way is to put extra whitespace around the
comment, and a formatter program should take that into account.
(That is especially applicable for a comment within a phrase.)
If neither of those solutions can be trusted, the comment
will have to go on a line of its own.</p>

<p>Prescriptive guides:</p>

<p>Holywell has an example of a bracketed comment preceding the statement, on its own line.</p>

<p>Vendor examples:</p>

<p><a href="https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/Comments.html#GUID-5C84C344-CEB3-4DBF-B748-337DE11CCE2A">
Oracle:</a> Bracketed comments may precede or may follow.</p>

<p><a href="https://www.ibm.com/support/knowledgecenter/SSEPGG_10.5.0/com.ibm.db2.luw.sql.ref.doc/doc/c0056402.html">
DB2:</a> Bracketed comments are at end of line (same as simple comments) but can include newlines (unlike simple comments).</p>

<p><a href="https://docs.microsoft.com/en-us/sql/t-sql/language-elements/slash-star-comment-transact-sql?view=sql-server-ver15">
SQL Server:</a> Bracketed multi-line comment precedes the whole statement.</p>

<p><a href="https://dev.mysql.com/doc/refman/8.0/en/comments.html">
MySQL:</a> Hints come after the word SELECT and clearly belong with it.</p>

<p><a href="https://mariadb.com/kb/en/comment-syntax/">
MariaDB:</a> Comments come at end of statement but before semicolon.</p>

<p><a href="https://www.tarantool.io/en/doc/2.3/reference/reference_sql/sql/">
Tarantool:</a> Comments come on the same line either before after the semicolon.</p>

<p>Blogs:</p>

<p>Toad has folding for: "multi-line comments, multiple single-line comments on consecutive lines"</p>

<H3 id="format-line-length">Format line length</H3><HR>

<p>Choice: Left margin: N?<br>
Choice: Right margin: N?<br>
Choice: Threshold = N?<br>
Choice: If SQL statement length &lt; Maximum line length: skip all other format choices?</p>

<p>Ordinarily Left margin = 1 because, as in editors, the minimum column number on a line is 1, not 0.
However, for indenting a left edge is called a
<a href="https://books.google.ca/books?id=CWrNgcnCeSYC&pg=PA31&lpg=PA31&dq=%22indenting%22+%22zero+point%22&source=bl&ots=8vzHYimkEJ&sig=ACfU3U0pztZ9Ho6lmZkJ4X3We1hq3VSnLg&hl=en&sa=X&ved=2ahUKEwjd1uS5xejoAhWlFjQIHVMUD10Q6AEwAXoECAsQKQ#v=onepage&q=%22indenting%22%20%22zero%20point%22&f=false">
"zero point"</a> as in editors, so "indent 0" means the Left margin.</p>

<p>Therefore Right margin - Left margin = Maximum line length.
"Maximum characters per line" would be a better term
but "Line length" is a term that infests style guides
so I stick with it.</p>

<p>There is no consensus what Maximum line length should be, and
computer
<a href="https://en.wikipedia.org/wiki/Characters_per_line#In_programming">
 style guides for other languages</a>
vary greatly.
Suggestions include: 72, 80, 120.
It might be useful to ask how wide is a screen, or how wide is a printed page,
but those too are things which vary greatly,
so it is prudent to assume that different people will choose different values.</p>

<p>"Threshold" -- not a common term -- is a position before
the Right margin. The correct effects of passing the Threshold
are not all clear to me, but I speculate that they include
squeezing the contents because space is getting dear.
For example, if Right margin = 80 and Threshold = 60
and length-of-text = 70, then one might ignore any changes
which require further indenting,
and ignore changes which require adding unnecessary spaces.</p>

<p>"If SQL statement length &lt; Maximum line length: skip all other format choices = yes"
means you do not have to indent anything if the entire statement can fit on one line.
In other words, if you decide = yes, then this short line remains as is:<br>
SELECT skill FROM employees;</p>

<p>But if you decide = no,<br>
or,<br>
if SQL statement length &gt;= Maximum length,<br>
then there is a need for more than one line.
The newlines should, if at all possible,
be on some lexical boundary.
Usually that means "newline for new clause" and I will devote several sections
to clauses, as well as to "Format lists".</p>

<p>Prescriptive guides:</p>

<p>Donnelly says: "Newlines should be used for any query that is at all complex or longer than 72 characters."</p>

<p>Mazur says:
"The only time you should place all of your SQL on a single line
is when you're selecting one thing and there's no additional complexity in the query:"</p>

<p>Vendor manuals:</p>

<p>Oracle SQL Developer once had options for "schema type = small SQL"
and "threshold for small SQL = N", and
(<a href="https://www.databaseusers.com/article/7532979/Searching+for+deailed+info+on+code+formatting+rules">
as far as I can make out</a>)
you could use this for the equivalent of "Choice: no indenting if statement length less than N".
This is no longer true.
Nevertheless I quote an earlier description:
"If you set the 'Schema Type' to small SQL - you have to mind the 'Threshold for small SQL'
as that allows you to leave code lines that don't meet that threshold untouched,
which is nice if you want to avoid unnecessary line breaks for very small lines of code."</p>

<p>Bloggers:</p>

<p>Factor says: "SQL code doesn't have to be broken into short lines like a Haiku poem
... to specify that there must always be a line-break between each phrase
(before the FROM, ON, and WHERE clauses, for example) can introduce an unnecessary amount of white space into code."</p>

<p><a href="https://www.fonts.com/content/learning/fontology/level-2/text-typography/length-column-width">
Fontology</a> says:
"To determine line length for optimum readability, a good guideline is between 9 and 12 words for unjustified text."
That establishes that "line length" can be the right phrase. But SQL Developer has an option "Max char line width".</p>

<p>This
<a href="https://forums.toadworld.com/t/formatter-puts-as-clause-on-a-separate-line/39050/4">
exchange on toadworld.com</a>
shows that Toad formatter by default goes as far as line length even if there are
clauses, but (in Toad parlance) "folds" if line length is small.
Also
<a href="http://toad.10940.n7.nabble.com/Formatter-JOIN-ON-td26506.html">
this</a>
shows how Toad "folds" when you change right margin.
It is pretty clear that it initially will not fold, but will fold on clause boundaries as you reduce right margin.
This is not quite the same as
Choice: No new line and indenting if statement length less than maximum line length?
it is more like
Choice: No new line and indenting if CLAUSE length less than maximum line length?
... I think the meaning is: fold on clause boundary if and only if line too long.</p>

<p>In another toadworld.com exchange, a Quest employee
<a href="https://forums.toadworld.com/t/connector-lines-for-start-end-of-code-blocks/32373/6">
says</a>
"I think it’s more intuitive that folding occurs at logical positions like open and close parens,
entire statements, entire blocks, etc. Folding on individual clauses, expressions,
and other pieces makes for a big headache and opens the door for all kinds of error."</p>

<H3 id="indenting-units">Indenting units</H3><HR>

<p>Choice: The indenting unit is a tab, or a space?<br>
Choice: For fixed indenting, the number of units is: N<br>
Choice: For fixed indenting, after the first level, the number of units is: N</p>

<p>To be exact, a tab is Unicode character U+0009 CHARACTER TABULATION
and a space is U+0020 SPACE. Usually the indenting unit is a space,
and with a fixed-width font there is no problem with that.
So choosing "number of units = N" means "fixed indenting is 2 spaces"
for level 1, 2 * 2 spaces for level 2, and so on.</p>

<p>Suggestions for a fixed indenting amount are: 2, 3, or 4 spaces.</p>

<p>Ordinarily, the indent amount is the same for every level.
Rarely, the indent amount is a larger amount (for example 4) for the first level,
and a smaller amount (for example 2) for later levels.</p>

<p>Prescriptive guides:</p>

<p>Benenson says: 2 spaces. Salvisberg says: 3 spaces. Mazur says: 4 spaces. 
Holywell says: Indent column definitions by four (4) spaces within the CREATE definition.</p>

<p>Vendors:</p>

<p>Oracle SQL Developer has options for "indent N spaces" and
"indent amount = space|tab", which to me indicates that
they realize that some people prefer tabs.</p>

<p>The SQL standard uses 4 for the first level, 2 for levels after the first level.</p>

<p>Bloggers:</p>

<p>Factor says: usually 2 or 3 spaces.</p>

<p>The Toad formatter default is 3 spaces.</p>

<p>Andy Mallon 
<a href="https://am2.co/2018/02/tsql-tuesday-99-tabs-vs-spaces/">
goes into detail</a> why spaces are preferable.</p>

<p>Bloggers:</p>

<p>ApexSQL, in
<a href="https://solutioncenter.apexsql.com/sql-query-basics-how-to-improve-readability-by-formatting-commas-spacing-and-aligning/">
SQL query basics – How to improve readability by formatting commas, spacing and alignment</a>, says
"you can also choose to add a fixed number of spaces after each column" (in a select list)
option for "each clause and each clause set argument begins on separate lines"</p>

<H3 id="format-clauses-deciding-what-is-a-clause">Format clauses deciding what is a clause</H3><HR>

<p>Choice: Decide what is a clause according to common sources?<br>
Choice: Decide what is a clause according to the statement's BNF?</p>

<p>When we're talking about
indenting or aligning, we're talking about lining up with what a
clause or expression is subordinate to.</p>

<p>Before saying "what to do with clauses" I must say "what is a clause".
There is no official definition that is appropriate.
We can point at a statement like<br>
SELECT something FROM something WHERE something ORDER BY something;<br>
and note that everybody agrees that SELECT / FROM / WHERE / ORDER BY
are "clause starts" (statement starts are a special form of clause starts).
So the general form for them is<br>
something-that-is-not-clause-start keyword-phrase-as-clause-start [content]</p>

<p>But not every keyword phrase is a clause start. Define more narrowly.</p>

<p>My definition of "common SQL statements" is: statements
that are defined in the SQL standard 9075-2 Foundation document,
and supported in Oracle plus DB2 plus SQL Server.</p>

<p>My definition of "common clauses" is: clauses that cause indenting
in examples from the vendor manuals. I do not mean "always cause
indenting", in fact the examples are a minority of all cases.
The clauses that caused level-1 indenting in at least two examples
in two different vendor manuals are:<br>
In ALTER TABLE: ADD, ALTER, DISABLE, DROP, ENABLE, REBUILD, WITH<br>
In CREATE TABLE: ON, WITH<br>
In CREATE TRIGGER: AFTER, BEFORE, FOR, REFERENCING<br>
In CREATE VIEW: AS, SELECT<br>
In DELETE: WHERE<br>
In GRANT: TO<br>
In INSERT: SELECT, VALUES<br>
In SELECT: SELECT, FROM, JOIN, WHERE, GROUP BY, ORDER BY, LIMIT<br>
In UPDATE: SET, WHERE<br>
... This is a very conservative list.<br>
... SELECT would cause indenting anyway because subqueries are clause boundaries.</p>

<p>If prescriptive guides are not explicit and vendor examples are lacking,
there is still the official BNF
<a href="https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form">
Backus-Naur form</a>
or railroad diagram.
Nobody explicitly says the BNF is an authority,
but if you decide that it is, it might help you
decide when deciding "when does a clause end" or "is this clause part of that clause".</p>

<p>The arbitrary and simplistic rules for using a BNF are:<br>
1. A keyword plus a series of non-keywords is a clause.
   (So a clause-start is the first keyword or phrase, and ends
   when there is another keyword after the series of non-keywords),
   or ends when the statement ends.)<br>
2. The first clause (the statement start) may have sub-clauses.<br>
3. Ignore BNF [options] words that are not in the statement that you are writing.</p>

<p>How well do they work?<br>
I will take BNFs for some statements from the SQL standard, and apply them to minimal statements.<br>
Assume that the clause choice is: change clause_start to indent-+1 + clause_start.
Assume that the lists choice is (we will define later in the <a href="#format-lists">Format lists</a> section).
Assume that the threshold is 0.</p>

<p>BNF = CREATE ROLE &lt;role name> [ WITH ADMIN &lt;grantor&gt; ]<br>
The clauses are CREATE ROLE ... and WITH ... So:<pre>
CREATE ROLE r
    WITH ADMIN g;</pre></p>

<p>BNF = CREATE [ RECURSIVE ] VIEW &lt;table name&gt; &lt;view specification&gt; AS &lt;query expression&gt; [ WITH [ &lt;levels clause&gt; ] CHECK OPTION ]<br>
My example will not use the optional &lt;levels clause&gt; so the clauses are<br>
CREATE VIEW ... and AS ... and WITH CHECK OPTION.<br>
It is also decided (see <a href="#format-clauses">"Format clauses"</a>) that SELECT is a clause too
but it is not in the main BNF and is therefore a sub-clause. So:<pre>
CREATE VIEW
  AS
    SELECT *
      FROM t
  WITH CHECK OPTION;</pre></p>

<p>BNF = DECLARE &lt;cursor name&gt; &lt;cursor properties&gt; FOR &lt;cursor specification&gt;<br>
The clauses are DECLARE and FOR. So:<pre>
DECLARE c CURSOR
  FOR
    SELECT *
      FROM t;</pre></p>

<p>BNF = FETCH &lt;fetch orientation&gt; FROM &lt;cursor name&gt; INTO &lt;fetch target list&gt;<br>
The clause starts are FETCH and FROM and INTO. So:<pre>
FETCH c
  FROM c
  INTO c;</pre></p>

<p>BNF = GRANT &lt;privileges&gt; TO &lt;grantee&gt; [ { &lt;comma&gt;&lt;grantee&gt; }... ] [ WITH HIERARCHY OPTION ] [ WITH GRANT OPTION ]  [ GRANTED BY &lt;grantor&gt;]<br>
The clause starts are GRANT, TO, WITH, GRANTED. So:<pre>
GRANT UPDATE (c) ON t
  TO c
  WITH GRANT OPTION;</pre></p>

<p>BNF = PREPARE &lt;SQL statement name&gt; [ &lt;attributes specification&gt; ] FROM &lt;SQL statement variable&gt;<br>
The clause starts are PREPARE, FROM. So:<pre>
PREPARE s
  FROM s;</pre></p>

<p>BNF = SET CONSTRAINTS &lt;constraint name list&gt; { DEFERRED | IMMEDIATE }<br>
The clause starts are SET, DEFERRED, IMMEDIATE. So:<pre>
SET CONSTRAINTS c
  DEFERRED;</pre></p>

<p>BNF = SET SESSION CHARACTERISTICS AS &lt;session characteristics list&gt;<br>
There are no clauses below SET. However, &lt;session characteristics list&gt;
is subject to the "Format lists" choice like any other list
but I said we will assume N = 5. So:<pre>
SET SESSION CHARACTERISTICS AS TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;</pre></p>

<p>BNF = UPDATE &lt;target table&gt; [ FOR PORTION OF &lt;application time period name&gt; FROM &lt;point in time 1&gt; TO &lt;point in time 2&gt; ] [ [ AS ] &lt;correlation name&gt; ] SET &lt;set clause list&gt; [ WHERE &lt;search condition&gt; ]<br>
I will not use FOR or AS or or FROM or TO.
Therefore the clauses are UPDATE... SET ... WHERE ... So:<pre>
UPDATE t
  SET c = v
  WHERE TRUE;</pre></p>

<p>In all cases the results are acceptable.</p>

<p>Prescriptive guides:</p>

<p>No prescriptive guide explicitly suggests making a clause list by either of the methods in this section.</p>

<p>Examples from vendor manuals:</p>

<p>For "Decide what is a clause according to common sources?" I looked at what
more than one vendor says. Of course, if you use only one vendor, your list could be larger.</p>

<p>I looked for examples that clearly do not work with
any combination of Choices along with:
Use the statement's BNF to decide what is a clause = yes.
Despite looking at a large sample, I found only one:
<a href="https://www.ibm.com/support/knowledgecenter/en/SSEPEK_10.0.0/sqlref/src/tpc/db2z_sql_granttableorviewprivileges.html">
DB2:</a><pre>
GRANT SELECT, UPDATE ON TABLE DSN8A10.DEPT
  TO PUBLIC;</pre>
In this case IBM seems to have decided that TO ... is a clause start but ON ... is not.</p>

<p>Bloggers:</p>

<p>This
<a href="https://dba.stackexchange.com/questions/171979/what-actually-is-a-sql-clause">
stackexchange thread</a>
had some people attempting to define "clause":</p>

<p>Tako Lee's
<a href="https://github.com/sqlparser/isf_notepad/blob/master/bin/Config/sqlformat/fo.json">
list of options for sqlparser</a>
is large because Tako Lee chose to allow different settings for different clauses.
I chose to list the settings only once unless I saw that prescriptive guides or vendors
were saying things like "indent +2 if it is JOIN, indent +4 if it is AND, etc.".</p>

<H3 id="format-clauses-by-indenting">Format clauses by indenting</H3><HR>

<p>Choice: change clause-start to newline + indent+0 + clause-start<br>
Or      change clause-start to newline + indent+0 + clause-start<br>
Or      change clause-start to clause-start + newline + indent+1<br>
Or      change clause-start to newline + indent+1 + clause-start<br>
And<br>
Choice: change SELECT to SELECT + newline + indent+1<br>
Or<br>
Choice: change clause-start to newline + indent+0 + clause-start + newline + indent-+1</p>

<p>Usually the prescriptive guides use the term "left align" where I use "indent+0".</p>

<p>Let us see the effect of each Choice setting on this SELECT statement:<br>
SELECT DISTINCT id FROM employees WHERE id &gt; 5 GROUP BY id;<br>
Assume indent amount is 4 spaces.</p>

<p>"change clause-start to newline + indent+0 + clause-start"<pre>
SELECT DISTINCT id
FROM employees
WHERE id > 5
GROUP BY id;</pre></p>

<p>"change clause-start to newline + indent+0 + clause-start + newline + indent+1"<pre>
SELECT DISTINCT
    id
FROM
    employees
WHERE
    id > 5
GROUP BY
    id;</pre></p>

<p>"change clause-start to newline + indent+1 + clause-start"<pre>
SELECT DISTINCT id
    FROM employees
    WHERE id > 5
    GROUP BY id;</pre>
This indenting helps emphasize that FROM and WHERE and GROUP BY
are "subordinate" to SELECT.</p>

<p>"change SELECT to SELECT + newline + indent+1"<br>
Benenson suggests "SELECT goes on its own line" and "Align all columns to the first column on their own line".<pre>
SELECT DISTINCT
  id
FROM employees
WHERE id > 5
GROUP BY id;</pre></p>

<H3 id="format-clauses-by-right-aligning-keywords">Format clauses by right-aligning keywords</H3><HR>

<p>change clause-start to newline + right-align word + clause-start<br>
Or      change clause-start to newline + right-align phrase + clause-start</p>

<p>"change clause-start to newline + right-align word + clause-start"<pre>
SELECT DISTINCT id
  FROM employees
 WHERE id > 5
 GROUP BY id;</pre></p>

<p>"change clause-start to newline + right-align phrase + clause-start"<pre>
SELECT DISTINCT id
           FROM employees
          WHERE id > 5
       GROUP BY id;</pre>
Notice in this example that there is a
<a href="https://en.wikipedia.org/wiki/River_(typography)">"river of white"</a>.
All the clause-starts have ended up on the left side of the river;
all the clause-ends (id and employees and id &gt; 5 and id) have ended up on the right side.
"Right align word" usually produces rivers but "right align phrase" does it more.</p>

<p>Prescriptive guides:</p>

<p>Donnelly says: new clauses makes new start of line. ON is not a clause-starter. rivers: yes, right-aligned indenting.
Donnelly describes rivers of white thus:
"The keywords that begin a clause should be right-aligned.
The idea is to make a single character column between the keywords and their objects."
Donnelly even shows an example where the statement-start (SELECT) is not at Left margin
because SELECT must right-align by phrase with GROUP BY:<pre>
  SELECT key_column, COUNT(1)
    FROM tablename
GROUP BY key_column;</pre></p>

<p>Holywell says: rivers: usually, right-aligned first-word indenting.
"Rivers are bad in typography, but helpful here."</p>

<p>In Taranov examples,
it looks like ON and AND are right-aligned, but FROM/WHERE/JOIN/GROUP BY/ORDER BY are indent+0.
This was not explained so I did not suggest a Choice for it.</p>

<p>Salvisberg says: rivers: yes, right-aligned indenting. i.e. align on first word, not align on phrase.</p>

<p>I am going to be repetitious now. Are subordinate clause-starts left-aligned or right-aligned?
Well, this is what left-align looks like:<pre>
UPDATE IGNORE
SET
WHERE
OR</pre>
This is what right-align looks like:<pre>
UPDATE IGNORE
   SET
 WHERE
    OR</pre>
Thus, the last character of each word is in the same position.
This is what right-align with the last word looks like:<pre>
UPDATE IGNORE
          SET
        WHERE
           OR</pre>
Thus, when the clause-start is a phrase rather than a single
word, the alignment is with the last word of the longest clause-start (IGNORE in this case)
rather than with the first word (UPDATE in this case).
If right-aligning is used, then number-of-spaces in indenting units will not matter.</p>

<p>* Oracle SQL Developer has an option: "Right-Align Master Keywords"
(but the number of "master" keywords is limited (as in SELECT ... INTO ... WHERE)), and
an option "Indent Main Keyword 2x" (they mean the lines after the verb),
It is
<a href="https://www.thatjeffsmith.com/archive/2018/04/18-1-new-formatting-option-right-align-query-keywords/">
relatively new</a>.</p>

<p>James Thigpen
has
<a href="https://github.com/roverdotcom/sql-style-guide">
an example like Donnelly's</a>, where SELECT is moved over to right-align with GROUP BY.</p>

<H3 id="format-clauses-by-aligning-contents">Format clauses by aligning contents</H3><HR>

<p>Choice: Format clauses by aligning contents?</p>

<p>If we are aligning contents, then all the clause starts are on the left of the
statement or subquery, and all the contents (the clause ends) are on the right.
This can also be accomplished with right-aligning phrases, but when we align
contents we are putting the spaces after the keyword phrase, not before the phrase.</p>

<p>Extract from an example from Taranov:
(Notice that the commas are not part of the deal -- see also the <a href="#dbvis">dbvis support question</a>.)<pre>
SELECT
         t1.Value1 AS Val1
       , t1.Value2 AS Val2
       , t2.Value3 AS Val3
INTO     #Table3
FROM     CTE_MyCTE AS t1
ORDER BY t2.Value2;</pre></p>

<p>Extract from the
<a href="http://www.tpc.org/tpc_documents_current_versions/pdf/tpc-h_v2.18.0.pdf">
TPC-H benchmark requirements:</a><pre>
select
       l_returnflag,
       l_linestatus,
       sum(l_quantity) as sum_qty,
       sum(l_extendedprice) as sum_base_price,
       sum(l_extendedprice*(1-l_discount)) as sum_disc_price,
       sum(l_extendedprice*(1-l_discount)*(1+l_tax)) as sum_charge,
       avg(l_quantity) as avg_qty, avg(l_extendedprice) as avg_price,avg(l_discount) as avg_disc,
       count(*) as count_order
from
       lineitem
where
       l_shipdate <= date '1998-12-01' -interval '[DELTA]' day (3)
group by
       l_returnflag,
       l_linestatus
order by
       l_returnflag, l_linestatus</pre></p>

<p>Prescriptive guides:</p>

<p>Mazur says:
"Some IDEs have the ability to automatically format SQL
so that the spaces after the SQL keywords are vertically aligned.
This is cumbersome to do by hand (and in my opinion harder to read anyway)
so I recommend just left aligning all of the keywords:"</p>

<H3 id="format-lists">Format lists</H3><HR>

<p>Choice: Lists maximum number of items per line = N?<br>
Choice: Lists start with: space, or newline + usual fixed indent + N levels, or newline + align past preceding word?<br>
Choice: Lists , i.e. end-of-line comma becomes , + newline or newline + , or newline + , + space?<br>
Choice: Lists have similar parts align?<br>
Choice: Lists ( i.e. initial left parenthesis becomes ( or newline + ( or newline + ( + newline?<br>
Choice: Lists ) i.e. final right parenthesis becomes ) or newline + )?</p>

<p>For this section, list means: a comma-delimited list of columns or expressions.
Examples of lists are SELECT expression-list FROM ...,
INSERT INTO t (column-list) VALUES (expression-list),
IN (expression-list),
CREATE TABLE ... (table-element-list)
routine-call (argument-list),
routine-definition (parameter-list).
I have seen formatters that have separate options for each type of list,
but none of the prescriptive guides recommend that.
I will also discuss CREATE TABLE ... (table-element-list) in a later section.</p>

<p>SQL people are used to seeing tables. Tables have rows and columns.
Therefore SQL people are used to seeing items on separate lines, with
the start of each item aligned.
Therefore in SQL this is okay even if other languages do not do it.
Sometimes a list which is vertical is called a "stack" or "stacked list".</p>

<p>Suppose that we're looking at<br>
SELECT DISTINCT alpha + 100 AS c1 /* one */, beta AS c200 /* two */, epsilon - 2 AS c3.</p>

<p>Set maximum number of items per line = 1.
That means that for every item there is a newline:<pre>
SELECT DISTINCT alpha + 1 AS c1 /* one */,
                beta AS c200 /* two */,
                epsilon - 2 AS c3</pre>
I have seen formatters that allow for setting N to
a number greater than 1, although the option is not in prescriptive guides.</p>

<p>Set start with = newline.
That means that there is a newline before the first item:<pre>
SELECT DISTINCT
                alpha + 100 AS c1 /* one */,
                beta AS c200 /* two */,
                epsilon - 2 AS c3</pre></p>

<p>Set comma becomes newline + comma + space.
That means the commas come at the start rather than at the end:<pre>
SELECT DISTINCT
                  alpha + 100 AS c1 /* one */
                , beta AS c200 /* two */
                , epsilon - 2 AS c3</pre>
Arguments that I have seen for comma-at-start style include:<br>
* it is easier to comment out columns (you do not have to comment out the line and then remove the comma on the previous line)<br>
* it is easier to add a comment after the expression (I do not understand this argument)<br>
* commas-at-end = yes may look natural to people who use left-to-right alphabets, but lots of people use right-to-left.</p>

<p>Set have similar parts align = yes.
That means not only the item starts, but also
the operators and ASes and comments align:<pre>
SELECT DISTINCT
                  alpha   + 100 AS c1   /* one */
                , beta          AS c200 /* two */
                , epsilon - 2   AS c3</pre>
Again, I have seen formatters that allow for this, although
the option is not in prescriptive guides (except for other statements).</p>

<p>Now put the list inside parentheses.</p>

<p>Set ( = newline + ( + newline.
That means we go now have a ( on its own line aligned with the commas:<pre>
SELECT DISTINCT
                (
                  alpha   + 100 AS c1   /* one */
                , beta          AS c200 /* two */
                , epsilon - 2   AS c3)</pre></p>

<p>Set ) = newline + )
That means the parentheses are now aligned:<pre>
SELECT DISTINCT
                (
                  alpha   + 100 AS c1   /* one */
                , beta          AS c200 /* two */
                , epsilon - 2   AS c3
                )</pre></p>

<p>Thus there are only 6 basic "choices" but some of the choices
have more than 2 possible settings, and the choices can be
combined independently, and sometimes people will want to
have different settings for each type of list.
So there are hundreds of possible settings.</p>

<p>Prescriptive guides:</p>

<p>Salvisberg, Taranov say: commas-at-start = yes.
            And Salvisberg says: space-after-the-comma = yes.</p>

<p>Celko, Mazur, Holywell say: commas-at-start = no.</p>

<p>Salvisberg says "operators aligned" -- perhaps he means assignment operators.</p>

<p>Vendor manuals:</p>

<p><a href="https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/SELECT.html#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6">
Oracle:</a> comma-lists mostly on same line but indenting when line too long, comma-at-end, no AS, ) at end</p>

<p><a href="https://www.ibm.com/support/knowledgecenter/SSEPEK_10.0.0/sqlref/src/tpc/db2z_sql_selectstatementexamples.html">
DB2:</a> keywords right aligned = no (2 spaces) and comma-lists mostly on same line</p>

<p><a href="https://docs.microsoft.com/en-us/sql/t-sql/queries/select-transact-sql?view=sql-server-ver15">
SQL Server:</a>  comma-lists mostly on same line</p>

<p>SQL Developer has an option "Before comma" which is equivalent to "Commas first = yes".</p>

<p>Bloggers / Others:</p>

<p>Joe Celko's programming style" says:
"“Put commas at the end of a line, not the start.
A comma, semicolon, question mark, or periods are visual signals that something has just ended, not that it is starting.
Having a comma at the start of a line will make the eye tick leftward as it looks for that missing word that was expected
before the comma.”</p>

<p><a href="https://www.simonholywell.com/post/2016/12/sql-style-guide-misconceptions/">
Simon Holywell says:</a> "There’s no way of being polite here - this [i.e. comma-at-start = yes]
looks hideous, weird and totally unconventional in a bad way."</p>

<p><a href="https://solutioncenter.apexsql.com/rules-of-sql-formatting-commas-and-spacing-in-t-sql/">
ApexSQL says:</a>
"However, most often commas as list-separators are written at the beginning of a line
to make commenting of list members easier in development. This is also a standard in Adventureworks2012 database:"</p>

<p>Factor says: "You'd probably also want to insist on a new line after each column definition."
        (but in SELECT etc.)
        "Now, no typesetter would agree to arrange this [list of my favourite cheeses]
        in a vertical list, because the page would contain too much white space...
        ... ...and they'd be most unlikely to want to put commas at the beginning of list elements.
        However, if the list elements consisted of longer strings, then it would be perfectly acceptable.
        In the same way, the rules for formatting SQL have to take into account the type of SQL statement
        being formatted, and the average length of each list element
        ...
        Commas, used as list separators, are often put at the beginning of lines.
        I realize that it makes the "commenting out" of list members easier during development,
        but it makes it difficult for those of us who are used to reading English text in books.
        Commas come at the end of phrases, with no space before them, but if they are followed
        by a word or phrase on the same line, then there is a space after the comma."</p>

<p>Factor also says: "Put a line-break between list items only when each list item averages more than thirty or so characters."</p>

<p>Re parentheses, see
<a href="https://docs.telemetry.mozilla.org/concepts/sql_style.html#parentheses">
Firefox Data Documentation SQL Style Guide re parentheses</a>.
</p>

<p>Oracle SQL Developer has multiple options which would especially
affect select lists and UPDATE ... SET lists and WHERE lists with
multiple conditions: "Align Equal signs (= &lt; &gt; ...)",
"Align Operator signs (* - + ...)", "Align AS keyword",
"Align on commas", "Align line comments [i.e. simple comments]",
"Align || at end of line", "Align variable declaration for stored procedures".
Taken together, these options all correspond to "Choices"
and presumably a procedure would look like this if they were all on:<pre>
CREATE PROCEDURE p (
                    first_parameter  CHAR(1)  := 'a';
                    second_parameter CHAR(22) := 'b';
                   )
INSERT INTO t1
  SELECT
    first_column      AS first_alias,
    second_column     AS b          , -- comment
    really_big_column AS c            -- comment
  FROM t2
  WHERE
        first_column   = 12345 -- comment
    AND second_column <= 0     -- comment
  ORDER BY
    fifth_column ||
    sixth_column
...</pre></p>

<p>
Bloggers:</p>

<p>Benenson says: SELECT goes on its own line".</p>

<p id="dbvis">
From an explanation on
<a href="https://support.dbvis.com/support/discussions/topics/1000076994">
support.dbvis.com</a><br>
"
1) The formatter indents the column names, ignoring the commas. So
with an indentation size of 4, the column name is indented to start in
column 4. If you have also selected Line Break Before Comma, the
comma will be appear before the column name. This is the intended
behavior.
"<br>
Thus: with indenting or aligning, plus commas before, you are not trying to line up
the commas, you are trying to line up the contents.
The formatter comes from
<a href="https://www.sqlinform.com">SQLinForm</a>.</p>

<p>Oracle SQL Developer had an option "For "Number of columns per line"</p>

<p>Toad had an option for "Stacked on more than N" (default 3), see
<a href="https://forums.toadworld.com/t/editing-toads-formatting-options/9209">here</a> and
<a href="https://forums.toadworld.com/t/code-formatter-incorrect-formatting-12-9-0-66/37773">here</a>.</p>

<p><a href="https://www.dhs.pa.gov/providers/Providers/Documents/Business%20and%20Tech%20Standards/Data%20Domain/Oracle%20PL%20SQL%20Naming%20and%20Coding.pdf">
Oracle PLSQL Coding and Naming Standards</a>
says "Parameters must be stacked unless less than three."</p>

<p>... These would all correspond with "Choice: Lists maximum number of items per line = 3".</p>

<H3 id="format-conditions">Format conditions</H3><HR>

<p>Choice: same as for Format lists?<br>
        or<br>
        change AND/OR to newline + indent+1 + AND/OR<br>
        or<br>
        change AND/OR to newline + indent+0 + AND/OR<br>
        or<br>
        change AND/OR to newline + right-align + AND/OR<br>
        or<br>
        change AND/OR to AND/OR + newline + indent-+0</p>

<p>Conditions are really just expressions that can return boolean values,
so they can appear anywhere, not just after WHERE or HAVING or ON or IF or WHERE.
But here I will illustrate with WHERE.</p>

<p>For simple conditions without AND/OR most examples show: WHERE condition.</p>

<p>The "same as for Format lists" setting would mean that a
a series of conditions can be regarded
as a list, with each AND/OR condition being one "item" of the list.
Potentially that would imply that a
string of conditions would have all their parts aligned, a setting
that we might also see for CASE operations, later.</p>

<p>The "change AND/OR to AND/OR + newline + indent-+0" setting
means AND/OR go to the end of a line, not the start of the next line.
This would be compatible with the idea that AND/OR are not "clause
starts", they are "operators".
And operators belong at the end of a line, if we follow Java conventions.</p>

<p>Prescriptive guides:</p>

<p>Extract from a Taranov example:<pre>
INNER JOIN dbo.Table3 AS t2
        ON t1.Value1 = t2.Value1
WHERE      t1.Value1 > 1
  AND      t2.Value2 >= 101</pre>
This fits with "clause starts on the left, clause ends on the right",
and "change AND/OR to newline + right-align + AND/OR"</p>

<p>Holywell:<pre>
WHERE ...
   OR ...
   OR ...</pre>
This fits with "same as for Formats list", "similar parts aligned", and
"change AND/OR to newline + indent+1 + AND/OR".</p>

<p>Mazur fits with "change AND/OR to AND/OR + newline + indent+0" (i.e. indent+1 from the where)<pre>
where 
    ... and 
    ...</pre>
Thus Mazur is the only one who says AND/OR-at-end.
"all conditions within WHERE are indented (4 spaces), AND/OR is at end of line"</p>

<p>Benenson fits with  "change AND/OR to newline + indent+0 + AND/OR"<pre>
WHERE
  ...
  AND ...</pre></p>

<p>Salvisberg, Holywell fit with: "change AND/OR to newline + right-align + AND/OR" (i.e. right-align from the where)<pre>
WHERE ...
  AND ...
WHERE ...
   OR ...</pre></p>

<p>Vendor manuals:</p>

<p>Example from
<a href="https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/SELECT.html#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6">Oracle</a>:<pre>
WHERE NOT (job_id = 'PU_CLERK' AND department_id = 30)</pre></p>

<p>Example from <a href="https://docs.microsoft.com/en-us/sql/t-sql/queries/where-transact-sql?view=sql-server-ver15">
SQL Server:"</a><pre> 
WHERE EmployeeKey <= 500 AND LastName LIKE '%Smi%' AND FirstName LIKE '%A%'; 
Examples from DB2:
WHERE WORKDEPT = 'E11' AND NOT JOB = 'ANALYST'
+
WHERE EDLEVEL > 12 AND
  (WORKDEPT = 'E11' OR WORKDEPT = 'E21')</pre>
... Quick summary: none of the vendor manuals' examples follow any special rules.</p>

<p>SQL Developer has an option for "Indent AND/OR" (they mean one additional fixed-units indent so AND/OR is one level after WHERE).</p>

<p>Bloggers:</p>

<p>From an article in <a href="https://blogs.oracle.com/oraclemagazine/writing-sql-in-oracle-application-express">
 Oracle Magazine:</a><pre>
WHERE     ...
      AND ...;</pre>
This fits with "same as for Formats list", "similar parts aligned", and
"change AND/OR to newline + indent+1 + AND/OR".</p>

<H3 id="format-subqueries">Format subqueries</H3><HR>

<p>Choice: change subquery start to subquery start, or newline + indent-+1 + subquery start</p>

<p>The "subquery start" is ( or ALL/IN/ANY/EXISTS ( or SELECT.
The Choices for ()s are the same as in section
<a href="#format-lists">Format lists</a>; for examples I chose the newline settings.</p>

<p>If "change subquery start to newline + indent-+1 + subquery start"<pre>
WHERE
  (
    SELECT ...
  )</pre></p>

<p>If "change SELECT to newline + indent+1 + SELECT + newline" and
"change FROM to newline + indent+2 + FROM".<pre>
CREATE VIEW v AS
  SELECT c
      FROM t;</pre>
Notice that the FROM is indented 4 spaces under the SELECT,
not 4 spaces under the CREATE, because sub-clauses are always
indented from the main clause, not from the statement start.</p>

<p>Prescriptive guides:</p>

<p>Salvisberg gives this example:<pre>
SELECT emp.last_name
      ,emp.first_name
  FROM employees emp
 WHERE emp.employee_id IN (SELECT j.employee_id
                             FROM jobs j
                            WHERE j.job_title like '%Manager%');</pre></p>

<p>Benenson says: (subquery-is-clause-start: yes)</p>

<H3 id="format-with">Format WITH</H3><HR>

<p>Choice: none, setting is as described in section <a href="#format-parentheses">Format parentheses</a>.</p>

<p>In section <a href="#format-subqueries">Format subqueries</a> the Choices involved putting ) at the end of
a SELECT without a newline, or aligning ) with (.
But in examples for WITH I regularly see a third way: align ( with WITH.
For example (this is from a
<a href="https://docs.telemetry.mozilla.org/concepts/sql_style.html#parentheses">
mozilla.org SQL Style Guide</a>)<pre>
WITH sample AS (
  SELECT
    client_id,
  FROM
    main_summary
  WHERE
    sample_id = '42'
)</pre></p>

<p>Prescriptive guides:</p>

<p>Taranov, Mazur, Benenson examples all show Align right parenthesis with WITH = yes.</p>

<H3 id="format-joins">Format joins</H3><HR>

<p>Choice: change JOIN to newline + indent+1 + JOIN, or newline + indent+0 + JOIN?<br>
Choice: change ON to ON, or newline + indent+1 + ON?<br>
Choice: old style join like JOIN?</p>

<p>JOIN is a sub-clause of FROM, so "indent+1" means "indent one level
after FROM", which may or may not be the same thing as "indent one level
after SELECT". ON is a sub-clause of JOIN, so "indent+1" means indent one level
from JOIN".</p>

<p>"old style join like JOIN = yes" would suggest that however you would format "CROSS JOIN" is how you would format ",".
But the vendor manual examples which have old style joins (Oracle, DB2, Tarantool)
have them as comma-separated lists ("PARTS, PRODUCTS", "employees, departments", "t1 AS a, t1 AS b").</p>

<p>Prescriptive guides:</p>

<p>Taranov shows: change JOIN to newline + right-align word, change ON to newline + right-align phrase + ON<pre>
SELECT
 INNER JOIN ...
         ON ...</pre></p>

<p>Holywell shows: change JOIN to newline + indent+1 + JOIN, change ON to newline + indent+0 + ON<pre>
FROM ...
     JOIN ...
     ON ...</pre>
Holywell explains: "Joins should be indented to the other side of the river and grouped with a new line where necessary."
But in another example Holywell shows JOIN and ON right-aligned with SELECT and FROM.</p>

<p>Salvisberg shows: change JOIN to newline + indent+1 + JOIN, + names align (as if it is a list) and
                  change ON to ON<pre>
FROM      ...
     JOIN ... ON ...</pre></p>

<p>Mazur, Benenson, Donnelly say or show: change JOIN to newline + indent+0 + JOIN, change ON to ON<pre>
FROM ...
JOIN ... ON ...</pre>
This is also the style of blogger <a href="https://github.com/roverdotcom/sql-style-guide">James Thigpen</a>.
Mazur suggests that ON might be on a different line if the condition is complex.</p>

<p>
Examples in vendor manuals:</p>

<p><a href="https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/SELECT.html#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6">
Oracle = inconsistent</a></p>

<p><a href="https://www.ibm.com/support/producthub/db2/docs/content/SSEPGG_11.5.0/com.ibm.db2.luw.sql.ref.doc/doc/r0059214.html">
DB2 = inconsistent</a></p>

<p><a href="https://docs.microsoft.com/en-us/sql/relational-databases/performance/joins?view=sql-server-ver15">
SQL Server = inconsistent</a></p>

<p>SQL Developer has an option for "JOIN statements" (they mean JOIN clauses).</p>

<H3 id="format-insert">Format INSERT</H3><HR>

<p>Choices: none needed.</p>

<p>If there is a list of target columns,
or if there is a list of VALUES columns, then see <a href="#format-lists">Format lists</a>.
If there is a VALUES or SELECT clause, then see <a href="#format-clauses">Format clauses</a>.
So the Choices are already made, there is nothing to do now
except give an example. This is one from Salvisberg, who
believes that the list of target columns should always be
specified, and consistently chooses the setting that puts
commas in front, and believes that a clause start should be
changed to newline + indent+1 + clause start.<pre>
INSERT INTO departments (department_id
                        ,department_name
                        ,manager_id
                        ,location_id)
   VALUES (departments_seq.nextval
          ,'Support'
          ,100
          ,10);</pre></p>

<H3 id="format-update">Format UPDATE</H3><HR>

<p>Choices: none needed</p>

<p>As with INSERT, the Choices are already made, there is
nothing to do now except give an example. This one is
from Holywell, who believes clause starts should be right-aligned
and commas in comma lists should be at end.<pre>
/* Updating the file record after writing to the file */
UPDATE file_system
   SET file_modified_date = '1980-02-22 13:19:01.00000',
       file_size = 209732
 WHERE file_name = '.vimrc';</pre></p>

<H3 id="format-create-table">Format CREATE TABLE</H3><HR>

<p>Choice: see <a href="#format-lists">Format lists</a>.</p>

<p>The table-element list in CREATE TABLE is a list.
Therefore the same 6 choices apply, although you might choose different settings.
This is what a CREATE TABLE will look like if the choices are:<br>
Lists maximum number of items per line = 2<br>
Lists start with: newline + usual fixed indent + 1 level<br>
Lists , i.e. end-of-line comma becomes , + newline<br>
Lists have similar parts align = yes<br>
Lists ( becomes (<br>
Lists ) becomes )</p>

<p>Alternate phrasing: Inside CREATE TABLE any list of columns or constraints is
a comma-delimited list so the "Format lists" rules apply.
<pre>
CREATE TABLE employees
    (id   INTEGER   PRIMARY KEY,      class  INTEGER,
     name CHAR(255) UNIQUE DEFAULT 5, markup INTEGER);</pre></p>

<p>Probably "items per line = 2" is
not an optimal choice; recommendations are either 1 or infinite.
The "similar parts align" works well because the parts
(name, data type, column constraint, default) are well defined and ordered,
but would look less lovely if the DEFAULT clause was
long and came before UNIQUE.
And, although saying ") becomes )" saves screen space, it is not the most common choice.
So people may be more likely to choose "items per line = 1"
and "similar parts align = no" and ) becomes newline + )
which results in
<pre>
CREATE TABLE employees
    (id  INTEGER PRIMARY KEY,
     class INTEGER,
     name CHAR(255) UNIQUE DEFAULT 5,
     markup INTEGER
    );</pre>
If you decide that you like aligning parentheses, then you will probably want
to be consistent and align CASE with END, or BEGIN with END.</p>

<p>Choice: table constraints come after column definitions?<br>
or Choice: column constraint immediately after column data type?</p>

<p>I can imagine it is good to add "UNIQUE (class, name)" as a final item on
a separate line, so that it does not interrupt the column list.
But I can imagine it is good to put "UNIQUE (class, name)" after the
definition of name and class.
(Remember that NOT NULL is a column constraint and it comes immediately after
the data type, so why not other constraints?)</p>

<p>If there is a big long foreign-key constraint, it might be broken up
because the earlier "Choices" determined that column lists get indented
with fixed indenting, aligned parentheses, etc. For example<pre>
CONSTRAINT constraint_name FOREIGN KEY REFERENCES table_name
  (column_name,
   column_name
  )</pre></p>

<p>If there is a long check constraint, it might be broken up
because the earlier "Indent clauses" choices decided what should
happen with AND / OR indenting.</p>

<p>Prescriptive guides:</p>

<p>Holywell says: "If it make senses to do so align each aspect of the query on the same character position.
For example all NOT NULL definitions could start at the same character position.
This is not hard and fast, but it certainly makes the code much easier to scan and read."</p>

<p>Holywell example:<pre>
CREATE TABLE staff (
    PRIMARY KEY (staff_num),
    staff_num      INT(5)       NOT NULL,
    first_name     VARCHAR(100) NOT NULL,
    pens_in_drawer INT(2)       NOT NULL,
                   CONSTRAINT pens_in_drawer_range
                   CHECK(pens_in_drawer >= 1 AND pens_in_drawer < 100)
);</pre>
This example also is consistent with Align right parenthesis with statement start = yes.
+ column constraint immediately after column data type = yes</p>

<p>Examples from vendor manuals</p>

<p><a href="https://www.ibm.com/support/knowledgecenter/da/SSEPGG_11.5.0/com.ibm.db2.luw.sql.ref.doc/doc/r0000927.html">
DB2:</a><pre>
CREATE TABLE EMPLOYEE_SALARY
  (DEPTNO   CHAR(3)      NOT NULL,
   DEPTNAME VARCHAR(36)  NOT NULL,
   EMPNO    CHAR(6)      NOT NULL,
   SALARY   DECIMAL(9,2) NOT NULL WITH DEFAULT)</pre>
Choices: no semicolon, everything upper case, INTEGER rather than INT, adjectives left-aligned, commas follow.</p>

<p><a href="https://docs.microsoft.com/en-us/sql/t-sql/statements/create-table-transact-sql?view=sql-server-ver15">
SQL Server:</a><pre>
CREATE TABLE dbo.PurchaseOrderDetail
(
    PurchaseOrderID int NOT NULL
        REFERENCES Purchasing.PurchaseOrderHeader(PurchaseOrderID),
    LineNumber smallint NOT NULL,
    ProductID int NULL
        REFERENCES Production.Product(ProductID),
    UnitPrice money NULL,
    ...
)</pre>
Notice: semicolons, keywords upper case, object names Pascal Case, adjectives not aligned, commas follow, INT preference.
        + REFERENCES (because it is a constraint?) is newline + more indent</p>

<p><a href="https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/CREATE-TABLE.html#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6">
Oracle:</a><pre>
CREATE TABLE departments_demo
    ( department_id    NUMBER(4)
    , department_name  VARCHAR2(30)
           CONSTRAINT  dept_name_nn  NOT NULL
    , manager_id       NUMBER(6)
    , location_id      NUMBER(4)
    , dn               VARCHAR2(300)
    ) ;</pre>
Notice: semicolons at end, keywords upper case, object names snake case, adjectives left-aligned, commas precede.
+ space before semicolon
+ column constraint immediately after column data type</p>

<p>Another
<a href="https://docs.oracle.com/en/database/oracle/oracle-database/18/sqlrf/CREATE-TABLE.html#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6">
Oracle</a> CREATE TABLE example:<pre>
CREATE TABLE books (title VARCHAR2(100), author person_t);</pre></p>

<p>Tarantool:<pre>
CREATE TABLE employees_demo
    (employee_id INTEGER,
     first_name STRING,
     last_name STRING NOT NULL,
     email STRING NOT NULL,
     phone_number STRING);</pre></p>

<p>SQL Standard 9075-12 document:<pre>
CREATE TABLE INFORMATION_SCHEMA_CATALOG_NAME
    ( CATALOG_NAME        SQL_IDENTIFIER,
      CONSTRAINT INFORMATION_SCHEMA_CATALOG_NAME_PRIMARY_KEY
        PRIMARY KEY ( CATALOG_NAME ),
      CONSTRAINT INFORMATION_SCHEMA_CATALOG_NAME_CHECK
        CHECK ( 1 = ( SELECT COUNT(*)
                      FROM INFORMATION_SCHEMA_CATALOG_NAME ) ),
      CONSTRAINT INFORMATION_SCHEMA_CATALOG_NAME_FK_CATALOG_NAME
        FOREIGN KEY ( CATALOG_NAME ) REFERENCES DEFINITION_SCHEMA.CATALOG_NAME
    );</pre>
Final ) is on a separate line aligned with ), space after (, space before ) -- those are choices in
Section <a href="#format-parentheses">Format parentheses</a>.
But for the CHECK clause ) ) is on the last line of the subquery -- that is a choice in Section subqueries.
All words upper case -- those are choices in Names sections.</p>

<H3 id="format-create-view">Format CREATE VIEW</H3><HR>

<p>Choice: AS SELECT becomes AS SELECT, or newline + AS SELECT, or AS + newline + fixed-indent + SELECT?</p>

<p>Choice: WITH CHECK OPTION aligns with AS?</p>

<p>The "AS SELECT" setting looks like:<pre>
CREATE VIEW view_name AS SELECT</pre>
The "newline + AS SELECT" setting looks like<pre>
CREATE VIEW view_name
AS SELECT</pre>
The "AS + newline + fixed-indent + SELECT" setting looks like<pre>
CREATE VIEW view_name AS
  SELECT</pre>
I cannot think of any principle that applies, except perhaps that AS is a special clause.
None of the prescriptive guides says anything about this, so I depend entirely on examples
from vendors and blogs.</p>

<p>In this list, some vendors appear more than once because they use more than one setting.</p>

<p>AS SELECT: nobody<br>
newline + AS SELECT: DB2, Celko<br>
newline + AS + fixed-indent + SELECT: nobody<br>
AS + newline + fixed-indent + SELECT: Oracle<br>
newline + AS + newline + SELECT: SQL Server, Factor<br>
newline + fixed-indent + AS SELECT: Oracle, DB2</p>

<p>Vendors:</p>

<p>Oracle: see
<a href="https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/CREATE-VIEW.html#GUID-61D2D2B4-DACC-4C7C-89EB-7E50D9594D30">
here</a>. Inconsistent. WITH READ ONLY aligns with AS.</p>

<p>DB2: see
<a href="https://www.ibm.com/support/knowledgecenter/SSEPGG_10.5.0/com.ibm.db2.luw.sql.ref.doc/doc/r0000935.html">
here</a>.</p>

<p>SQL Server: see
<a href="https://docs.microsoft.com/en-us/sql/t-sql/statements/create-view-transact-sql?view=sql-server-ver15">
here</a>. Consistent. WITH CHECK OPTION aligns with AS.</p>

<p>Blogs:</p>

<p>Joe Celko,
<a href="https://books.google.ca/books?id=i-19BAAAQBAJ&pg=PA123&lpg=PA123&dq=celko+%22create+view%22&source=bl&ots=cRMP4KTSwt&sig=ACfU3U0ldhels0IZCiArHXEHdNqlmyeXMA&hl=en&sa=X&ved=2ahUKEwj1xcjKudfoAhVUo54KHXU5DN8Q6AEwAHoECA0QKQ#v=onepage&q=celko%20%22create%20view%22&f=false">
SQL for Smarties: Advanced SQL Programming</a> shows
WITH CHECK OPTION is level-1 indent from CREATE.</p>

<p>Sharad Maheshwari and Ruchin Jain,
<a href="https://books.google.ca/books?id=nt-T0cfaWPoC&pg=PA458&lpg=PA458&dq=%22create+view%22+%22vw%22+prefix&source=bl&ots=ZHvX9BhM43&sig=ACfU3U0VGvR758Gfo0MqzNBm69MzxbWZbQ&hl=en&sa=X&ved=2ahUKEwibn5in_eXoAhVfJzQIHTBUBCgQ6AEwAHoECAsQKQ#v=onepage&q=%22create%20view%22%20%22vw%22%20prefix&f=false">
"DBMS – Complete Practical Approach"</a>
say: "Everything after the AS keyword must be enclosed in parentheses."</p>

<p>The
<a href="https://docs.teradata.com/reader/eWpPpcMoLGQcZEoyt5AjEg/qkhVaT6vD8O7i5U6jr1nKg">
Teradata manual</a> has<pre>
CREATE VIEW dept AS
 SELECT   deptno(TITLE 'Department Number'),
          deptname(TITLE 'Department Name'), 
          loc (TITLE 'Department Location'), 
          mgrno(TITLE 'Manager Number') 
 FROM department;</pre>
which is consistent with "AS + newline + fixed-indent + SELECT".</p>

<H3 id="format-create-procedure-or-create-function">Format CREATE PROCEDURE or CREATE FUNCTION</H3><HR>

<p>Choice: indent first line of routine?<br>
Choice: AS as in CREATE VIEW?</p>

<p>"indent first line of routine" is a Choice
because I have seen it occasionally.
But zero prescriptive guides recommend it and zero vendor examples show it.
I believe that there is an influence from other languages that have:<pre>
function_name_definition ()
{
  statements;
}</pre>
The equivalent of { ... } is BEGIN ... END, so:<pre>
create_routine_statement_start ()
BEGIN
  ...
END;</pre>
I call that "the usual way".</p>

<p>The parameter list might be followed by a descriptive phrase,
for which I know of no rule.
I have no guidance for whether LANGUAGE or other characteristics phrases are clause starts.</p>


<p>For "AS as in CREATE VIEW" I chose not to repeat all
the Choices in Format CREATE VIEW. I have assumed that,
whatever you like for newlines and indenting there,
you will like here too. (This applies only for the
dialects that have CREATE ... AS ... or CREATE ... IS ...).</p>

<p>Vendor examples:</p>

<p>Oracle: <a href="https://docs.oracle.com/en/database/oracle/oracle-database/19/lnpls/CREATE-FUNCTION-statement.html#GUID-B71BC5BD-B87C-4054-AAA5-213E856651F2">
the usual way</a>.</p>

<p>DB2: <a href="https://www.ibm.com/support/producthub/db2/docs/content/SSEPGG_11.5.0/com.ibm.db2.luw.sql.ref.doc/doc/r0003493.html">
inconsistent</a>.</p>

<p>SQL Server: <a href="https://docs.microsoft.com/en-us/sql/t-sql/statements/create-function-transact-sql?view=sql-server-ver15">
the usual way</a>, with newlines before and after AS.</p>

<p>MySQL: <a href="https://dev.mysql.com/doc/refman/8.0/en/create-procedure.html">
the usual way</a>.</p>

<p>MariaDB: <a href="https://mariadb.com/kb/en/create-function/">
inconsistent</a>.</p>

<p>Bloggers:</p>

<p>Factor: (in Chapter 1 "Writing Readable SQL", Listing 1-7)
shows the usual way, with newlines before and after AS.</p>

<H3 id="format-create-trigger">Format CREATE TRIGGER</H3><HR>

<p>Choice: change create-trigger clause to newline + indent+0 + create-trigger clause?
                                                                                                                    
This is not really different from the Choice for
<a href="#format-create-procedure-or-create-function">Format CREATE PROCEDURE or CREATE FUNCTION</a>.
We have an initial CREATE ... object_name, some modifiers, and then a triggered-action
statement which is usually a compound BEGIN/END statement.</p>

<p>According to our guidance via the SQL standard BNF, ON should be treated as a clause start.
However, the only prescriptive guide that has a CREATE TRIGGER example (Salvisberg) shows otherwise.
And the vendor manual examples are inconsistent.</p>

<p>Prescriptive guides:</p>

<p>Salvisberg shows: change create-trigger clause to newline + indent+0 + create-trigger clause = yes:<pre>
CREATE OR REPLACE TRIGGER dept_br_u
BEFORE UPDATE ON departments FOR EACH ROW
BEGIN
END;/</pre></p>

<p>Vendor manual examples:</p>

<p><a href="https://docs.oracle.com/en/database/oracle/oracle-database/19/lnpls/plsql-triggers.html#GUID-EC6A8FA1-9E60-4374-9905-639F4F100D83">
Oracle</a> shows BEFORE and ON as clauses. So is REFERENCING. So is FOR EACH ROW.</p>

<p><a href="https://www.ibm.com/support/knowledgecenter/SSEPEK_10.0.0/sqlref/src/tpc/db2z_sql_createtrigger.html">
DB2</a> shows AFTER and FOR EACH ROW and WHEN are clauses. Indents the BEGIN/END! Sometimes indents twice!</p>

<p><a href="https://docs.microsoft.com/en-us/sql/t-sql/statements/create-trigger-transact-sql?view=sql-server-ver15">
SQL Server</a> shows ON and FOR are clauses.</p>

<p><a href="https://dev.mysql.com/doc/refman/8.0/en/trigger-syntax.html">
Mysql</a> shows
BEFORE is BEFORE. FOR EACH ROW is newline + indent+0 + FOR EACH ROW.
Or
BEFORE is newline + indent+1 + BEFORE. FOR EACH ROW is newline + indent+1 + FOR EACH ROW.
inconsistent.</p>

<p><a href="https://mariadb.com/kb/en/create-trigger/">
MariaDB</a> shows indent+1 for AFTER, indent+2 for UPDATE.</p>

<p>Tarantool shows BEFORE and FOR EACH ROW are not indented. BEGIN is indented!</p>

<H3 id="format-case-expression">Format CASE expression</H3><HR>

<p>Choice: change WHEN/END to newline + indent+0 + WHEN/END (i.e. they left-align with CASE)?<br>
Choice: change WHEN/END to newline + indent+1 + WHEN/END?<br>
Choice: change THEN to THEN, or to newline + indent+2 + THEN?<br>
Choice: Change END to END, or to newline + indent+0 + END?</p>

<p>The indenting is relative to CASE.</p>

<p>CASE ... END is analogous to a statement.
So whenever a prescriptive guide says indent=yes or left-align=yes for a statement,
I would expect it to say something similar for CASE ... END.
So in a consistent world there would be no need for this "Format CASE expressions"
section, but I have to add it because prescriptive guides and formatters have
options for it.</p>

<p>If there is an AS alias in a select list, it follows END on the same line.</p>

<p>I have not seen suggestions that a series of
WHEN ... THEN ... should be treated as a "list" and therefore
be aligned as in <a href="#format-lists">Format lists</a>. I have, however, seen
<a href="https://forums.toadworld.com/t/formatter-puts-as-clause-on-a-separate-line/39050/4">a suggestion</a>
that CASE expressions should be treated as items in a list, for example<pre>
SELECT
   ''                               AS a,
   CASE
   WHEN
   END                              AS b,
   ''                               AS c ...</pre>
This could be stated for subqueries too.</p>

<p>Prescriptive guides:</p>

<p>Taranov shows: change WHEN to WHEN, change THEN to newline + indent+0 (align with WHEN), END aligns with CASE<pre>
CASE WHEN ...
     THEN ...
     WHEN ...
     THEN ...
END</pre></p>

<p>Holywell shows: change WHEN/END to newline + indent+0 + WHEN/END = yes: and THEN on the same line<pre>
CASE ...
WHEN ... THEN ...
WHEN ... THEN ...
END</pre></p>

<p>Benenson says (re CASE statements) "try to align WHEN, THEN, and ELSE together inside CASE and END"<pre>
CASE WHEN ...
     THEN ...
     ELSE ...
END</pre>
Not quite like Taranov because ELSE is elsewhere.</p>

<p>Mazur, Salvisberg show: change WHEN/ELSE to newline + indent+1 + WHEN/ELSE = yes: and THEN on the same line<pre>
CASE ...
   WHEN ... THEN ...
   WHEN ... THEN ...
   ELSE ...
END</pre>
Salvisberg adds "Try to use CASE rather than an IF statement with multiple ELSIF paths."
Mazur adds "Each <code>when</code> should be on its own line (nothing on the case line)
and should be indented one level deeper than the case line.
The <code>then</code> can be on the same line or on its own line below it, just aim to be consistent."</p>

<p>Vendor examples:</p>

<p><a href="https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/CASE-Expressions.html#GUID-CA29B333-572B-4E1D-BA64-851FABDBAE96">
Oracle:</a> inconsistent</p>

<p><a href="https://www.ibm.com/support/producthub/db2/docs/content/SSEPGG_11.5.0/com.ibm.db2.luw.sql.ref.doc/doc/r0023458.html">
DB2:</a> same as Mazur, Salvisberg</p>

<p><a href="https://docs.microsoft.com/en-us/sql/t-sql/language-elements/case-transact-sql?view=sql-server-ver15">
SQL Server:</a> same as Mazur, Salvisberg</p>

<p><a href="https://dev.mysql.com/doc/refman/8.0/en/control-flow-functions.html#operator_case">
MySQL:</a> inconsistent</p>

<p><a href="https://mariadb.com/kb/en/case-operator/">
MariaDB:</a> single line</p>

<p>Tarantool: single line</p>

<p>Oracle SQL Developer has separate options for indent of CASE, WHEN, THEN, and AND/OR.</p>

<p>Bloggers:</p>

<p>Toad formatter has an option "Position THEN on the same line".</p>

<p>Factor shows: change WHEN/ELSE to newline + indent+1 + WHEN/ELSE = yes,
              change THEN to newline + indent+2 + THEN<pre>
CASE ...
  WHEN ...
    THEN ...
  WHEN ...
    THEN ...
END</pre></p>

<p><a href="https://documentation.red-gate.com/sp10/sql-code-formatting-and-styles/customizing-your-formatting-style">
SQL Prompt</a> has options for placing WHEN / ELSE / THEN on new lines, and for aligning ELSE with WHEN.</p>

<p>Holywell example:<pre>
SELECT CASE postcode
       WHEN 'BN1' THEN 'Brighton'
       WHEN 'EH1' THEN 'Edinburgh'
       END AS city
  FROM office_locations
 WHERE country = 'United Kingdom'
   AND opening_time BETWEEN 8 AND 9
   AND postcode IN ('EH1', 'BN1', 'NN1', 'KW1');</pre>
... It looks like "right align word" but then there is no river. Or, there are two rivers.</p>

<p>
<H3 id="format-blocks-the-usual-way">Format blocks the usual way</H3><HR>

<p>Choice: Format blocks the usual way?</p>

<p>For this purpose a "block" is a group of statements enclosed by a "control statement".</p>

<p>In standard SQL (SQL/PSM) the control statements that enclose statements are:
BEGIN ... END, CASE ... END CASE, IF ... END IF, LOOP ... END LOOP, WHILE ... END WHILE,
REPEAT ... END REPEAT, FOR ... END FOR.
Naturally in Oracle or Oracle imitators (PL/SQL) the list differs, but
the effect of saying "yes" is the same:
Any statements between the verb and the END are indented N spaces.
The END aligns with the verb.
WHEN and ELSE are treated as control verbs.
IF condition THEN and WHEN condition THEN are single lines.
Example (with indent-amount = 2):<pre>
BEGIN
  sql-statement;
  LOOP
    sql-statement;
    IF condition THEN
      sql-statement;
    ELSE
      sql-statement;
    END IF;
  END LOOP;
END;</pre>
That is what I have seen in every source that has a consistent set of examples.
Therefore I think it is okay to say that is the "usual" way.</p>

<p>Choice: labels on same line as control verb?</p>

<p>If labels on same line = yes, using an SQL/PSM label for the example:<pre>
BEGIN
  loop_label: LOOP
    sql-statement;
  END LOOP loop_label;
END;</pre>
If labels on same line = no, using a PL/SQL label for the example:<pre>
BEGIN
  &lt;&lt;loop_label&gt;&gt;
  LOOP
    sql-statement;
  END LOOP loop_label;
END;</pre>
Notice, in the first example, how END aligns with loop_label not with LOOP.
I do not know whether this is common, but it is in the MySQL manual.</p>

<p>Choice: FOR ... LOOP is all one line: yes or no.<br>
If all one line = yes:<br>
<code>FOR iteration LOOP</code><br>
If all one line = no:<br>
<code>FOR iteration</code><br>
<code>LOOP</code><br>
That is the only example that I could find of a difference between
Salvisberg's recommendations and the Oracle manual.</p>

<p>Choice: a short IF ... END IF; can go on one line: yes or no<br>
This is about whether the "usual" form is followed rigidly for blocks,
even if for non-blocks it is okay to avoid "haiku".</p>

<p>Remember:
Modifiers of verbs go with the verb (see definition of "phrase"), so BEGIN ATOMIC has ATOMIC on the same line as BEGIN.
And DECLARE EXIT HANDLER FOR NOT FOUND is a single line.</p>

<p>Prescriptive guides:</p>

<p>Most of the prescriptive guides do not have anything to say about control statements.</p>

<p>Salvisberg says: indent blocks the usual way: yes. labels on same line: no. FOR ... LOOP is all one line: no.
Salvisberg also advises: avoid goto because there is no indenting that can indicate its effect on the flow,
and always have labels for loops. Example:<pre>
&lt;&lt;while_loop&gt;&gt;
WHILE (i <= co_max_value)
LOOP
   i := i + co_increment;
END LOOP while_loop;</pre>
... So different line for LOOP, and label has its own line.</p>

<p>Vendor manual examples:</p>

<p><a href="https://docs.oracle.com/database/121/LNPLS/controlstatements.htm#LNPLS435">
Oracle:</a>
  indent blocks the usual way: yes. labels on same line: no. FOR ... LOOP is all one line: yes.
  a short IF ... END IF; can go one line: no</p>

<p><a href="https://www.ibm.com/support/knowledgecenter/en/SSEPEK_10.0.0/sqlref/src/tpc/db2z_loopstatement4nativesqlpl.html">
DB2:</a>
     THEN is on same line as IF: yes.
  a short IF ... END IF; can go one line: no</p>

<p><a href="https://docs.microsoft.com/en-us/sql/t-sql/language-elements/else-if-else-transact-sql?view=sql-server-ver15">
SQL Server:</a>
    the examples given on this page are so wildly inconsistent that we'd have to say: there is no rule.
  a short IF ... END IF; can go one line: no</p>

<p>MySQL:
  indent blocks the usual way: yes. labels on same line: yes. FOR ... LOOP is all one line: n/a.
  a short IF ... END IF; can go one line: yes</p>

<p><a href="https://mariadb.com/kb/en/begin-end/">
MariaDB:</a>  not consistent, ignored</p>

<p>Oracle SQL Developer has an option "After statements" and one of the
options is "double break", that is, put two newlines after each statement.</p>

<H3 id="format-blocks-with-analogies-to-other-guides-and-choices">Format blocks with analogies to other guides and choices</H3><HR>

<p>Choice: Format blocks as you do for Format lists?</p>

<p>The previous section was about formatting blocks the usual way.
The reason you might want indenting some other way would, I suppose, be:
"because that is what we do in [insert language name here]".</p>

<p>I will illustrate WHILE in SQL/PSM blocks but the same considerations
are applicable for other conditional statements and for PL/SQL.</p>

<p>Once again, we can do "Choice re-use".
Start with the six Choices at the beginning of section <a href="#format-lists">Format lists</a>.
Substitute "statement" for "item", substitute ";" for ",", substitute "DO" for "(", substitute "END" for ")".
Now we have:<br>
Choice: Lists maximum number of statements per line = N?<br>
Choice: Lists start with: space, or newline + usual fixed indent + N levels, or newline + align past preceding word?<br>
Choice: Lists ; i.e. end-of-line semicolon becomes ; + newline or newline + ; or newline + ; + space?<br>
Choice: Lists have similar parts align?<br>
Choice: Lists DO i.e. initial left parenthesis becomes DO or newline + DO or newline + DO + newline?<br>
Choice: Lists END i.e. final right parenthesis becomes END or newline + END?</p>

<p>For example, if<br>
maximum number of statements per line = 1,<br>
lists start with usual fixed indent + 1 level,<br>
end-of-line semicolon becomes ; + newline,<br>
similar parts align = no,<br>
DO becomes newline + DO + newline,<br>
END becomes END,
we get:<br>
<code>WHILE condition DO</code><br>
<code>statement;</code><br>
<code>statement; END WHILE;</code></p>

<p>Now that we are talking about SQL as a procedural language,
it is more legitimate to compare with indentation styles in other languages.
The functional equivalent for SQL block begin ... end is usually { ... } braces.
So it is useful to look at the Wikipedia article
<a href="https://en.wikipedia.org/wiki/Indentation_style">Indentation style</a>
section
<a href="https://en.wikipedia.org/wiki/Indentation_style#Brace_placement_in_compound_statements">
"Brace placement in compound statements"</a>.</p>

<p>The following is an SQL variation of the table in that section.
I am assuming indentation with 4 spaces, and space-before-semicolon = no.</p>

<p><pre>
DO ... END placement        Style
--------------------        -----

WHILE condition DO          K&amp;R and variants
    statement;
    statement;   
END WHILE;

WHILE condition              Allman
DO
    statement;
    statement;
END WHILE;

WHILE condition              GNU
    DO
        statements
    END WHILE;

WHILE condition              Whitesmiths
    DO
    statements
    END WHILE;

WHILE condition              Horstmann + Pico
DO    statement;
      statement;
END WHILE;

WHILE condition DO            Ratliff
    statement;
    statement;
    END WHILE;

WHILE condition               Lisp
    DO statement;
       statement;
END WHILE;

WHILE condition               Haskell
    DO statement
    ; statement
    ;
    END WHILE
</pre></p>

<H3 id="format-declare">Format DECLARE</H3><HR>

<p>Choices: none needed</p>

<p>As with INSERT UPDATE etc., the Choices are already made, there is
nothing to do now except give an example. This one is
from Taranov, who believes definitions should be aligned
(as in <a href="#format-create-table">Format CREATE TABLE</a>), and data types should be lower case
(as in <a href="#data-types">Data types</a>).
<br>
<code> DECLARE @myGoodVarchareVariable  varchar(50);</code><br>
<code> DECLARE @myGoodNVarchareVariable nvarchar(90);</code><br>
<code> DECLARE @myGoodCharVariable      char(7);</code><br>
<code> DECLARE @myGoodNCharVariable     nchar(10);</code><br></p>

<p>If there was a default then it would not cause a newline,
because DEFAULT was not established to be a clause start
according to any of the criteria shown in previous sections.</p>

<p>If there was a multiple-column declaration then
the Choice that would apply is as in <a href="#format-lists">Format lists</a>.</p>

<H3 id="#format-overflow">Format overflow</H3><HR>

<p>Choice: if overflow ignore Maximum line length, or word wrap, or format = no.</p>

<p>An "overflow" occurs when a line of SQL text can go past the Right margin.</p>

<p>The previous sections have shown many ways to format an SQL statement
onto multiple lines. Therefore overflow should be rare.</p>

<p>But -- hopefully very rarely -- a single clause or a single list item will
cause overflow past the maximum length. What then?</p>

<p>Setting "ignore Maximum line length" means "go ahead and overflow".
It is not a big deal if the line is on a screen, just result will be
a scroll bar or a return to the leftmost column position.</p>

<p>Setting "word wrap" means what in CSS would be called
<a href="https://www.w3schools.com/cssref/css3_pr_word-wrap.asp">
word-wrap: normal</a>
or in my terminology it means "if the next word would overflow, newline and indent 0".</p>

<p>Setting "format = no", that is, "do not try to format a statement that would
cause overflow", might help readability if the original format contained newlines.</p>

<p>Since "format = no" implies that you will have to figure out something readable by yourself,
the <a href="https://www.oracle.com/technetwork/java/codeconventions-150003.pdf">
Java code conventions</a>
might help because the "general principles" are applicable to SQL if the too-long line is due to a single expression. They are:<br>
"When an expression will not fit on a single line, break it according to these general principles:<br>
•Break after a comma.<br>
•Break before an operator.<br>
•Prefer higher-level breaks to lower-level breaks.<br>
•Align the new line with the beginning of the expression at the same level on the previous line.<br>
•If the above rules lead to confusing code or to code that’s squished up against the right margin, just indent 8 spaces instead."</p>

<p>Bloggers:</p>

<p>Commonwealth of Pennsylvania Department of Public Welfare,
<a href="https://www.dhs.pa.gov/providers/Providers/Documents/Business%20and%20Tech%20Standards/Data%20Domain/Oracle%20PL%20SQL%20Naming%20and%20Coding.pdf">
"Oracle PLSQL Coding and Naming Standards"</a>,
says "It is allowed to overshoot right margin if code cannot be accommodated in 78 characters."</p>

<H3 id="formatters-or-pretty-printers">Formatters or pretty printers</H3><HR>

<p>If you have a good GUI client, it will add colour highlighting on your screen.</p>

<p>If you have a good formatter, it will automatically take care of some of the Choices that I raised here.
If your group uses Toad, SQL Developer, SQL Server Management Studio,
SQLinForm, etc., just accept what they offer.</p>

<p>Tao Klerks and Steve Culshaw have come up with a github.com page
<a href="https://github.com/TaoK/PoorMansTSqlFormatter/wiki/SQL-Formatter-comparisons">
"SQL Formatter comparisons"</a>
which lists more formatters than I dreamed existed, and some of them are
open source, and some of them are online.</p>

<p>Google "sql lint" and you will see a few more products that will advise but not change.</p>

<p>Bloggers:</p>

<p>Lester I. McCann (writing about C)
<a href="https://www2.cs.arizona.edu/~mccann/indent_c.html">says:</a>
"What about programs that will automatically indent source code for you?
Such "crutches" do exist, but I discourage their use on code that is being written from scratch
because you are likely to develop bad habits if you begin to rely on the program to fix your
mistakes for you."</p>

<H3 id="contributors">Contributors</H3><HR>

<p><a href="https://github.com/pgulutzan">https://github.com/pgulutzan</a>
<br>
<br>
<br>
<br></p>

<p>
The final section of this guide is a copy of the GNU General Public License (GPL).
It is possible to use GPL for other than software, as explained at
<a href="https://www.gnu.org/licenses/gpl-faq.html#GPLOtherThanSoftware">the gnu.org FAQ</a>.
FLOSS manuals <a href="https://www.adamhyde.net/1198-2/">are under GPL</a>.
So is this document.</p>

<p>All references to "this program" or "software" mean "this guide", the Descriptive SQL Style Guide.</p>

<H3 id="gpl-version-2-license">GPL Version 2 License</H3><HR>

<p>
<pre>

		    GNU GENERAL PUBLIC LICENSE
		       Version 2, June 1991

 Copyright (C) 1989, 1991 Free Software Foundation, Inc.,
 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA
 Everyone is permitted to copy and distribute verbatim copies
 of this license document, but changing it is not allowed.

			    Preamble

  The licenses for most software are designed to take away your
freedom to share and change it.  By contrast, the GNU General Public
License is intended to guarantee your freedom to share and change free
software--to make sure the software is free for all its users.  This
General Public License applies to most of the Free Software
Foundation's software and to any other program whose authors commit to
using it.  (Some other Free Software Foundation software is covered by
the GNU Lesser General Public License instead.)  You can apply it to
your programs, too.

  When we speak of free software, we are referring to freedom, not
price.  Our General Public Licenses are designed to make sure that you
have the freedom to distribute copies of free software (and charge for
this service if you wish), that you receive source code or can get it
if you want it, that you can change the software or use pieces of it
in new free programs; and that you know you can do these things.

  To protect your rights, we need to make restrictions that forbid
anyone to deny you these rights or to ask you to surrender the rights.
These restrictions translate to certain responsibilities for you if you
distribute copies of the software, or if you modify it.

  For example, if you distribute copies of such a program, whether
gratis or for a fee, you must give the recipients all the rights that
you have.  You must make sure that they, too, receive or can get the
source code.  And you must show them these terms so they know their
rights.

  We protect your rights with two steps: (1) copyright the software, and
(2) offer you this license which gives you legal permission to copy,
distribute and/or modify the software.

  Also, for each author's protection and ours, we want to make certain
that everyone understands that there is no warranty for this free
software.  If the software is modified by someone else and passed on, we
want its recipients to know that what they have is not the original, so
that any problems introduced by others will not reflect on the original
authors' reputations.

  Finally, any free program is threatened constantly by software
patents.  We wish to avoid the danger that redistributors of a free
program will individually obtain patent licenses, in effect making the
program proprietary.  To prevent this, we have made it clear that any
patent must be licensed for everyone's free use or not licensed at all.

  The precise terms and conditions for copying, distribution and
modification follow.

		    GNU GENERAL PUBLIC LICENSE
   TERMS AND CONDITIONS FOR COPYING, DISTRIBUTION AND MODIFICATION

  0. This License applies to any program or other work which contains
a notice placed by the copyright holder saying it may be distributed
under the terms of this General Public License.  The "Program", below,
refers to any such program or work, and a "work based on the Program"
means either the Program or any derivative work under copyright law:
that is to say, a work containing the Program or a portion of it,
either verbatim or with modifications and/or translated into another
language.  (Hereinafter, translation is included without limitation in
the term "modification".)  Each licensee is addressed as "you".

Activities other than copying, distribution and modification are not
covered by this License; they are outside its scope.  The act of
running the Program is not restricted, and the output from the Program
is covered only if its contents constitute a work based on the
Program (independent of having been made by running the Program).
Whether that is true depends on what the Program does.

  1. You may copy and distribute verbatim copies of the Program's
source code as you receive it, in any medium, provided that you
conspicuously and appropriately publish on each copy an appropriate
copyright notice and disclaimer of warranty; keep intact all the
notices that refer to this License and to the absence of any warranty;
and give any other recipients of the Program a copy of this License
along with the Program.

You may charge a fee for the physical act of transferring a copy, and
you may at your option offer warranty protection in exchange for a fee.

  2. You may modify your copy or copies of the Program or any portion
of it, thus forming a work based on the Program, and copy and
distribute such modifications or work under the terms of Section 1
above, provided that you also meet all of these conditions:

    a) You must cause the modified files to carry prominent notices
    stating that you changed the files and the date of any change.

    b) You must cause any work that you distribute or publish, that in
    whole or in part contains or is derived from the Program or any
    part thereof, to be licensed as a whole at no charge to all third
    parties under the terms of this License.

    c) If the modified program normally reads commands interactively
    when run, you must cause it, when started running for such
    interactive use in the most ordinary way, to print or display an
    announcement including an appropriate copyright notice and a
    notice that there is no warranty (or else, saying that you provide
    a warranty) and that users may redistribute the program under
    these conditions, and telling the user how to view a copy of this
    License.  (Exception: if the Program itself is interactive but
    does not normally print such an announcement, your work based on
    the Program is not required to print an announcement.)

These requirements apply to the modified work as a whole.  If
identifiable sections of that work are not derived from the Program,
and can be reasonably considered independent and separate works in
themselves, then this License, and its terms, do not apply to those
sections when you distribute them as separate works.  But when you
distribute the same sections as part of a whole which is a work based
on the Program, the distribution of the whole must be on the terms of
this License, whose permissions for other licensees extend to the
entire whole, and thus to each and every part regardless of who wrote it.

Thus, it is not the intent of this section to claim rights or contest
your rights to work written entirely by you; rather, the intent is to
exercise the right to control the distribution of derivative or
collective works based on the Program.

In addition, mere aggregation of another work not based on the Program
with the Program (or with a work based on the Program) on a volume of
a storage or distribution medium does not bring the other work under
the scope of this License.

  3. You may copy and distribute the Program (or a work based on it,
under Section 2) in object code or executable form under the terms of
Sections 1 and 2 above provided that you also do one of the following:

    a) Accompany it with the complete corresponding machine-readable
    source code, which must be distributed under the terms of Sections
    1 and 2 above on a medium customarily used for software interchange; or,

    b) Accompany it with a written offer, valid for at least three
    years, to give any third party, for a charge no more than your
    cost of physically performing source distribution, a complete
    machine-readable copy of the corresponding source code, to be
    distributed under the terms of Sections 1 and 2 above on a medium
    customarily used for software interchange; or,

    c) Accompany it with the information you received as to the offer
    to distribute corresponding source code.  (This alternative is
    allowed only for noncommercial distribution and only if you
    received the program in object code or executable form with such
    an offer, in accord with Subsection b above.)

The source code for a work means the preferred form of the work for
making modifications to it.  For an executable work, complete source
code means all the source code for all modules it contains, plus any
associated interface definition files, plus the scripts used to
control compilation and installation of the executable.  However, as a
special exception, the source code distributed need not include
anything that is normally distributed (in either source or binary
form) with the major components (compiler, kernel, and so on) of the
operating system on which the executable runs, unless that component
itself accompanies the executable.

If distribution of executable or object code is made by offering
access to copy from a designated place, then offering equivalent
access to copy the source code from the same place counts as
distribution of the source code, even though third parties are not
compelled to copy the source along with the object code.

  4. You may not copy, modify, sublicense, or distribute the Program
except as expressly provided under this License.  Any attempt
otherwise to copy, modify, sublicense or distribute the Program is
void, and will automatically terminate your rights under this License.
However, parties who have received copies, or rights, from you under
this License will not have their licenses terminated so long as such
parties remain in full compliance.

  5. You are not required to accept this License, since you have not
signed it.  However, nothing else grants you permission to modify or
distribute the Program or its derivative works.  These actions are
prohibited by law if you do not accept this License.  Therefore, by
modifying or distributing the Program (or any work based on the
Program), you indicate your acceptance of this License to do so, and
all its terms and conditions for copying, distributing or modifying
the Program or works based on it.

  6. Each time you redistribute the Program (or any work based on the
Program), the recipient automatically receives a license from the
original licensor to copy, distribute or modify the Program subject to
these terms and conditions.  You may not impose any further
restrictions on the recipients' exercise of the rights granted herein.
You are not responsible for enforcing compliance by third parties to
this License.

  7. If, as a consequence of a court judgment or allegation of patent
infringement or for any other reason (not limited to patent issues),
conditions are imposed on you (whether by court order, agreement or
otherwise) that contradict the conditions of this License, they do not
excuse you from the conditions of this License.  If you cannot
distribute so as to satisfy simultaneously your obligations under this
License and any other pertinent obligations, then as a consequence you
may not distribute the Program at all.  For example, if a patent
license would not permit royalty-free redistribution of the Program by
all those who receive copies directly or indirectly through you, then
the only way you could satisfy both it and this License would be to
refrain entirely from distribution of the Program.

If any portion of this section is held invalid or unenforceable under
any particular circumstance, the balance of the section is intended to
apply and the section as a whole is intended to apply in other
circumstances.

It is not the purpose of this section to induce you to infringe any
patents or other property right claims or to contest validity of any
such claims; this section has the sole purpose of protecting the
integrity of the free software distribution system, which is
implemented by public license practices.  Many people have made
generous contributions to the wide range of software distributed
through that system in reliance on consistent application of that
system; it is up to the author/donor to decide if he or she is willing
to distribute software through any other system and a licensee cannot
impose that choice.

This section is intended to make thoroughly clear what is believed to
be a consequence of the rest of this License.

  8. If the distribution and/or use of the Program is restricted in
certain countries either by patents or by copyrighted interfaces, the
original copyright holder who places the Program under this License
may add an explicit geographical distribution limitation excluding
those countries, so that distribution is permitted only in or among
countries not thus excluded.  In such case, this License incorporates
the limitation as if written in the body of this License.

  9. The Free Software Foundation may publish revised and/or new versions
of the General Public License from time to time.  Such new versions will
be similar in spirit to the present version, but may differ in detail to
address new problems or concerns.

Each version is given a distinguishing version number.  If the Program
specifies a version number of this License which applies to it and "any
later version", you have the option of following the terms and conditions
either of that version or of any later version published by the Free
Software Foundation.  If the Program does not specify a version number of
this License, you may choose any version ever published by the Free Software
Foundation.

  10. If you wish to incorporate parts of the Program into other free
programs whose distribution conditions are different, write to the author
to ask for permission.  For software which is copyrighted by the Free
Software Foundation, write to the Free Software Foundation; we sometimes
make exceptions for this.  Our decision will be guided by the two goals
of preserving the free status of all derivatives of our free software and
of promoting the sharing and reuse of software generally.

			    NO WARRANTY

  11. BECAUSE THE PROGRAM IS LICENSED FREE OF CHARGE, THERE IS NO WARRANTY
FOR THE PROGRAM, TO THE EXTENT PERMITTED BY APPLICABLE LAW.  EXCEPT WHEN
OTHERWISE STATED IN WRITING THE COPYRIGHT HOLDERS AND/OR OTHER PARTIES
PROVIDE THE PROGRAM "AS IS" WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESSED
OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.  THE ENTIRE RISK AS
TO THE QUALITY AND PERFORMANCE OF THE PROGRAM IS WITH YOU.  SHOULD THE
PROGRAM PROVE DEFECTIVE, YOU ASSUME THE COST OF ALL NECESSARY SERVICING,
REPAIR OR CORRECTION.

  12. IN NO EVENT UNLESS REQUIRED BY APPLICABLE LAW OR AGREED TO IN WRITING
WILL ANY COPYRIGHT HOLDER, OR ANY OTHER PARTY WHO MAY MODIFY AND/OR
REDISTRIBUTE THE PROGRAM AS PERMITTED ABOVE, BE LIABLE TO YOU FOR DAMAGES,
INCLUDING ANY GENERAL, SPECIAL, INCIDENTAL OR CONSEQUENTIAL DAMAGES ARISING
OUT OF THE USE OR INABILITY TO USE THE PROGRAM (INCLUDING BUT NOT LIMITED
TO LOSS OF DATA OR DATA BEING RENDERED INACCURATE OR LOSSES SUSTAINED BY
YOU OR THIRD PARTIES OR A FAILURE OF THE PROGRAM TO OPERATE WITH ANY OTHER
PROGRAMS), EVEN IF SUCH HOLDER OR OTHER PARTY HAS BEEN ADVISED OF THE
POSSIBILITY OF SUCH DAMAGES.

		     END OF TERMS AND CONDITIONS

	    How to Apply These Terms to Your New Programs

  If you develop a new program, and you want it to be of the greatest
possible use to the public, the best way to achieve this is to make it
free software which everyone can redistribute and change under these terms.

  To do so, attach the following notices to the program.  It is safest
to attach them to the start of each source file to most effectively
convey the exclusion of warranty; and each file should have at least
the "copyright" line and a pointer to where the full notice is found.

    <one line to give the program's name and a brief idea of what it does.>
    Copyright (C) <year>  <name of author>

    This program is free software; you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation; either version 2 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License along
    with this program; if not, write to the Free Software Foundation, Inc.,
    51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.

Also add information on how to contact you by electronic and paper mail.

If the program is interactive, make it output a short notice like this
when it starts in an interactive mode:

    Gnomovision version 69, Copyright (C) year name of author
    Gnomovision comes with ABSOLUTELY NO WARRANTY; for details type `show w'.
    This is free software, and you are welcome to redistribute it
    under certain conditions; type `show c' for details.

The hypothetical commands `show w' and `show c' should show the appropriate
parts of the General Public License.  Of course, the commands you use may
be called something other than `show w' and `show c'; they could even be
mouse-clicks or menu items--whatever suits your program.

You should also get your employer (if you work as a programmer) or your
school, if any, to sign a "copyright disclaimer" for the program, if
necessary.  Here is a sample; alter the names:

  Yoyodyne, Inc., hereby disclaims all copyright interest in the program
  `Gnomovision' (which makes passes at compilers) written by James Hacker.

  <signature of Ty Coon>, 1 April 1989
  Ty Coon, President of Vice

This General Public License does not permit incorporating your program into
proprietary programs.  If your program is a subroutine library, you may
consider it more useful to permit linking proprietary applications with the
library.  If this is what you want to do, use the GNU Lesser General
Public License instead of this License.


</pre>
</p>

</body>
</html>

