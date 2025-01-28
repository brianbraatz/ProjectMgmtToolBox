---
created: 2024-03-22T14:07:17 (UTC -05:00)
tags: []
source: https://www.scriptrunnerhq.com/inspiration/blog/top-10-most-commonly-used-jira-query-language-functions?utm_term=&utm_campaign=&utm_source=adwords&utm_medium=ppc&hsa_acc=7742523188&hsa_cam=20410443246&hsa_grp=155366488747&hsa_ad=669677581103&hsa_src=g&hsa_tgt=dsa-1462257790783&hsa_kw=&hsa_mt=&hsa_net=adwords&hsa_ver=3&gad_source=1&gclid=Cj0KCQjw2PSvBhDjARIsAKc2cgOjMiW_BCZy0xqHLRthQBp7fU1lqt_82xFGKDQSatJGMWyYf-hsf0IaAlBwEALw_wcB
author: 
---

# Top 10 most commonly used scripted JQL functions

source: https://www.scriptrunnerhq.com/inspiration/blog/top-10-most-commonly-used-jira-query-language-functions?utm_term=&utm_campaign=&utm_source=adwords&utm_medium=ppc&hsa_acc=7742523188&hsa_cam=20410443246&hsa_grp=155366488747&hsa_ad=669677581103&hsa_src=g&hsa_tgt=dsa-1462257790783&hsa_kw=&hsa_mt=&hsa_net=adwords&hsa_ver=3&gad_source=1&gclid=Cj0KCQjw2PSvBhDjARIsAKc2cgOjMiW_BCZy0xqHLRthQBp7fU1lqt_82xFGKDQSatJGMWyYf-hsf0IaAlBwEALw_wcB

> ## Excerpt
> Looking for JQL queries to conduct advanced searches in Jira? Create your own with this tool, or check out the top 10 most used ScriptRunner JQL functions now.

