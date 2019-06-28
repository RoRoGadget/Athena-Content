# SwiftUI for React Native Developers

SwiftUI, a declarative UI framework for Apple platforms, has arrived! Developers with React Native experience may notice some similarities to the philosophies Apple has imbued into their new UI framework. Utilizing structs as immutable value types for view modeling, a declarative syntax, and with their new async event library Combine, a reactive architecture.

That buzzword soup is something to celebrate from Apple, and even though it has barely landed on the Apple Beta program, it may be prudent to evaluate the new technology against React Native, an equally viable choice.

So I attempted to go through React Native’s ‘Basics’ guide and recreate each component they created to highlight the common components developers would use.

These basic guides were actually what I used when learning to make React Native apps so hopefully my attempt at recreating them can illuminate some complexities, and bugs that I encountered when using SwiftUI.

Here is a link to the playground I created for all of the tutorials.

## 1. Hello World

Hello World is the de facto example used in introducing a new language or technology.

There are certain similarities that should be pointed out. Component is the base class for React Native visual elements. While SwiftUI conforms to the View protocol to define a value type that represents a View.

Text rendering is similar in how succinct it is.

Styling is where React Native and SwiftUI diverge. But the differences will be highlighted in later examples.

<script src="https://gist.github.com/RoRoGadget/bbd78b98139d6664af30c18c1605544d.js"></script>


## 2. State

**React Native:**

State handling is an important concept in React Native. React components are controlled using props or state. Props are passed from the parent. But changes to the component are handled via state

In the React Native example the state is toggled using a timer. Changing the isShowingText value on each interval.

**SwiftUI:**

State in SwiftUI is handled in a similar fashion as ReactNative.

From the documentation:

*When the state updates, the view invalidates its appearance and updates itself.*

**Note:** Due to SourceKit crashes in Xcode Playground when using Timer, I chose to use the Toggle component to modify the @State of the SwiftUI component.

@State is a propertyDelegate. Property delegates have been a proposed feature which isn’t officially in the language yet. Here is an article describing the ‘compiler black magic’ used in the new SwiftUI framework.’

<script src="https://gist.github.com/RoRoGadget/3fcfb9621ad7066a42c3ca5823de2da4.js"></script>

## 3. Style

**React Native:**

Besides syntax, styling is where a lot of differences are most prominent.

React components utilize javascript objects with key value pairs representing style parameters. Similar to CSS, but utilizing camel-case instead.

The React Native example shows the complexities of single and compounded styles.Providing a singly style object sets the specific styles for the Text component. Providing an array will cause the last style to have precedence.

**SwiftUI:**

SwiftUI styling utilizes modifier functions that customize the display, behavior and interactivity of the components.

Modifier method results are not persistent and can be overridden (line 22 / 23).

<script src="https://gist.github.com/RoRoGadget/64c93007972521fa49664a908b3dbb20.js"></script>

## 4. Size

**React Native:**

The size of React Native components is declared using style objects with explicit width and height values.

**SwiftUI:**

SwiftUI utilizes the frame modifier function which has parameters for the width and height.

<script src="https://gist.github.com/RoRoGadget/5cc63f02eab1d2a6c786173b7ee6e216.js"></script>

## 5. Text Input

**React Native:**

Text input of ReactNative components utilizes the TextInput component. the onChangeText prop mutates the state of the component causing re-renders of the associated text component.

**SwiftUI:**

Text input in SwiftUI can be achieved in a similar fashion by binding the text state of to a TextField type.

StylingTextField components can be done using the textFieldStyle method with a TextFieldStyle member.

<script src="https://gist.github.com/RoRoGadget/67001d269fe1e4fdce0cabbe8aee612e.js"></script>

## 6. Touch input

**React Native:**

Touch Input in React Native has a button abstraction which renders button components in the respective platforms. They allow title, color and press handlers.

They also have multiple touch abstractions called TouchableHighlight, TouchableOpacity, TouchableNativeFeedback, and TouchableWithoutFeedback components for responding to touch interactions.

**SwiftUI:**

SwiftUI has Button components where title and action handlers can be assigned.

Styling is done using modifier methods likeborderlessButtonStyle, popUpButtonStyle, pullDownButtonStyle, and linkButtonStyle.

<script src="https://gist.github.com/RoRoGadget/6c0e741e616bafd8a19b8b8c12436f46.js"></script>

## 7. Scroll View

**React Native:**

Scroll views in React Native present heterogenous components inline both vertically and horizontally.

Scroll views are also able to use pagination and allow pinch to zoom gestures.

**SwiftUI:**

SwiftUI ScrollView instances render content vertically and sequentially.

Note: Current SwiftUI components with collections of view instances as their body can run into complex closure result type errors of the compiler. Something to watch out for.

<script src="https://gist.github.com/RoRoGadget/e8dbf7f243e3a866f92622098280b135.js"></script>

## 8. Lists

**React Native:**

Lists and table views are very common UI patterns used on mobile platforms but macOS as well!

ReactNative makes rendering lists very easy with the FlatList component.

The key property of each item in the array of data is important as it allows the list to track unique items in its collection.

**SwiftUI:**

SwiftUI also makes rendering lists simple.

In place of the key prop React Native uses, you call the identified(by:) method to return a collection identified by the keypath of the value.

Styling of list items is done for each element so the potential for non uniform table views with cells with different heights.

<script src="https://gist.github.com/RoRoGadget/9ff6961fd30af2bda98a711cf6b3bca3.js"></script>

## 9. Section Lists

**React Native:**

And finally, The SectionList component can present multiple logical sections with headers and footers.

**SwiftUI:**

SwiftUI utilizes Section objects which contain header, footer and content closures to display individual sections.

The inner contents in each section are individual Text instances rendered from a ForEach instance which computes views on demand from a collection.
