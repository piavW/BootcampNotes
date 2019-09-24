
## About the Legacy Code Challenge
Learn about Ruby on Rails through testing, using Pry.

In the legacy code there are bugs, some parts are broken.

We're supposed to document all aspects of the application in the README-file! Also fill the code with written acceptance tests for the entire workflow, use unittests with RSpec, fix the broken stuff. 

I need to have grasp about what my pair-programmer is doing. 

**HINTs:**
- there is a Dot after signed in successfully and signes out successfully!!! 
- one userstory = 1 feature test & rspectest = 1 pull request.

To do first
- Go through the application and write userstories for the different part of the application!

The user stories will be what we base our featuretests on. 

Store the userstories in the pivotaltracker.com - we need to sign up individually to the application. 
    - In icebox -click on add story title, story description (user story - as a visitor, in or der to send messages, i would like to log in to the mailboxer app), 
    - add a task - write feature test 
        (don't need to have unittest since we're not saving any information!)
    Can also add a comment like - please remember to add a background because the user already exists. 

Add all the userstories for the applicatin. 
Drag the chosen story that you're working on over the the current iteration/backlog. Work on  max 4 stories at the same time. 

Only use the pivotaltracker.com for starting to store user stories, assign people to the user stories, add 0 points. 


The AUT cycle and RPS are for the evenings! Only work on legacycode during school-hours. 
---

# Team 2: Pia, Alex, Jonas, Luca, Miyesier, Sverrir. 

Issues in the legacy code:

- conversation sent to trash also shows up in inbox if someone replies to it. 
- replies to a trashed message doesn't affect inbox counter
- replies to a trashed message are also shown in trash
- replies to a trashed message shows up in sent as the full conversation. 
- in inbox it doesn't show the name of the sender, but it shows if we press the "view". 
- We have both errormessages and alertboxes - CHOOSE ONE!
- when getting a url it's not a hyperlink...
- the application is a chat but they call it mailboxer with inbox etc. 
---