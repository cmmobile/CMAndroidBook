# 3:Functions

### **Question 1**

The `contains(element: String)` function returns `true` if the string `element` is contained in the string it's called on. What will be the output of the following code?

```text
val decorations = listOf ("rock", "pagoda", "plastic plant", "alligator", "flowerpot")
println(decorations.filter {it.contains('p')})
```

* [ ] `[pagoda, plastic, plant]`
* [ ] `[pagoda, plastic plant]`
* [x] `[pagoda, plastic plant, flowerpot]`
* [ ] `[rock, alligator]`

### **Question 2**

In the following function definition, which one of the parameters is required?

```text
fun shouldChangeWater(
    day: String, 
    temperature: Int = 22,
    dirty: Int = 20,
    numDecorations: Int = 0
): Boolean {...}
```

* [ ] `numDecorations`
* [ ] `dirty`
* [x] `day`
* [ ] `temperature`

#### **Question 3**

You can pass a regular named function \(not the result of calling it\) to another function. How would you pass `increaseDirty( start: Int ) = start + 1` to `updateDirty(dirty: Int, operation: (Int) -> Int)`?

* [ ] `updateDirty(15, &increaseDirty())`
* [ ] `updateDirty(15, increaseDirty())`
* [ ] `updateDirty(15, ("increaseDirty()"))`
* [x] `updateDirty(15, ::increaseDirty)`

