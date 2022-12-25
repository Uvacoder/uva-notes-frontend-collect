## 05. `useImperativeHandle`

`useImperativeHandle` is used to customize what value is exposed to the parent when it uses ref. This should be used with `forwardRef`.

```js
import React, { useImperativeHandle } from 'react';

function Child(props, ref) {
    useImperativeHandle(ref, () => 'Some value');

    return <h1>Hello</h1>
}

export default React.forwardRef(Child);
```

```js
import React, { useRef, useEffect } from 'react';
import Child from './child';

function Parent() {
    const childRef = useRef();

    useEffect(() => {
        console.log(inputEl.current); 
        //output: 'Some value'
        //Not DOM element anymore
    }, []);

    return <Child ref={childRef}/>
}

export default Parent;
```

- `useImperativeHandle` can be used to expose only the input DOM element to the parent.
