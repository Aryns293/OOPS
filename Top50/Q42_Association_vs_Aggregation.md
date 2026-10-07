# Q42 Association vs Aggregation vs Composition

## 🎯 Interview Answer
These three terms define how objects connect to one another in object-oriented design. The key difference lies in **ownership** and **lifecycle dependency**.

---

## 🗣️ What to Say in an Interview (The 3 Concepts)

### 1️⃣ Association (The Umbrella Term)
- **What it is:** A general **"uses-a"** or **"knows-a"** relationship.
- **Ownership:** None. Two classes are related but completely independent of each other.
- **Lifecycle:** Both objects can be created and destroyed independently.
- **Easy Example:** A `Doctor` and a `Patient`. A doctor can see many patients, and a patient can see many doctors. If the doctor leaves the hospital, the patient still exists.

### 2️⃣ Aggregation (Weak Ownership)
- **What it is:** A specialized form of association. It represents a **"has-a"** relationship.
- **Ownership:** Weak. The child object belongs to the parent object, but it can also belong to other objects.
- **Lifecycle:** Independent. The part can exist independently of the whole. If the parent object is destroyed, the child object still exists.
- **Easy Example:** A `Team` and `Players`. A team *has* players. If the team is dissolved, the players still exist independently and can join another team.

### 3️⃣ Composition (Strong Ownership)
- **What it is:** A stricter form of aggregation. It represents a **"part-of"** relationship.
- **Ownership:** Strong. The child object exclusively belongs to the parent object.
- **Lifecycle:** Dependent. The part **cannot** exist without the whole. If the parent object (the whole) is destroyed, the child object (the part) is destroyed with it.
- **Easy Example:** A `House` and `Rooms`. A house *is composed of* rooms. If the house is demolished, the rooms cease to exist.

---

## 💻 Code Examples to Mention

```cpp
// Aggregation (Weak - pass by pointer/reference)
class Team {
    Player* p;  // Team doesn't manage Player's memory
public:
    Team(Player* player) : p(player) {}
};

// Composition (Strong - nested object or managed memory)
class House {
    Room r;  // When House dies, Room dies
public:
    House() { /* Room is automatically created inside House */ }
};
```

---

## 📊 Diagram (UML Notation)
If asked to draw them on a whiteboard:
```text
Association: A ---> B                   (Simple Arrow)
Aggregation: A <>-- B                   (Hollow diamond at 'A', pointing to B)
Composition: A <#>-- B                  (Filled diamond at 'A', pointing to B)
```

---

## 🎯 Summary to Impress
- **Association:** Objects know each other (Doctor & Patient).
- **Aggregation:** Weak "has-a", independent lifecycles (Team & Players).
- **Composition:** Strong "part-of", dependent lifecycles (House & Rooms).
- Use **Aggregation** when parts can be shared or outlive the container.
- Use **Composition** when parts are tightly bound to the container's existence.
