# C# Live Project Sprint

The Management Portal software is used to manage a collection of jobs. Admins are able to create and distribute a weekly schedule assigning users to certain jobs. Users are able to keep track of which job they are assigned to for the week.

The primary components of this project include the creation of registered users, differentiation between users and admins, creation of "Jobs" with necessary details, adding users to those jobs with an instance of "Schedule" for each user on each job.

The secondary components include a Chat feature (for all users to have a single main chat room for discussion) and Company News (where admins can create announcements for all employees to read).

### List of Technologies Used:
- Azure DevOps
- Visual Studio 2017
- Git and Team Foundation Server
- C# ASP.Net MVC
- Entity Framework 6
- PagedList.Mvc
- Leafletjs
- Leafet Routing Machinge API
- Geolocation API
- Bootstrap 4
- Slack and Google Meet for communications
  


## User Story 5327: Show Directions on Map Load

###### pic user story

### What is the issue?

This user story required auto populating the project's current map with a start location using the user's current location and an end location with the job site's location immediately after page load.

###### pic app before

### How is the issue resolved?

The current project map was created using leftletjs and leaflet routing machine. I researched them to understand their implementations. Then, I researched how to get a user's current location and found the Geolocation API and it's getCurrentPosition method to get the start location. Then I used the JobSite object's latitude and longitude properties saved in the JobSites database table to get the ending location.

###### pic code before, database, code after

### What is the end result?

The result is that when a user goes to the job site's detail page, they will see a map with the starting and ending location auto populated with the user's current location and the job site's location, the written directions, and a red polyline connecting the 2 locations.

###### pic app after
