# Frogger---Classic-Arcade-Game
Recreation of the Classic Arcade Game: Frogger

This project was created using C# and Unity. It showcases player input for movement, enemy collisions, life counter, scene switches, sound effect/music, and custom graphics. 

After completing the Tech Academy's C# and Unity Course of the Game Developer Bootcamp, I collaborated with my fellow students for two weeks to develop full-scale classic arcade games using the aformentioned software. Working on a piece of a larger project provided a great learning environment for working within an existing product, and experience integrating my work into the larger product. I got to operate in the capacity of a professional developer, and experience how they work with the time, resources, and customer stories they have. Since each person worked on a different game, I got to develop every back-end and front-end detail of my game. I am extremely proud I get to say that virtually every aspect of Frogger is my own work. I learned the value of utilizing my resources to the fullest extent to complete my project, including using my instructor, who helped me through many bugs and Unity issues. Over the two week sprint, I also had the opportunity to work on project management and team programming skills that I'm confident and excited to use on future projects.

Below are descriptions of the stories I worked on, along with code snippets code files, and final product images.

<h3>Player Controlls</h3>
 
 The player can move in basic up, down, left, and right directions. The player controlls also keep the player from being able to move out of the frame of the camera.


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

<h3>Player Movement</h3>

For Level 2, the player must navigate across a river by jumping on logs. I struggled with how to achieve this, as I couldn't figure out how to make the player "stick" to the log. I realized, the player didn't have to stick, it just had to look like it did. My end result was that if the player was at a certain position on the y-axis, it would move just like the log at the same y-axis location, making it look like the sprite was on the log.

<h4>Moving Right</h4>
 {
        //right
        if (transform.position.y >= -2.8 && transform.position.y <= 1.0 || transform.position.y == .08)
        {
            Debug.Log("left");
            transform.Translate(-Vector3.left * Time.deltaTime * 3);
        }
    }
   
 <h4>Moving Left</h4>   
 {
      //left

       if (transform.position.y >= -0.9500 && transform.position.y <= -0.8500 || transform.position.y == 2.5)
       {
           Debug.Log("left");
           transform.Translate(-Vector3.right * Time.deltaTime * 3);
       }

   }

<h4>Enemy Collisions</h4>

Shoot an asteroid to win!
