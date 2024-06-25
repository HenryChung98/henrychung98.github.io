---
layout: single
title: "Clone Level Devil_Setting"
categories: project
tags: [clone-game]
author_profile: false
search: true
use_math: true
---

Since it is really hard and there are so many things that I have to handle(physics, collision), I decided to remake clone game from scratch with Unity.

### Programming languages / engine used

- C#
- Unity
### Wall Setup

No need to any code for now, just add Rigidboy 2D with gravity scale = 0, freeze rotation and Box Collider 2D.
![des1](/assets/images/2024-06-08-levelDevilClone1/des1.png)

And I added a Material with both of Friction and Bounciness 0 because player object will be stuck when the object attached to the side of the wall.

### Player Setup
Also need Rigidbody 2D with freeze rotation z and Box Collider 2D.

#### Move
You can simply handle horizontal move.

```C#
[SerializeField] private float moveSpeed = 3f;
void Update{
    float horizontalInput = Input.GetAxisRaw("Horizontal");
}
```

I got two sprites for player and it's facing depends on user input. When going right side, facing right and going left, facing left. 

```C#
[SerializeField] private Sprite facingRight;
[SerializeField] private Sprite facingLeft;
private SpriteRenderer spriteRenderer;

void Start(){
    rb = GetComponent<Rigidbody2D>();   
    spriteRenderer = GetComponent<SpriteRenderer>();
    }

void Update{
    if (horizontalInput > 0) // Moving right
    {
        spriteRenderer.sprite = facingRight;
    }
    else if (horizontalInput < 0) // Moving left
    {
        spriteRenderer.sprite = facingLeft;
    }
}
```

And player should not be out of the screen.

```C#
if (transform.position.x <= -8.7f){
    transform.position = new Vector2(-8.7f, transform.position.y);
}

if (transform.position.x >= 8.7f){
    transform.position = new Vector2(8.7f, transform.position.y);
}
if (transform.position.y <= -4.8f){
    transform.position = new Vector2(transform.position.x, -4.8f);
}

if (transform.position.y >= 4.8f){
    transform.position = new Vector2(transform.position.x, 4.8f);
}
```

I gave gravity scale 4 to the player object, and when it falls down, the velocity increases so I want to set the max fall speed.
```C#
[SerializeField] private float maxFallSpeed = -2f;
.
.
.
if (rb.velocity.y < maxFallSpeed)
{
    rb.velocity = new Vector2(rb.velocity.x, maxFallSpeed);
}
```
#### Jump

```C#
[SerializeField] private float jumpForce = 5f;

private void Jump(){
    rb.AddForce(Vector2.up * jumpForce, ForceMode2D.Impulse);
}

```

This code can simply make player jump, but it will be able to jump infinitly. Need to handle that player can jump once player is grounded.

First, need to add Empty object to Player object to check isGrounded at Hierarchy and need Ground object with layer named Ground. I added Ground object at the top of the wall. 

```C#
public Transform groundCheck;
public LayerMask groundLayer;
private bool isGrounded;


isGrounded = Physics2D.OverlapCapsule(groundCheck.position, new Vector2(0.6f, 0.4f), CapsuleDirection2D.Horizontal, 0, groundLayer);

if (Input.GetKeyDown(KeyCode.UpArrow) && isGrounded){
    Jump();
}
```
Physics2D.OverlapCapsule(Vector2 point, Vector2 size, CapsuleDirection2D direction, float angle, int layerMask);

This method is used in Unity to detect all colliders that collide with the capsule-shaped region using a 2D physical engine. It is mainly used to check whether it has touched the ground or to detect collisions within a specific area.

#### Dead

I created empty string with Deat tag, and Box Collider checked isTrigger. 

```C#
private void OnTriggerEnter2D(Collider2D other){
    
    if (other.gameObject.CompareTag("Dead")){
        Destroy(gameObject);
        isDead = true;
    }
}
```

When player collides with Dead, it will just destroy so I want to make simple animation.

I want to create 4 particles and spread it in 4 directions.

```C#
public class Particle : MonoBehaviour
{
    [SerializeField] private float speed = 3f;
    public float direction;
    public Vector3 targetObject;
    
    void Start(){
        Destroy(gameObject, 1f);
    }
    void Update()
    {
        if (direction == 0){
            transform.Translate(Vector2.right * speed * Time.deltaTime);
        }
        if (direction == 1){
            transform.Translate(Vector2.left * speed * Time.deltaTime);
        }
        if (direction == 2){
            transform.Translate(Vector2.up * speed * Time.deltaTime);
        }
        if (direction == 3){
            transform.Translate(Vector2.down * speed * Time.deltaTime);
        }
    }
}
```
The particle is moving depends on the direction and destoryed in 1 second. Now I'll handle the particle in player class.

