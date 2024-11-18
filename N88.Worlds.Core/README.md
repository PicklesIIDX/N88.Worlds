# N88.Worlds
A barebones library to manage entities and components for an Entities Components Systems (ECS) architecture.

# Usage

Instantiate a world, create some entities, bind components to them, and have your systems request components for 
operations.

```C#
// your initialization code
var world = new World();
var entity1 = world.CreateEntity();
world.TryBindComponentToEntity(entity1, new MockComponent());
world.TryGetComponentMappedToEntity(entity1, out MockComponent? entity1Component);
entity1Component!.Count.Should().Be(0);

var entity2 = world.CreateEntity();
world.TryBindComponentToEntity(entity2, new MockComponent());
world.TryGetComponentMappedToEntity(entity2, out MockComponent? entity2Component);
entity2Component!.Count.Should().Be(0);

// your system code elsewhere in the codebase that does a write operation
foreach (var component in world.GetComponentsForAllEntities<MockComponent>())
{
    component!.Count += 10;
}

// your system code elsewhere in the codebase that does a read operation
world.TryGetComponentMappedToEntity(entity1, out entity1Component);
entity1Component!.Count.Should().Be(10);

world.TryGetComponentMappedToEntity(entity2, out entity2Component);
entity2Component!.Count.Should().Be(10);
```