# Platformer documentation

# The first episode

**Game.java**

- The **`Game`** class represents the main class of the game.
- The class has two instance variables: **`gameWindow`** and **`gamePanel`**.
- The **`Game`** constructor initializes **`gamePanel`** by creating a new **`GamePanel`** object and initializes **`gameWindow`** by creating a new **`GameWindow`** object and passing **`gamePanel`** as an argument.

**GamePanel.java**

- The **`GamePanel`** class extends the **`JPanel`** class and represents the game panel.
- The **`GamePanel`** constructor takes no arguments.
- The **`paintComponent`** method is overridden to draw a rectangle on the panel.

**GameWindow.java**

- The **`GameWindow`** class represents the main window of the game.
- The class has one instance variable: **`jframe`**, which is a **`JFrame`** object.
- The **`GameWindow`** constructor takes a **`GamePanel`** object as an argument.
- The **`GameWindow`** constructor initializes **`jframe`** by creating a new **`JFrame`** object, sets its size to 400x400 pixels, sets the default close operation to exit the application when the window is closed, adds the **`gamePanel`** to the frame, and makes the frame visible.

**MainClass.java**

- The **`MainClass`** class represents the main entry point of the application.
- The **`main`** method is the entry point of the application and creates a new **`Game`** object.

# **We add inputs and move our rectangle**

**KeyboardInputs.java**

- The **`KeyboardInputs`** class represents a class that handles keyboard input.
- The class implements the **`KeyListener`** interface to listen for keyboard events.
- The class has one instance variable: **`gamePanel`**, which is a **`GamePanel`** object that represents the game panel.
- The **`KeyboardInputs`** constructor takes a **`GamePanel`** object as an argument and initializes the **`gamePanel`** instance variable.
- The class has three methods that override the methods of the **`KeyListener`** interface: **`keyTyped`**, **`keyReleased`**, and **`keyPressed`**.
- The **`keyTyped`** and **`keyReleased`** methods are empty since they are not needed for this implementation.
- The **`keyPressed`** method is implemented to handle keyboard input. It checks the key code of the pressed key and calls the corresponding method in the **`gamePanel`** object to change the delta values of the **`GamePanel`** object. If the 'W' key is pressed, it calls **`changeYDelta`** with a value of -5, if the 'A' key is pressed, it calls **`changeXDelta`** with a value of -5, if the 'S' key is pressed, it calls **`changeYDelta`** with a value of 5, and if the 'D' key is pressed, it calls **`changeXDelta`** with a value of 5.

**MouseInputs.java**

- The **`MouseInputs`** class represents a class that handles mouse input.
- The class implements the **`MouseListener`** and **`MouseMotionListener`** interfaces to listen for mouse events and mouse motion events.
- The class has one instance variable: **`gamePanel`**, which is a **`GamePanel`** object that represents the game panel.
- The **`MouseInputs`** constructor takes a **`GamePanel`** object as an argument and initializes the **`gamePanel`** instance variable.
- The class has seven methods that override the methods of the **`MouseListener`** and **`MouseMotionListener`** interfaces: **`mouseClicked`**, **`mousePressed`**, **`mouseReleased`**, **`mouseEntered`**, **`mouseExited`**, **`mouseMoved`**, and **`mouseDragged`**.
- The **`mouseClicked`**, **`mousePressed`**, **`mouseReleased`**, **`mouseEntered`**, and **`mouseExited`** methods are not implemented and are empty.
- The **`mouseMoved`** method is implemented to handle mouse motion events. It receives a **`MouseEvent`** object as an argument and sets the position of the rectangle in the **`gamePanel`** object to the position of the mouse cursor.
- The **`mouseDragged`** method is not implemented and is empty.

**Game.java**

- The **`Game`** constructor has been updated to include a call to **`requestFocus`** on the **`gamePanel`** object.
- The **`requestFocus`** method is called to ensure that the **`GamePanel`** object has focus when the game is started.

```java
public Game() {
    gamePanel = new GamePanel();
    gameWindow = new GameWindow(gamePanel);
    gamePanel.requestFocus();
}
```

The **`gamePanel.requestFocus()`** method call has been added to the end of the constructor to ensure that the **`GamePanel`** object has focus when the game is started. This is important because it allows the **`GamePanel`** object to receive keyboard input and mouse input from the user.

**GamePanel.java**

