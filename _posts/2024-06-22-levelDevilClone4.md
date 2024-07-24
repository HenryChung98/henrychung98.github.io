---
layout: single
title: "Clone Level Devil_Saw Blade"
categories: project
tags: [clone-game, unity]
author_profile: false
search: true
use_math: true
---

### Saw Blade

I want to make saw blade to rotate everytime.

```csharp
public class SawBlade : MonoBehaviour
{
private float rotationAngle = 20f;

    void Start()
    {
        InvokeRepeating("Rotate", 0.05f, 0.05f);
    }

    void Rotate()
    {

        transform.Rotate(0, 0, rotationAngle);
    }
}
```

InvokeReating is called "Rotate" function every 50 milliseconds.

But if I add event collider, there is a problem.

Since this object rotates every 50 milliseconds, event object also rotates if I add event collider in the saw object. So I made empty object named SawObj and add saw blade object, event object, and so on in that.

### Pace

```csharp
public float[] targetPosX;
public float moveSpeed = 3f;
private int direction = 1;
```

Need two very end positions.

```csharp
if (transform.position.x <= targetPosX[0]){
    direction = -1;
}
else if (transform.position.x >= targetPosX[1]){
    direction = 1;
}
```

If saw blade is attached targetPos which are very end, change the direction.

```csharp
float move = transform.position.x - direction * moveSpeed * Time.deltaTime;
transform.position = new Vector2(move, transform.position.y);
```

It moves continuosly.
