# react-fundamentals-notes


# Table of Contents

1.  [Overview](#org644fda4)
2.  [01 Setup](#org9a122e8)
    1.  [Emoji key](#orgc038465)
3.  [02 Hello World](#orgbb1e6fc)
    1.  [Personal Take](#org897793e)
4.  [03 Intro to raw React APIs](#org6a593b9)
    1.  [Personal Take](#org851b62d)
5.  [04 Using JSX](#org2bf77c6)
6.  [05 Create Custom Components](#org1c831a4)
    1.  [Solution render jsx from functions](#orgfe81eeb)
    2.  [ECS01 custom component with React.createElement](#org01ddbff)
    3.  [ECS02 custom component with JSX](#org91bbef8)
    4.  [ECS03 runtime validation with PropTypes](#org60f7c9b)
    5.  [ECS04 use prop-types package](#org4caa0fb)
    6.  [ECS05 React Fragments](#orgff1e74b)
7.  [06 Styling](#orgd6a8593)
    1.  [Solution: The style prop](#org354adbc)
    2.  [EC01: Create a custom component](#orgba8f5f6)
    3.  [EC02: accept a size prop to encapsulate styling](#org6c12884)
8.  [07 Forms](#orgc3b678c)
    1.  [Solution Form Basics](#org43a2764)
    2.  [ECS01 using refs](#org771c7dc)
    3.  [ECS02 validate lower-case](#org913768b)
    4.  [ECS03 control the input value](#orge678f97)
9.  [08 Rendering Arrays](#org7a554df)
    1.  [Solution: Render Arrays](#org2eb431c)
    2.  [ECS01: Focus demo](#org3b0f162)



<a id="org644fda4"></a>

# Overview


<a id="org9a122e8"></a>

# 01 Setup


<a id="orgc038465"></a>

## Emoji key

Helpful Emoji 🐨 💪 🏁 💰 💯 🦉 📜 💣 👨‍💼 🚨

Each exercise has comments in it to help you get through the exercise. These fun emoji characters are here to help you.

Kody the Koala Bear 🐨 will tell you when there&rsquo;s something specific you should do

Matthew the Muscle 💪 will indicate what you&rsquo;re working with an exercise

Chuck the Checkered Flag 🏁 will indicate that you&rsquo;re working with a final version

Marty the Money Bag 💰 will give you specific tips (and sometimes code) along the way

Hannah the Hundred 💯 will give you extra challenges you can do if you finish the exercises early.

Olivia the Owl 🦉 will give you useful tidbits/best practice notes and a link for elaboration and feedback.

Dominic the Document 📜 will give you links to useful documentation

Berry the Bomb 💣 will be hanging around anywhere you need to blow stuff up (delete code)

Peter the Product Manager 👨‍💼 helps us know what our users want

Alfred the Alert 🚨 will occasionally show up in the test failures with potential explanations for why the tests are failing.


<a id="orgbb1e6fc"></a>

# 02 Hello World

      <body></body>
      <script type="module">
        let root = document.createElement('div')
        root.id = 'root'
        document.body.append(root)
    
        let div = document.createElement('div')
        div.textContent = 'Hello Worldsss'
        div.className = 'container'
        document.getElementById('root').append(div)
      </script>
    </html>

`document` is the object you interact with in JavaScript that represents the HTML DOM.
`document` has quite a few methods on it to explore

Why would you want to `setAttribute` over directly modifying said attribute?

    let root = document.createElement('div')
    root.setAttribute('id', 'root')

My solution works but you can also directly append the `div` created to the root element in JS

    root.append(div)

Without actually appending the element, it will sit in memory and not be useful for anyone

[insertion methods](https://javascript.info/modifying-document)

Inserting elements into the dom through JavaScript will be useful for React portals down the road.


<a id="org897793e"></a>

## Personal Take

Playing around with the document object helped solidify what properties are available to me and how easy it is to update and modify properties in JavaScript. At first, I didn&rsquo;t realize that you can just access the body tag as an attribute on document.


<a id="org6a593b9"></a>

# 03 Intro to raw React APIs

unpkg can access any package on npm and make it available via a url (cdn).

React has a `umd` build that lets us use it as a cdn.

`React` and `ReactDOM` are now availabe on the page as objects.

    const elementProps = {id: 'element', children: 'Hello World!'}
    const reactElement = React.createElement('div', elementProps)
    ReactDOM.render(reactElement, rootElement)

Children prop can be set as an object like above or as individual arguments after the second argument. They will all get &rsquo;slurped&rsquo; up into the children object.

Extra Credit:

    const reactElement = React.createElement
     'div',
      null,
      React.createElement('span', null, 'Hello'),
      React.createElement('span', null,  ' '),
      React.createElement('span', null, 'World!')
    )

`createElement` can accept more than 2 parameters and the third can be another `createElement` call


<a id="org851b62d"></a>

## Personal Take

It&rsquo;s cool to see how the magic happens underneath (jsx)! The extra credit exercise helped a lot in understanding how to compose createElement calls. I had never seen the object notation for the children object so seeing that compared to the React docs where they pass in `null` was interesting!


<a id="org2bf77c6"></a>

# 04 Using JSX

JSX lets you write markup will still being in JavaScript land.

The compiled &rsquo;raw&rsquo; React code is available in the `head` of the document when compiling with babel. (Not something you&rsquo;d want to do in production)

    const elementJsx = <div className="container"> Hello World from JSX </div>

“Interpolation” is defined as &ldquo;the insertion of something of a different nature into something else.&rdquo;

In our case, we insert JavaScript inside of a string and it will get converted. Not all JavaScript is valid in that interpolation, you can&rsquo;t do statements inside of an iterpolation.

What is a statement and what is an expression?

You can interpolate inside JSX as well.

    const greeting = 'Hello World'
    const myClassName = 'container'
    const element = <div className={myClassName}>{greeting}></div>

📜 The react docs for JSX are pretty good: <https://reactjs.org/docs/introducing-jsx.html>

Here are a few sections of particular interest for this extra credit:

<https://reactjs.org/docs/introducing-jsx.html#embedding-expressions-in-jsx>
<https://reactjs.org/docs/introducing-jsx.html#specifying-attributes-with-jsx>

`children` is a prop passed to jsx as well as what content you put within the tags of your JSX:

    const elementJsx = <div className="container" children >Hello World from JSX</div>

If you were to pass all your props with a `createElement` call you would just pass it like so:

    const element = React.createElement('div', props)
    // or...
    const element = React.createElement('div', {id: 'my-thing', ...props})

On a conflict in props, the right most prop will win the conflict and set the prop.

    const element = <div id="my-thing" {...props} className="default" />

`default=` will be set as `className=`


<a id="org1c831a4"></a>

# 05 Create Custom Components


<a id="orgfe81eeb"></a>

## Solution render jsx from functions

Programmers love to abstract things!

We can use functions to abstract our JSX to create react Elements inside the function and re-use that all over the place

    const message = ({children}) => <div className="message">{children}</div>
    
    
    const element = (
      <div className="container">
       {message({children: 'Hello Worldss'})
       {message({children: 'Goodbye Worldss'})}
      </div>
    )


<a id="org01ddbff"></a>

## ECS01 custom component with React.createElement

You can pass functions to the React.createElement directly. React will create an element that waits to call into the function passed that contains the html that you want to render (when React renders to the page)

    const element = (
          <div className="container">
            {React.createElement(message, {children: 'Hello Worlds'})}
            {React.createElement(message, {children: 'Goodbye Worldss'})}
          </div>
        )


<a id="org91bbef8"></a>

## ECS02 custom component with JSX

React components need to have a capitalized first letter for a component.

The React.createElement passes a string when you don&rsquo;t capitalize

    const Message = ({children}) => <div>{children}</div>
    
    const element = (
      <div className="container">
        <Message>Hello world Message</Message>
      </div>
    )


<a id="org60f7c9b"></a>

## ECS03 runtime validation with PropTypes

PropTypes are React&rsquo;s mechanism for letting others know how they are supposed to use the component you created. They will throw an error when a prop is of a different type than what you specify.

    Message.propTypes = {
      subject(props, propName, componentName) {
        if (typeof props[propName] !== 'string') {
          return new Error('Some useful error message here')
        }
      },
      greeting(props, propName, componentName) {
        if (typeof props[propName] !== 'string') {
          return new Error('Some useful error message here')
        }
      },
    }

React does not use PropTypes in production, they get removed from the code entirely. They can cause performance problems.


<a id="org4caa0fb"></a>

## ECS04 use prop-types package

There is a `proptypes` package that has prebuilt validators for you so you don&rsquo;t need to define them yourself like above.

Props are not set to required by default but you can make a prop required by adding an `!`

    Message.propTypes = {
      subject: PropTypes.string!,
      greeting: PropTypes.string,
    }

PropTypes aren&rsquo;t adding too much benefit if you are using a &rsquo;typed&rsquo; language like TypeScript


<a id="orgff1e74b"></a>

## ECS05 React Fragments

React has a feature called Fragments that lets you group Components together in JSX without adding a ton of divs to your code.

Fragements are super handy when the structure of your HTML is important

They let you put two (or more) elements side by side when the DOM structure needs to be something very specific


<a id="orgd6a8593"></a>

# 06 Styling


<a id="org354adbc"></a>

## Solution: The style prop

2 ways to do it:

1.  Inline styles with the style prop
2.  Regular CSS with the className prop

In react, you set inline styles with `{}` which is a combination of JSX expression and object expression

styles must be cameCased and not kebab-cased.

The `class` property is set as `className` in React.


<a id="orgba8f5f6"></a>

## EC01: Create a custom component

when you pass `props` into a component and spread them, the `className` prop will be over-ridden if you spread props after the declaration of `className`

    const Box = {className = '', style = '', ...otherProps} =>
      console.log(props) || (
        <div
          className={`box ${className}`}
          style={{fontStyle: 'italic', ...style}}
          {...otherProps}
        />
      )

What props get applied is a big deal when it comes to styling in React.

Default component styles should be postioned first with the rest of the styles spread into the object as the last piece.


<a id="org6c12884"></a>

## EC02: accept a size prop to encapsulate styling

You should consider the api of your React component.

having to write the `box--small` for every small box can be annoying and you could forget how sizing was implemented.

Much easier would be to pass size=&ldquo;small&rdquo;


<a id="orgc3b678c"></a>

# 07 Forms


<a id="org43a2764"></a>

## Solution Form Basics

Alot of React form stuff is really just DOM concepts

inputs automatically perform a post request with the inputed data and id of the input.

In React, we often times don&rsquo;t want this behavior and should pass in the `event` and call `event.preventDefault()` so we can handle exactly how we want form submission to go

    const handleSubmit = event => {
      event.preventDefault()
      alert(event.target.usernameInput.value)
    }

The event that is passed is a &rsquo;synthetic&rsquo; React event.

`console.dir(event.target)` will give the form itself so you can see all the properties on the form

`event.target[0].value` is the value of your form but that is a primitive way to access the form input values

Whatever you `name` or `id`  a form input, you&rsquo;ll be able to access the value of that input in the handler


<a id="org771c7dc"></a>

## ECS01 using refs

a ref is a special React specific thing that will set a reference to a DOM node.
You create them with `React.useRef`

If it&rsquo;s a simple input, using the `event` is a better option

    function UsernameForm({onSubmitUsername}) {
      let inputRef = React.useRef('')
    
      const handleSubmit = event => {
        event.preventDefault()
        console.log(event.target)
        alert(inputRef.current.value)
      }
    
    
      return (
        <form onSubmit={handleSubmit}>
          <div>
            <label htmlFor="usernameInput">Username:</label>
            <input ref={inputRef} id="usernameInput" type="text" />
          </div>
          <button type="submit">Submit</button>
        </form>
      )
    }


<a id="org913768b"></a>

## ECS02 validate lower-case

You can add a `handleChange` to the input itself to perform logic on the input `onChange` which will run on each keystroke.

    const handleChange = event => {
        const {value} = event.target
    
        const isLowerCase = value === value.toLowerCase()
        setError(isLowerCase ? null : 'Username must be lower case')
      }


<a id="orge678f97"></a>

## ECS03 control the input value

You can change user input by setting `event.target.value` to something you decide but this isn&rsquo;t the Idiomatic React way. This mutates the input value imparatively

    <input value={myInputValue} />

React allows us to set a value prop on the input Once we do that, React ensures that the value of that input can never change from the value of the myInputValue variable.

Typically you’ll want to provide an onChange handler as well so you can be made aware of “suggested changes” to the input’s value (where React is basically saying &ldquo;if I were controlling this value, here’s what I would do, but you do whatever you want with this&rdquo;).

When you maintain input values in state, you can use that state elsewhere in the component instead of accessing the event (like `onSubmit`)


<a id="org7a554df"></a>

# 08 Rendering Arrays


<a id="org2eb431c"></a>

## Solution: Render Arrays

the `key` prop is meant to tell react which piece of data is which so when the data changes, React won&rsquo;t get confused as to what item is what

Any component that is maintaining state over time needs a unique key. The index of the item is the default behavior and doesn&rsquo;t work well, just silence the warning

    {items.map(item => (
    // 🐨 add a key prop to the <li> below. Set it to item.id
      <li key={item.id}>
        <button onClick={() => removeItem(item)}>remove</button>{' '}
        <label htmlFor={`${item.value}-input`}>{item.value}</label>{' '}
        <input id={`${item.value}-input`} defaultValue={item.value} />
      </li>
    ))}


<a id="org3b0f162"></a>

## ECS01: Focus demo
