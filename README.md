

# Barter

**![photo_2020-06-01 21.35.39](https://i.ibb.co/JzJXh6r/photo-2020-06-01-21-35-39.png)**

## Milestone 2 

![Poster](https://i.ibb.co/SVJpXdv/poster.jpg)

### Features

Up to this point, we have implemented the core functionalities of the game which includes:

1. Creating of accounts and being able to log in.
2. Creating of characters and editing the characters apperance.
3. Being able to select which monster to battle in the quest page.
4. Timed boss fight and clearing the mission.
5. Integration with backend for saving and retrieving of data.

### Prototype

[Link To Prototype](https://streamable.com/e/0vwlb5)

### Tests

- Unit Testing on the backend
  -  Ensure that objects are able to be created properly and stored in the database in the backend
- Self Testing
  - We tested the flow from scene to ensure that everything is integrated properly and that there are no wild bugs
- Usability Testing with friends
  - We showed some of our friends the prototype video of our application to see if it made sense, some feedback that we got was:
    1. Show the duration of the boss fight in the boss select scene
    2. UI of the Create Character Page needs to be optimised for mobile (especially the dropdown)

### Program Flow

![program_flowchart](https://i.ibb.co/qjgN7Py/barter-high-level-diagram-2.png)

### Class Diagram

![class_diagram](https://i.ibb.co/wMz3SKw/barter-class-diagram-1.png)

### Features for Milestone 3

1. Drop system
   1. Bosses will randomly drop equipments (will tweak this) (Percentage based drop)

2. Chat feature
   1. Player are able to communicate and send messages to each other in game
3. Achievement system
   1. Instead of promoting unnecessary competition, we have chosen to implement an achievement system instead to reward players.
4. Different timings for bosses
   1. Allows for flexibility in terms of tasks for players.

## **Proposed Level of Achievement:**

Artemis

## **Motivation**

Students for some reason, have a strong tendency to get themselves addicted to new games right before exams, when they are supposed to be studying (unsubstantiated fact but from real life examples). What if we could create a game for these students to play, and also keep them productive at the same time? Even better, we can introduce network effects when we allow people to team up in game to complete tasks togethers.

We understand that there are applications that gamify productivity such as Forest, where you grow trees when you leave your phone alone, as well as Habitica, a gamified task manager where you “level up” upon clearing tasks, these apps however lack the sense of immersion that games bring about and does not satisfy the strong urge to game and to be productive at the same time.

## **Aim**

We hope to build a **multiplayer game** where users can choose to **battle monsters alone** or **with friends**.

1. Nostalgic and relatable art style
2. Revolves around the concept of battles. One battle is 60 minutes and will allow a player to take out 1 boss
3. Players are rewarded upon finishing battles
4. Players can join parties to battle bosses together

## **User Stories**

- As a user, I want to be able to set **different** timers for my tasks and fight monsters
- As a user, I want to be able to synchronise my data across devices
- As a user, I want to be able to be rewarded when fighting bosses
- As a user, I want to be able to invite my friends and play with them

## **Features and Timeline**

### Features:

1. Time-based battle (60mins) where each task is represented in a monster
2. Multiplayer battle where everyone contributes to fighting a monster. (If one person leaves, everyone dies)
3. Level System
4. Leaderboard system
5. Guild system
6. Achievement system
7. Cosmetic drops from killing monsters (Collection based)

### Timeline:

##### Features to be completed by the mid of June:

1. Time-based battle
   - Simple UI where the user is brought into an animated boss battle
2. Authentication and accounts
   - Users will be able to log into their accounts and data is persisted online

##### Features to be completed by the mid of July:

1. Drop system
   1. Bosses will randomly drop equipments (will tweak this) (Percentage based drop)

2. Chat feature
   1. Player are able to communicate and send messages to each other in game
3. ~~Leaderboard~~ Achievement system
   1. Instead of promoting unnecessary competition, we have chosen to implement an achievement system instead to reward players.
4. Different timings for bosses
   1. Allows for flexibility in terms of tasks for players.

##### Features to be completed by the mid of Aug:

1. Multiplayer system

2. Players can take part in party battles (Design in the same style as guild)
   2. Synchronized players
   3. Guild system
      - Players can be part of guilds where they can monitor each other’s progress as well as communicate in game channel
   4. Achievement System
      - Upon completion of different tasks, users will be able to unlock achievements which gives them cosmetic rewards 

2. Landing site
   - For SEO and attracting users to download the application

## **Tech Stack** (for now)

1. **Unity**
2. **Django**
3. **React Native**
4. **Postgresql**
5. C#
6. React (Landing site)

## **Project Log**

| S/N  | Task                                                | Date      | Josiah (hrs) | Yu Ming (hrs) | Remarks                                                      |
| ---- | --------------------------------------------------- | --------- | ------------ | :------------ | :----------------------------------------------------------- |
| 1    | Meeting with Advisor Bang Jie                       | 13/5/2020 | 1            | 1             | Consulted Bang Jie on the feasibility of doing a trading application and realising that it is probably not the wisest thing to do. |
| 2    | Brainstorming for new ideas                         | 14/5/2020 | 2            | 2             | Pivoted and stuck on an idea of a gamified productivity application. |
| 3    | Project Consultation 1                              | 16/5/2020 | 2            | 2             | Consulted Kai Jun on the feasibility of our gamified application and settled on our core features. |
| 4    | Discussion on which Assets to use                   | 19/5/2020 | 2            | 2             | Looked through the Unity market together and figuring out which assets to get. |
| 5    | Learning to use Unity                               | 20/5/2020 | 3            | 3             | Watched youtube tutorials to get a hang of how GameScenes in Unity works and how C# scripts hooks to the components and links with other objects. |
| 6    | Project Consultation 2                              | 23/5/2020 | 2            | 2             | Got a second opinion from Ryan, who has gaming development experience who guided us on how to structure our program flow and which features to focus on first.<br /><br />Ryan suggested the use of OOP to design our program and also to first implement our single player features and getting our core application to work before moving on to the multiplayer features. |
| 7    | Learning to use Unity Teams                         | 25/5/2020 | 2            | 2             | Managed to share Assets and Game Scenes with each other using Unity sharing features. |
| 8    | Building Mockups                                    | 27/5/2020 | 4            | 4             | Used Figma to create mockups for Barter                      |
| 9    | Login Scene                                         | 28/5/2020 | 2            | 2             | Built LoginScene without attaching logic.                    |
| 10   | Character Creation Scene                            | 29/5/2020 | 2            | 2             | Built CharacterCreationScene without attaching logic.        |
| 11   | Battle Scene                                        | 30/5/2020 | 2            | 2             | Built BattleScene without attaching logic.                   |
| 12   | Class Diagrams and Component Flow                   | 31/5/2020 | 4            | 4             | Used draw.io to create class diagrams and component flow for Barter. |
| 13   | Created User models                                 | 2/6/2020  | 5            | 5             | Created User models in Django backend with JWT Authentication. |
| 14   | Hooked Login with User APIs                         | 4/6/2020  | 5            | 5             | Connected Login Scene and Signup Scene with User APIs        |
| 15   | Created Character models                            | 9/6/2020  | 5            | 5             | Created Character models in Django backend that links to each User |
| 16   | Hooked Select Character with Character APIs         | 11/6/2020 | 5            | 5             | Connected Character Select Scene and Character Create Scene with Character APIs |
| 17   | Creating Storage class in Unity                     | 16/6/2020 | 3            | 3             | Created a Storage class that allows us to pass data from one scene to another |
| 18   | Figuring out how to use prefabs in Unity            | 18/6/2020 | 3            | 3             | Figured out the use of Prefabs especially in Dynamic UIs, integrated into  Select Character Scene |
| 19   | Created Monster models                              | 23/6/2020 | 4            | 4             | Created Monster models in Django backend                     |
| 20   | Hooked Quests with Monster APIs                     | 25/6/2020 | 3            | 3             | Connected Quest with Monster APIs as well as used prefabs to populate the list. |
| 21   | Making Character Objects load from apperance config | 26/6/2020 | 3            | 3             | Figured out how to store the character's appearance in a Json config and reloading it each time the scene is rendered. |

