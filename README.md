# Unity-Coding-Guidelines

## Objective

The goal of this document is to set up a uniform coding style for all Unity developers in the team. You're welcome to pitch in ideas and contribute to shaping this document. We don’t expect everyone to write perfectly clean code, but this will be enforced via PR. 

## Naming Conventions
 
| Type | Convention | 
|----------|----------|
| Public Fields    | _camelCase ( class scope ), camelCase ( method scope ) |
| Private / Protected Fields   |  PascalCase |
| Constant | ALLCAPS_ALLCAPS |
| Interface | IDestroyable |
| Boolean | IsGameOver ( starts with an auxiliary verb ), _isGameOver |
| Event  | ButtonClickEvent ( Event suffix ) |
| Event Callback | OnButtonClicked ( On prefix ) / OnButtonClickedCallback  |
| Method | MethodNamePascalCase()  |



Read more : [ Unity Naming and Code Style Tips - Unity Technologies ](https://unity.com/how-to/naming-and-code-style-tips-c-scripting-unity#casing-terminology)

## Namespaces

When creating a new script, check if there is an existing namespace that matches it. If not, make a new one under your namespace. 
Use singular form for namespace extensions. 

Eg:

> ```csharp
> CompanyName.System  // Recommended
> CompanyName.Systems // Not recommended
> ```

## Style Guide 

Use Descriptive names
Avoid abbreviations. Use full, descriptive names rather than short forms.

> ```csharp
> public class AudioManager { ... } // Recommended
> public class AudMgr { ... } // Not recommended
> ```

## Reconsider public fields

Use properties instead to provide access to the fields.

> ```csharp
> private int _maxHealth; 
> public int MaxHealth { get { return _maxHealth; } }
> ```
 

## Use singular names for enums

Enum names should be singular, with members in PascalCase.


> ```csharp
> public enum GameState 
> {
>  Initializing, 
>  Playing, 
>  Paused, 
>  GameOver 
> }
> ```

Read more : [Writing Cleaner code that scales - Unity Technologies](https://resources.unity.com/games/create-code-style-guide-e-book?ungated=true)

## Code Documentation Style

Use XML documentation comments. Eg :

> ```csharp
> /// <summary> 
> /// Moves the player to a specified position. 
> /// </summary>
> public void MovePlayer()
> ```
 

You may use the following tags in addition to summary :

param : Describes each parameter of a method.

returns : Describes what the method returns (for non-void methods).

It is recommended to document all class and their public methods. If you think a private or protected method requires documentation, please add comment for them too.

## Regions

If you can group methods together, use #region to group them together, especially for larger classes. This can also help decide when to split up a class.

## TODO comments

Use TODO comments to mark places in code that need further work or refactoring. Add your initials to the todo comment.

> //ToDo - AB - This causes a performance issue. Plz fix using TZV1-0000

If you add a ToDo comment for a refactor that is not covered by a ticket, make sure to talk to the team lead to make a ticket for that issue.

## Design Patterns & Principles
 
Recommend checking out Design Patterns such as : Factory, Builder, Singleton, Facade, Adapter, Observer, Strategy, State in either of these links below.

[Level up your code with game programming patterns - Unity Technologies](https://resources.unity.com/games/level-up-your-code-with-game-programming-patterns?ungated=true)

[Design Patterns - Refactoring Guru](https://refactoring.guru/design-patterns)

 

# Dos & Don’ts
 

## Avoid use of UnityEvents
We encourage you to use System.Action instead of UnityEvents. This is to make it easy to find dependencies / logic flow of scripts via IDE. 

## Use Start and Awake sparingly
Initialization should be done in an Initialize function that is called by a parent. Use Start and Awake sparingly for initializing variables within script scope. This is to avoid race conditions when a script is initializing variables using data from other scripts that are not initialized. ( This can be project specific )

## Limit use of Update()
Try to avoid adding code to the Update func. It is resource intensive to have calculations in the update loop. If possible, refactor it to run based on events or user input.

## Use object pooling
Unity Instantiation and Destroy are resource intensive. It is recommended to use object pooling ( using UnityEngine.Pool ) instead of repeated instantiation and destroy of the same prefab. For networked prefabs, you will need custom object pooling solutions or a pooling feature provided by the network plugin.

## Reduce use of hardcoded magic strings / numbers
A magic string/number is a string/number that appears in code without explanation or context. 

> ``` csharp
> eg :  Heading.text = "Hello" // "Hello" is a magic string
> ```

It is easy to make typos and it is hard to refactor them when they are reused in multiple locations. Replaces them with one of the following options  

- Constant variables 
- Enum variable
- Serialized variables exposed to Unity inspector
- Data stored in Scriptable objects.

## Cache variables and references
Cache variables whenever possible. If a calculation is performed or Get() is called multiple times in a script, cache it. 

Eg : Instead of yield return new WaitForEndofFrame, define a WaitForEndofFrame variable, initialize it during Start or Init and reuse the variable in loop.

## Avoid use of GetComponent and Gameobject.Find
Although it might seem easy to use GetComponent & GetComponentInChildren calls, it is recommended to keep the usage to minimum. There are multiple alternatives :

- Serialize and expose the variable in Inspector : If the reference is within a prefab, it is recommended to set the reference to variable via inspector. 

- Set it during initialization : If the reference is outside the prefab and you have a root level script, pass the reference either during Initialization of prefab or use a Set function.

It is recommended to cache variables instead of using GetComponent multiple times.

<br>

# Team Culture

<br>

## No Blame

No blame culture means focusing on learning from mistakes instead of blaming people. It encourages everyone to share errors without fear, so the team can find solutions together. This builds trust, improves morale, and helps the organization get better and fix issues faster.

## Ownership

Take responsibility for everything around you, whether it is your fault or not. When you make a mistake, acknowledge it and learn from it. Focus on solution than blaming others. If someone is not explaining something to you properly, it is not your fault, but you have a responsibility to communicate that with them and ask for better explanations and clarifications. 

## Ask for help

If you can’t find something in these documentation or in ChatGPT, ask for help. There is no shame in asking for help. If you are getting invited to too many meetings and it is interrupting the flow of your work, reach out to Agnel and we will get that fixed. 

## Work-Life Balance

Make sure you have a work life balance and you respect personal time of others, especially if they are in different time zones. Make use of Slack’s scheduled message if the person is in a different time zone and not working at the moment.

