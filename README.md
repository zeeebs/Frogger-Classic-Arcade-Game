# Frogger---Classic-Arcade-Game
Recreation of the Classic Arcade Game: Frogger

This project was created using C# and Unity. It showcases player input for movement, enemy collisions, life counter, scene switches, sound effects and music, and custom graphics. 

After completing the Tech Academy's C# and Unity Course of the Game Developer Bootcamp, I collaborated with my fellow students for two weeks to develop full-scale classic arcade games using the aformentioned software. Working on a piece of a larger project provided a great learning environment for working within an existing product, and experience integrating my work into the larger product. I got to operate in the capacity of a professional developer, and experience how they work with the time, resources, and customer stories they have. Since each person worked on a different game, I got to develop every back-end and front-end detail of my game. I am extremely proud I get to say that virtually every aspect of Frogger is my own work. I learned the value of utilizing my resources to the fullest extent to complete my project, including using my instructor, who helped me through many bugs and Unity issues. Over the two week sprint, I also had the opportunity to work on project management and team programming skills that I'm confident and excited to use on future projects.

Below are descriptions of the stories I worked on, along with code snippets code files, and final product images.
<ul>
<li><a href="#Player Controlls">Player Controlls</a></li>
<li><a href="#Player Movement">Player Movement</a></li>
<li><a href="#Enemy Collision">Enemy Collision</a></li>
<li><a href="#Scene Switches">Scene Switches</a></li>
<li><a href="#Other Skills">Other Skills</a></li>
<li><a href="#Images">Images</a></li>
 </ul>
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
<p id="Player Controlls">
<h3>Player Controlls</h3>
 
The player can move in basic up, down, left, and right directions. The player controlls also keep the player from being able to move out of the frame of the camera.

```
    Rigidbody rigidBody;
    SpriteRenderer spriteRenderer;
    float distance = 1.7f;


    void Start()
    {
        rigidBody = GetComponent<Rigidbody>();
    }

    void Update()
    {
        

        if (transform.position.y <= -4.3f)
        {
            transform.position = new Vector3(transform.position.x, -4.3f, 0);
        }

        if (transform.position.x >= 7.5f)
        {
            transform.position = new Vector3(7.5f, transform.position.y, 0);
        }

        else if (transform.position.x <= -7.5f)
        {
            transform.position = new Vector3(-7.5f, transform.position.y, 0);
        }

        if (Input.GetKeyDown(KeyCode.LeftArrow)) //left
        {
            transform.Translate(-Vector3.right * distance);

        }

        if (Input.GetKeyDown(KeyCode.RightArrow)) //right
        {
            transform.Translate(Vector3.right * distance);
        }

        if (Input.GetKeyDown(KeyCode.DownArrow)) //down
        {
            transform.Translate(-Vector3.up * distance);
        }

        if (Input.GetKeyDown(KeyCode.UpArrow)) //up
        {
            transform.Translate(Vector3.up * distance);
        }

    }
```
</p>
<p id="Player Movement">
<h3>Player Movement</h3>

For Level 2, the player must navigate across a river by jumping on logs. I struggled with how to achieve this, as I couldn't figure out how to make the player "stick" to the log. I realized, the player didn't have to stick, it just had to look like it did. My end result was that if the player was at a certain position on the y-axis, it would move just like the log at the same y-axis location, making it look like the sprite was on the log.

Moving right:

```
{
if (transform.position.y >= -2.8 && transform.position.y <= 1.0 || transform.position.y == .08)
        {
            Debug.Log("left");
            transform.Translate(-Vector3.left * Time.deltaTime * 3);
        } 
 }
```
Moving Left:
```
 {
 if (transform.position.y >= -0.9500 && transform.position.y <= -0.8500 || transform.position.y == 2.5)
       {
           Debug.Log("left");
           transform.Translate(-Vector3.right * Time.deltaTime * 3);
       }
}
```

This behavior was taken from how I made the enemy (the car) move in Level 1.

Moving Right   
```
   void Update()
    {
        if (transform.position.x > 10.6f)
        {
            transform.position = new Vector3(-10.6f, transform.position.y, 0);

        }
        else
        {
            transform.Translate(-Vector3.left * Time.deltaTime * 3);
        }
    } 
```    

