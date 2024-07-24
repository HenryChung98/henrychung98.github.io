---
layout: single
title: "Clone Level Devil_Events"
categories: project
tags: [clone-game, unity]
author_profile: false
search: true
use_math: true
---

### Spawn

Spawner class

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Spawner : MonoBehaviour
{
    [SerializeField] private GameObject obj;
    public float spawnInterval;
    public float[] spawnPosX;
    public float[] spawnPosY;
    public bool activate;
    public float waitSeconds;
    public bool isDestruct;
    public float destructTime;
    private List<GameObject> spawnedObjs = new List<GameObject>();


    void Update(){
        if (activate){
            if (waitSeconds != 0f){
                StartCoroutine(awaitSeconds(waitSeconds, spawnInterval));
                activate = false;
            }
            else{
                StartCoroutine(spawn(spawnInterval));
                activate = false;
            }
        }

    }
```

if waitSeconds is not 0, Spawn object after n seconds.

else, spawn object once is called.

```csharp
void Start()
{
        if (spawnPosX.Length != spawnPosY.Length)
    {
        Debug.LogError("Length of spawnPosX and spawnPosY are different.");
        return;
    }
}
```

If length of spawnPosX and Y are different, notify it and return nothing.

```csharp
private IEnumerator spawn(float interval){
    for (int i = 0; i < spawnPosX.Length; i++){
        Vector2 spawnPos = new Vector2(spawnPosX[i], spawnPosY[i]);
        GameObject newObj = Instantiate(obj, spawnPos, Quaternion.identity);

        spawnedObjs.Add(newObj);
        yield return new WaitForSeconds(interval);
    }
```

Spawn objects on depending on the length of spawnPosX and Y.

```csharp
    if (isDestruct)
    {
        foreach (GameObject spawnedObj in spawnedObjs)
        {
            yield return new WaitForSeconds(destructTime);
            Destroy(spawnedObj);
        }
        spawnedObjs.Clear();
    }
    }
```

Destroy spawned objects if isDestruct is true.

Pretty same except there is await for n seconds.

```csharp
    private IEnumerator awaitSeconds(float second, float interval){
        yield return new WaitForSeconds(second);
        for (int i = 0; i < spawnPosX.Length; i++){
            Vector2 spawnPos = new Vector2(spawnPosX[i], spawnPosY[i]);

            GameObject newObj = Instantiate(obj, spawnPos, Quaternion.identity);

            spawnedObjs.Add(newObj);
            yield return new WaitForSeconds(interval);
        }
        if (isDestruct)
        {
            foreach (GameObject spawnedObj in spawnedObjs)
            {
                yield return new WaitForSeconds(destructTime);
                Destroy(spawnedObj);
            }
            spawnedObjs.Clear();
        }

    }
}
```

### Sizing

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Sizing : MonoBehaviour

    public float targetScaleX = 0f;
    public float targetScaleY = 0f;
    public float scaleSpeed;
    public bool isDestruct;
    public float destructTime;
.
.
.
    void Update()
    if (targetScaleX != 0f)
    {
        // Save currentScale and set newScale.
        float currentScaleX = transform.localScale.x;
        float newScaleX = Mathf.Lerp(currentScaleX, targetScaleX, scaleSpeed * Time.deltaTime);

        // change the scale
        transform.localScale = new Vector3(newScaleX, transform.localScale.y, transform.localScale.z);
    }
    .
    .
    .
```

```csharp
// If it is close enough to the target scale, set the target scale to zero so that it does not continue to convert.

        if (Mathf.Abs(newScaleX - targetScaleX) < 0.01f)
        {
            targetScaleX = 0f;
            if (isDestruct){
                StartCoroutine(Destructor(destructTime));
            }
        }

```

Handling ScaleY is exactly same as this code.
