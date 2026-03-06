---
layout: default
---

# Session Plan

2.5 hours in total: lecture + practical

- Lecture (first 30-45 mins)
- Practical session working through course material
  - Demonstrators available to answer questions

---

# Programme Structure

<v-clicks>

- Many ways to structure the same programme
- Important because it affects:
  - Maintainability
  - Extensibility
- No substitute for proper planning:
  - What entities do we need to represent?
  - What data do we need about them?
  - How are those entities related?

</v-clicks>

---
layout: two-cols
---

# Example: Astrophysics

```python
temperature = 0
steps = int(1e8)

for _ in range(steps):
    gas = initialise_gas(temperature)
    photons = generate_photons()
    temperature += calculate_temperature(gas, photons)

print(f"Temperature is: {temperature}")
```

::right::

<div class="pl-32">

```mermaid {scale: 0.7}
flowchart TD
    A["initialise gas"] --> B["generate photons"]
    B --> C["calculate temperature"]
    C --> D{"more steps?"}
    D -- yes --> A
    D -- no --> E["print result"]
```
</div>

---
layout: two-cols
---

# Example: Astrophysics

```python
temperature = 0
steps = int(1e8)
photon_source = "Black hole"

for _ in range(steps):
    gas = initialise_gas(temperature)
    if photon_source == "Black hole":
        photons = generate_photons_black_hole()
    elif photon_source == "White dwarf":
        photons = generate_photons_white_dwarf()
    temperature += calculate_temperature(gas, photons)

print(f"Temperature is: {temperature}")
```

<v-clicks>

- Expand to a new use case
- Add another photon source while reusing existing logic

</v-clicks>

::right::

<div class="pl-16">

```mermaid {scale: 0.5}
flowchart TD
    A["initialise gas"] --> B{"photon source?"}
    B -- black hole --> C1["generate black hole photons"]
    B -- white dwarf --> C2["generate white dwarf photons"]
    C1 --> D["calculate temperature"]
    C2 --> D
    D --> E{"more steps?"}
    E -- yes --> A
    E -- no --> F["print result"]
```

</div>

---
layout: two-cols
---

# Example: Astrophysics

```python
temperature = 0
steps = int(1e8)
photon_source = "Black hole"
temperature_model = "Matthews"

for _ in range(steps):
    gas = initialise_gas(temperature)
    if photon_source == "Black hole":
        photons = generate_photons_black_hole()
    elif photon_source == "White dwarf":
        photons = generate_photons_white_dwarf()

    if temperature_model == "Matthews":
        temperature += calculate_temperature_matthews(gas, photons)
    elif temperature_model == "Sims":
        temperature += calculate_temperature_sims(gas, photons)

print(f"Temperature is: {temperature}")
```

<v-clicks>

- Modify existing behavior for another model
- Branching starts to spread through core loops

</v-clicks>

::right::

<div class="pl-32">

```mermaid {scale: 0.43}
---
config:
  flowchart:
    nodeSpacing: 8
    rankSpacing: 20
---
flowchart TD
    A["initialise gas"] --> B{"photon source?"}
    B -- black hole --> C1["generate black hole photons"]
    B -- white dwarf --> C2["generate white dwarf photons"]
    C1 --> D{"temperature model?"}
    C2 --> D
    D -- Matthews --> E1["calculate temperature Matthews"]
    D -- Sims --> E2["calculate temperature Sims"]
    E1 --> F{"more steps?"}
    E2 --> F
    F -- yes --> A
    F -- no --> G["print result"]
```

</div>

---
layout: two-cols
---

# Example: University Department

<v-clicks>

- Toy model: simple but illustrative
- <span class="font-bold">Purpose</span>: record papers written by the department
- Data and behavior are separate:
  - `academics` and `papers` store state
  - `write_paper()` modifies that state

</v-clicks>

::right::

```python
academics = []
papers = []

def write_paper(academics, papers, academic, paper):
    academics.append(academic)
    papers.append(paper)

write_paper(academics, papers, "Sam Mangham", "Mangham2018")
write_paper(academics, papers, "Steve Crouch", "Crouch2016")
```

---
layout: two-cols
---

# Example: University Department

- Clear split between <span class="text-[#1f5f99] font-semibold">data</span> and <span class="text-[#2f7d32] font-semibold">functions</span>

<div class="mt-8">

