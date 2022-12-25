# 2. useMemo for expensive calculations

React put all the logic and state management within a function component.

This power comes with an unfortunate limitation that calculations performed within render will be performed every single render, regardless of whether the inputs for the calculations change.

```jsx
// useMemo for expensive calculations
// http://localhost:3000/isolated/exercise/02.js

import React from 'react'
import Downshift from 'downshift'
import { useForceRerender } from '../utils'
import { getItems } from '../filter-cities'

function Menu({
  getMenuProps,
  inputValue,
  getItemProps,
  highlightedIndex,
  selectedItem,
  setItemCount,
}) {
  // Returns a memoized value.
  const items = React.useMemo(() => getItems(inputValue), [inputValue])

  const itemsToRender = items.slice(0, 100)
  setItemCount(itemsToRender.length)
  return (
    <ul
      {...getMenuProps({
        style: {
          width: 300,
          height: 300,
          overflowY: 'scroll',
          backgroundColor: '#eee',
          padding: 0,
          listStyle: 'none',
        },
      })}
    >
      {itemsToRender.slice(0, 100).map((item, index) => (
        <ListItem
          key={item.id}
          getItemProps={getItemProps}
          items={items}
          highlightedIndex={highlightedIndex}
          selectedItem={selectedItem}
          index={index}
        />
      ))}
    </ul>
  )
}
```

Remember that the function passed to `useMemo` runs during rendering. Don’t do anything there that you wouldn’t normally do while rendering. For example, side effects belong in `useEffect,` not `useMemo`.

If no array is provided, a new value will be computed on every render.

- http://kcd.im/usememo
