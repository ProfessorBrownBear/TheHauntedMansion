# 🎃 Haunted House Lab - Quick Reference Sheet

## 🔮 Kotlin Concepts Quick Guide

### 1️⃣ **Companion Objects (Static Members)**
```kotlin
class MyClass {
    companion object {
        const val CONSTANT = 42        // Like static final in Java
        fun staticMethod() { }          // Like static method in Java
    }
}
// Usage: MyClass.CONSTANT, MyClass.staticMethod()
```

### 2️⃣ **Data Classes**
```kotlin
data class Explorer(val name: String, var power: Int)
// Auto-generates: equals(), hashCode(), toString(), copy(), componentN()

val alice = Explorer("Alice", 50)
val bob = alice.copy(name = "Bob")  // New instance with changed name
```

### 3️⃣ **Interfaces**
```kotlin
interface Supernatural {
    fun interact()                     // Abstract method
    fun materialize() = "Appears!"     // Default implementation
}

class Spirit : Supernatural {
    override fun interact() { /* ... */ }
}
```

### 4️⃣ **Enums**
```kotlin
enum class RoomType(val danger: Int) {
    CELLAR(5),
    ATTIC(3);
    
    fun enter() = "Entering ${this.name}"
}
```

### 5️⃣ **Equals & Copy**
```kotlin
// Data class (automatic):
data class Item(val name: String)

// Regular class (manual):
class Artifact(val name: String) {
    override fun equals(other: Any?): Boolean {
        if (this === other) return true
        if (other !is Artifact) return false
        return name == other.name
    }
    
    fun copy(name: String = this.name) = Artifact(name)
}
```

### 6️⃣ **Try-Catch Blocks**
```kotlin
val result = try {
    dangerousOperation()
    "Success"
} catch (e: SpecificException) {
    handleSpecific(e)
    "Handled specific"
} catch (e: Exception) {
    "General error: ${e.message}"
} finally {
    cleanup()  // Always runs
}
```

### 7️⃣ **Deep vs Shallow Copy**
```kotlin
// Shallow Copy (shares nested objects):
val copy1 = original.copy()  // Nested lists are same reference!

// Deep Copy (independent nested objects):
val copy2 = original.copy(
    artifacts = original.artifacts.map { it.copy() }.toMutableList()
)
```

### 8️⃣ **Pass by Reference**
```kotlin
fun modify(explorer: Explorer) {
    explorer.power += 10  // Modifies original!
}

val hero = Explorer("Hero", 50)
modify(hero)  // hero.power is now 60
```

### 9️⃣ **Nullable Types & Elvis Operator**
```kotlin
var spirit: Spirit? = null           // Can be null

// Safe call (?.)
val name = spirit?.name              // null if spirit is null

// Elvis operator (?:)
val displayName = spirit?.name ?: "No Spirit"

// Let with null check
spirit?.let { 
    println("Found: ${it.name}")
}

// Not-null assertion (!!) - use carefully!
val forcedName = spirit!!.name      // Throws NPE if null
```

### 🔟 **Type Declarations**
```kotlin
// Explicit (clear for APIs, complex cases)
val explorer: Explorer = Explorer("Alice", 50)
fun getPower(): Int = 42

// Implicit (local vars, obvious types)
val name = "Alice"              // Inferred as String
val list = listOf(1, 2, 3)      // Inferred as List<Int>

// Required explicit for nullables
val nullable: String? = null    // Must be explicit
```

---

## 🎮 Game Commands Reference

| Command | Effect | Risk/Reward |
|---------|--------|-------------|
| **1. Explore Room** | Enter new room, possible spirit encounter | Risk: Sanity loss / Reward: Power gain |
| **2. Search Artifacts** | Find magical items | 60% success rate, cursed items possible |
| **3. Ghost Detector** | Scan for spirits | Safe way to interact with spirits |
| **4. Open Box** | Random outcome | High risk, high reward |
| **5. Read Scroll** | Gain power | May crumble to dust |
| **6. Perform Ritual** | Major power boost | Requires 50+ power, can backfire |
| **7. Check Inventory** | View artifacts | No risk |
| **8. Try to Escape** | Win if power ≥ 100 | Lose sanity if fail |

---

## 🏚️ Room Danger Levels

| Room | Danger | Max Power | Strategy |
|------|--------|-----------|----------|
| Kitchen | 1 | 10 | Safe for beginners |
| Library | 2 | 15 | Good start |
| Attic | 3 | 20 | Moderate risk |
| Cellar | 4 | 25 | Higher rewards |
| Master Bedroom | 5 | 30 | Dangerous! |
| Ritual Chamber | 10 | 50 | Expert only! |

---

## 👻 Spirit Types

| Type | Behavior | Power Grant |
|------|----------|-------------|
| **Friendly** | Gives power | 50% of spirit's power |
| **Neutral** | Observes | None |
| **Hostile** | -15 sanity | None |
| **Mischievous** | Random | 0-10 random |

---

## ⚠️ Common Pitfalls & Solutions

| Problem | Solution |
|---------|----------|
| **NullPointerException** | Use safe calls (?.) and Elvis (?:) |
| **Shallow copy issues** | Create deep copies for mutable collections |
| **Type mismatch** | Check nullable vs non-nullable |
| **Reference confusion** | Remember: objects are passed by reference |
| **Missing equals()** | Use data class or override manually |

---

## 📝 Exercise Checklist

- [ ] Create `TrapType` enum with damage property
- [ ] Build `Spell` data class with auto methods
- [ ] Implement `Enchantable` interface
- [ ] Add companion object to Spell class
- [ ] Write nullable handling function
- [ ] Create custom exception handlers
- [ ] Implement deep copy function
- [ ] Show type inference examples
- [ ] **Bonus:** Extend game with 5+ concepts

---

## 🎯 Victory Conditions

**TO WIN:**
- Power Level ≥ 100
- Sanity > 0

**TO LOSE:**
- Sanity ≤ 0 (claimed by spirits!)

**TIPS:**
- Start with safe rooms (Kitchen, Library)
- Build power gradually
- Avoid cursed artifacts
- Use ghost detector before risky actions
- Save rituals for when power > 50

---

## 💡 Quick Debugging

```kotlin
// Print current state
println("Power: ${explorer.powerLevel}, Sanity: ${explorer.sanity}")

// Check if null
println("Spirit is null? ${spirit == null}")

// Check references
println("Same object? ${obj1 === obj2}")

// Check equality
println("Equal content? ${obj1 == obj2}")

// Type checking
println("Is Spirit? ${entity is Spirit}")
```

---

**Remember: In the haunted house, null safety is your best friend! 👻**

*Happy Halloween Coding! 🎃*