```mermaid {theme: 'neutral', scale: 0.9}
---
config:
  themeCSS: |
    .node rect { rx: 18px; ry: 18px; }
    .cluster rect { rx: 24px; ry: 24px; }
---
flowchart TB
    subgraph D1["Data"]
      direction TB
      A1["<b>Academics:</b><br/>Sam Mangham<br/>Steve Crouch"]
      P1["<b>Papers:</b><br/>Mangham2018<br/>Crouch2016"]
    end

    W1["Write paper"]
    D1 -.-> W1

    classDef data fill:#9dc3e6,stroke:#5d87b8,color:#000
    classDef func fill:#a9d08e,stroke:#6e9458,color:#000
    class D1,A1,P1 data
    class W1 func
```

</div>

::right::

```python
academics = []
papers = []

def write_paper(academics, papers, academic, paper):
    academics.append(academic)
    papers.append(paper)

write_paper(academics, papers, "Sam Mangham", "Mangham2018")
write_paper(academics, papers, "Steve Crouch", "Crouch2016")
```

---
layout: two-cols
---

# Example: University Department

- <span class="text-[#1f5f99] font-semibold">Data</span> meaning becomes unclear!

<div class="mt-8">

```mermaid {theme: 'neutral', scale: 0.9}
---
config:
  themeCSS: |
    .node rect { rx: 18px; ry: 18px; }
    .cluster rect { rx: 24px; ry: 24px; }
---
flowchart TB
    subgraph D2["Data"]
      direction TB
      A2["<b>Academics:</b><br/>Sam Mangham<br/>Steve Crouch<br/><span style='color:#b91c1c;font-weight:700'>Steve Crouch</span>"]
      P2["<b>Papers:</b><br/>Mangham2018<br/>Crouch2016<br/>Crouch2023"]
    end

    W2["Write paper"]
    D2 -.-> W2

    classDef data fill:#9dc3e6,stroke:#5d87b8,color:#000
    classDef func fill:#a9d08e,stroke:#6e9458,color:#000
    class D2,A2,P2 data
    class W2 func
```

</div>

::right::

```python
academics = []
papers = []

def write_paper(academics, papers, academic, paper):
    academics.append(academic)
    papers.append(paper)

write_paper(academics, papers, "Sam Mangham", "Mangham2018")
write_paper(academics, papers, "Steve Crouch", "Crouch2016")
write_paper(academics, papers, "Steve Crouch", "Crouch2023")
```

---
layout: two-cols
---

# Object-Oriented Programming (OOP)

<v-clicks>

- Procedural style often separates structured <span class="text-[#1f5f99] font-semibold">data</span> from the <span class="text-[#2f7d32] font-semibold">operations</span> on them
- OOP puts state and behavior into classes
- Procedural design thinks about task flow
- OOP design starts from entities (objects) and their relationships
- Classes define interfaces for safe and consistent interaction with <span class="text-[#1f5f99] font-semibold">data</span>

</v-clicks>

::right::

<div class="h-full flex items-start justify-center pl-8">

```mermaid {scale: 1.1}
---
config:
  themeVariables:
    fontSize: 13px
  themeCSS: |
    .node rect { rx: 18px; ry: 18px; }
    .cluster rect { rx: 24px; ry: 24px; }
---
flowchart TB
    subgraph P["Procedural Programming"]
      direction LR
      D1["Data"] ~~~ F1["Functions"]
    end

    subgraph O["Object-Oriented Programming"]
      direction TB
      subgraph C["Class Functions"]
        D2["Data"]
      end
    end

    P ~~~ O

    style P fill:none,stroke:none
    style O fill:none,stroke:none
    style C fill:#a9d08e,stroke:#6e9458,stroke-width:2px,color:#000
    classDef data fill:#9dc3e6,stroke:#5d87b8,stroke-width:2px,color:#000
    classDef func fill:#a9d08e,stroke:#6e9458,stroke-width:2px,color:#000
    class D1,D2 data
    class F1 func
```

</div>

---
layout: two-cols
---

# Encapsulation

<v-clicks>

- Classes bundle related <span class="text-[#1f5f99] font-semibold">data</span> and <span class="text-[#2f7d32] font-semibold">functions</span> (<span class="text-[#2f7d32] font-semibold">methods</span>) together
- Classes are blueprints of the entities you represent
- <span class="font-semibold text-gray-700">Objects</span> are instances of classes
- Objects can share behaviour while storing different <span class="text-[#1f5f99] font-semibold">data</span> and states

