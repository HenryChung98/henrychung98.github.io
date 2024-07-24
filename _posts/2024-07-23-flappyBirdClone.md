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

### Score

First I created GameManager script and I will handle score in this script.

```csharp
using TMPro; // to handle text

public class GameManager : MonoBehaviour
{
    public int score;
    public TextMeshProUGUI scoreText;
    public static GameManager instance;
    void Awake()
        {
            if (instance == null)
            {
                instance = this;
                
            }
        }
    void Start()
    {
        score = 0;
    }
    void Update()
    {
        scoreText.text = score.ToString();
    }
    public void AddScore()
    {
        score++;

    }
}
```

And created Score script to check whether player pass between the pipes.

```csharp
public class Score : MonoBehaviour
{
    void Update()
    {

    }

    private void OnTriggerEnter2D(Collider2D other){

        if (other.gameObject.CompareTag("Player")){
            GameManager.instance.AddScore();
        }
    }
}
```

![des2](/assets/images/2024-07-23-flappyBirdClone/des2.png)

### Main Scene

I wanted to make a button to start the game.

Create a MainScene roughly with start button and when the button clicked, game is started. Code is really short.

```csharp
using UnityEngine.SceneManagement; // need this to handle scene

public class SceneLoader : MonoBehaviour
{
public void LoadGameScene()
    {
        SceneManager.LoadScene("GameScene");
    }
}
```

![des4](/assets/images/2024-07-23-flappyBirdClone/des4.png)

### Game Over

I created panel, score, best score and button and combine in a empty object named GameOver. This was deactivated and when player dies, it wil be activated and when button is clicked, load the gamescene so that you can re-start it.

![des3](/assets/images/2024-07-23-flappyBirdClone/des3.png)

##### Learned New

I found that 'PlayerPrefs' which is database offered by Unity so you can save data permanently.

I will handle best score with this method.

```csharp
void Start()
{
    // read best score from database, 0 is default value
    bestScore = PlayerPrefs.GetInt("BestScore", 0);
}
.
.
.
// set best score
if (score > bestScore){
    bestScore = score;
    PlayerPrefs.SetInt("BestScore", bestScore);
}
bestScoreText.text = "Best Score: " + bestScore.ToString();
.
.
// this will be executed when user quit the game
void OnApplicationQuit(){
    PlayerPrefs.SetInt("BestScore", bestScore);
}
```