Moving Left
```
void Update()
    {
        if (transform.position.x < -10.6f)
        {
            transform.position = new Vector3(10.6f, transform.position.y, 0);

        }
        else
        {
            transform.Translate(-Vector3.right * Time.deltaTime * 3);
        }
    }
```
</p>
<p id="Enemy Collisons">
<h3>Enemy Collisions</h3>
For Level 1, the player is crossing a street and, if struck by a car, loses a life. In Level 2, the player is crossing a river and loses a life if they "fall" in the river. The player only has 3 lives per level, if they lose all three it is game over and they must return to the first level to continue playing.

```
{
    float pauseCount = 1f;
    float pauseCounter = 0f;

    public AudioSource livesAudio;

    public void OnCollisionEnter(Collision other)
    {
        Debug.Log("hit");
        livesAudio.Play();
        transform.position = new Vector3(transform.position.x, -4000f, 0);
        transform.position = new Vector3(transform.position.x, -4.3f, 0);
        ReduceLives();
    }

    public int playerLives = 3;
    public Image PlayerLives;
    public GameObject FrogPlayer;

    public Sprite livesZero;
    public Sprite livesOne;
    public Sprite livesTwo;
    public Sprite livesThree;

    public int ReduceLives()
    {
        playerLives -= 1;
        return playerLives;
    }

    void Update()
    {

        if (playerLives == 3)
        {
            PlayerLives.sprite = livesThree;
            Debug.Log("Three Lives Left");
        }

        if (playerLives == 2)
        {
            PlayerLives.sprite = livesTwo;
            Debug.Log("2 Lives Left");
        }

        if (playerLives == 1)
        {
            PlayerLives.sprite = livesOne;
            Debug.Log("1 Life Left");
        }

        if (playerLives == 0)
        {
            pauseCounter += Time.deltaTime;
            if (pauseCounter >= pauseCount)
            {
                PlayerLives.sprite = livesZero;

                GameOver();
            }
        }

        void GameOver()
        {
            SceneManager.LoadScene(20);
        }

    }
}
```    
</p>
<p id="Scene Switches">    
<h3>Scene Switches</h3>

There are 7 scene switches in order to progress through the game. This includes the collaborative main menu, the game over scene when the player loses all their lives, and a finishing scene for beating both levels. These scene switches are either triggered upon finishing a level, losing all the lifes, or by clicking a  button Below is one example:

```
{
    public void SceneSwitch()
    {
        SceneManager.LoadScene(12);
    }
}
```
</p>
<p id="Other Skills">
<h3>Other Skills</h3>
<ul>
<li>Learning how to approach a project from almost the very beginning. I learned how to segment out a project into more digestible pieces that can realistically be completed versus looking at it just as a whole.</li>

<li>Experiencing a real world example of project management using Sprint and Agile Methodologies.</li>
<li>Exhausting all possible bug fixes that I could think of or find before asking for help. I wanted to not only try everything in my knowledge base before asking for help, but I wanted to challenge myself to solve a problem that I had not   experienced before. </li>
<li>Being able to create and use my own artwork was also a fun experience.</li>
</ul>

</p>
<p id="Images">
<h3>Images</h3>

Lastly, here are some images from the final product. All the artwork was self-made using Procreate.

![Frogger Main Menu](https://github.com/zeeebs/Frogger---Classic-Arcade-Game/assets/125938574/a7430b34-1a37-4c9d-a691-a44ca26ab863)

![Frogger Level 1](https://github.com/zeeebs/Frogger---Classic-Arcade-Game/assets/125938574/3fb3a1c2-aee0-4ec8-b325-c064bd52e5fa)

![Frogger Level 2](https://github.com/zeeebs/Frogger---Classic-Arcade-Game/assets/125938574/d696f9a3-6e41-4602-8297-7dd3d8316838)

![Frogger Game Over](https://github.com/zeeebs/Frogger---Classic-Arcade-Game/assets/125938574/ebd118c7-794f-41a0-b9bb-5faaf5f19c2e)

![Frogger Next Level](https://github.com/zeeebs/Frogger---Classic-Arcade-Game/assets/125938574/8de2f639-bf17-4fe7-8ed4-d07ce60877ce)

![Frogger Won](https://github.com/zeeebs/Frogger---Classic-Arcade-Game/assets/125938574/e7c2de3d-610c-4734-9b9b-40437f815e78)



  