</v-clicks>

::right::

<div class="h-full flex flex-col items-center pl-6">
<div class="text-center w-[88%] mb-2 text-[15px] leading-tight font-normal">Procedural Programming</div>

<div class="w-[88%] flex justify-center">

```mermaid {scale: 0.62}
---
config:
  themeVariables:
    fontSize: 13px
  flowchart:
    nodeSpacing: 12
    rankSpacing: 20
  themeCSS: |
    .node rect { rx: 18px; ry: 18px; }
    .cluster rect { rx: 22px; ry: 22px; }
---
flowchart TB
    subgraph PP[" "]
      direction LR
      A1["<b>Academics:</b><br/>Sam Mangham<br/>Steve Crouch<br/><span style='color:#b91c1c;font-weight:700'>Steve Crouch</span>"]
      P1["<b>Papers:</b><br/>Mangham2018<br/>Crouch2016<br/>Crouch2023"]
      W1["Write paper"]
      A1 ~~~ P1 ~~~ W1
    end

    style PP fill:none,stroke:none
    classDef data fill:#9dc3e6,stroke:#5d87b8,color:#000
    classDef funcs fill:#a9d08e,stroke:#6e9458,color:#000
    class A1,P1 data
    class W1 funcs
```

</div>

<div class="text-center w-[88%] mb-2 text-[15px] leading-tight font-normal">Object-Oriented Programming</div>

<div class="w-[88%] flex justify-center">

```mermaid {scale: 0.62}
---
config:
  themeVariables:
    fontSize: 14px
  flowchart:
    nodeSpacing: 12
    rankSpacing: 20
  themeCSS: |
    .node rect { rx: 18px; ry: 18px; }
    .cluster rect { rx: 22px; ry: 22px; }
---
flowchart TB
    subgraph C1["Academic Class"]
      direction LR
      N1["Name"]
      P2["Papers"]
      W2["Write<br/>paper"]
      N1 ~~~ P2 ~~~ W2
    end

    style C1 fill:#b8b8b8,stroke:#666,color:#000,stroke-width:2px
    classDef data fill:#9dc3e6,stroke:#5d87b8,color:#000
    classDef funcs fill:#a9d08e,stroke:#6e9458,color:#000
    class N1,P2 data
    class W2 funcs
```

</div>

<div class="mt-3 w-full flex flex-col gap-2 items-center">
<div class="w-[88%] flex justify-center">

```mermaid {scale: 0.54}
---
config:
  themeVariables:
    fontSize: 14px
  flowchart:
    nodeSpacing: 10
    rankSpacing: 24
    subGraphTitleMargin:
      bottom: 10
  themeCSS: |
    .node rect { rx: 18px; ry: 18px; }
    .cluster rect { rx: 22px; ry: 22px; }
---
flowchart TB
    subgraph O1["Academic Object"]
      direction LR
      N2["Sam<br/>Mangham"]
      P3["Mangham2018"]
      W3["Write<br/>paper"]
      N2 ~~~ P3 ~~~ W3
    end

    style O1 fill:#d0d0d0,stroke:#777,color:#000,stroke-width:2px
    classDef data fill:#9dc3e6,stroke:#5d87b8,color:#000
    classDef funcs fill:#a9d08e,stroke:#6e9458,color:#000
    class N2,P3 data
    class W3 funcs
```

</div>
<div class="w-[88%] flex justify-center">

```mermaid {scale: 0.54}
---
config:
  themeVariables:
    fontSize: 14px
  flowchart:
    nodeSpacing: 10
    rankSpacing: 18
    subGraphTitleMargin:
      bottom: 10
  themeCSS: |
    .node rect { rx: 18px; ry: 18px; }
    .cluster rect { rx: 22px; ry: 22px; }
---
flowchart TB
    subgraph O2["Academic Object"]
      direction LR
      N3["Steve<br/>Crouch"]
      P4["Crouch2016<br/>Crouch2023"]
      W4["Write<br/>paper"]
      N3 ~~~ P4 ~~~ W4
    end

    style O2 fill:#d0d0d0,stroke:#777,color:#000,stroke-width:2px
    classDef data fill:#9dc3e6,stroke:#5d87b8,color:#000
    classDef funcs fill:#a9d08e,stroke:#6e9458,color:#000
    class N3,P4 data
    class W4 funcs
```

