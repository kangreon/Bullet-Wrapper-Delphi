# Bullet Wrapper Delphi
Это объектно-ориентированная обертка над библиотекой [Bullet Physics SDK](https://github.com/bulletphysics/bullet3/) для языка программирования Delphi.

[Bullet Physics SDK](https://github.com/bulletphysics/bullet3/): real-time collision detection and multi-physics simulation for VR, games, visual effects, robotics, machine learning etc.

## License

## Сборка библиотеки BulletWD.dll 
Для сборки библиотеки *BulletWD* понадобится [CMake](https://cmake.org/download/) и *Visual Studio 2012* (для примера). 
Выполните следующие шаги:
 1. Создайте на диске *D:\\* папку с именем *BulletGame* (для примера).
 2. Скачайте последнюю версию библиотеки [Bullet Wrapper Delphi](https://github.com/kangreon/Bullet-Wrapper-Delphi/archive/master.zip) и распакуйте ее. Должна получиться такая структура папок: D:\BulletGame\ [ bullet3-master, BulletWD, BulletWD_DLL]
 2. Скачайте [Bullet Physics SDK](https://github.com/bulletphysics/bullet3/) и распакуйте в папку *D:\BulletGame\\*, чтобы **Bullet Physics SDK** оказался в папке *bullet3-master*.
 3. При помощи [CMake](https://cmake.org/download/) сгенерируйте файлы проекта для Visual Studio 2012 (для примера) из папки *D:\BulletGame\bullet3-master* в папку *D:\BulletGame\bullet3-master\build*.
 4. Откройте проект *D:\BulletGame\bullet3-master\build\ALL_BUILD.vcxproj* и выполните построение **ALL_BUILD**.
 5. Откройте решение *D:\BulletGame\BulletWD_DLL\BulletWD.sln* и выполните построение **BulletWD**. Если построение прошло успешно, в папке *D:\BulletGame\BulletWD_DLL\Debug\\* найдете необходимую библиотеку **BulletWD.dll**.

## Пример использования
В данный момент BulletWD можно использовать в своих проектах на языке программирования Delphi, в версии среды разработки Embarcadero® Delphi XE и новее под операционной системой Windows. В перспективе, можно портировать под FreePascal. 
Чтобы узнать, как использовать **BulletWD** с языком программирования *Delphi* в среде программирования *Embarcadero® Delphi XE7* воспользуйтесь следующей инструкцией:

 1. Скачайте последнюю версию библиотеки [Bullet Wrapper Delphi](https://github.com/kangreon/Bullet-Wrapper-Delphi/archive/master.zip).
 2. Распакуйте в любое удобное для вас место на жестком диске, например *D:\BulletGame\*.
 3. Выполните построение библиотеки BulletWD.dll или скачайте готовый бинарник.
 4. Запустите демонстрационный **Delphi** проект *D:\BulletGame\BulletWD\Bullet.dproj* в среде *Delphi*.
 5. Если необходимо, поменяйте путь к библиотеки BulletWD.dll в файле *Bullet\BulletBase.pas*. Путь указывается в константе **BulletDll**.
 6. Выполните построение демонстрационного проекта.

Если все прошло без проблем, вы увидите демонстрационное приложение, выводящее различные примитивы, которые взаимодействуют между собой при помощи **Bullet Physics**.
В своем проекте вам нужно подключить все модули из папки *D:\BulletGame\BulletWD\Bullet\\* и указать путь к библиотеке **BulletWD.dll**.

## Objects with a complete wrapper

## Пример
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
Для просмотра полного примера, воспользуйтесь инструкцией в разделе **Пример использования**.
