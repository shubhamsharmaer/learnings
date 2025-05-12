# Notes for 07-05-2025

## Problem❓: Multi checkbox CHECK with Single Select All CheckBox

### Solution ✅

#### Made 2 states 
 ```javascript
 selectAll, setSelectAll = usestate(false)
 checkBox, setCheckBox = useState(
    new Array(any_array.length).fill(false)
 )
 ```
 `checkBox is storing [false, false, false, ....]`

#### markAllCheck ()

```javascript
    const markAllCheck = () => {
        // toggle parent checkbox
        const newState = !selectAll
        setSelectAll(newState)
        
        // fill the checkStates ['state', 'state',...]
        setCheckBox(new Array(array.length).fill(newState))
    }
```
#### handleSelectAll ()

```javascript
    const handleSelectAll = (index) => {
        // Create a copy of the checkedStates array
        const updatedStates = [...checkBox]
        // Toggle the checked state for the specific index
        updatedStates[index] = !updatedStates[index]
        // update checkBox state
        setCheckBox(updatedStates)
    }

```
#### SELECT ALL CHECK INPUT
```javascript
    <input 
        onClick={makeAllDone}
        type="checkbox" name="Select All" 
        className='size-5'
        checked={selectAll}
        onChange={() => {}}
        id="" /> 
```

#### Multi Small Check Input
```javascript
    <input
    onChange={() => handleInputCheck(index)}
    type="checkbox"
    checked={checkedStates[index]}
    className="form-checkbox h-5 w-5 text-blue-600"
    />
```