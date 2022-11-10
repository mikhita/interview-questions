# interview-questions
- [Explain event delegation]
answer: Event delegation is when a parent element automatically adds event listeners to its children elements. The event listener will fire anytime an event is triggered on the child element, due to event “bubbling” (event propagation).
- [Explain how this works in JavaScript]
answers: 
If the new keyword is used when calling the function, this inside the function is a brand new object.
function ConstructorExample() {
    console.log(this);
    this.value = 10;
    console.log(this)
}
new ConstructorExample();
// -> {}
// -> { value: 10 }
If apply, call, or bind are used to call a function, this inside the function is the object that is passed in as the argument.

function fn() {
    console.log(this);
}
var obj = {
    value: 5
};
var boundFn = fn.bind(obj);
boundFn();     // -> { value: 5 }
fn.call(obj);  // -> { value: 5 }
fn.apply(obj); // -> { value: 5 }
 If a function is called as a method — that is, if dot notation is used to invoke the function — this is the object that the function is a property of. In other words, when a dot is to the left of a function invocation, this is the object to the left of the dot. (ƒ symbolizes function in the code blocks)

var obj = {
    value: 5,
    printThis: function() {
        console.log(this);
    }
};
obj.printThis(); // -> { value: 5, printThis: ƒ }
If a function is invoked as a free function invocation, meaning it was invoked without any of the conditions present above, this is the global object. In a browser, it’s window.

function fn() {
    console.log(this);
}
// If called in browser:
fn(); // -> Window {stop: ƒ, open: ƒ, alert: ƒ, ...}
*Note that this rule is the same as rule 3 — the difference is that a function that is not declared as a method automatically becomes a property of the global object, window. This is therefore an implicit method invocation. When we call fn(), it’s interpreted as window.fn(), so this is window.

console.log(fn === window.fn); // -> true
If the function is an ES2015 arrow function, it ignores all the rules above and receives the this value of its surrounding scope at the time it’s created. To determine this, go one line above the arrow function’s creation and see what the value of this is there. It will be the same in the arrow function.


const obj = {
    value: 'abc',
    createArrowFn: function() {
        return () => console.log(this);
    }
};
