#classes and constructors/methodes and orject oriented variables

#class MyGame original source from https://api.arcade.academy/en/latest/examples/platform_tutorial/step_01.html 


import arcade
import random

# Constants for Screen
SCREEN_WIDTH = 1000
SCREEN_HEIGHT = 650
SCREEN_TITLE = "My Cool Game"

#Constants for scale of sprites 
CHARACTER_SCALING = 0.1
Animal_Scaling = 0.4
TILE_SCALING = 0.1

MOVEMENT_SPEED = 5

class MyGame(arcade.Window):
    """
    Main application class.
    """

    def __init__(self): #init runs everytime a object is created
        
        # Call the parent class and set up the window
        super().__init__(SCREEN_WIDTH, SCREEN_HEIGHT, SCREEN_TITLE)

        arcade.set_background_color(arcade.csscolor.AQUAMARINE)

    #gui camera is created to add a score board
    #this add a top layer to the window and wont be affected if character moves around
        self.gui_camera = None
        self.score = 0
        self.Level = 1
        self.counter = 0
        self.flag = True
#############################################
#Only Used for testing . Just Ignore        
        # Sprite lists
        #self.player_list = None
        #self.wall_list = None

        # Set up the player
        #self.player_sprite = None

        # This variable holds our simple "physics engine"
        #self.physics_engine = None

###########################################       

    def setup(self):
        """Set up the game here. Call this function to restart the game."""

    # Create the Sprite lists
        self.player_list = arcade.SpriteList()
        #self.wall_list = arcade.SpriteList(use_spatial_hash=True)
        self.bear_list = arcade.SpriteList(use_spatial_hash=True)
        self.animal_list= arcade.SpriteList()

        # Set up the player, specifically placing it at these coordinates.
        image_source = ":resources:images/animated_characters/Joanna Pics/stick.png"
        self.player_sprite = arcade.Sprite(image_source, CHARACTER_SCALING)
        self.player_sprite.center_x = 64
        self.player_sprite.center_y = 128
        self.player_list.append(self.player_sprite)

        # Set up the player, specifically placing it at these coordinates.
        animal_source = ":resources:images/animated_characters/Joanna Pics/peng.png"
        self.animal_sprite = arcade.Sprite(animal_source, Animal_Scaling)
        self.animal_sprite.center_x = 200
        self.animal_sprite.center_y = 200
        self.animal_list.append(self.animal_sprite)



        self.animal_move = 1

        self.y_move = 0
        
        
        ######LET OFF WITH TRYING TO GET ANIMAL TO MOVE
        ##### EXAMPLE HERE
        ###https://www.geeksforgeeks.org/python-arcade-adding-moving-platforms/

        #Physics engine to move around
       # self.physics_engine = arcade.PhysicsEnginePlatformer(self.animal_sprite)



    # Changing the direction 
        if self.animal_sprite.center_y < 600:
            self.animal_sprite.change_x = 1
        if self.animal_sprite.center_x > 500:
            self.animal_sprite.center_x = -1
                    
      
        coordinate_list = []

        for x in range(self.Level):
            coordinate_list.append([random.randrange(SCREEN_WIDTH- 50), random.randrange(SCREEN_HEIGHT - 50)])
        
        for coordinate in coordinate_list:
            # Add a obsticals on the ground (aka trash)
            bear = arcade.Sprite(
                ":resources:images/animated_characters/Joanna Pics/trash.png", TILE_SCALING
            )
            bear.position = coordinate
            self.bear_list.append(bear)

        self.flag = False

        #Set up Gui camera to keep score
        self.gui_camera = arcade.Camera(self.width, self.height)

            
    def on_draw(self):
        """Render the screen."""

        self.clear()

        
        # Code to draw the screen goes here
        #self.wall_list.draw()
        self.player_list.draw()
        self.bear_list.draw()
        self.animal_list.draw()
        



        # Activate the GUI camera before drawing GUI elements
        self.gui_camera.use()

        # Draw score on the screen
        score_text = f"Score: {self.score}"
        level_text = f"Level: {self.Level}"
        #The f in front of strings tells Python to look at the values inside {}
        #and substitute them with the values of the variables if exist
        arcade.draw_text(score_text,10,10,arcade.csscolor.WHITE,18)
        arcade.draw_text(level_text,200,10,arcade.csscolor.WHITE,18)

    #Control Character
    def on_key_press(self, key, modifiers):
        """
        Called whenever the mouse moves.
        """
        if key == arcade.key.UP:
            self.player_sprite.change_y = 5
        elif key == arcade.key.DOWN:
            self.player_sprite.change_y = -5
        elif key == arcade.key.LEFT:
            self.player_sprite.change_x = -5
        elif key == arcade.key.RIGHT:
            self.player_sprite.change_x = 5
    #Stops character from cont. going up/down , left/right
    def on_key_release(self, key, modifiers):
       
        if key == arcade.key.UP or key == arcade.key.DOWN:
         self.player_sprite.change_y = 0
        elif key == arcade.key.LEFT or key == arcade.key.RIGHT:
            self.player_sprite.change_x = 0
            

    def Levels(self,numberOflevel):
        
        coordinate_list = []

        for x in range(numberOflevel):
            coordinate_list.append([random.randrange(SCREEN_WIDTH- 50), random.randrange(SCREEN_HEIGHT - 50)])
        
        for coordinate in coordinate_list:
            # Add an obstical on the ground (aka bears)
            bear = arcade.Sprite(
                ":resources:images/animated_characters/Joanna Pics/trash.png", TILE_SCALING
            )
            bear.position = coordinate
            self.bear_list.append(bear)
    

    #update is need to keep checking for changes and to apply them
    def update(self, delta_time):
        """ Movement and game logic """

        self.player_list.update()
        self.player_list.update_animation()

        self.animal_list.update()
        self.animal_list.update_animation()

        
        ##self.physics_engine.update()


        #self.animal_sprite.center_y -= 1

        self.animal_sprite.change_x = self.animal_move
        self.animal_sprite.change_y = self.y_move
  
        # Changing the direction of enemy movement
        if self.animal_sprite.center_x < 800: 
            self.animal_move = 1
            self.y_move = random.randrange(0,5)
        
        else:
            self.animal_move = -1

        # Generate a list of all sprites that collided with the player.
        hit_list =  arcade.check_for_collision_with_list(self.player_sprite,self.bear_list)

        # Loop through each colliding sprite, remove it
        for bear in hit_list:
            bear.kill()
            self.score = self.score + 1
            
        #flag variable only exist to make sure this part of the code doesnt run until the
            #bear_list has something in it at least once
            #len is to see if there are more collectables left befor going to next level
        if len(self.bear_list) == 0 and self.flag == False and self.score == 1:
         self.Level = self.Level +1
         self.Levels(2)
         
        elif len(self.bear_list) == 0 and self.score == 3:
         self.Levels(3)
         self.Level = self.Level +1
        elif len(self.bear_list) == 0 and self.score == 6:
         self.Levels(4)
         self.Level = self.Level +1
        elif len(self.bear_list) == 0 and self.score == 10:
         self.Levels(4)
         self.Level = self.Level +1

        
         
            
            
        

       
       
            

def main():
    """Main function"""
    window = MyGame()
    window.setup()
    arcade.run()


if __name__ == "__main__":
    main()