Create a function that create particle.
```C#
[HideInInspector] public bool isDead;
[SerializeField] private GameObject particle;

private void CreateParticle(int direction){
    GameObject spawnedParticle = Instantiate(particle, transform.position, Quaternion.identity);
    Particle moveParticle = spawnedParticle.GetComponent<Particle>();
    if (moveParticle != null)
    {
        moveParticle.direction = direction;
    }
}
```

and call 4 times in dead.

```C#
CreateParticle(0); 
CreateParticle(1); 
CreateParticle(2);
CreateParticle(3);
```

![des2](/assets/images/2024-06-08-levelDevilClone1/des2.png)


![des3](/assets/images/2024-06-08-levelDevilClone1/des3.png)

### Event
There are many events such as wall moving, instantiating trap and so on. When player passes specific area, event occurs. So I made Box Collider with Event tag. 

To make moving wall, need 2 classes: MoveObject, EventHandler.

EventHandler class passes values that need to move wall, and MoveObject class make an object move depending the passed values. 


EventHandler class
```C#
[SerializeField] private GameObject pObj;
[SerializeField] private bool moving;

[SerializeField] private MoveObject moveObjVar;
[SerializeField] private bool moveUp;
[SerializeField] private bool moveDown;
[SerializeField] private bool moveRight;
[SerializeField] private bool moveLeft;
[SerializeField] private float targetPosX;
[SerializeField] private float targetPosY;
[SerializeField] private float moveSpeed;

private void OnTriggerEnter2D(Collider2D other){
    if (other.gameObject.CompareTag("Player")){
        if (moving){
            moveObjVar.moveSpeed = moveSpeed;
            moveObjVar.isDestruct = isDestruct;
            moveObjVar.waitSeconds = waitSeconds;

            if (moveLeft){
                moveObjVar.moveLeft = true;
                moveObjVar.targetPosX = targetPosX;
            }
            if (moveRight){
                moveObjVar.moveRight = true;
                moveObjVar.targetPosX = targetPosX;
            }
            .
            .
            .
        }
    }
}
```

MoveObject class
```C#
public bool moveLeft;
public bool moveRight;
public bool moveUp;
public bool moveDown;

public float targetPosX;
public float targetPosY;
.
.

void Update(){
     if (moveLeft){
        float move = transform.position.x - moveSpeed * Time.deltaTime;
        transform.position = new Vector2(move, transform.position.y);
        if (transform.position.x <= targetPosX){
            moveLeft = false;
        }
    }

    if (moveRight){
        float move = transform.position.x + moveSpeed * Time.deltaTime;
        transform.position = new Vector2(move, transform.position.y);
        if (transform.position.x >= targetPosX){
            moveRight = false;
        }
    }
    .
    .
    .
}

```

![des4](/assets/images/2024-06-08-levelDevilClone1/des4.png)

![des5](/assets/images/2024-06-08-levelDevilClone1/des5.png)


### Stage Clear

When player is attached a door, considered stage is cleared and move to next stage. 

In player class simply pass boolean value

```C#
if (other.gameObject.CompareTag("Door")){
    clearStage = true;
    gameObject.SetActive(false);
}
```

and GameManager class get this value

```C#
using UnityEngine.SceneManagement; // need this for handling scene

public Player playerVar;
[SerializeField] private string nextStageScene;
private IEnumerator awaitFunction(string act){
    else if (act == "clearStage"){
        yield return new WaitForSeconds(1f);
        SceneManager.LoadScene(nextStageScene);
    }
}

void Update(){
    if (playerVar.clearStage){
        StartCoroutine(awaitFunction("clearStage"));
    }
}

```

Since there is short animation for screen transition, I made the function with await method. You can make reset function with this method When player is dead.


### Audio
Before code, add an audio source in inspector window.

```C#
[SerializeField] private AudioClip[] audioClips; // if more than two audio sources
private AudioSource audioSource;

void Start()
{
    audioSource = GetComponent<AudioSource>();
}

void someEvent(){
    audioSource.clip = audioClips[0]; // switch current audio source
    audioSource.Play();
}