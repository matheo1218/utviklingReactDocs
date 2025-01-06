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
        console.log(`The car was relesed in ${car.releaseDate}`);
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
The car was relesed in 2001
This car is not bought second hand

This is a Car
The car was relesed in 2024
The car is Car
This car is bought second hand
```

## React Hooks
### Introduction
React hooks are functions that can "hook" into states and such in React <br>
[For a more detailed explanation of hooks](https://www.w3schools.com/react/react_hooks.asp)<br>
Simply speaking, they are an easy way to use the state and rendering-system that makes React so good<br>
This documentation will show the two most important hooks to learn at the start, what they do, and why to use them<br>

### UseState
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
### UseEffect
### Using React hooks together
