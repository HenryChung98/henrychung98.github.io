---
layout: single
title: "Flappy Bird Clone"
categories: project
tags: [clone-game, unity]
author_profile: false
search: true
use_math: true
---

### Programming languages / engine used

- C#
- Unity


### Background Move

I got two same background components, and they move right to left. When the backgrounds pass certain position, move back to right.


```csharp
public class Background : MonoBehaviour
{
    [SerializeField] private float moveSpeed = 5f;

    void Update()
    {
         transform.position += Vector3.left * moveSpeed * Time.deltaTime;
        if (transform.position.x < 0.6f){
            transform.position = new Vector3(24.45f, -1.8f, 0);
            }
    }
}
```


### Player

#### Jump
Player is simply when clicked, it jumps. Unity offers physics thing, so I just need to add Rigidbody 2D to player component and set.

```csharp
public class Player : MonoBehaviour
{
    [SerializeField] private float jumpForce = 3f; 
    private Rigidbody2D rb;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        if (Input.GetMouseButtonDown(0)) // mouse-left click
        {
            Jump();
        }
    }

    void Jump()
    {
        rb.velocity = Vector2.up * jumpForce;
    }
}
```
#### Collision 

When player goes to out of the screen or collide pipe, it dies. Write code for triggerEnter that if it collides an object which has tag 'Dead', destroyed.

```csharp
private void OnTriggerEnter2D(Collider2D other){
    
        if (other.gameObject.CompareTag("Dead")){
            Destroy(gameObject);
        }
    }
```

And I added two empty object which has collider and 'Dead' tag and place at the top and bottom of the screen.

### Pipe

#### Spawn

Now need to handle pipe. There are two pipes and there is an empty objects which has 'Score' tag so when player pass between two pipes, user get a score.

![des1](/assets/images/2024-07-23-flappyBirdClone/des1.png)

And add edge collider for pipes and 'Dead' tag as well.

After, I added spawner to spawn pipes, and pipes will be spawned at random Y position at every 3 seconds.

```csharp
public class Spawner : MonoBehaviour
{
    [SerializeField] private GameObject pipes;
    private float maxY = 3.3f;
    private float minY = -0.8f;
    
    void Start()
    {
        StartCoroutine(SpawnPipe());
    }

    private IEnumerator SpawnPipe(){
        while (true){
            float spawnY = Random.Range(minY, maxY);

            Instantiate(pipes, new Vector3(transform.position.x, spawnY, transform.position.z), Quaternion.identity);
            yield return new WaitForSeconds(3f);
        }
    }
}
```
#### Move

And pipe should move to left. Pretty same idea as background, but it should be destory if it goes to out of the screen. Otherwise, memory leak is occured.

```csharp
public class Pipe : MonoBehaviour
{
    [SerializeField] private float moveSpeed = 5f;
    void Update()
    {
        transform.position += Vector3.left * moveSpeed * Time.deltaTime;
        if (transform.position.x < -7.5f){
            Destroy(gameObject);
        }
    }
}
```