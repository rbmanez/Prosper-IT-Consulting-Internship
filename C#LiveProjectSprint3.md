# C# Live Project Sprint 3
## Table of Contents
- [C# Live Project Sprint 3 General Information](#c-live-project-sprint-3-general-information)
- [User Story 1: Personal Photo Refator](#user-story-1-personal-photo-refator)
- []()
- []()
- []()




## C# Live Project Sprint 3 General Information
The Management Portal software is used to manage a collection of jobs. Admins are able to create and distribute a weekly schedule assigning users to certain jobs. Users are able to keep track of which job they are assigned to for the week.

The primary components of this project include the creation of registered users, differentiation between users and admins, creation of "Jobs" with necessary details, adding users to those jobs with an instance of "Schedule" for each user on each job.

The secondary components include a Chat feature (for all users to have a single main chat room for discussion) and Company News (where admins can create announcements for all employees to read).

#### List of Technologies Used:
- C# ASP.Net MVC
- HTML, CSS, JavaScript
- Azure DevOps
- Visual Studio 2017
- Git and Team Foundation Server
- Entity Framework 6
- Bootstrap 4
- Slack and Google Meet for communications




## User Story 1: Personal Photo Refator
[]()

#### What is the issue?
This user story required making the PersonalProfilesController and its view responsible for uploading profile pictures for personal profiles. It also required adding full CRUD capabilities for profile pictures.

#### How is the issue resolved?
The feature to upload profile pictures was previously handled by the ManageController and it was accessing the ProfilePicture property from the User model. I deleted the ProfilePicture property from the User model and added it to the PersonalProfile model instead. Inside PersonalProfilesController I added logic for CRUD functionality.

###### ProfilePicture property inside PersonalProfile model
```c#
public byte[] ProfilePicture { get; set; }
```

I took the logic for uploading a profile picture from the ManageController and transfered it to PersonalProfilesController and made some adjustments to make it work for the views that needed access to it.

###### Code snippet of PersonalProfilesController dealing with profile picture and CRUD
()[]

I updated all the view files that dealt with the profile picture since PersonalProfilesController was now in charge of that logic.

###### Access to profile picture (or default picture for users without profile pictures)
```cshtml
<img id="ProfileImg" src="@Url.Action("Photo", "PersonalProfiles" , new { UserId=User.Identity.GetUserId() })" height="48" width="48" />
```

###### Link to upload profile picture
```cshtml
@Html.ActionLink("Upload your profile image here", "ProfilePicture", "PersonalProfiles")
```

###### Links to update, see details, and delete for profile picture
```cshtml
@Html.ActionLink("Update", "ProfilePicture", "PersonalProfiles") |
@Html.ActionLink("Details", "Details", new { id = Model.ProfileID }) |
@Html.ActionLink("Delete", "DeleteProfilePicture", new { id = Model.ProfileID })
```

###### Logic to upload profile picture via POST
```cshtml
@using (Html.BeginForm("ProfilePicture", "PersonalProfiles", FormMethod.Post, new { enctype = "multipart/form-data" }))
```
	
###### Logic for profile picture delete confirmation via POST
```cshtml
@using (Html.BeginForm("DeleteProfilePicture", "PersonalProfiles", FormMethod.Post))
```

#### What is the result?
The result is a fully functioning CRUD feature for profile pictures that is now being handled by PersonalProfilesController and its views.

###### PersonalProfiles/Edit view showing default profile picture (for users who has not uploaded their own profile picture) and the update, details, and delete features.
[]()
	
###### PersonalProfiles/ProfilePicture view for uploading profile picture
[]()

###### PersonalProfiles/Details view (I uploaded a new profile picture)
[]()

###### PersonalProfiles/DeleteProfilePicture view for delete confirmation
