Jonh Dang's Weather Data Compiler.
JONHDANG@MAIL.com 10/8/22
## Prerequisites
 - [Node.js ~v6.9.1](https://nodejs.org/en/): A JavaScript runtime. The code base should be relatively independant of the Node.js version being run.
 - [Yarn](https://yarnpkg.com/lang/en/) (Optional but highly recommended): Depedency management software that typically outperforms npm at installation speed.

## Tested envionments
 - Windows 10 Home (OS Build 14393.1066)
 - OS X El Captain 10.11.6
	
### Browser support
I used the assignment to try out new features of JavaScript and CSS such as promises and CSS Grid. 
This limits the compatibility of the app to modern browsers only. The Webpack transpiler loaders should provide extended compatibility, however, for the sake of marking, the app works correctly on the following browsers:
 - Google Chrome +58.0.3029.110 (64-bit)
 - Firefox +53.0.3

## Installation instructions 
0. Make sure [Node.js](https://nodejs.org/en/download/) is installed.
1. Open up a terminal.
2. `cd` to desired folder.
3. `git clone https://github.com/Monash-University-FIT3077/fulllambda-Assignments.git`
4. `cd fulllambda-Assignments/Assignment_2`
5. Run `npm install`. If you have yarn installed you can use `yarn install`. Wait for all the node packages to finish downloading.
6. Run `npm run backend-start`. Wait for the the *'Webpack configuration complete'* message to be printed to the console.
7. Open up another terminal.
8. Run `npm run frontend-start`. Wait for Webpack to finish again.
9. Open a browser.
10. Type into the URL bar: *'localhost:3000'*.

**Note:**  I had wait for the backend's compilation to finish before running `npm run frontend-start`. This is an issue with having two Webpack builds running at the same time in the same folder with similar configurations. It is assumed that a solution to this problem is out of scope for this assignment.

## UML Diagrams
- [Class diagrams](/UML/Class_Diagrams/README.md)
- [Sequence diagrams](/UML/Sequence_Diagrams/README.md)


## Engineering philosophies and patterns used
 - **[The observer pattern](https://en.wikipedia.org/wiki/Observer_pattern):** The observer pattern was used for on click events and in the `LocationMonitoringManager` & `SessionMonitoringManager`. Rge observer pattern mimics the [Android SDK's implementation of the observer pattern](https://developer.android.com/guide/topics/ui/ui-events.html#EventListeners).
 - **[Factory pattern](https://en.wikipedia.org/wiki/Factory_method_pattern):** We use the factory pattern to allow the `FullLambdaWeatherService` to create a `WeatherClient` from a `WeatherClientFactory` so that the service does not need to know the underlying steps to create the client. Retry-client-creation functionality will be written into the `FullLambdaWeatherService` as an example of using the pre-existing factory code to potentially build multiple `Promise<WeatherClient>`s.
 - **Seperate GUI and logic**: We almost totally avoid any logic on the frontend of rge project. This allows us to provide functionality that is independant of the user's interface. In fact, the only frontend class that performs limited controller functionality is the `WeatherPageContainer` which links the view to the [socket.io](https://socket.io) API. All other frontend classes concern themselves with rendering the DOM in a particular way.
 - **[MVC (Model, view, controller)](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller):** The model, view and controller (as previously discussed) are seperated. The `WeatherPageContainer` determines how inputs are interpreted, all other `React.Component`s serve as view type classes. All business type logic is handled by the backend server.

### Current loggin guidelines
- **Green text:** successful
- **Red text:** error information
- **Cyan text:** important information
- **Purple text:** parameterized information
- **White text:** General/other

### Git patterns
The development-master pattern is used in conjuction with feature branches. Code is merged (usually) via pull requests.

**master:** The development branch should be merged into this branch whenever a new version/set of features, ideally bug free, have been completed.

**development:** Features should be merged into this branch once implemented. This branch should maintain transpilability and compilability. Known bugs are allowed to be merged into this branch. Developers can work on the development branch for minor changes to the codebase.

**Feature branches**: Feature branches contain major refactored code or implementations of new functionality. Code from feature branches should be merged into the development via pull requests.


It also has a google map which can be used to toggle location pins for a weather service.

