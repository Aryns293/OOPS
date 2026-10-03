# Q42 Association vs Aggregation

**Interview Answer:**
Association: General “uses-a” relationship. Two classes are related but independent.

Aggregation: “Has-a” with weak ownership. The part can exist independently of the whole. Example: Team has Players; players can exist without the team.

Composition: “Has-a” with strong ownership. The part cannot exist without the whole. Example: House has Rooms; rooms don’t exist without the house.

Diagram:

text
Association: A ---> B
Aggregation: A <>-- B (hollow diamond)
Composition: A <#>-- B (filled diamond)
Summary: Aggregation = weak, Composition = strong. Both are “has-a”.
