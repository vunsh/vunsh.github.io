# Week 0

## College Board Notes, 5.1 - 5.6
### 5.1
Beneficial and Harmful effects of **computer innovation**

_Pros_
* Innovation in technology leads to other branches of tech utilizing such technology. Iphones and Wiis used accelerometers from the automobile industry to enhance their product. 
* Computer innovation is used to enhance human lives, including health and safety. New quadcopter technology allows first responders to search for stranded people a lot easier.
* Video game technologies like VR can get people up and moving while playing video games.

_Cons_
* Players of active video games can get injured easily. Excessive use of video games can hurt eyes
* Quadcopters often fly in unregulated zones, which is illegal and dangerous. It can also be a breach of privacy.

## College Board Notes, 5.5 - 5.6
### 5.5
Legal and ethical concerns

* In a modern coding world, students and engineers alike use open source code on the internet to build their own projects. Most code is licensed, which means proper legal proceedings need to occur depending on the use of that code.
* There are software and companies like Qualcomm that make and sell licensing rights to make the process of using open source code easy. These companies make money off of this unique business model.
* Every time open source code is used and published income for the companies that own such code changes depending on the license.
* It is also important to have ethical concerns in mind. When taking someone else's code it is important to understand where it comes from and how the author intended for it to be used.
* If code is used unethically, legal issues can also become relevant, thus tying the licensing and patents to ethical concerns.
* To combat code being taken that belongs to you, it is important to license your repository on GitHub.

For my project, I have chosen The Unlicense. This license has no conditions and is free for commercial use, modification, private use, etc. I chose this option because this is an educational project in which I plan to make no money out of. As a public repository, the code is public for anyone to use and make programs off of if they choose to. 

### 5.6
Safe Computing

* Safe computing is an extremely important practice that evolves in form as technology develops
* In a modern day technological world, safe computing is very easy with software and Multi-Factor authentication
* When making a website that accesses personal information, it is crucial to keep in mind privacy concerns for the user. You must differentiate the data you choose to display on the site to ensure the user's privacy.
* An example of a modern day software for safe computing is biometrics in phones. Many phones are switching to touch and face ID for unlocking and accessing secure information.
* Physical technologies like locks are starting to have biometrics as well.
* Most financial systems such as crypto block chains require multi authentication to access personal information. Even social medias are giving the option to enable multi authentication if wanted.
* As a developer, it is important to offer these security options to users. User security is more than just protecting data, its a level of trust the company strengthens with its user.
* The more faith a user has in an application, the more likely they are to use such application.
* An example of encryption being used in PBL projects are unique API keys required to access data. This can also be applied to encryption keys needed to access database values.

# Create Task
## Plan
StudyBot - Learning brought to Discord.

Setup Discord Application Instance.

Setup Github Repository.

Create handler to make commands and handle events in an organized manner.

Create command interface in StudyBot.

Setup MongoDB database for communication between bot and website.

Include ability to alter database on the website.

## Purpose
The purpose of Studybot is to bring learning to students on Discord, an extremely popular social media platform. Discord has an extensive API and developer tools that allow for bots and applications to be made that can directly interact with Discord and its users. Studybot has many features that enhance the learning experience of users while they browse Discord. You are able to schedule reminders and view them right on the application, and get notifications when your reminders occur. In addition, you are able to play music by either searching for a song through Discord or supplying a YouTube video link. This allows users to collaborate with peers in voice channels while also listening to music with them. Studybot also has the capability to play audio tracks such as podcasts or study guides, adding another way to study while on Discord. It is an extremely user friendly bot that is a fun addition to any Discord server.

In the video (attatched in the video section) of Studybot in use, its invite link on the PBL website is displayed. Upon clicking the invite button, you are sent directly to Discord's invite api and through there you can invite the bot. The video showcases Studybot's music functionality and the reminders. It quickly goes over how a database is used for reminders as well. To make the bot peform tasks, users send a message in a channel with the bot prefix, which is "s!". They can then use different commands to interact with the bot, and the bot responds. For example, s!play relaxing music will make Studybot search up "relaxing music" on youtube and play the first result in a voice channel.

## Code Examples
Lists are frequently used in Studybot, and are vital to its performance. Below is an example list taken straight from an SQL database entry for a reminder.


![image](https://user-images.githubusercontent.com/77084624/156261494-f739ce3e-43e3-4582-8b78-61b3300af49d.png)


As shown, this list has keys that represent different data that is important to this specific reminder. This data is used when a user views active reminders using s!reminders. Time represents how many minutes the reminder was scheduled for, current represents the date timestamp object of when the reminder was created, and reminder represents the actual task the user supplied to be reminded for. After a user's reminder is done, Studybot deletes the entries in the database for that reminder, leaving an empty list.

Another example of a list being used is through the music functionality of Studybot. 
![image](https://user-images.githubusercontent.com/77084624/156262087-8493b696-4fd9-4131-be7e-4bb70bc3020a.png)
This code shows how the list "queries" is altered depending on inputs from the user. Queries represents the song query that will be played by the bot. When a user tries to play another song while an active song is already playing, the requested song is pushed to the list "queries". After the current song is over, the bot will automatically move to the next item in the list "queries" and play that song. This process can be done an infinite amount of times until the user leaves the channel or stops the music. The query system is vital to music as it allows for users to request songs to play beforehand rather than at that present moment. If the list is empty, the music() function is called which plays the song the user provided.

Procedures, or functions are an important part of the music functionality in Studybot
![image](https://user-images.githubusercontent.com/77084624/156262613-7226f7ef-ad41-4c69-8ff2-84a1014b0810.png)
This music function shows the behind the scenes process that actually plays the music for the user. It passes in the query the user provides for the function argument and first runs a function to search the query on youtube with yts, an api. After verifying there is a voice channel to join for the bot to play music, it uses the response from the yts function to supply the video id of the first result into a link. Another api, ytdl, then takes in the link to the video and plays it in the voice channel. Lastly, the bot makes sure that the list "queries" has the right values by pushing the current playing song off the list and moving each item up 1 spot.

The music function only makes a ytdl api call initially if the list queries is empty. It first checks for items in the list, and if there is none it plays the song directly by passing the user query into music(). However, if queries is not empty the function takes a different route. Instead of searching for the song with the api and playing it, which would interrupt the current song, it passes the query into the list and stores it. Once the song currently playing's duration has passed, music() is called on the first value in the list queries. 

The result of the first call with no values in "queries" is a direct playing of the supplied song. The result of the second call while another song is currently playing is the alteration of "queries" by adding the supplied song to the end of the list. After the duration of the current song, the music function is then called on the next item in queries.

## Video
https://drive.google.com/file/d/1d1HkROOBFQTdc_VvAPCG3pWgQNsxGq4d/view?usp=sharing 