- The **`GamePanel`** constructor has been updated to create instances of **`KeyboardInputs`** and **`MouseInputs`** and add them as listeners to the **`GamePanel`** object.
- The **`changeXDelta`** and **`changeYDelta`** methods have been added to change the delta values of the rectangle and repaint the panel.
- The **`setRectPos`** method has been added to set the position of the rectangle to the current mouse position and repaint the panel.
- The **`paintComponent`** method has been updated to use the current values of **`xDelta`** and **`yDelta`** to draw the rectangle.

```java
public GamePanel() {
    mouseInputs = new MouseInputs(this);
    addKeyListener(new KeyboardInputs(this));
    addMouseListener(mouseInputs);
    addMouseMotionListener(mouseInputs);
}
```

The **`GamePanel`** constructor has been updated to create instances of **`KeyboardInputs`** and **`MouseInputs`** and add them as listeners to the **`GamePanel`** object. This allows the **`GamePanel`** object to receive keyboard input and mouse input from the user.

```java
public void changeXDelta(int value) {
    this.xDelta += value;
    repaint();
}

public void changeYDelta(int value) {
    this.yDelta += value;
    repaint();
}

public void setRectPos(int x, int y) {
    this.xDelta = x;
    this.yDelta = y;
    repaint();
}
```

The **`changeXDelta`** and **`changeYDelta`** methods have been added to change the delta values of the rectangle and repaint the panel. The **`setRectPos`** method has been added to set the position of the rectangle to the current mouse position and repaint the panel.

```java
public void paintComponent(Graphics g) {
    super.paintComponent(g);
    g.fillRect(xDelta, yDelta, 200, 50);
}
```

The **`paintComponent`** method has been updated to use the current values of **`xDelta`** and **`yDelta`** to draw the rectangle. When the **`repaint`** method is called, the **`paintComponent`**
method is invoked and the rectangle is redrawn with the updated position.

# The Game loop Episode.

**MouseInputs.java**

- The **`mouseMoved`** method has been commented out.
- The **`mouseClicked`** method has been updated to call the **`spawnRect`** method in the **`GamePanel`** class and pass the current mouse position as arguments.

```java
@Override
public void mouseMoved(MouseEvent e) {
    //gamePanel.setRectPos(e.getX(), e.getY());
}

@Override
public void mouseClicked(MouseEvent e) {
    gamePanel.spawnRect(e.getX(), e.getY());
}
```

The **`mouseMoved`** method has been commented out since it is not needed for this implementation. The **`mouseClicked`** method has been updated to call the **`spawnRect`** method in the **`GamePanel`** class and pass the current mouse position as arguments. This method call allows a new rectangle to be spawned at the current mouse position when the mouse button is clicked.

**Game.java**

- The **`Game`** class now implements the **`Runnable`** interface and overrides its **`run`** method.
- The **`startGameLoop`** method has been added to create a new thread and start the game loop.
- The game loop has been implemented in the **`run`** method, with a target frame rate of 120 FPS.
- The game loop calculates the time since the last frame, updates the game state, and repaints the game panel.
- The game loop also calculates and prints the frames per second (FPS) every second.

```java
public class Game implements Runnable {

    private GameWindow gameWindow;
    private GamePanel gamePanel;
    private Thread gameThread;
    private final int FPS_SET = 120;

    public Game() {
        gamePanel = new GamePanel();
        gameWindow = new GameWindow(gamePanel);
        gamePanel.requestFocus();
        startGameLoop();
    }

    private void startGameLoop() {
        gameThread = new Thread(this);
        gameThread.start();
    }

    @Override
    public void run() {
        double timePerFrame = 1000000000.0 / FPS_SET;
        long lastFrame = System.nanoTime();
        long now = System.nanoTime();

        int frames = 0;
        long lastCheck = System.currentTimeMillis();

        while (true) {
            now = System.nanoTime();
            if (now - lastFrame >= timePerFrame) {
                gamePanel.repaint();
                lastFrame = now;
                frames++;
            }

            if (System.currentTimeMillis() - lastCheck >= 1000) {
                lastCheck = System.currentTimeMillis();
                System.out.println("FPS: " + frames);
                frames = 0;
            }
        }
    }
}
```

The **`Game`** class now implements the **`Runnable`** interface and overrides its **`run`** method. The **`startGameLoop`** method has been added to create a new thread and start the game loop. The game loop has been implemented in the **`run`** method, with a target frame rate of 120 FPS. The game loop calculates the time since the last frame, updates the game state, and repaints the game panel. The game loop also calculates and prints the frames per second (FPS) every second.

