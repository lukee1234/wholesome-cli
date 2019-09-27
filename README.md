![A Command Line Tool that facilitates code generation for Flutter projects.](https://www.clawstudios.com/assets/wholesome/icon.png)

Wholesome is a Command Line Tool that aims to facilitate code generation for [Flutter](https://flutter.dev/) projects, proposing a default architecture based on BLoC pattern.

## Requeriments
This tool is executed using [pub](https://pub.dev/) and generate code for [Flutter](https://flutter.dev/) projects this means that you will need:
 - [Dart SDK](https://dart.dev/get-dart)
 - [Flutter](https://flutter.dev/docs/get-started/install)

## Installation
Since the tool is still on development and it is on an early version for testing, you must install it from the git repository using local source or online source.

### Online
You can install the tool with this repo link running the following line:

    pub global activate --source git https://github.com/clawstudios/wholesome-cli.git

### Local
If you clonned the reopository, you can install the tool with the following line repalcing 'path' with the path where is located the repo on your computer

    pub global activate --source path <path>

### Add executable folder to $PATH
To execute Wholesome from your command line, you need to add the [pub](https://pub.dev/) cache folder to the PATH.
Check out the [Running Script](https://dart.dev/tools/pub/cmd/pub-global#running-a-script) section in the [pub-global](https://dart.dev/tools/pub/cmd/pub-global) dart documentation to add the path correctly to you Operating System.

## Before Starting

The whole tool is based on the following folder structure.
*You can read more about each folder in the section of each subcommand of the generator.*

    / myproject
      |- .idea
      |- android
      |- assets
      |- ios
      |- lib
        |- common
        |- components
            |- mycomponent
                |- mycomponent.bloc.dart
                |- mycomponent.events.dart
                |- mycomponent.state.dart
                |- mycomponent.view.dart
        |- guards
        |- models
        |- pages
            |- mypage
                |- mypage.bloc.dart
                |- mypage.events.dart
                |- mypage.state.dart
                |- mypage.view.dart
        |- services
      |- test



## Commands
Every Wholesome command needs to be executed by the **wsm** binary. At the moment, you will be able to run the following commands and subcommands:
 - new
 - generate
	 - component
	 - guard
	 - model
	 - page
	 - service

## New

The **new** command generates a new Flutter project with the provided name, the [previously detailed folder](https://discord.gg/zyghfFq) folder structure and some boilerplate code.

    wsm new myproject
    
*This command will run 'flutter new' and then will generate the structure and files.*

This command also generates the following files inside the **common** folder:
 - assets.dart
 - colors.dart
 - helpers.dart
 - routes.dart
 - styles.dart

### Assets, Colors and Styles
These are files for storing constants with asset paths, custom colors, or custom styles that you need to reuse on every part of the app.

You can import the files in the following way:

    import  'package:myproject/common/assets.dart'  as ASSETS;
    import  'package:myproject/common/colors.dart'  as COLORS;
    import  'package:myproject/common/styles.dart'  as STYLES;

### Helpers
This is a file created to put all the helper functions that you will use to develop your app.

You need to import it like this:

    import  'package:myproject/common/helpers.dart'  as HELPERS;
 
And you will find two methods for printing to console.

    HELPERS.printError('This is an error message.');
    HELPERS.printWarn('This is a warning message.');

### Routes
In this file you will find a ROUTES Map in where you can add routes and associate them with the generated Page constructor.

For more information about routing, please check [Flutter Routing Docs](https://flutter.dev/docs/development/ui/navigation) .

## Generate

This command generates boilerplate code, it receives **one subcommand as a parameter** and you must **execute this command under a Flutter Project** 

    wsm generate <subcommand>

### Component

A component is a reutilizable implementation of code that could have one or more files.

#### Stateful Component
For components that need state management, Wholesome generates a set of files inside a folder named the same as the component (as you can see in the [Before Starting](https://discord.gg/zyghfFq) section, inside the 'components' folder)

    wsm generate component <name>

**Generated Files:** 

**name.bloc.dart**
This file contains all the Business Logic and also is intended to manage the State of the component through events.

**name.events.dart**
Contains an abstract class ready to be extended by custom events used to comunicate between BLoC and View.

**name.state.dart**
Contains a class with the State data of the component and only can be modified by the BLoC.

**name.view.dart:**
Is a StatefulWidget with a BLoC instance in it and a dispose implementation that includes the _bloc.dispose() call that is needed to shutdown the BLoC controllers when disposing the view.

#### Stateless Component (NOT IMPLEMENTED YET)
For components without state management, Wholesome will generate only a StatelessWidget that will be used as a view.

    wsm generate component <name> -s
    # or
    wsm generate component <name> -stateless

### Guard

Guard classes have methods to manage the access to one or more views, we think that a singleton with a  **canActivate** method that returns a boolean is a start, and can be extended as needed.
*We know we need to implement a proper way to handle a view lifecycle *
*These files are created under 'guards' folder as shown in the [Before Starting](https://discord.gg/zyghfFq) section.*

    wsm generate guard <name>

### Model

Models are classes that represents different data models handled inside an app such as user data to show in a profile view.
*Models are located inside 'models' folder. (check the [previously detailed folder](https://discord.gg/zyghfFq) structure).*

    wsm generate model <name>

### Page

Pages are StatefulWidgets with the same structure as components, but they can be accessed navigating to their specific route and represent a whole view. 

In pages is where you will instantiate components and trigger events to the BLoC for handling state and model mutations.

*Pages are located inside 'pages' folder. (check the [previously detailed folder](https://discord.gg/zyghfFq) folder structure).*

    wsm generate page <name>

See Routes Section to know how to add a route to your page.

### Service

Services are singletons that exposes methods to interact with the external resources such as APIs or Databases.

*Services are located inside 'services' folder. (check the [previously detailed folder](https://discord.gg/zyghfFq) folder structure).*

    wsm generate service <name>

## Credits
This tool is a development in progress by [Claw Studios](https://www.clawstudios.com/) and is under BSD License. 

If you want to help, contribute or report a bug please use the following channels
- [Slack](https://join.slack.com/t/clawstudios/shared_invite/enQtNzYyNTY2NzI1ODEwLWM1MzEzODc2ZDYxNDY5MmY4NWRkNWRhMzM4MTliM2I3NjM5MjIzM2Q5Y2U0ZTYwZmRkNjc0N2Q3NjRlYTA0MmI)
- [Discord](https://discord.gg/zyghfFq)
- info@clawstudios.com

