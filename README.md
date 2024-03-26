# PixelRush
### Video Demo:  https://youtu.be/Bvk-0628oBo
### Description: In this game, the player has one life. 
To survive, the player needs to avoid monsters like in Google's dinosaur game.
- Additionally, the player has 5 magic shots
TODO
Open the project in the pycharm program(Python will be installed automatically) > In the upper right corner, click on the green Run button > Enjoy!

In this game, the player has one life. 
To survive, the player needs to avoid monsters like in Google's dinosaur game.

-Introduction
I want to explain the most important parts of my code, at least the majority of them.

First, I imported the pygame library, which allows me to work and develop the game.
Then, using the clock variable and its method, I set the frames per second to slow down the animations.
After that, I called the main method, which starts the game, similar to the main function in the C language; this method is pygame.main().
Using the screen variable and its method, I set the screen's width and height, where the first value is the width and the second value is the height. For example, here's the code: screen = pygame.display.set_mode((612, 350)).
Then, I set the window title. Afterward, I added an image using the icon variable, like the other variables containing methods.
Next, I added images to the walk_left and walk_right arrays to create animations.
In my code, you'll notice the .convert_alpha() method; it was used to convert the program into a mobile game, but I decided to leave everything as is because it would be easier.
The ghost variable contains our enemy; then, in the ghost_list_in_game array, we use it as some sort of storage.
Everything I've written so far is just a small part of the code, so I'll try to explain it in chunks.
After that, I set the position of the character and the background.
Then, I initialized various variables and set how often enemies appear.
After that, I created a game-over screen and created a variable where you can set the number of bullets left.
I created an empty list and the image itself. Then, we have the gameplay variable set to True; it's very important, but I'll come back to it later.
In line 39, I set how high the player can jump.
Next, I added bg.mp3, and using the play() method, I made it play.

-I would like to note that as we approach the end, we will start dissecting the code into parts because the code is interconnected, and what is written at the beginning will interact with what is written at the end and vice versa.

By interaction, I mean that towards the end, around line 100 or so, there will be functional parts, so I'm trying to break down the code in detail to avoid problems later on.
Now, we'll move to line 58 and then return when we analyze the functional part. Our gameplay = True isn't random; it's necessary for the loop we'll be using.
Here we are at line 61 and the loop named running.
Now that our process has started, we have the first condition if gameplay:, meaning if gameplay == True, then I set the player's position.
Honestly, it would be much better to use object-oriented programming because here I'm creating variables when needed, but I could have created separate files and classes, and everything would have been smoother.
Now we'll move on to the function, which is quite simple despite how it looks; here's the code:   if ghost_list_in_game:
            for (i, el) in enumerate(ghost_list_in_game):
                screen.blit(ghost, el)
                el.x -= 10
-What's happening? the ghost moves to the left by 10 pixels.
Next, we move on to the next function, but before that, I'd like to say that I haven't explained everything because I want to leave it for when I'll be dissecting the more important parts.
Next, we have this code.:    keys = pygame.key.get_pressed()
        if keys[pygame.K_LEFT]:
            screen.blit(walk_left[player_anim_count], (player_x, player_y))
        else:
            screen.blit(walk_right[player_anim_count], (player_x, player_y))

-Here we see that if a key is pressed, the player moves left/right.
Additionally, we ensure that there are keys for left and right movement.
Remember how I created the variable is_jump where we set the player's height? Now it's time to use it. Without the function we're about to write, the player simply won't be able to dodge enemies, proving that this is one of the most important functions.
Here's the code we have:  if not is_jump:
            if keys[pygame.K_SPACE]:
                is_jump = True
        else:
            if jump_count >= -8:
                if jump_count > 0:
                    player_y -= (jump_count ** 2) / 2
                else:
                    player_y += (jump_count ** 2) / 2
                jump_count -= 1
            else:
                is_jump = False
                jump_count = 8
-This isn't a function but a condition, but I'll refer to it as a function because this part of the code plays an important role.
So, I used if not because it's easier to start with an easy task and then tackle a harder one. Furthermore, if the player isn't jumping, then the condition is checked: if pygame.K_SPACE is pressed, meaning it's True, then the player's position changes, and the player jumps.
Next, if this doesn't happen, then if the player is above or equal to -8, they jump. If it's above 0, then they fall. If it's less than 0, then they stop jumping.
-I don't want to delve into every detail to explain the most important thing and not to hold back, so let's move on.
Simply put, our function, or rather condition, checks if the player presses the spacebar. If they do, we check if they are jumping. If they are, they jump until the jump is completed, and when it's done, they fall down.
Moving on, we have: 
        if player_anim_count == 3:
            player_anim_count = 0
        else:
            player_anim_count += 1


        bg_x -= 2
        if bg_x == -612:
            bg_x = 0
Here we start the animation, and I'll explain how this part of the code works, but before that, I want to apologize for calling conditions functions. I named them that way because there are many, and it's just easier to call them that.

So, here's how it goes: we have three images for each direction, representing the animation for walking right and left (3 is the fourth image, and 0 is the first).
When we reach the fourth image, which is 3/3, it's replaced by image 0, which is the first one. If it's not the fourth image, we increment it by 1, thus changing the images.
Now, you might ask why the condition should only be executed once. My answer is that all conditions are within one larger loop.
So, now we have the background moving, and you might wonder how it's possible that the player is moving while the background stays still. It's like walking in place, but we need the background to move too.
Here, we subtract 2 from the background's position, and since it's constant, it keeps moving. But think about it: if it's constantly moving left, it will be endless. Just like with the animation, it's the same.
So, if the background goes beyond the map's limits, which is when the value is -612, it resets to zero, and that's how we get the animation for both the character and the background.
Now we'll have monster animation, but explaining it doesn't make sense because it works the same way as the background movement. The only thing I'll explain is how the death, or rather, the monster attacks work.

So, now we'll have our monsters attacking. From the beginning, we created an array for each bullet, and now our code checks how many bullets we have.
We insert the image into the game that we loaded, and then each bullet moves forward every time.
If a bullet hits our enemy, both the bullet and the enemy are removed, so that's how it happens.
That's how the ghost attack system works, and I think we can end it here.