**GamePanel.java**

- A new inner class **`MyRect`** has been added, which represents a rectangle that moves around the screen.
- An **`ArrayList`** of **`MyRect`** objects has been added to keep track of all the rectangles that have been spawned.
- The **`paintComponent`** method now updates and draws all the **`MyRect`** objects in the **`rects`** list.
- The **`updateRectangle`** method has been modified to change the color of the rectangle when it bounces off the walls.
- The **`getRndColor`** method has been added to generate a random color.
- The **`xDelta`** and **`yDelta`** variables have been changed to **`float`** instead of **`int`**.
- The **`changeXDelta`** and **`changeYDelta`** methods have been modified to simply update the **`xDelta`** and **`yDelta`** variables, without calling **`repaint()`**.
- The **`setRectPos`** method has been modified to simply update the **`xDelta`** and **`yDelta`** variables, without calling **`repaint()`**.
- The **`spawnRect`** method has been added to add a new **`MyRect`** object to the **`rects`** list at the specified position.

# Episode 04, we add images

There is no significant change in the **`MouseInputs`** class. The only change is the removal of the code in the **`mouseClicked`** method that printed "Mouse clicked!" to the console. 

In this update to the **`GamePanel`** class, the following changes have been made:

1. The class now loads an image file (**`player_sprites.png`**) from the resources directory using an **`InputStream`** and the **`ImageIO`** class. The image is stored in a **`BufferedImage`** object named **`img`**.

```java
private void importImg() {
		InputStream is = getClass().getResourceAsStream("/player_sprites.png");

		try {
			img = ImageIO.read(is);
		} catch (IOException e) {
			e.printStackTrace();
		}

	}
```

1.  The size of the **`GamePanel`** has been changed to a fixed size of 1280x800 pixels using the **`setPanelSize()`** method.

```java
private void setPanelSize() {
		Dimension size = new Dimension(1280, 800);
		setMinimumSize(size);
		setPreferredSize(size);
		setMaximumSize(size);
	}
```

1. The **`paintComponent()`** method has been updated to draw a sub-image of the **`img`** object on the **`GamePanel`**. The sub-image is created using the **`getSubimage()`** method of **`BufferedImage`** class, and its position and size are defined by the **`(xDelta, yDelta)`** position and **`(128, 80)`** size.

```java
public void paintComponent(Graphics g) {
		super.paintComponent(g);

		subImg = img.getSubimage(1 * 64, 8 * 40, 64, 40);
		g.drawImage(subImg, (int) xDelta, (int) yDelta, 128, 80, null);
	}
```

Overall, the changes to the **`GamePanel`** class introduce image loading and display on the game panel, and set a fixed size for the panel.

In this update to the **`GameWindow`** class, the window is now centered on the screen and made non-resizable. Additionally, the window is packed, which resizes the window to its preferred size based on the components it contains. Here is the modified code:

```java
public class GameWindow {
    private JFrame jframe;

    public GameWindow(GamePanel gamePanel) {
        jframe = new JFrame();
        jframe.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jframe.add(gamePanel);
        jframe.setLocationRelativeTo(null);  // Center the window
        jframe.setResizable(false);  // Make the window non-resizable
        jframe.pack();  // Resize the window to its preferred size
        jframe.setVisible(true);
    }
}
```

# **We add Animations to the game.**

In the **`keyPressed`** method, I added a switch statement to handle each key press, and call the **`setDirection()`** method on the **`gamePanel`** object with the appropriate direction constant.

In the **`keyReleased`** method, I added a switch statement to handle each key release, and call the **`setMoving(false)`** method on the **`gamePanel`** object to stop the player from moving in that direction.

I also imported the **`Directions`** constants from a separate **`Constants`** class using the static import syntax to make the code more readable.

In the **`GamePanel`** class, the following changes have been made:

