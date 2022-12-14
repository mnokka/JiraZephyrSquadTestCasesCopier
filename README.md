# Jira Zephyr Squad tests from one project to another 
  
Zephyr Squad own test export does zillions of duplicates for each testcases, it also does not copy issue descriptions. 
Commercial Better Excel export plugin does better job, but must be limited 1000 issues max at the exporttime (otherwise it crashes Jira due memory binge usage).  1000 tests can be JQL queried by using test case creation time (including minutes) as fetch criteria. 
  
If source project uses Epic as definition for test area (test cases are linked to some defining Epic), Epics must be copied to target project. (Script Runner project copy nor clone cant not handle test case steps)

Finally source project Epics-test case links must be recreated in target project (and remove possible test case duplicates)   

Couple of helper utilities were created

1) copy components from one project to another

2) copy descriptions from source project test case to matching target project test case (to get text layout correctly copied)

3) copy normal Jira data from source project test case to matching target project test case (in order to fix stuff not exported by Better Excel)


(other solution is to bulk clone/move issues in 1000 query sets. This will copy data and creating links (Epic-test case) also, no need to use any of these
data manipulation tools)s


<br />
<br />
<br />   
### Copy one projects Epics (summary+description) to another project. For Jira Data Center usage
<br />
<br />
<br />

Install Python libraries:  
pip install -r requirements.txt    
<br />
<br />

    
usage: CopyEpics.py [-h] [-v] [-w password] [-u user] [-s server_address] [-r on|off]  
<br />
<br />


options:  
  -h, --help         show this help message and exit  
  -v                 Show version&author and exit  
  -w password        <JIRA password>  
  -u user            <JIRA user account>  
  -s server_address  <JIRA service>  
  -r on|off          <DryRun - do nothing but emulate. On by default>
  
  
Note: source and target projects hardcoded  

EXAMPLE: CopyEpics.py -u MYUSERNAME -w MYPASSWORD -s https://MYOWNJIRA.fi/  
<br />
<br />
<br />
<br />
###Browse source project and find Epic-Test case linkage pairs. Remove possible copies of of matched test case (fixing Zephyr Squad importer errors). Recreating links to target project

Note:source and target projects hardcoded   

EXAMPLE: FindCreateEpicTestLinks.py -u MYUSERNAME -w MYPASSWORD -s https://MYOWNJIRA.fi/   

<br />
<br />
<br />
<br />  

### Copy source project components to target project  
  
Note:source and target projects hardcoded 
  
EXAMPLE: CopyComponents.py -u MYUSERNAME -w MYPASSWORD -s https://MYOWNJIRA.fi/   


### Copy source project test case "normal Jira data" to target project matching test case (created during excel import)

Note:source and target projects hardcoded 
  
EXAMPLE: CopyTestJiraData.py -u MYUSERNAME -w MYPASSWORD -s https://MYOWNJIRA.fi/


### Copy source project descriptions to target project test cases

Note: This fixes original data copier issue (description was UTF-8 encoded, but not backwards and JQL 
special chras filtered out to make query possible); uses raw data for copy  

Uses log parsed file for source test case --> target test case relation creation 

EXAMPLE: CopyDescriptions.py -u MYUSERNAME -w MYPASSWORD -s https://MYOWNJIRA.fi/



