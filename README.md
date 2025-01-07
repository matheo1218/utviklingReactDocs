# React TS Documentation
## Table of contents
- [Introduction](#introduction)
- [Static types](#static-types)
- [React Hooks](#react-hooks)

## Introduction
React is a framework that is based on JavaScript, or TypeScript in our case
In this documentation I will show some of the basic functions in React that will be useful for a beginner

## React TS vs React JS
### Introduction
React is a framework of either JavaScript or TypeScript. But what is the difference between those two?
In short, TS is a more object- and type-oriented version of JS. Where all types in JS are dynamic, TS add the option of static types, as well as interfaces
Underneath you will find a few examples of the difference between the two

### Examples
#### Static types
In JavaScript , you would define a `string`, a `number`, and a `boolean` value like this
```tsx
    const tekst = "string"; // As you can see, all the variables are defined in the same way
    const nummer = 17;
    const trueOrFalse = true;
```

In Typescipt, you would define a `string`, a `number`, and a `boolean` value like this
```tsx
    const tekst: string = "string"; // As you can see, all the variables define what type they are
    const nummer: number = 17;
    const trueOrFalse: boolean = true;
```

You can also see a difference when declaring a function
```tsx
    function PrintText(input) {
        console.log(input);
    }
```

In Typescipt, you can define the parameters type as a string. This saves you from having to error handle what happends if the input is not a string, as the code will do that for you
```tsx
    function PrintText(input: string) {
        console.log(input);
    }
```

#### Interfaces
You can also define interfaces
Interfaces is like a class from C#
Its a template that can predefine what content an object should contain
```tsx
    interface Car {
        model: string;
        releaseDate: number;
        color: string;
        isBoughtSecondHand: boolean;
    }
```
When you have defined an interface like the one above, you have defined that a car should always have a model which is a string, a release date which is a number, and so on
```tsx
    interface Car {
        model: string;
        releaseDate: number;
        color?: string;
        isBoughtSecondHand: boolean;
    }
```
Can you see whats different in this interface?
By putting the `?` behind `color` you have defined that color can be undefined, and is therefore not required

#### Interfaces as static types
Static type could have been very hard for objects, as using an own `object`-class would not give you any of the benefits of static typing
With the use of intefaces, you can define a static type that branches, and use this interface when defining a variable
```tsx
    interface Car {
        model: string;
        releaseDate: number;
        color?: string;
        isBoughtSecondHand: boolean;
    }

    const CarlsCar: Car = {
        model: "Tesla Model X",
        releaseDate: 2001,
        isBoughtSecondHand: true
    }

    const RichardsCar: Car = {
        model: "Car",
        releaseDate: 2024,
        color: "Red",
        isBoughtSecondHand: false
    }

    function ProvideCarInfo(car: Car) {
        console.log(`This is a ${car.model}`);
        console.log(`The car was released in ${car.releaseDate}`);
        if(car.color) {
            console.log(`The car is ${car.model}`);
        }
        console.log(`This car ${car.isBoughtSecondHand?"is":"is not"} bought second hand`);
    }

    ProvideCarInfo(CarlsCar);
    ProvideCarInfo(RichardsCar);
```
The code above would log the following in the console:

```
This is a Tesla Model X
The car was released in 2001
This car is not bought second hand

This is a Car
The car was released in 2024
The car is Car
This car is bought second hand
```

## React Hooks
### Introduction
React hooks are functions that can "hook" into states and such in React <br>
[For a more detailed explanation of hooks](https://www.w3schools.com/react/react_hooks.asp)<br>
Simply speaking, they are an easy way to use the state and rendering-system that makes React so good<br>
Each time there is a state-change, there is also a rerender<br>
This documentation will show the two most important hooks to learn at the start, what they do, and why to use them<br>

### UseState
A useState is a variable saved in a state, which works excellent when building responsive websites that should be able to scale
```tsx
    const [name, setName] = useState<string>("");
```
When declaring a useState you get returned two values, the read and the change
The leftmost value `name` is the value of the state, which you can read in your code
The other value `setName` is the functions that allow you to change the value of a state
```tsx
    // YOU SHOULD NEVER WRITE
    name = "Henrik";
    // Instead define it the correct way:
    setName("Henrik");
```
After the `useState` you define the type of the state, inside `<>`
The above useState will only accept the type `string``
Lastly, inside the `()` you define the states initial value
```tsx
    // This will not work
    const [name, setName] = useState<string>(25);

    // This, however, will
    const [name, setName] = useState<string[]>(["Karl", "Fredrik"]);

    // You can also define a useState with an interface
    interface Car {
        model: string;
        releaseDate: number;
        color?: string;
        isBoughtSecondHand: boolean;
    }

    const [car, setCar] = useState<Car>({
        model: "Tesla Model X",
        releaseDate: 2001,
        isBoughtSecondHand: true
    });
```
Underneath is an example of how you can use a useState
```tsx
    export default function DisplayScore() {
        const [score, setScore] = useState(0);
        return (
            <div>
                <p>{score}</p>
                <button onClick={() => setScore(score+1)}>+</button>
                <button onClick={() => setScore(score-1)}>-</button>
            </div>
        );
    }
```

### UseEffect
A useEffect is a function that gets called each re-render
These are used when you want something to happen, or something to change, on a render
```tsx
    useEffect(() => {
        // This is the default setup of a useEffect
        // The code inside the {} will be executed on each re-render
        // That means that the console.log below would be called each time you clicked the button from the example above
        console.log("Re-render triggered");
    });
```

However, you can also limit what kind of re-renders you want to trigger the `useEffect` <br>
`useEffect`s allow a second parameter, after the function that gets called <br>
This parameter is an array containing dependensies, defining which type of re-renders will trigger the code
```tsx
    export default function DisplayScore() {
        const [score, setScore] = useState(0);

        useEffect(() => {
            // This useEffect will trigger each time the state "score" re-renders
            // This includes when it is defined
            // If i were to click the "+" button 3 times, the console would say: 
            // 0, 1, 2, 3
            console.log(score);
        },[score]);

        return (
            <div>
                <p>{score}</p>
                <button onClick={() => setScore(score+1)}>+</button>
                <button onClick={() => setScore(score-1)}>-</button>
            </div>
        );
    }
```
You can also define that you only want the useEffect to be called at the first render, by adding an empty depenency-array
```tsx
    useEffect(() => {

    },[]);
```
If you add multiple dependencies, the function will be called each time either of them causes a re-render

### Using React hooks together