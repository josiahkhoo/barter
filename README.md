

# Barter

![barter-poster](https://i.imgur.com/SFdewwH.png)

- [Barter](#barter)
  * [Milestone 3](#milestone-3)
    + [Features and Deliverables](#features-and-deliverables)
  * [Prototype](#prototype)
  * [Architecture and Technologies](#architecture-and-technologies)
    + [Architecture](#architecture)
    + [Backend Services](#backend-services)
    + [Database Schema](#database-schema)
  * [Tests](#tests)
    + [Integration Tests](#integration-tests)
    + [Unit Tests](#unit-tests)
    + [Usability Testing with friends](#usability-testing-with-friends)
  * [User Experience](#user-experience)
  * [Program Flow](#program-flow)
  * [Proposed Level of Achievement](#proposed-level-of-achievement)
  * [Motivation](#motivation)
  * [Aim](#aim)
  * [User Stories](#user-stories)
  * [Timeline](#timeline)
    + [Features](#features)
    + [Timeline](#timeline)
        * [Features to be completed by the mid of June](#features-to-be-completed-by-the-mid-of-june)
        * [Features to be completed by the mid of July](#features-to-be-completed-by-the-mid-of-july)
        * [Features to be completed by the mid of Aug](#features-to-be-completed-by-the-mid-of-aug)
  * [Tech Stack](#tech-stack)
  * [Project Log](#project-log)


## Milestone 3

![Poster](https://i.imgur.com/UD2H1Ey.jpg)

### Features and Deliverables

In our previous milestone, we have implemented the core functionalities of the game, which includes:

1. Creating of accounts and being able to log in.
2. Creating of characters and editing the characters apperance.
3. Being able to select which monster to battle in the quest page.
4. Timed boss fight and clearing the mission.
5. Integration with backend for saving and retrieving of data.

In Milestone 3, we have added the features that we set out to do and implemented multiplayer functionalities properly:

1. **Equipment System**
   1. Users are able to earn and equip items from boss fights. 
   2. These equipments are collectible and can be equipped, customized and seen when battling others
   3. We have four different types of equipments that a character can equip, helmet, armour, shield and sword.
2. **Drop System**
   1. Bosses will randomly drop equipments after each fight.
   2. The quality of the equipment increases based on the boss difficulty (how long the battle is) and how many players are required to take down the boss.
3. **Friend System**
   1. Players are now able to add each other as friends in game by entering their username.
   2. Edges are used to connect friends. If there is a bidirectional edge between two users, there are considered as friends. If it is a directional edge between two users, it is represented as a friend request.
   3. We would want to implement a feature where you can invite your friends straight into your party in the future.
4. **Chat Feature**
   1. Players are able to communicate and send messages to each other in game.
   2. This is achieved through polling the backend for updates.
   3. We initially wanted to use Firebase to do this, but the Firebase package was not working well on Unity for us. We want to eventually improve this by using websockets in the future.
5. **Achievement system**
   1. Instead of promoting unnecessary competition, we have chosen to implement an achievement system instead to reward players.
   2. For now, the achievements only display the users records including: total battles, battles won, total productive time.
6. **Different timings for bosses**
   1. Allows for flexibility in terms of tasks for players.
   2. There was an initial feedback that it was too rigid if we set everything as thirty minutes. We contemplated making it adjustable so that users could choose how much time they would want to spend. However, we decided on creating different bosses with different timings instead, so as to provide the flexibility as well as support our boss difficulty systems.
7. **Party Feature**
   1. Players form parties before fighting multiplayer battles. This helps to promote collaboration and healthy peer support.
   2. This is acheived through polling the backend for updates and using Redis as a key-value store for faster read and writes (about 10x faster than PostgreSQL)

## Prototype

[Link To Prototype](https://josiahkhoo.github.io/barter-web/)

Please run the prototype in a browser that supports WebGL. As Character Creation is broken on WebGL, we have created a few dummy accounts for you to test our features out. The scaling might be abit whack so please zoom out until your screen and login page looks like this for the most optimal gaming experience :-) (for us its around 50% zoomed out)

![optimal-chrome](https://i.imgur.com/sExoH2K.png)

**Beta Accounts Information**

```
username: beta1
password: Barter123
chara1: Beta1_one
chara2: Beta1_two

username: beta2
password: Barter123
chara1: Beta2_one
chara2: Beta2_two

username: beta3
password: Barter123
chara1: Beta3_one
chara2: Beta3_two
```



## Architecture and Technologies

[Link to barter-unity repo](https://github.com/josiahkhoo/barter-unity)

[Link to barter-django repo](https://github.com/josiahkhoo/barter-django)

### Architecture

![app_architecture](https://i.imgur.com/7Xg8ViT.png)

Barter is built using several technologies:

1. **Frontend: Unity and GitHub Pages**
   1. We used Unity because it allowed for cross platform deployment, including mobile for our core application and web for rapid prototyping and showing to users.
   2. GitHub pages was used to host our WebGL application so that users can give feedback and test our application
2. **Backend: Django, PostgreSQL and Redis**
   1. We used Django and PostgreSQL as our backend server and database respectively because it allowed for writing views and creating models easily and systematically, saving us development time. Make queries is easy as well and it helped to manage the connection to the database. We were also able to write an Auth service easily and use JWT for user verification.
   2. Redis was used as our cache because it had fast read-write times compared to PostgreSQL and helped to speed up API calls.
3. **Services: AWS and Digital Ocean**
   1. We used Digital Ocean because we were able to deploy a PaaS as a docker image on a container hosted in Singapore for an affordable cost ($5/month), allowing faster network transactions. We hosted our backend and redis on this docker image.
   2. We used AWS RDS to hold our database for now because it was free :'-) and it helped to manage our database for us, saving maintanence time.

### Backend Services

![backend_image](https://i.imgur.com/QVDElVT.png)

Our backend is futher broken down into multiple services, which is routed during API calls.

1. **User and Auth Service**
   1. Implemented JWT authentication
   2. Django uses the [PBKDF2](https://en.wikipedia.org/wiki/PBKDF2) algorithm with a SHA256 hash to store passwords
   3. Friend requests and logic are also processed in this layer
2. **Character Service**
   1. Creating characters and storing of character appearances in json.
3. **Party Service**
   1. Uses UUID to generate 6 digit alphanumeric party codes, with up to two billion combinations, handles for collisions as well.
   2. Uses Redis to store Party information and for polling.
4. **Monster Service**
   1. Stores the different monsters that we have.
   2. Links monsters with equipment dropset.
5. **Battle Service**
   1. Used to create a battle object in our database for tracking when someone enters a fight.
   2. When the battle is completed, a request is made to complete the battle and generate equipment dropped by the monster.
6. **Chat Service**
   1. Allows for polling and creates a chat object whenever a party is instantiated or when two characters becomes friends.
7. **Inventory Service**
   1. Allows for creation of inventory from battle objects (each item generated is tagged a battle, something like an entity tag)

### Database Schema

![class_diagram](https://i.ibb.co/wMz3SKw/barter-class-diagram-1.png)

## Tests

### Integration Tests

- Integration Tests - User
  - Able to login with username and password
  - Able to create an account with username, password and email
  - Able to stop users from creating accounts with a username or email that is already in used
  - Able to stop users from creatings accounts with weak passwords (done on client side)
- Integration Tests - Character
  - Shows all characters under the user
  - Able to create character with a randomly chosen apperance (Not working for WebGL)
  - Able to equip items that are owned by the character and updating the json apperance config
  - Able to get achievements from the individual character level
- Integration Tests - Party
  - Able to create party from a chosen boss fight
  - Able to join via a 6 digit access-code
  - Able to show new characters who have joined the party
  - Able to add a ready flag to characters who are ready
  - Able to transit to Battle Page when everyone in the party is ready
  - Able to remove characters who have left the party
- Integration Tests - Monster
  - Able to render list of monsters to battle (singleplayer and multiplayer)
  - Able to render items that the monster drops
  - Able to render party size required for multiplayer monsters
  - Able to render duration required for multiplayer monsters
- Integration Tests - Battle
  - Able to create a battle object when fighting a monster
  - Able to render the boss tagged to the Battle
  - Able to set the time of the fight based on the bosses' time attribute
  - Able to end a battle and generate equipment
  - Able to leave a battle midway and check that battle was not completed
- Integration Tests - Chat
  - Able to receive updates when another user sends a message
  - Able to see an update when current user sends a message
  - Able to see messages another user sends when current user is offline
  - Able to send messages to other user when other user us offline
- Integration Tests - Inventory
  - Able to filter inventory based on chosen weapon type
  - Able to equip item from inventory and update the character
  - Able to see new equipments when a battle is complete and an equipment is dropped

### Unit Tests

- Unit Tests - User
  - _authenticate_credentials: Tries to authenticate the given credentials. If authentication is
    successful, return the user and token. If not, throw an error.
  - create_user: Tries to create user. If username or email exists, throw an error.
  - add_friend: Tries to add friend by username. If username does not exist, throw an error.
- Unit Tests - Character
  - equip_equipment: Tries to equip an equipment. If character does not have an equipment, throw error.
- Unit Tests - Party
  - join_party: Tries to join a party with access code. If no party with that access code, throw an error.
  - poll: Update party with your current ready state, if party is all ready and party size meets boss required party size, highlight that the party is ready.
- Unit Tests - Monster
  - get_drop: Randomly generates a drop item based on its equipment set.
- Unit Tests - Battle
  - set_state_complete: Tries to complete the battle. If the battle is already complete, throw an error.

### Usability Testing with friends

- Showed friends the UI mockup to see what features they would like to see and what things need to be changed.
- Showed friends the working prototype to see what their feedback on it was, whether there were any weird glitches or any UI that needs to be change. They used the beta account to try our single player battles, party battles, chats and all the other functions. Helped us to spot a few bugs and fix them.

## User Experience

![all_pages](https://i.imgur.com/mBTr3sx.png)

[Link To Figma File](https://www.figma.com/file/zAajSFuggmIjo1JBQ5YMcV/Barter?node-id=1%3A104)

We had a total of 22 pages by the end of Milestone 3. We took into consideration several factors when designing our interfaces:

1. Simplicity and functionality
   1. "The best interfaces are almost invisible to the user. They avoid unnecessary elements and are clear in the language they use on labels and in messaging."
      We tried to keep to having less than 5 buttons on 1 screen to make it simple and easy for the user to digest information.
   2. Common UI elements like the + button were used to help the user understand instantly what the button can do.
   3. Where more complicated UI elements were required, we labelled it with text to allow the user to know what it is for.
   4. Fonts used are very cartoonish in nature to drive the point that it is a game home and to make text visible for users as well.
   5. Links between scenes are clear with their functions. This is designed in a way so that there will be minimum scenes with no additional scenes that will add additional complexity to the game and confuse the user.
2. Nostalgia
   1. We chose to use 2D UI elements for our games that had a strong rustic platformer game theme because it allows the user to relate easily to the entire gamified premise of the productivity application upon opening the application.
   2. Our character and boss design is also similar to popular 2D MMORPG games like MapleStory for the same reason as well.
3. Colours
   1. Colours such as dark brown was chosen to bring the player back to the ancient land and additional colour contrast are used to further enhance the meaning of of various aspect of the game. eg. better equipments have golden rings as compare to lower tier equipment drops. Simple colour toggle between green "Ready" button and reddish brown "Unready" button.

## Program Flow

![program_flowchart](https://i.imgur.com/K7xJbRl.png)

[Link To Figma File](https://www.figma.com/file/zAajSFuggmIjo1JBQ5YMcV/Barter?node-id=1%3A104)

To view this at a higher resolution and see how everything flows, please view our Figma file above.

## Proposed Level of Achievement

Artemis

## Motivation

Students for some reason, have a strong tendency to get themselves addicted to new games right before exams, when they are supposed to be studying (unsubstantiated fact but from real life examples). What if we could create a game for these students to play, and also keep them productive at the same time? Even better, we can introduce network effects when we allow people to team up in game to complete tasks togethers.

We understand that there are applications that gamify productivity such as Forest, where you grow trees when you leave your phone alone, as well as Habitica, a gamified task manager where you collect equipment upon clearing tasks, these apps however lack the sense of immersion that games bring about and does not satisfy the strong urge to game and to be productive at the same time.

## Aim

We hope to build a **multiplayer game** where users can choose to **battle monsters alone** or **with friends**.

1. Nostalgic and relatable art style
2. Revolves around the concept of battles. One battle is x minutes and will allow a player to take out 1 boss
3. Players are rewarded upon finishing battles
4. Players can join parties to battle bosses together

## User Stories

- As a user, I want to be able to set **different** timers for my tasks and fight monsters
- As a user, I want to be able to synchronise my data across devices
- As a user, I want to be able to be rewarded when fighting bosses
- As a user, I want to be able to invite my friends and play with them

## Timeline

### Features

1. Time-based battle (60mins) where each task is represented in a monster
2. Multiplayer battle where everyone contributes to fighting a monster. (If one person leaves, everyone dies)
4. Leaderboard system
6. Achievement system
7. Cosmetic drops from killing monsters (Collection based)
6. Friend system
7. Equipment system

### Timeline

##### Features to be completed by the mid of June

1. Time-based battle
   - Simple UI where the user is brought into an animated boss battle
2. Authentication and accounts
   - Users will be able to log into their accounts and data is persisted online

##### Features to be completed by the mid of July

1. Drop system
   1. Bosses will randomly drop equipments (will tweak this) (Percentage based drop)

2. Chat feature
   1. Player are able to communicate and send messages to each other in game
3. ~~Leaderboard~~ Achievement system
   1. Instead of promoting unnecessary competition, we have chosen to implement an achievement system instead to reward players.
4. Different timings for bosses
   1. Allows for flexibility in terms of tasks for players.

##### Features to be completed by the mid of Aug

1. Multiplayer system

2. Players can take part in party battles
   2. Synchronized players
   4. Achievement System
      - Upon completion of different tasks, users will be able to unlock achievements which gives them cosmetic rewards 


## Tech Stack

1. **Unity**
2. **Django**
3. **React Native**
4. **Postgresql**
5. C#

## Project Log

| S/N  | Task                                                  | Date      | Josiah (hrs) | Yu Ming (hrs) | Remarks                                                      |
| ---- | ----------------------------------------------------- | --------- | ------------ | :------------ | :----------------------------------------------------------- |
| 1    | Meeting with Advisor Bang Jie                         | 13/5/2020 | 1            | 1             | Consulted Bang Jie on the feasibility of doing a trading application and realising that it is probably not the wisest thing to do. |
| 2    | Brainstorming for new ideas                           | 14/5/2020 | 2            | 2             | Pivoted and stuck on an idea of a gamified productivity application. |
| 3    | Project Consultation 1                                | 16/5/2020 | 2            | 2             | Consulted Kai Jun on the feasibility of our gamified application and settled on our core features. |
| 4    | Discussion on which Assets to use                     | 19/5/2020 | 2            | 2             | Looked through the Unity market together and figuring out which assets to get. |
| 5    | Learning to use Unity                                 | 20/5/2020 | 3            | 3             | Watched youtube tutorials to get a hang of how GameScenes in Unity works and how C# scripts hooks to the components and links with other objects. |
| 6    | Project Consultation 2                                | 23/5/2020 | 2            | 2             | Got a second opinion from Ryan, who has gaming development experience who guided us on how to structure our program flow and which features to focus on first.<br /><br />Ryan suggested the use of OOP to design our program and also to first implement our single player features and getting our core application to work before moving on to the multiplayer features. |
| 7    | Learning to use Unity Teams                           | 25/5/2020 | 2            | 2             | Managed to share Assets and Game Scenes with each other using Unity sharing features. |
| 8    | Building Mockups                                      | 27/5/2020 | 4            | 4             | Used Figma to create mockups for Barter                      |
| 9    | Login Scene                                           | 28/5/2020 | 2            | 2             | Built LoginScene without attaching logic.                    |
| 10   | Character Creation Scene                              | 29/5/2020 | 2            | 2             | Built CharacterCreationScene without attaching logic.        |
| 11   | Battle Scene                                          | 30/5/2020 | 2            | 2             | Built BattleScene without attaching logic.                   |
| 12   | Class Diagrams and Component Flow                     | 31/5/2020 | 4            | 4             | Used draw.io to create class diagrams and component flow for Barter. |
| 13   | Created User models                                   | 2/6/2020  | 5            | 5             | Created User models in Django backend with JWT Authentication. |
| 14   | Hooked Login with User APIs                           | 4/6/2020  | 5            | 5             | Connected Login Scene and Signup Scene with User APIs        |
| 15   | Created Character models                              | 9/6/2020  | 5            | 5             | Created Character models in Django backend that links to each User |
| 16   | Hooked Select Character with Character APIs           | 11/6/2020 | 5            | 5             | Connected Character Select Scene and Character Create Scene with Character APIs |
| 17   | Creating Storage class in Unity                       | 16/6/2020 | 3            | 3             | Created a Storage class that allows us to pass data from one scene to another |
| 18   | Figuring out how to use prefabs in Unity              | 18/6/2020 | 3            | 3             | Figured out the use of Prefabs especially in Dynamic UIs, integrated into  Select Character Scene |
| 19   | Created Monster models                                | 23/6/2020 | 4            | 4             | Created Monster models in Django backend                     |
| 20   | Hooked Quests with Monster APIs                       | 25/6/2020 | 3            | 3             | Connected Quest with Monster APIs as well as used prefabs to populate the list. |
| 21   | Making Character Objects load from apperance config   | 26/6/2020 | 3            | 3             | Figured out how to store the character's appearance in a Json config and reloading it each time the scene is rendered. |
| 22   | Created Chat models in the backend                    | 30/6/2020 | 5            | 5             | Created Chat models in Django backend and tested to see whether messages can be sent |
| 23   | Created Party models in the backend                   | 3/7/2020  | 4            | 4             | Created Party models in Django backend and tested to see whether we could join parties using different characters through APIs |
| 24   | Created Battle models in the backend                  | 5/7/2020  | 3            | 3             | Created Battle models in Django backend and tested to see whether we could complete the battle using APIs |
| 25   | Added Friend system                                   | 8/7/2020  | 5            | 5             | Created Friend models in Django backend and tested to see whether we could add friends using it |
| 26   | Created Friend List Page in Unity                     | 11/7/2020 | 3            | 3             | Created Friend list, add friend, view friend request, friend prefab and friend request prefab |
| 27   | Hooked Friends with Friends APIs                      | 14/7/2020 | 3            | 3             | Hooked the friends page to the backend APIs                  |
| 28   | Created Chat Page in Unity                            | 17/7/2020 | 3            | 3             | Created chat list, message prefab                            |
| 29   | Hooked Chat with Chat APIs                            | 20/7/2020 | 6            | 6             | Hooked the chat page to the backend APIs, including polling and sending messages and testing to make sure two different people can receive it, also realised spent an awful amount of time on Firebase to realise that it doesn't work for us... |
| 30   | Touched up UI                                         | 23/7/2020 | 5            | 5             | Got some feedback from friends, went to do some UI touch ups and making sure its more usable |
| 31   | Created Party Page in Unity                           | 24/7/2020 | 3            | 3             | Created party page, character list and character prefab.     |
| 32   | Hooked Party with Party APIs                          | 24/7/2020 | 4            | 4             | Connected the party page with Party APIs and made sure that it polls properly and transits to battle scene properly. |
| 33   | Created Inventory Page in Unity                       | 25/7/2020 | 3            | 3             | Created inventory page, equipment prefab (which was hard to do for us because an equipment was a sprite and we didn't really have experience with that) |
| 34   | Hooked Inventory with Equipment APIs                  | 25/7/2020 | 3            | 3             | Hooked inventory page with backend APIs and tested to see if equipments could be equipped and if the character reflected the change. |
| 35   | Created Rewards Page in Unity                         | 26/7/2020 | 3            | 3             | Created rewards page in and used the equipment prefab.       |
| 36   | Linked Rewards Page with Battle API                   | 26/7/2020 | 2            | 2             | Linked rewards with the completed battle object to render the won item. |
| 37   | Added Achievement View and Battle Logs API to backend | 26/7/2020 | 3            | 3             | Added achievement and battle logs APIs to backend that queried the characters battles and generated a summary log. |
| 38   | Created Achievements Page and Battle Logs Page        | 26/7/2020 | 3            | 3             | Created Achievement Page, Battle Logs Page, Achievement Prefab and Battle Log prefab. Also integrated it with the backend. |
| 39   | Deployment to GitHub pages                            | 27/7/2020 | 4            | 4             | Deployed to Github Pages and fixed all null references so that WebGL could work properly, still has some scaling issues because of the resolution that we built it at. |
| 40   | Documentation                                         | 27/7/2020 | 5            | 0             | Touched up the documentation for Milestone 3.                |
| 41   | Video                                                 | 27/7/2020 | 0            | 5             | Created a video to showcase Barter and its features.         |
|      | Total Hours                                           |           | 134          | 134           |                                                              |





