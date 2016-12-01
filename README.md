# Bullet-Wrapper-Delphi
Object-oriented wrapper for Delphi programming language.

## License

## Build instructions for library

## How to use the wrapper

## Objects with a complete wrapper

## Example
Create a dynamic rigidbody:
```
  begin
    ColShape := TSphereShape.Create(1);
    FCollisionShapes.Add(ColShape);

    /// Create Dynamic Objects
    StartTransform := TTransform.Identity;
    Mass := 1;

    //rigidbody is dynamic if and only if mass is non zero, otherwise static
    IsDynamic := Mass <> 0;

    LocalInertia := TPoint3D.Create(0, 0, 0);

    if IsDynamic then
      ColShape.CalculateLocalInertia(Mass, LocalInertia);

    startTransform.SetOrigin(TPoint3D.Create(2, 10, 0));

    //using motionstate is recommended, it provides interpolation capabilities,
    //and only synchronizes 'active' objects
    MyMotionState := TDefaultMotionState.Create(StartTransform);
    RbInfo := TRigidBodyConstructionInfo.Create(Mass, MyMotionState, ColShape, LocalInertia);
    Body := TRigidBody.Create(RbInfo);

    FDynamicsWorld.AddRigidBody(Body);
  end;
```
For viewing of a complete example open the SimpleDemo project.
