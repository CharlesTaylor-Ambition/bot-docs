---
title: Actions in adaptive dialogs - reference guide
description: Describing the adaptive dialog prebuilt actions
keywords: bot, actions, adaptive dialogs
author: WashingtonKayaker
ms.author: kamrani
manager: kamrani
ms.topic: conceptual
ms.service: bot-service
ms.date: 06/09/2020
monikerRange: 'azure-bot-service-4.0'
---

# Actions in adaptive dialogs - reference guide

[!INCLUDE [applies-to-v4](../includes/applies-to-v4-current.md)]

This article lists the actions defined in the Bot Framework SDK, grouped by their general purpose.

<!--
- [Responding to users](#activities)
- [Conditional statements](#conditional-statements)
- [Dialog management](#dialog-management)
- [Managing properties](#manage-properties)
- [Accessing external resources](#access-external-resources)
- [Debugging options](#debugging-options)
-->

- For an introduction to this topic, see the [Actions in adaptive dialogs][1] concept article.
- For information on how you request user input, an important and very useful type of action, see [Asking for user input using adaptive dialogs][7].

## Activities

| Activity to accomplish                         | Action Name                                | What this action does                                                    |
| ---------------------------------------------- | ------------------------------------------ | ------------------------------------------------------------------------ |
| Send any activity such as responding to a user.| [SendActivity](#send-activity)             | Sends an activity, such as a response to a user.            |
| Update an activity                             | [UpdateActivity](#update-activity)         | Updates an activity that was sent.                                        |
| DeleteActivity                                 | [DeleteActivity](#delete-activity)         | Deletes an activity that was sent.                                        |
| Get activity members                           | [GetActivityMembers](#get-activity-members)| Gets a list of activity members and saves it to a property in [memory][11].|

For a code sample see [Activities examples](#activities-examples).
<!--
## Requesting user input

For information on how you request user input, see [Asking for user input using adaptive dialogs][7].

>[!TIP]
> _Inputs_ are an important and very useful type of action that is covered in the [Asking for user input using adaptive dialogs][7] article.
-->

## Conditional statements

The first two actions are conditional statements designed to help your bot make decisions based on any pre-defined condition that you have created. These conditions are specified by a set of conditional statements having boolean expressions which are evaluated to a boolean value of true or false.

The remaining actions relate to looping statements which enable you to repeat the execution of a block of code for every element in a collection.

| Activity to accomplish | Action Name                    | What this action does                                                                                |
| ---------------------- | ------------------------------ | ---------------------------------------------------------------------------------------------------- |
| Branch: if/else        | [IfCondition](#ifcondition)    | Runs a set of actions based on a Boolean expression. |
| Branch: Switch (Multiple options) | [SwitchCondition](#switchcondition) | Runs a set of actions based on a pattern match. |
| Loop: for each item    | [ForEach](#foreach)            | Loops through a set of values stored in an array.                                                     |
| Loop: for each page (multiple items) | [ForEachPage](#foreachpage) | Loops through a large set of values stored in an array, one page at a time.             |
| Exit a loop            | [BreakLoop](#break-loop)       | Exits the enclosing loop. |
| Continue a loop        | [ContinueLoop](#continue-loop) | Starts the next iteration of the enclosing loop. |
| Goto a different Action| [GotoAction](#goto-action) | Transfers control to the specified action, identified by the action's ID. |

For code samples see [Create a condition examples](#create-a-condition-examples).

<!--TODO P1: Regarding BreakLoop & ContinueLoop - Need better explanation.
There's a mix of concepts going on here. There's the action sequence, which are the action list that's getting run for any given trigger. And then there are dialogs, which are either a parent dialog, a child dialog, or an action in the chain. Reducing confusion between action sequences and dialogs would probably help.  -->

## Dialog management

| Activity to accomplish | Action Name                      | What this action does                                                     |
| ---------------------- | -------------------------------- | ------------------------------------------------------------------------- |
| Begin a new dialog     | [BeginDialog](#begindialog)      | Begins executing another dialog. When that dialog finishes, the execution of the current trigger will resume.    |
| Cancel a dialog        | `CancelDialog`<!--[CancelDialog](#canceldialog)-->| Cancels the active dialog. Use when you want the dialog to close immediately, even if that means stopping mid-process.|
| Cancel all dialogs     | [CancelAllDialogs](#cancelalldialogs)| Cancels all active dialogs including any active parent dialogs. Use this if you want to pop all dialogs off the stack, you can clear the dialog stack by calling the dialog context's cancel all dialogs method. Emits the `CancelAllDialogs` event.|
| End this dialog        | [EndDialog](#enddialog)          | Ends the active dialog.  Use when you want the dialog to complete and return results before ending. Emits the `EndDialog` event.|
| End dialog turn        | [EndTurn](#endturn)              | Ends the current turn of conversation without ending the dialog.          |
| Repeat this dialog     | [RepeatDialog](#repeatdialog)    | Used to restart the parent dialog.                                        |
| Replace this dialog    | [ReplaceDialog](#replacedialog)  | Replaces the current dialog with a new dialog                             |
| GetConversationMembers| [GetConversationMembers](#get-conversation-members) | Enables you to get a list of the conversation members and save it to a property in [memory][11].|
| EditActions    | [EditActions](#editactions) | Enables you to edit the current action sequence on the fly based on user input. Especially useful when handling [interruptions][interruptions].  |

For code samples see [Dialog management examples](#dialog-management-examples).

<!--TODO P1: Revisit table structure for activities: https://github.com/MicrosoftDocs/bot-docs-pr/pull/2115#discussion_r420272686 --->

## Manage properties

| Activity to accomplish | Action Name                           | What this action does                          |
| ---------------------- | ------------------------------------- | ---------------------------------------------- |
| Edit an array          | [EditArray](#editarray)               | Performs an operation on an array.             |
| Delete a property      | [DeleteProperty](#deleteproperty)     | Removes a property from [memory][11].          |
| Delete properties      | [DeleteProperties](#deleteproperties) | Removes multiple properties at once.           |
| Create or update a property | [SetProperty](#setproperty)      | Sets a property's value in [memory][11].       |
| Create or update properties | [SetProperties](#setproperties)  | Sets the value of multiple properties at once. |

For code samples see [Manage properties examples](#manage-properties-examples).

## Access external resources

| Activity to accomplish | Action Name                  | What this action does                                                         |
| ---------------------- | ---------------------------- | ----------------------------------------------------------------------------- |
| Begin a skill dialog   | [BeginSkill](#beginskill)    | Begins a skill and forwards activities to the skill until the skill ends. |
| Send an HTTP request   | [HttpRequest](#httprequest)  | Makes an HTTP request to an endpoint.                                    |
| Emit a custom event    | [EmitEvent](#emitevent)      | Raises a custom event. Add a [custom trigger][8] to the adaptive dialog to react to the event. |
| Sign out a user        | [SignOutUser](#sign-out-user)| Signs out the currently signed in user.                                        |
| Call custom code       | [CodeAction](#codeaction)    | Calls custom code. The custom code must be asynchronous, take a dialog context and an object as parameters, and return a dialog turn result. |

For code samples see [Access external resource examples](#access-external-resource-examples).

## Debugging options

| Activity to accomplish | Action Name                     | What this action does                                                       |
| ---------------------- | ------------------------------- | --------------------------------------------------------------------------- |
| Log to console         | [LogAction](#log-action)        | Writes to the console and optionally sends the message as a trace activity. |
| Emit a trace event     | [TraceActivity](#traceactivity) | Sends a trace activity with whatever payload you specify.                   |

For code samples see [Debugging option examples](#debugging-option-examples).

## Source code examples

### Activities examples

#### Send activity

Sends an activity.

```csharp
// Example of a simple SendActivity step
var greetUserDialog = new AdaptiveDialog("greetUserDialog");
greetUserDialog.Triggers.Add(new OnIntent()
{
    Intent = "greetUser", 
    Actions = new List<Dialog>() {
        new SendActivity("Hello")
    }
});

// Example that includes reference to property on bot state.
var greetUserDialog = new AdaptiveDialog("greetUserDialog");
greetUserDialog.Triggers.Add(new OnIntent()
{
    Intent = "greetUser",
    Actions = new List<Dialog>()
    {
        new TextInput()
        {
            Property = "user.name",
            Prompt = new ActivityTemplate("What is your name?")
        },
        new SendActivity("Hello, ${user.name}")
    }
});
```

#### Update activity

Updates an activity that was previously sent. This ID is returned from the call to `SendActivity`.

```csharp
new UpdateActivity ()
{
    ActivityId = "id",
    Activity = new ActivityTemplate("updated value")
}
```

#### Delete activity

Deletes an activity that was previously sent. Requires the ID of the previous activity.

```csharp
new DeleteActivity ()
{
    ActivityId = "id"
}
```

#### Get activity members

Gets the members of the activity associated with this turn and saves the list to a property.

```csharp
new GetActivityMembers()
{
    Property = "turn.activityMembers"
}
```

See [language generation in adaptive dialogs][9] to learn more about using language generation instead of hard coding actual response text in the _send activity_ action.

### Create a condition examples

#### IfCondition

Branches the conversational flow based on a specific condition. Conditions are expressed using [Adaptive expressions][10].

```csharp
var addToDoDialog = new AdaptiveDialog("addToDoDialog");
addToDoDialog.Triggers.Add(new OnIntent()
{
    Intent = "addToDo",
    Actions = new List<Dialog>()
    {
        // Save the userName entity from a recognizer.
        new SaveEntity("dialog.addTodo.title", "@todoTitle"),
        new TextInput()
        {
            Prompt = new ActivityTemplate("What is the title of your todo?"),
            Property = "dialog.addTodo.title"
        },
        // Add the current todo to the todo's list for this user.
        new EditArray()
        {
            ItemsProperty = "user.todos",
            Value = "=dialog.addTodo.title"
            ChangeType = EditArray.ArrayChangeType.Push
        },
        new SendActivity("Ok, I have added ${dialog.addTodo.title} to your todos."),
        new IfCondition()
        {
            Condition = "toLower(dialog.addTodo.title) == 'call santa'",
            Actions = new List<Dialog>()
            {
                new SendActivity("Yes master. On it right now \\[You have unlocked an easter egg] :)")
            }
        },
        new SendActivity("You now have ${count(user.todos)} items in your todo.")
    }
});
```

#### SwitchCondition

Branches a conversational flow based on the outcome of an expression evaluation. See [Adaptive expressions][10] for more information.

```csharp
// Create an adaptive dialog.
var cardDialog = new AdaptiveDialog("cardDialog");
cardDialog.Triggers.Add(new OnIntent()
{
    Intent = "ShowCards",
    Actions = new List<Dialog>()
    {
        // Add choice input.
        new ChoiceInput()
        {
            // Output from the user is automatically set to this property
            Property = "turn.cardDialog.cardChoice",

            // List of possible styles supported by choice prompt.
            Style = ListStyle.Auto,
            Prompt = new ActivityTemplate("What card would you like to see?"),
            Choices = new ChoiceSet(new List<Choice>() {
                new Choice("Adaptive card"),
                new Choice("Hero card"),
                new Choice("Video card")
            })
        },
        // Use SwitchCondition step to dispatch to right dialog based on choice input.
        new SwitchCondition()
        {
            Condition = "turn.cardDialog.cardChoice",
            Cases = new List<Case>()
            {
                new Case("Adaptive card",  new List<Dialog>() { new SendActivity("${AdaptiveCardRef()}") } ),
                new Case("Hero card", new List<Dialog>() { new SendActivity("${HeroCard()}") } ),
                new Case("Video card",     new List<Dialog>() { new SendActivity("${VideoCard()}") } ),
            },
            Default = new List<Dialog>()
            {
                new SendActivity("[AllCards]")
            }
        }
}));
```

#### ForEach

The Foreach loop is a convenient way to retrieve elements of an array or a collection. It is often used to perform action on each item in a collection.

```csharp
var rootDialog = new AdaptiveDialog(nameof(AdaptiveDialog))
{
    Generator = new TemplateEngineLanguageGenerator(),
    Triggers = new List<OnCondition>()
    {
        new OnUnknownIntent()
        {
            Actions = new List<Dialog>()
            {
                new SetProperty()
                {
                    Property = "turn.colors",
                    Value = "=createArray('red', 'blue', 'green', 'yellow', 'orange', 'indigo')"
                },
                new Foreach()
                {
                    ItemsProperty = "turn.colors",
                    Actions = new List<Dialog>()
                    {
                        // By default, dialog.foreach.value holds the value of the item
                        // dialog.foreach.index holds the index of the item.
                        // You can use short hands to refer to these via
                        //      $foreach.value
                        //      $foreach.index
                        new SendActivity("${$foreach.index}: Found '${$foreach.value}' in the collection!")
                    }
                }
            }
        }
    }
};
```

#### ForEachPage

Used to apply steps to items in a collection. Page size denotes how many items from the collection are selected at a time.

```csharp
var rootDialog = new AdaptiveDialog(nameof(AdaptiveDialog))
{
    Generator = new TemplateEngineLanguageGenerator(),
    Triggers = new List<OnCondition>()
    {
        new OnUnknownIntent()
        {
            Actions = new List<Dialog>()
            {
                new SetProperty()
                {
                    Property = "turn.colors",
                    Value = "=createArray('red', 'blue', 'green', 'yellow', 'orange', 'indigo')"
                },
                new ForeachPage()
                {
                    ItemsProperty = "turn.colors",
                    PageSize = 2,
                    Actions = new List<Dialog>()
                    {
                        // By default, dialog.foreach.page holds the value of the page
                        //      $foreach.page
                        new SendActivity("Page content: ${join($foreach.page, ', ')}")
                    }
                }
            }
        }
    }
};
```

#### Break Loop

Breaks out of a loop or the current action sequence.

```csharp
var rootDialog = new AdaptiveDialog(nameof(AdaptiveDialog))
{
    Generator = new TemplateEngineLanguageGenerator(),
    Triggers = new List<OnCondition>()
    {
        new OnUnknownIntent()
        {
            Actions = new List<Dialog>()
            {
                new SetProperty()
                {
                    Property = "turn.colors",
                    Value = "=createArray('red', 'blue', 'green', 'yellow', 'orange', 'indigo')"
                },
                new Foreach()
                {
                    ItemsProperty = "turn.colors",
                    Actions = new List<Dialog>()
                    {
                        new IfCondition()
                        {
                            Condition = "$foreach.value == 'green'",
                            Actions = new List<Dialog>()
                            {
                                new BreakLoop()
                            },
                            ElseActions = new List<Dialog>()
                            {
                                // By default, dialog.foreach.value holds the value of the item
                                // dialog.foreach.index holds the index of the item.
                                // You can use short hands to refer to these via 
                                //      $foreach.value
                                //      $foreach.index
                                new SendActivity("${$foreach.index}: Found '${$foreach.value}' in the collection!")
                            }
                        },
                    }
                }
            }
        }
    }
};
```

#### Continue Loop

Continues the current loop or action sequence without processing the rest of the statements.

```csharp
var rootDialog = new AdaptiveDialog(nameof(AdaptiveDialog))
{
    Generator = new TemplateEngineLanguageGenerator(),
    Triggers = new List<OnCondition>()
    {
        new OnUnknownIntent()
        {
            Actions = new List<Dialog>()
            {
                new SetProperty()
                {
                    Property = "turn.colors",
                    Value = "=createArray('red', 'blue', 'green', 'yellow', 'orange', 'indigo')"
                },
                new Foreach()
                {
                    ItemsProperty = "turn.colors",
                    Actions = new List<Dialog>()
                    {
                        new IfCondition()
                        {
                            // Skip items at even position in the collection.
                            Condition = "$foreach.index % 2 == 0",
                            Actions = new List<Dialog>()
                            {
                                new ContinueLoop()
                            },
                            ElseActions = new List<Dialog>()
                            {
                                // By default, dialog.foreach.value holds the value of the item
                                // dialog.foreach.index holds the index of the item.
                                // You can use short hands to refer to these via 
                                //      $foreach.value
                                //      $foreach.index
                                new SendActivity("${$foreach.index}: Found '${$foreach.value}' in the collection!")
                            }
                        },
                    }
                }
            }
        }
    }
};
```

#### Goto action

Jump to a labelled action within the current action scope.

```csharp
var adaptiveDialog = new AdaptiveDialog()
{
    Triggers = new List<OnCondition>()
    {
        new OnBeginDialog()
        {
            Actions = new List<Dialog>()
            {
                new GotoAction()
                {
                    ActionId = "end"
                },
                new SendActivity("this will be skipped."),
                new SendActivity()
                {
                    Id = "end",
                    Activity = new ActivityTemplate("The End.")
                }
            }
        }
    }
};
```

### Dialog management examples

#### BeginDialog

Starts a new dialog and pushes it onto the dialog stack. `BeginDialog` requires the name of the target dialog, which can be any type of dialog including Adaptive dialog or Waterfall dialog etc.

The `BeginDialog` action defines a property named `ResultProperty` that allows you to specify where to save the results when the dialog ends.

```csharp
new BeginDialog("BookFlightDialog")
{
    // Any value returned by BookFlightDialog will be captured in the property specified here.
    ResultProperty = "$bookFlightResult"
}
```

> [!TIP]
> Just like when invoking any dialog in the Bot Framework SDK, when calling `BeginDialog` to invoke an adaptive dialog, you can use the `options` parameter to pass input information for the dialog.

#### EndDialog

Ends the active dialog by popping it off the stack and returns an optional result to the dialog's parent.

By default, adaptive dialogs have their `defaultResultProperty` set to `dialog.results` so anything that is set in that [memory scope][11] will automatically be returned to the caller in scenarios when the dialog auto ends itself. If you end the dialog using the `EndDialog` action you'll need to specify what is returned to the caller in the `value` property.

```csharp
new EndDialog()
{
    // Value property indicates value to return to the caller.
    Value = "=$userName"
}
```

> [!TIP]
> Adaptive dialogs will end automatically by default if the dialog has completed running all of its actions. To override this behavior, set the `AutoEndDialog` property on Adaptive Dialog to false.

#### CancelAllDialogs

Deletes all dialogs on the stack, including parent and child dialogs.

```csharp
new CancelAllDialogs()
```

#### EndTurn

Ends the current turn of conversation without ending the dialog.

```csharp
new EndTurn()
```

#### RepeatDialog

Restarts the parent dialog. This is particularly useful if you are trying to have a conversation where the bot is paging results to the user that they can navigate through.

> [!IMPORTANT]
> Make sure to use `EndTurn()` or one of the Inputs to collect information from the user so you do not accidentally end up implementing an infinite loop.

<!--TODO P2: Need a better code example--->

```csharp
var rootDialog = new AdaptiveDialog(nameof(AdaptiveDialog))
{
    Triggers = new List<OnCondition>()
    {
        new OnUnknownIntent()
        {
            Actions = new List<Dialog>()
            {
                new TextInput()
                {
                    Prompt = new ActivityTemplate("Give me your favorite color. You can always say cancel to stop this."),
                    Property = "turn.favColor",
                },
                new EditArray()
                {
                    ArrayProperty = "user.favColors",
                    Value = "=turn.favColor",
                    ChangeType = EditArray.ArrayChangeType.Push
                },
                // This is required because TextInput will skip prompt if the property exists - which it will from the previous turn.
                // Alternately you can also set `AlwaysPrompt = true` on the TextInput.
                new DeleteProperty() {
                    Property = "turn.favColor"
                },
                // Repeat dialog step will restart this dialog.
                new RepeatDialog()
            }
        },
        new OnIntent("CancelIntent")
        {
            Actions = new List<Dialog>()
            {
                new SendActivity("You have ${count(user.favColors)} favorite colors - ${join(user.favColors, ',', 'and')}"),
                new EndDialog()
            }
        }
    },
    Recognizer = new RegexRecognizer()
    {
        Intents = new List<IntentPattern>()
        {
            new IntentPattern()
            {
                Intent = "HelpIntent",
                Pattern = "(?i)help"
            },
            new IntentPattern()
            {
                Intent = "CancelIntent",
                Pattern = "(?i)cancel|never mind"
            }
        }
    }
};
```

#### ReplaceDialog

Starts a new dialog and replaces on the stack the currently active dialog with the new one.

```csharp
// This sample illustrates the use of ReplaceDialog tied to explicit user confirmation
// to switch to a different dialog.

// Create an adaptive dialog.
var getUserName = new AdaptiveDialog("getUserName");
getUserName.Triggers.Add(new OnIntent()
{
    Intent = "getUserName",
    Actions = new List<Dialog>()
    {
        new TextInput()
        {
            Property = "user.name",
            Prompt = new ActivityTemplate("What is your name?")
        },
        new SendActivity("Hello ${user.name}, nice to meet you!")
    }
});

getUserName.Triggers.Add(new OnIntent()
{
    Intent = "GetWeather",
    Actions = new List<Dialog>()
    {
        // confirm with user that they do want to switch to another dialog
        new ChoiceInput()
        {
            Prompt = new ActivityTemplate("Are you sure you want to switch to talk about the weather?"),
            Property = "turn.contoso.getWeather.confirmChoice",
            Choices = new ChoiceSet(new List<Choice>()
            {
                new Choice("Yes"),
                new Choice("No")
            })
        },
        new SwitchCondition()
        {
            Condition = "turn.contoso.getWeather.confirmChoice",
            Cases = new List<Case>()
            {
                // Call ReplaceDialog to switch to a different dialog.
                // BeginDialog will keep current dialog in the stack to be resumed after child dialog ends.
                // ReplaceDialog will remove current dialog from the stack and add the new dialog.
                {
                    Value = "Yes",
                    Actions = new List<Dialog>()
                    {
                        new ReplaceDialog("getWeatherDialog")
                    }
                },
                {
                    Value = "No",
                    Actions = new List<Dialog>()
                    {
                        new EndDialog()
                    }
                }
            }
        }
    }
});
```

#### Get conversation members

Gets the members of the current conversation and saves the list to a property.

```csharp
new GetConversationMembers()
{
    Property = "turn.convMembers"
}
```

#### EditActions

Modifies the current sequence of actions. Specifically helpful when handling [interruptions][interruptions]. You can use EditActions to insert or remove actions anywhere in the sequence, including adding actions to the beginning or end of the sequence.

```csharp
var rootDialog = new AdaptiveDialog(nameof(AdaptiveDialog))
{
    Generator = new TemplateEngineLanguageGenerator(),
    Recognizer = new RegexRecognizer()
    {
        Intents = new List<IntentPattern>()
        {
            new IntentPattern()
            {
                Intent = "appendSteps",
                Pattern = "(?i)append"
            },
            new IntentPattern()
            {
                Intent = "insertSteps",
                Pattern = "(?i)insert"
            },
            new IntentPattern()
            {
                Intent = "endSteps",
                Pattern = "(?i)end"
            }
        }
    },
    Triggers = new List<OnCondition>()
    {
        new OnUnknownIntent()
        {
            Actions = new List<Dialog>()
            {
                new ChoiceInput()
                {
                    Prompt = new ActivityTemplate("What type of EditAction would you like to see?"),
                    Property = "$userChoice",
                    AlwaysPrompt = true,
                    Choices = new ChoiceSet(new List<Choice>()
                    {
                        new Choice("Append actions"),
                        new Choice("Insert actions"),
                        new Choice("End actions"),
                    })
                },
                new SendActivity("This message is after your EditActions choice..")
            }
        },
        new OnIntent()
        {
            Intent = "appendSteps",
            Actions = new List<Dialog>() {
                new SendActivity("In append steps .. Steps specified via EditSteps will be added to the current plan."),
                new EditActions()
                {
                    Actions = new List<Dialog>() {
                        // These steps will be appended to the current set of steps being executed.
                        new SendActivity("I was appended!")
                    },
                    ChangeType = ActionChangeType.AppendActions
                }
            }
        },
        new OnIntent() {
            Intent = "insertSteps",
            Actions = new List<Dialog>() {
                new SendActivity("In insert steps .. "),
                new EditActions()
                {
                    Actions = new List<Dialog>() {
                        // These steps will be inserted before the current steps being executed.
                        new SendActivity("I was inserted")
                    },
                    ChangeType = ActionChangeType.InsertActions
                }
            }
        },
        new OnIntent()
        {
            Intent = "endSteps",
            Actions = new List<Dialog>()
            {
                new SendActivity("In end steps .. "),
                new EditActions()
                {
                    // The current sequence will be ended. This is especially useful if you are looking to end an active interruption.
                    ChangeType = ActionChangeType.EndSequence
                }
            }
        }
    }
};
```

### Manage properties examples

#### SetProperty

Used to set a property's value in [memory][11]. The value can either be an explicit string or an expression. See [adaptive expressions][10] to learn more about expressions.

```csharp
new SetProperty()
{
    Property = "user.firstName",
    // If the value of user.name is 'Mahatma Gandhi', this sets first name to 'Mahatma'
    Value = "=split(user.name, ' ')[0]"
},
```

#### SetProperties

Initialize one or more properties in a single action.

```csharp
new SetProperties()
{
    Assignments = new List<PropertyAssignment>()
    {
        new PropertyAssignment()
        {
            Property = "user.name",
            Value = "Vishwac"
        },
        new PropertyAssignment()
        {
            Property = "user.age",
            Value = "=coalesce($age, 30)"
        }
    }
}
```

#### DeleteProperty

Removes a property from [memory][11].

```csharp
new DeleteProperty
{
    Property = "user.firstName"
}
```

#### DeleteProperties

Delete more than one property in a single action.

```csharp
new DeleteProperties()
{
    Properties = new List<StringExpression>()
    {
        new StringExpression("user.name"),
        new StringExpression("user.age")
    }
}
```

#### EditArray

Used to perform edit operations on an array property.

```csharp
var addToDoDialog = new AdaptiveDialog("addToDoDialog");
addToDoDialog.Triggers.Add(new OnIntent()
{
    Intent = "addToDo",
    Actions = new List<Dialog>() {
        // Save the userName entity from a recognizer.
        new SaveEntity("dialog.addTodo.title", "@todoTitle"),
        new TextInput()
        {
            Prompt = new ActivityTemplate("What is the title of your todo?"),
            Property = "dialog.addTodo.title"
        },
        // Add the current todo to the todo's list for this user.
        new EditArray()
        {
            ItemsProperty = "user.todos",
            Value = "=dialog.addTodo.title"
            ChangeType = EditArray.ArrayChangeType.Push
        },
        new SendActivity("Ok, I have added ${dialog.addTodo.title} to your todos."),
        new SendActivity("You now have ${count(user.todos)} items in your todo.")
}));
```

### Access external resource examples

#### BeginSkill

The `BeginSkill` action starts the specified skill, manages the forwarding of activities to the skill and receiving activities from the skill, and processes the skill result if any when the skill ends.

<!-- TODO--->

#### HttpRequest

Use this to make HTTP requests to any endpoint.

<!--TODO P1: Would be good to call out that the properties support data binding. So you can have reference to memory in URI, body etc.
the body property supports adaptive expressions, so it contains the body of the request or an expression that evaluates to the body of the request. --->

```csharp
new HttpRequest()
{
    // Set response from the http request to turn.httpResponse property in memory.
    ResultProperty = "turn.httpResponse",
    Method = HttpRequest.HttpMethod.POST,
    Header = new Dictionary<string,string> (), /* request header */
    Body = { }                                 /* request body */
};

```

#### EmitEvent

Used to raise a custom event that your bot can respond to. You can control bubbling behavior on the event raised so it can be contained just to your own dialog or bubbled up the parent chain.

```csharp
var rootDialog = new AdaptiveDialog(nameof(AdaptiveDialog))
    {
        Generator = new TemplateEngineLanguageGenerator(),
        Triggers = new List<OnCondition>()
        {
            new OnUnknownIntent()
            {
                Actions = new List<Dialog>()
                {
                    new TextInput()
                    {
                        Prompt = new ActivityTemplate("What's your name?"),
                        Property = "user.name",
                        AlwaysPrompt = true,
                        OutputFormat = "toLower(this.value)"
                    },
                    new EmitEvent()
                    {
                        EventName = "contoso.custom",
                        EventValue = "=user.name",
                        BubbleEvent = true,
                    },
                    new SendActivity("Your name is ${user.name}"),
                    new SendActivity("And you are ${$userType}")
                }
            },
            new OnDialogEvent()
            {
                Event = "contoso.custom",

                // You can use conditions (expression) to examine value of the event as part of the trigger selection process.
                Condition = "turn.dialogEvent.value && (substring(turn.dialogEvent.value, 0, 1) == 'v')",
                Actions = new List<Dialog>()
                {
                    new SendActivity("In custom event: '${turn.dialogEvent.name}' with the following value '${turn.dialogEvent.value}'"),
                    new SetProperty()
                    {
                        Property = "$userType",
                        Value = "VIP"
                    }
                }
            },
            new OnDialogEvent()
            {
                Event = "contoso.custom",

                // You can use conditions (expression) to examine value of the event as part of the trigger selection process.
                Condition = "turn.dialogEvent.value && (substring(turn.dialogEvent.value, 0, 1) == 's')",
                Actions = new List<Dialog>()
                {
                    new SendActivity("In custom event: '${turn.dialogEvent.name}' with the following value '${turn.dialogEvent.value}'"),
                    new SetProperty()
                    {
                        Property = "$userType",
                        Value = "Special"
                    }
                }
            },
            new OnDialogEvent()
            {
                Event = "contoso.custom",
                Actions = new List<Dialog>()
                {
                    new SendActivity("In custom event: '${turn.dialogEvent.name}' with the following value '${turn.dialogEvent.value}'"),
                    new SetProperty()
                    {
                        Property = "$userType",
                        Value = "regular customer"
                    }
                }
            }
        }
    };
```

#### Sign out user

Sign out current signed in user that's been signed in using an [`OAuth` Input][4].

```csharp
new SignOutUser()
{
    UserId = "userid",
    ConnectionName = "connection-name"
}
```

#### CodeAction
<!--TODO P1: We should create a separate article that describes how to migrate waterfall steps to code actions. There are a couple of gotchas. (https://github.com/MicrosoftDocs/bot-docs-pr/pull/2115#discussion_r425436817)-->
As the name implies, this action enables you to call a custom piece of code.

```csharp
// Example customCodeStep method
private async Task<DialogTurnResult> CodeActionSampleFn(DialogContext dc, System.Object options)
{
    await dc.Context.SendActivityAsync(MessageFactory.Text("In custom code step"));
    // This code step decided to just return the input payload as the result.
    return dc.EndDialogAsync(options)
}

// Adaptive dialog that calls a code step.
var rootDialog = new AdaptiveDialog(rootDialogName) {
    Triggers = new List<OnCondition>()
    {
        new OnUnknownIntent()
        {
            Actions = new List<Dialog>()
            {
                new CodeAction(CodeActionSampleFn),
                new SendActivity("After code step")
            }
        }
    }
};
```

### Debugging option examples

#### TraceActivity

Sends a trace activity with a payload you specify.

> [!NOTE]
> Trace activities can be captured as transcripts and are only sent to Emulator to help with debugging.

```csharp
new TraceActivity()
{
    // Name of the trace event.
    Name = "contoso.TraceActivity",
    ValueType = "Object",
    // Property from memory to include in the trace
    ValueProperty = "user"
}
```

#### Log action

Writes to the console and optionally sends the message as a trace activity.

```csharp
new LogAction()
{
    Text = new TextTemplate("Hello"),
    // Automatically sends the provided text as a trace activity
    TraceActivity = true
}
```

## Additional Information

- To learn about actions specific to gathering user input, see the [asking for user input using adaptive dialogs][7] article.
- To learn more about adaptive expressions see the [adaptive expressions][10] article.

[1]:../v4sdk/bot-builder-concept-adaptive-dialog-Actions.md
[2]:../v4sdk/bot-builder-concept-adaptive-dialog-triggers.md
[3]:https://www.qnamaker.ai/
[4]:../adaptive-dialog/adaptive-dialog-prebuilt-inputs.md#oauthinput
[5]:../v4sdk/bot-builder-concept-dialog.md
[6]:../adaptive-dialog/adaptive-dialog-prebuilt-inputs.md#interruptions
[7]:../adaptive-dialog/adaptive-dialog-prebuilt-inputs.md
[8]:../v4sdk/bot-builder-concept-adaptive-dialog-triggers.md#custom-event-trigger
[9]:../v4sdk/bot-builder-concept-adaptive-dialog-generators.md
[10]:../v4sdk/bot-builder-concept-adaptive-expressions.md
[11]:../v4sdk/bot-builder-concept-adaptive-dialog-memory-states.md
[12]:https://www.qnamaker.ai/
[13]:https://github.com/microsoft/botbuilder-samples
[oauthinput]: ../adaptive-dialog/adaptive-dialog-prebuilt-inputs.md#oauthinput
[interruptions]: ../v4sdk/bot-builder-concept-adaptive-dialog-interruptions.md