</div>
</div>
</div>

---
layout: two-cols
---

# Defining a Class in Python

<v-clicks>

- A class is a definition: a template for creating objects
- `__init__` runs when an object is created
- `self` refers to the specific object being operated on

</v-clicks>

::right::

```python {none|1|2-4|2-4,6-7}{at:1}
class Academic:
    def __init__(self, name):
        self.name = name
        self.papers = []

    def write_paper(self, title):
        self.papers.append(title)
```

---
layout: two-cols
---

# Creating Objects

<v-clicks>

- Objects are instances of a class
- Each object has its own independent state
- Same class, different data
- `Academic` is the class; `sam` and `steve` are objects
- Think of `sam.write_paper("X")` calls `Academic.write_paper(sam, "X")`

</v-clicks>

::right::

```python
sam = Academic("Sam Mangham")
sam.write_paper("Mangham2018")

steve = Academic("Steve Crouch")
steve.write_paper("Crouch2016")
steve.write_paper("Crouch2023")

print(sam.papers)    # ["Mangham2018"]
print(steve.papers)  # ["Crouch2016", "Crouch2023"]
```

---
layout: two-cols
---

# Defining a Class in C++

<v-clicks>

- C++ enforces type safety and access control at compile time
- Data members are private by default in robust class design

</v-clicks>

::right::

```cpp
#include <string>
#include <utility>
#include <vector>

class Academic {
 public:
  explicit Academic(std::string name) : name(std::move(name)) {}

  void write_paper(const std::string& title) {
    papers.push_back(title);
  }

 private:
  std::string name;
  std::vector<std::string> papers;
};
```

```cpp
Academic sam("Sam Mangham");
sam.write_paper("Mangham2018");
```

---
layout: two-cols
---

# Entity Diagrams

<v-clicks>

- Consider the entities in your problem
  - What do they do?
  - What properties do they have?
  - How do they relate?
- Let us consider a university department...

</v-clicks>

::right::

<div v-click>

```mermaid
---
config:
  themeCSS: |
    .block rect { rx: 18px; ry: 18px; }
  block:
    padding: 40
---
block-beta
  columns 5
  space space Office["Office"] space space
  space space space space space
  Admin["Admin"] space PhD["PhD Student"] space Lecturer["Lecturer"]
  space space space space space
  space space Papers["Papers"] space Courses["Courses"]

  Admin -- "Has" --> Office
  PhD -- "Has" --> Office
  Lecturer -- "Has" --> Office
  PhD -- "Writes" --> Papers
  Lecturer -- "Writes" --> Papers
  Lecturer -- "Teaches" --> Courses

  classDef cls fill:#c7ddf2,stroke:#5d87b8,color:#000
  classDef obj fill:#d6e6cf,stroke:#6e9458,color:#000
  class Office,Admin,PhD,Lecturer cls
  class Papers,Courses obj
```

</div>

---
layout: two-cols
---

# Inheritance and Composition

<v-clicks>

- Inheritance models an "is-a" relationship
- Composition models a "has-a" relationship
- Use inheritance only for true subtype relationships, not code reuse

</v-clicks>

::right::

<div class="pl-32">

```plantuml
@startuml
!theme spacelab
skinparam classAttributeIconSize 0

together {
  class Person {
    +name
    +office
  }
  class Paper {
    +title
    +text
  }
}

class Admin
class Academic {
  +papers
  +write_paper()
}
class PhDStudent {
  +graduate()
}
class Lecturer {
  +courses
  +teach_course()
}

Person -r[hidden]- Paper

Person <|-- Admin
Person <|-- Academic
Academic <|-- PhDStudent
Academic <|-- Lecturer
Academic *-- Paper : writes
@enduml
```

</div>

---
layout: two-cols
---

# Inheritance and Composition

<v-clicks>

- A similar problem can be modelled with composition instead
- Think of `Author` and `Instructor` as roles
- This avoids deep inheritance chains
- Pick the design with the clearest maintenance path

</v-clicks>

::right::

<div class="pl-16">

```plantuml
@startuml
!theme spacelab
skinparam classAttributeIconSize 0

together {
  class Person {
    +name
    +office
  }
  class Author {
    +papers
    +write_paper()
  }
}

class Instructor {
  +courses
  +teach_course()
}

class Admin
class Academic
class Lecturer
class Librarian

Person -r[hidden]- Author

Person <|-- Admin
Person <|-- Academic
Admin <|-- Librarian
Academic <|-- Lecturer

Academic *-r- Author : has role
Librarian *-u- Instructor : has role
Lecturer *-u- Instructor : has role
@enduml
```

