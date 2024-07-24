---
layout: single
title: "Clone Level Devil_Warp"
categories: project
tags: [clone-game, unity]
author_profile: false
search: true
use_math: true
---

When player collides warp object, transform the position to position of warpTarget.

```csharp
[SerializeField] private GameObject player;
[SerializeField] private GameObject particle;
[SerializeField] private Vector3[] warpTarget;
private AudioSource audioSource;
int i = 0;
```

```csharp
void Start(){
    audioSource = GetComponent<AudioSource>();
}

private void OnTriggerEnter2D(Collider2D other){
    if (other.gameObject.CompareTag("Player")){
        StartCoroutine(warpPlayer());
    }
}
```

I made it IEnumerator function since I want to add simple animation. Otherwise, player will just transform to target postion with no animation.

```csharp
    private IEnumerator warpPlayer(){
        audioSource.Play();
        player.gameObject.SetActive(false);
```

Once player collides warp object, set player's active to false.

player become particle when warping, and I added some code for Particle class.

```csharp
GameObject warpForm = Instantiate(particle, transform.position, Quaternion.identity);
Particle moveParticle = warpForm.GetComponent<Particle>();
moveParticle.direction = 4;
moveParticle.targetObject = warpTarget[i];
```

```csharp
// Particle.cs
public Vector3 targetObject;

if (direction == 4){
    Vector2 direction = (targetObject - transform.position).normalized;
    transform.Translate(direction  * (speed * 5) * Time.deltaTime);
}
```

So targetObject in Particle class is assgined by warpTagetPos.

```csharp
        yield return new WaitForSeconds(1f);
        player.gameObject.SetActive(true);

        player.transform.position = warpTarget[i];
        i++;
        if (i >= warpTarget.Length){
            i = 0;
        }
    }

```

After 1 second, player is transformed to target postion and set active to true.

An warp object could warp various postion, so warpTarget is array and once player is transformed to all position in warpTarget, the next index of the target position will be first index.


![des1](/assets/images/2024-06-22-levelDevilClone3/des1.png)


![des2](/assets/images/2024-06-22-levelDevilClone3/des2.png)


![des3](/assets/images/2024-06-22-levelDevilClone3/des3.png)