---
![Jamie Echlin](https://cdn.sanity.io/images/ozw8esko/production/a0c0e40ed3708e8f85da4963b46543df088879e7-600x600.png)

Jamie Echlin

12th January, 2024

![Data center icon](https://cdn.sanity.io/images/ozw8esko/production/da690fbc8c2524a5f1174ccc58e0e6c894d9811a-267x267.png?h=50)

![Server icon](https://cdn.sanity.io/images/ozw8esko/production/e5a5914dc396ce3210bde2cdd295f299b457dfc1-268x267.png?h=50)

## The Top 10 Jira Query Language (JQL) functions from ScriptRunner

Looking for JQL queries to conduct advanced searches in Jira? Create your own with this tool, or check out the top 10 most used ScriptRunner JQL functions now.

## **Build your JQL query**

Not sure how to translate what you're looking for into JQL? Let our JQL builder tool do it for you.

_**Note:** This tool is AI-powered. We've done our best to teach it well, but if you spot something that doesn't look right, please use the feedback buttons to let us know! For best experience, please use on desktop._

### Top 10 ScriptRunner JQL functions

Many Jira users or admins have to perform search queries using Jira Query Language (JQL) everyday. But JQL out-of-the-box can be limiting. Luckily, JQL functions in ScriptRunner let you perform complex searches and create custom Jira Software boards.

ScriptRunner offers a large library of useful JQL functions, as well as the ability to [create your own queries](https://docs.adaptavist.com/sr4js/latest/features/jql-functions). The reference guide below features 10 of the most popular functions in ScriptRunner for Jira Server and Data Center, including the correct syntax and examples for each.

Feel free to print it, share it, or just read on below.

### 1\. EpicsOf - Query on epic links

This ScriptRunner JQL function allows you to query on epic links, such as finding all epics that have unresolved stories.  

**issueFunction in epicsOf (Subquery)**

Example: issueFunction in epicsOf ("resolution = unresolved")

##### Example for ‘epicsOf’

Let’s say you need to keep up on the opened epics in your main project called Mobile App (Mobile). You could create a filter using 'epicsOf' that would find all of the epics with unresolved issues in the Mobile project:

```javascript
1issueFunction in epicsOf("resolution=empty and project=Mobile")
```

### 2\. issuesinEpics - Find all stories for open epics

Using this ScriptRunner JQL function, you can find all stories for open epics in a project, and then look specifically at the status of issues, such as ‘in progress.’

**issueFunction in issuesInEpics (Subquery)**

Example: issueFunction in issuesInEpics ("project=JRA and status = 'in progress'")

##### Example for ‘issuesinEpics’

As a project manager, you might want to look at open epics and then at issues in specific statuses to see how many open, in progress, or other issues’ statues are in the current project. Specifically, you may want to see issues in the open epics that are also open, so you can gauge the work your team has yet to start. This is what you’d have to type in the search box to see all your "to do" issues within epics in the specific Mobile project:

```javascript
1issueFunction in issuesInEpics("project=Mobile and status='to do'")
```

### 3\. linkedIssuesOf - Return linked issues

Using the ‘linkedIssuesOf’ JQL function you can return linked issues, such as all unresolved issues that are blocked by open issues.

**linkedIssuesOf(Subquery, \[link name\])**

Example: linkedIssuesOf ("status="Open", "blocks") and resolution is empty

##### Example for ‘linkedIssuesOf’

To find all unresolved issues that are blocked by issues in a "to do" status. This ScriptRunner JQL function will help you see the issues that are waiting on other issues which the team hasn't started yet, equipping you with the information to take action on the blockers.

```javascript
1issueFunction in linkedIssuesOf ("status='to do'","blocks") AND resolution = empty
```

### 4\. linkedIssuesOfRecursive - Return linked issues recursively

This function allows you to return linked issues recursively. That is, to return all issues that are linked both directly and indirectly to the results of the initial query. The example query below returns all issues linked to Jira-1. Check out the example to get a more detailed explanation of this function.

**issueFunction in linkedIssuesOfRecursive (Subquery)**

Example: issueFunction in linkedIssuesOfRecursive("issue =Jira-1")

##### Example for ‘linkedIssuesOfRecursive’

As a developer, you may need to see how a bug issue affects your product in multiple ways, so you must find all links, both direct and indirect, that trace back to that main bug issue.

With the ‘linkedIssuesOfRecursive’ ScriptRunner JQL function, you can see all issues that link back to the main issue you selected, including blocks links, duplicates, clones, and more.

```javascript
1issueFunction in linkedIssuesOfRecursive ("issue =adlearn-711")
```

### 5\. linkedIssuesOfAllRecursive - Include subtask and epic links with no link type specified

This ScriptRunner JQL function allows you to include the subtask and epic links when you don't specify a link type. Otherwise, it functions identically to linkedissuesofRecursive.

**issueFunction in linkedIssuesOf AllRecursive**

Example: issueFunction in linkedIssues OfAllRecursive("issue =ADLEARN-711")

##### Example for ‘linkedIssuesOfAllRecursive’

As a developer, you may need to see how a bug issue affects your product in multiple ways, so you must find all links, both direct and indirect, that trace back to that main bug issue. And if you want to dig deeper in this search, you can use this function to look at all recursive links that also include all epics and all subtasks for an issue as well.

Including all items connected to the issue expands the search and gives an even greater scope of where an issue is linked in Jira:

```javascript
1issueFunction in linkedIssuesOfAllRecursive ("issue =adlearn-711")
```

### 6\. subtasksOf - Query on epic links

This JQL function allows you to query on epic links, such as finding all epics that have unresolved stories.

**issueFunction in subtasksOf (Subquery)**

Example: issuefunction in subtasksOf ("issuetype = story and status != closed")

##### Example for ‘subtasksOf’

Use this ScriptRunner JQL function when you want to see the subtasks that are still open, but their parent issue is resolved. In the Mobile project, this is how you get a list of all subtasks with parent issues that are marked resolved, but the sub-tasks are still open:

```javascript
1issueFunction in subtasksOf("project=Mobile and resolution is not empty") and status="to do"
```

### 7\. parentsOf - Return the parents of issues specified in the subquery

This ScripRunner JQL function allows you to return the parents of issues that you specify in the subquery. For example, you can find the parent issues of all issues where you are the assignee of an open sub-task using the resolution is empty and currentUser function.

**issueFunction in parentsOf (Subquery)**

Example: issueFunction in parentsOf ("resolution is empty and assignee = currentUser()")

##### Example for ‘parentsOf’

If you want to see the parents of subtask issues you specify in a subquery, use the ParentsOf function.

For example, you may want to see all of the parent issues where you are the assignee of an open sub-task:

```javascript
1issueFunction in parentsOf("resolution is empty and assignee = currentUser()")
```

### 8\. expression - Compare attributes of fields

This JQL function lets you compare attributes of fields including system estimate and date fields, as well as any numeric, date, or datetime custom field.

For example, you can find issues where work logged on the issue was more than originally estimated.

**issueFunction in expression (Subquery, expression)**

Example: issueFunction in expression ("", "timespent > originalestimate")

##### Example for ‘expression’

As a project manager, you may want to find out what issues were poorly estimated on, specifically those issues where more work was logged on the issue than originally estimated. For that case, you can use the expression JQL function.

```javascript
1issueFunction in expression ('',"timespent" > originalestimate)
```

### 9\. commented - Return issues based on a comment query

This function allows you to return issues based on a comment query. Your comment query can include a date query, username, roles, as well as comment types such as internal. For example, using the ‘commented’ JQL function in ScriptRunner you can search for issues with only internally visible comments.

**issueFunction in expression (Subquery, expression)**

Example: issueFunction in expression ("", "timespent > originalestimate")

##### Example for ‘commented’

As a service desk manager, you may want to find all of the internal comments made during the last three weeks.

Here’s how you would use the ‘commented’ JQL function to see a list of issues that contain internal comments from the last three weeks:

```javascript
1issuefunction in commented ("visibility internal after -3w")
```

### 10\. lastComment - See the last comment for an issue

This JQL function allows you to see the last comment for an issue based on your query. For example, you can find issues where the person last commenting is not in the Developers role. Or, remove the "not" and search for the last comment of someone in the Developers role.

**issueFunction in lastComment (comment query)**

Example: issueFunction not in lastComment ("inRole Developers")

##### Example for ‘lastComment’

As a project manager, you may want to find issues with comments where the last comment was made within the last hour. If you were tracking down a recent correspondence and needed to see what the latest is on the issues in the Mobile project within the last hour, you would use ‘lastComment’ along with specifying the project in the query. This ScriptRunner JQL function gives me all the issues in the Mobile project that had comments made within the last hour.

```javascript
1project = Mobile AND issueFunction in lastComment ("after -1h")
```

## Want to explore further?

If you haven’t experienced the full power of ScriptRunner for Jira yet, try it now with a 30-day free trial.
