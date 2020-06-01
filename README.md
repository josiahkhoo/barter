

# Barter

**![photo_2020-06-01 21.35.39](https://i.ibb.co/JzJXh6r/photo-2020-06-01-21-35-39.png)**

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

- As a user, I want to be able to set timers for my tasks and fight monsters
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
2. Drop system
   - Bosses will randomly drop equipments (will tweak this) (Percentage based drop)

##### Features to be completed by the mid of July:

1. Leaderboard system
   - Players are able to see where they stand in terms of how much bosses they have slain
2. Chat feature
   - Player are able to communicate and send messages to each other in game

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

### Program Flow

![program_flowchart](https://i.ibb.co/qjgN7Py/barter-high-level-diagram-2.png)

### Class Diagram (WIP)

![class_diagram](https://i.ibb.co/wMz3SKw/barter-class-diagram-1.png)

### Mockups

![mockup](https://i.ibb.co/KyQBPdd/photo-2020-06-01-21-36-06.jpg)

## **Tech Stack** (for now)

1. **Unity**
2. **Django**
3. **React Native**
4. **Postgresql**
5. C#
6. React (Landing site)

## **Project Log**

| S/N  | Task                              | Date      | Josiah (hrs) | Yu Ming (hrs) | Remarks                                                      |
| ---- | --------------------------------- | --------- | ------------ | :------------ | :----------------------------------------------------------- |
| 1    | Meeting with Advisor Bang Jie     | 13/5/2020 | 1            | 1             | Consulted Bang Jie on the feasibility of doing a trading application and realising that it is probably not the wisest thing to do. |
| 2    | Brainstorming for new ideas       | 14/5/2020 | 2            | 2             | Pivoted and stuck on an idea of a gamified productivity application. |
| 3    | Project Consultation 1            | 16/5/2020 | 2            | 2             | Consulted Kai Jun on the feasibility of our gamified application and settled on our core features. |
| 4    | Discussion on which Assets to use | 19/5/2020 | 2            | 2             | Looked through the Unity market together and figuring out which assets to get. |
| 5    | Learning to use Unity             | 20/5/2020 | 3            | 3             | Watched youtube tutorials to get a hang of how GameScenes in Unity works and how C# scripts hooks to the components and links with other objects. |
| 6    | Project Consultation 2            | 23/5/2020 | 2            | 2             | Got a second opinion from Ryan, who has gaming development experience who guided us on how to structure our program flow and which features to focus on first.<br /><br />Ryan suggested the use of OOP to design our program and also to first implement our single player features and getting our core application to work before moving on to the multiplayer features. |
| 7    | Learning to use Unity Teams       | 25/5/2020 | 2            | 2             | Managed to share Assets and Game Scenes with each other using Unity sharing features. |
| 8    | Building Mockups                  | 27/5/2020 | 4            | 4             | Used Figma to create mockups for Barter                      |
| 9    | Login Scene                       | 28/5/2020 | 2            | 2             | Built LoginScene without attaching logic.                    |
| 10   | Character Creation Scene          | 29/5/2020 | 2            | 2             | Built CharacterCreationScene without attaching logic.        |
| 11   | Battle Scene                      | 30/5/2020 | 2            | 2             | Built BattleScene without attaching logic.                   |
| 12   | Class Diagrams and Component Flow | 31/5/2020 | 4            | 4             | Used draw.io to create class diagrams and component flow for Barter. |

