---
layout: single
title: "Flappy Bird Clone"
categories: project
tags: [clone-game, unity]
author_profile: false
search: true
use_math: true
---

### Background

Rendered two background prefabs and they move to left. When background posX reach to out of the frame, reset posX

```csharp
public class Background : MonoBehaviour
{
    [SerializeField] private float moveSpeed = 5f;

    void Update()
    {
        transform.position += Vector3.left * moveSpeed * Time.deltaTime;
        if (transform.position.x < -2.3f){
            transform.position = new Vector3(20.5f, 1.9f, 0);
            }
    }
}
```

### Player

#### Jump

Player simply jumps when clicked. Unity provides physics features, so I just need to add a Rigidbody 2D component to the player and configure it.

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

When the player goes off the screen or collides with a pipe, it dies.OnTriggerEnter destroys the player if it collides with an object tagged 'Dead'.

```csharp
private void OnTriggerEnter2D(Collider2D other){

        if (other.gameObject.CompareTag("Dead")){
            Destroy(gameObject);
        }
    }
```

### Pipe Spawner

Created a spawner that spawns a pipe at a random Y position within the frame

```csharp
public class Spawner : MonoBehaviour
{
    [SerializeField] private GameObject pipes;
    private float maxY = 2.8f;
    private float minY = -2.6f;

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

### Pipe

The pipe itself gets destroyed when its posX moves outside the frame.

```csharp
public class Pipe : MonoBehaviour
{
    [SerializeField] private float moveSpeed = 1f;
    void Update()
    {
        transform.position += Vector3.left * moveSpeed * Time.deltaTime;
        if (transform.position.x < -4.5f){
            Destroy(gameObject);
        }
    }
}
```

And there is an empty objects which has 'Score' tag between pipes so when player pass between two pipes, user get a score.

![des1](/assets/images/2024-07-23-flappyBirdClone/des1.png)

### Game Manager

#### Scene Load

Scene Load functions(main menu scene, game playing scene(restart))

```csharp
    public void Restart(){
        SceneManager.LoadScene("GameScene");
    }

    public void BackMainMenu(){
        SceneManager.LoadScene("MainScene");
    }
```

Get best score from unity local storage when start.

```csharp
void Start()
    {
        // reset
        score = 0;
        if (scoreText != null){
            scoreText.gameObject.SetActive(true);
        }

        // get value of best score from unity local storage, if null, set to 0
        bestScore = PlayerPrefs.GetInt("BestScore", 0);
    }
```

Declare a toggle function which switches isPaused boolean variable, and this variable is checked in update function.

```csharp
    public void TogglePause()
    {
        isPaused = !isPaused;
        pausePanel.gameObject.SetActive(isPaused);
    }
```

In Update function, check isPaused, is Player dead, and convert score text to string.

```csharp
public class Score : MonoBehaviour
{
    void Update()
    {
        scoreText.text = score.ToString();

        Time.timeScale = isPaused ? 0 : 1;

        if (!player){
            GameOver();
        }
    }
}
```

This function is called when player pass between the pipes.

```csharp
public void AddScore()
    {
        score++;
    }
```

When gameover, check is current score greater than best score, and if yes, update it.

```csharp
 private void GameOver(){
        scoreText.gameObject.SetActive(false);
        endScoreText.text = score.ToString();
        if (score > bestScore){
            bestScore = score;
            newRecord.gameObject.SetActive(true);
            PlayerPrefs.SetInt("BestScore", bestScore);
        }
        bestScoreText.text = bestScore.ToString();

        // hide pause button
        PauseBtn.gameObject.SetActive(false);
        // show game over panel
        panel.SetActive(true);

```

Four different medals are displayed depending on the score.

```csharp
        if (score >= 40){
            Medal.sprite = platinum;
        }
        else if (score >= 30){
            Medal.sprite = gold;
        }
         else if (score >= 20){
            Medal.sprite = silver;
        }
         else if (score >= 10){
            Medal.sprite = bronze;
        }
        else{
            // if score is less than 10, no medal
            Medal.gameObject.SetActive(false);
            Medal.sprite = null;
        }
    }
```

Before the application quits, save best score on local storage

```csharp
    void OnApplicationQuit()
    {
        PlayerPrefs.SetInt("BestScore", bestScore);
    }
```