- Added several import statements at the top, including some static import statements for constants.
- Added instance variables to keep track of the player's current action (e.g. idle, running), direction (e.g. left, right), and animation state (e.g. which frame of the current animation is being displayed).
- Modified the **`importImg`** method to also close the input stream after reading the image.
- Modified the **`loadAnimations`** method to load each animation frame from the player image into a 2D array of images.
- Modified the **`setDirection`** method to set the player's direction and indicate that the player is moving.
- Modified the **`setMoving`** method to indicate whether or not the player is moving.
- Added the **`updateAnimationTick`**, **`setAnimation`**, and **`updatePos`** methods to update the animation state, current action, and player position, respectively, based on the player's current movement and direction.
- Modified the **`paintComponent`** method to update the animation state, current action, and player position, and then to draw the appropriate frame of the player's animation based on these values.

Created a new **`Constants`** class that includes inner classes with constant values for **`Directions`** and **`PlayerConstants`**. Included a method **`GetSpriteAmount`** that returns the number of sprites that are associated with each player action. This method is used in the **`GamePanel`** class to determine the number of sprites to display for each player action. The addition of the **`Constants`** class improves the organization of the code by providing a centralized location for constant values to be stored.

# **We add the update part to the gameloop.**

It looks like you have added the **`update()`** method which calls **`updateGame()`** in the **`GamePanel`** class. Also, you have added the game loop, which runs in the **`run()`** method and calculates the time for each frame and update. You are using a **`deltaF`** variable to count the number of frames and a **`deltaU`** variable to count the number of updates that need to be made. The loop updates the game and repaints the game panel depending on the value of **`deltaU`** and **`deltaF`**. Finally, you are also printing the FPS and UPS at the end of each second.

In the **`GamePanel`** class, the method **`updateGame()`** has been added, and the methods **`updateAnimationTick()`**, **`setAnimation()`**, and **`updatePos()`** have been moved to **`updateGame()`**. The **`aniSpeed`** variable has been changed to 25, which means that the animation will change less frequently.

# **Adding the player class and changing how we move**

A new class called **`Entity`** is added. This class is an abstract class that has two fields for the **`x`**
and **`y`** coordinates of the entity, as well as a constructor to initialize these fields. However, this class doesn't have any methods or behavior specified yet.

The `Player` class is a subclass of `Entity` and it holds the game logic of the player. The class has the properties for player movement, direction, and animation. The `Player` class is responsible for updating the position and the animation of the player and rendering it on the game screen.

The main changes are:

- Removed the implementation of methods and variables that were related to the game panel
- Added fields and methods to control the movement, animation, and attack of the player
- Added the `loadAnimations()` method which loads the sprites of the player
- Added the `update()` and `render()` methods which update the player's position and render the player on the game screen, respectively
- Added `resetDirBooleans()` method to reset the booleans that control the player's movement direction
- Added `setAttacking()` method to set the player's attacking state
- Added fields and methods for player direction, animation, and attacking.

In the **`GamePanel`** class, the **`updateGame`** method has been emptied and no longer performs any updates on the game state. The **`paintComponent`** method now fills the entire game panel with a white color and also calls the **`render`** method of the **`Game`** instance to draw the game state.

The constructor of the **`GamePanel`** class now takes a **`Game`** instance as a parameter and stores it in a private field. This is used in the **`paintComponent`** method to call the **`render`** method of the **`Game`** instance.

In the updated **`Game`** class, a new **`Player`** object is created and is used to render the player in the game. The **`update()`** method is used to update the player and the **`render()`** method is used to render the player.

Additionally, the **`windowFocusLost()`** method is added to reset the player's direction booleans to false when the game loses focus.

```java
// New variable declaration for player
private Player player;

...

// Initialization of player
private void initClasses() {
    player = new Player(200, 200);
}

...

// Update method that updates the player
public void update() {
    player.update();
}

...

// Render method that renders the player
public void render(Graphics g) {
    player.render(g);
}

...

// Method to reset player direction booleans when game loses focus
public void windowFocusLost() {
    player.resetDirBooleans();
}

...

// Getter for player object
public Player getPlayer() {
    return player;
}
```

In the **`GameWindow`** class, a new **`WindowFocusListener`** was added to handle the case where the game window loses focus. The **`windowLostFocus`** method is implemented to call the **`windowFocusLost`** method of the game panel's **`Game`** object. This will reset the player movement direction boolean variables when the game window loses focus.

```java
jframe.addWindowFocusListener(new WindowFocusListener() {
    @Override
    public void windowLostFocus(WindowEvent e) {
        gamePanel.getGame().windowFocusLost();
    }

    @Override
    public void windowGainedFocus(WindowEvent e) {
        // TODO Auto-generated method stub
    }
});
```
