# 3. React.memo for reducing unnecessary re-renders

Here's the lifecycle of a React app:

```
→  render → reconcilitation → commit
         ↖                   ↙
              state change
```

Let's define a few terms:

- The "render" phase: create React elements React.createElement
- The "reconciliation" phase: compare previous elements with the new ones
- The "commit" phase: update the DOM (if needed).

```jsx
// React.memo for reducing unnecessary re-renders
// http://localhost:3000/isolated/exercise/03.js

import React from 'react'
import Downshift from 'downshift'
import { getItems } from '../workerized-filter-cities'
import { useAsync, useForceRerender } from '../utils'
function Menu({
  getMenuProps,
  inputValue,
  getItemProps,
  highlightedIndex,
  selectedItem,
  setItemCount,
}) {
  const { data: items = [] } = useAsync(
    React.useCallback(() => getItems(inputValue), [inputValue])
  )
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
      {itemsToRender.map((item, index) => (
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

// 🐨 Memoize the Menu here using React.memo

function ListItem({
  getItemProps,
  items,
  highlightedIndex,
  selectedItem,
  index,
}) {
  const item = items[index]
  return (
    <li
      {...getItemProps({
        index,
        item,
        style: {
          backgroundColor: highlightedIndex === index ? 'lightgray' : 'inherit',
          fontWeight:
            selectedItem && selectedItem.id === item.id ? 'bold' : 'normal',
        },
      })}
    >
      {item.name}
    </li>
  )
}
      <Downshift
        onChange={(selection) =>
          alert(
            selection ? `You selected ${selection.name}` : 'Selection Cleared'
          )
        }
        itemToString={(item) => (item ? item.name : '')}
      >
        {({
          getInputProps,
          getItemProps,
          getLabelProps,
          getMenuProps,
          isOpen,
          inputValue,
          highlightedIndex,
          selectedItem,
          setItemCount,
        }) => (
          <div>
            <div>
              <label {...getLabelProps()}>Find a city</label>
              <div>
                <input {...getInputProps()} />
              </div>
            </div>
            <Menu
              getMenuProps={getMenuProps}
              inputValue={inputValue}
              getItemProps={getItemProps}
              highlightedIndex={highlightedIndex}
              selectedItem={selectedItem}
              setItemCount={setItemCount}
            />
          </div>
        )}
      </Downshift>
    </>
  )
}

////////////////////////////////////////////////////////////////////
//                                                                //
//                 Don't make changes below here.                 //
// But do look at it to see how your code is intended to be used. //
//                                                                //
////////////////////////////////////////////////////////////////////

function Usage() {
  return <FilterComponent />
}

export default Usage
```

A React Component can re-render for any of the following reasons:

1. Its props change
2. Its internal state changes
3. It is consuming context values which have changed
4. Its parent re-renders
