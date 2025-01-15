# React TS Documentation
## Table of contents
- [Introduction](#introduction)
- [Static types](#static-types)
- [React Hooks](#react-hooks)
- [Usefull Functions](#usefull-functions)

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
The above useState will only accept the type `string`
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
As you saw in one of the examples above that you can use `useState`s to trigger the functions of the `useEffect`
Underneath is another example of how you can use both
```tsx 
    export default function DisplayScore() {
        const [score, setScore] = useState(0);
        const [threeScore, setThreeScore] = useState(0);
    
        useEffect(() => {
            // This useEffect will trigger each time the state "score" re-renders
            // It then sets the state of threeScore to three times the newest state of score
            setThreeScore(score * 3);
        },[score]);

        useEffect(() => {
            // This useEffect will trigger each time the state "threeScore" re-renders
            // If i were to click the "+" button 3 times, the console would say: 
            // 0, 3, 6, 9
            console.log(threeScore);
        },[threeScore]);

        return (
            <div>
                <p>{score}</p>
                <button onClick={() => setScore(score+1)}>+</button>
                <button onClick={() => setScore(score-1)}>-</button>
            </div>
        );
    }
```


## Usefull Functions
In this part, we'll show some of the most usefull functions in React, and how they can be used
- [Fetch](#fetch)

### Fetch
#### Introduction
The fetch command is the best way to fetch data from an API `Objectively, Axios is bad :(`
It's a simple function, that takes a few parameters, and makes it possible to communicate with other services
[For more documentation, look here](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

#### Fetch as a promise
The fetch function returns a promise. This means that you will not get returned a string, but rather a promise that it is trying to fetch a string
There is two popular ways to make the function return data instead of a promise, and this docs will  focus on my favorite
```tsx
    async function fetchData() {
        fetch("examplesite.com/api/test-api");
        // This will return a promise

        await fetch("examplesite.com/api/test-api");
        // This will fetch the data that gets returned by the request
    }

    fetchData();
```
By `await`ing the fetch function inside an `async` function, the code will return the correct data
You can look at `async` as a command that the code should wait for code to finish if its told so, and `await` as a marker that tells you to wait
If you wait for a promise to finish, it will return the data it promised
As a rule of thumb, you should always `await` a fetch function

#### The parameters of fetch
##### URL
The first parameter is the URL. That is the service youre trying to reach with the fetch function
```tsx
    async function fetchData() {
        const url: string = "examplesite.com/api/test-api"
        fetch(url);
    }

    fetchData();
```
##### Method
Technically, there is only two parameters, where the seconds paramameter is an object filled with data, but we'll count that as multiple
Fetch often follows the consept `CRUD` (Create, read, update, delete)
With fetch, this is divied into four methods: `POST, GET, PUT, DELETE`
The method is defined inside an object

```tsx
    async function fetchData() {
        const url: string = "examplesite.com/api/test-api";
        const METHOD: string = "GET";
        const secondParameterObject = {
            method: METHOD
        }
        fetch(url, secondParameterObject);
    }

    fetchData();
```
The method is defined as a string inside the second parameter object

##### Headers
The second parameter of the object is the headers parameter
The header contains data of how the api should process the request
It can include things such as which format the request is, and its authorization
Different kind of requests will nead different headers
```tsx
    async function fetchData() {
        const url: string = "examplesite.com/api/test-api";
        const METHOD: string = "POST";
        const HEADERS = {
            "Content-Type":"application/json", // This is the most used header, and is telling the api that the request will contain json
            "Authorization":"Bearer lja56iojgoi54eo9i4j4e09gjej4g"
        }
        const secondParameterObject = {
            method: METHOD,
            headers: HEADERS,
        }
        fetch(url, secondParameterObject);
    }

    fetchData();
```

###### Body
The third and final parameter of the object is the body.
Only `POST`, `PUT`, and `DELETE` allow the use of `BODY`
A body must contain the kind of data defined in the headers

```tsx
    async function fetchData() {
        const url: string = "examplesite.com/api/test-api";

        const METHOD: string = "POST";

        const HEADERS = {
            "Content-Type":"application/json",
            "Authorization":"Bearer lja56iojgoi54eo9i4j4e09gjej4g"
        }

        const BODY = {
            arms: 2,
            name: "Henrik"
        }

        const jsonBODY = json.stringify(BODY); // You have to make sure the data that is sent in is the same as the headers, in this case json

        const secondParameterObject = {
            method: METHOD,
            headers: HEADERS,
            body: jsonBODY,
        }
        fetch(url, secondParameterObject);
    }

    fetchData();
```

### Map
#### Introduction
The `map` function is one of the most usefull functions when creating a responsive and scaleable application
It allows you to display data from an array in the `HTML` part of TSX  
Functionally it works the same as a `forEach`-loop, but can be used inside the `HTML`, making it better for this usecase

#### Examples
The `map` function must be used inside `{}`
The examle underneath will show how you can use the map function to display easy data from an array
```tsx
    export default function MapDisplayer() {
        const arrayOfData: string[] = ["Hello", "World"];
        return (
            <div>
                {arrayOfData&&arrayOfData.map((data, index) => ( // Data = The index of the array youre currently on, index = the index
                    <p key={index}>{data}</p> // This would display both Hello and World. To differentiate the p tags from eachother, you give them the key value, thats set to the index
                ))}
            </div>
        );
    }
```
If you wonder why it was written `arrayOfData&&arrayOfData.map`, that simply checks if arrayOfData exists before displaying<br>
This example will show how you can use the `map` function with an object
```tsx
    export default function MapDisplayer() {
        interface PersonInterface {
            name: string;
            age: number;
            favoriteFood: string;
        }

        const arrayOfData: PersonInterface[] = [{
            name: "Henrik",
            age: 18,
            favoriteFood: "Slicers"
        } , {
            name: "Mathias",
            age: 29,
            favoriteFood: "Hot dogs"
        }];

        return (
            <div>
                {arrayOfData&&arrayOfData.map((person, index) => (
                    <p key={index}>{person.name} is {person.age} years old, and likes eating {person.favoriteFood}</p> 
                ))}
            </div>
        );
    }
```
As you can see, you can use the properties of the object to display even more information

## The previous chapters mixed
### Introduction
Now, we'll try to mix all of the different things we've looked at in this documentation
### Example
```tsx
    interface PersonInterface { // Defining an interface
        firstname: string;
        lastname: string;
        age: number;
        id: number;
        adress: string;
    }

    export default function ExampleFunction() {
        const [personArray, setPersonArray] = useState<PersonInterface[]>([]); // Creating a useState personArray that is an array of persons

        async function FetchData() {
            const response = await fetch("https://testapi.com/api/fetch-person-data"); // Fetching data
            const data = await response.json();
            setPersonArray(data); // And setting that data as the value of the useState
        }

        useEffect(() => {
            FetchData(); //Fetching the data the first time the site loads
        },[])

        return (
            <div>
                {personArray && personArray.length && personArray.map((person, index) => ( // If the useState exists, and its length is more than 0, then you should map it
                    <div key={index}>
                        <p>{person.firstname} {person.lastname}</p>
                        <p>{person.age}</p>
                        <p>{person.id}</p>
                        <p>{person.adress}</p>
                    </div>
                ))}
            </div>
        );
    }
```