</div>

---
layout: two-cols
---

# Diamond inheritance

<v-clicks>

- Multiple inheritance can create ambiguous paths
- Which parent's method gets called?
- Languages handle this differently:
  - Python: Method Resolution Order (MRO)
  - C++: virtual inheritance
- This complexity is a key reason to prefer composition if possible

</v-clicks>

::right::

<div class="pl-8">

```plantuml
@startuml
!theme spacelab
skinparam classAttributeIconSize 0

class Person {
  +name
}

class Academic {
  +write_report()
}

class Admin {
  +write_report()
}

class DeptHead

Person <|-- Academic
Person <|-- Admin
Academic <|-- DeptHead
Admin <|-- DeptHead

note right of DeptHead : Which write_report()?
@enduml
```

</div>

---
layout: two-cols
---

# Polymorphism

<v-clicks>

- Same interface, different implementations
- Abstract classes/interfaces are not instantiated directly
- Concrete subclasses provide behaviour-specific overrides

</v-clicks>

::right::

<div class="pl-10">

```plantuml
@startuml
!theme spacelab
skinparam classAttributeIconSize 0

abstract class Academic {
  +papers
  +write_paper()
  {abstract} +describe_duty()
}

class PhDStudent {
  +describe_duty()
}

class ResearchSoftwareEngineer {
  +write_paper()
  +describe_duty()
}

Academic <|-- PhDStudent
Academic <|-- ResearchSoftwareEngineer
@enduml
```

</div>

---
layout: two-cols
---

# Example: Object-Oriented Redesign

<v-clicks>

- Abstract base class defines the interface
- Concrete subclasses provide specific behaviour
- No `if/elif` branching needed: just swap the subclass

</v-clicks>

::right::

```python {all|1-3|5-8,10-13|all}{at:1}
class PhotonSource:
    def generate(self):
        raise NotImplementedError

class BlackHole(PhotonSource):
    def generate(self):
        # black hole photon generation
        return photons

class WhiteDwarf(PhotonSource):
    def generate(self):
        # white dwarf photon generation
        return photons
```

---

# Example: Object-Oriented Redesign

```plantuml
@startuml
!theme spacelab
skinparam classAttributeIconSize 0
skinparam ArrowFontColor #446e9b
scale 0.84

abstract class TemperatureModel {
  +calculate_temperature(gas, photons)
}
class MatthewsModel {
  +calculate_temperature(gas, photons)
}
class SimsModel {
  +calculate_temperature(gas, photons)
}

abstract class PhotonSource {
  +generate()
}
class BlackHole {
  +generate()
}
class WhiteDwarf {
  +generate()
}

class GasCloud {
  -temperature_model: TemperatureModel
  +temperature
  -structure
  +calculate_temperature(photons)
  +calculate_structure()
}

TemperatureModel <|-- MatthewsModel
TemperatureModel <|-- SimsModel
PhotonSource <|-- BlackHole
PhotonSource <|-- WhiteDwarf

GasCloud *-- TemperatureModel : has-a
GasCloud ..> PhotonSource : uses
@enduml
```

---
layout: two-cols
---

# Example: Object-Oriented Redesign

<v-clicks>

- Polymorphism: `PhotonSource` is abstract
- Composition: `GasCloud` owns a temperature model
- Encapsulation: temperature logic and state live inside `GasCloud`
- Inheritance: `SimsModel` is a temperature model

</v-clicks>

::right::

```python
steps = int(1e8)
photon_source = BlackHole()
gas_cloud = GasCloud(
    temperature_model=MatthewsModel(),
    start_temperature=0,
)

for _ in range(steps):
    gas_cloud.calculate_structure()
    photons = photon_source.generate()
    gas_cloud.calculate_temperature(photons)

print(f"Temperature is: {gas_cloud.temperature}")
```

---

# Today's Session

- Python (or C++)
  - Classes
- Design concepts
  - Encapsulation
  - Composition
  - Inheritance
  - Polymorphism

<div v-click class="mt-4 border border-teal-500 rounded p-3 text-sm text-teal-700">
OOP is one paradigm among many. Model your problem and choose the simplest design that keeps changes local and behaviour explicit.
</div>
