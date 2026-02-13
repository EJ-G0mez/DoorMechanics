# Door Mechanic

## This Project is a collection of different type of doors with different mechanics for different uses

This project is meant to be a *learning and practical* execution of multiple doors types with different mechanics of interaction to open them for myself and a guide to others to implement something similar into their games/projects. The following project has these type of doors based on the following opening methods:

  1. Button-based doors
  2. Physics based doors
  3. Automatically opened based doors
  4. Doors opened with keys

This project can be viewed functioning in the following demo reel here: 

This README document is meant to record all of the features this code has, giving a thrurough explanation with the use of Diagrams, Images, and PseudoCode meant to resemble the Unreal Engine 5 block structure.

# Content

<details>

  <summary>Syntaxis, Diagrams and Media</summary>

  # Syntaxis, Diagram and Media

  ## How is this document organized and how should you read it?
  
  This section is to give an understanding of how the document will be formated and organized as well as explaining the diagrams that will be placed around this document.

  ### Syntax

  All of the added or edited functions, structures or events will be added to this document. Any default classes, structures, etc, that are in the base Unreal Engine default projects, will only be added if they are specifically mentioned in the context of the coding.

  The coding will be done in a pseudocode that will ressemble as much as possible a object oriented language

  Example:

  ```
    class newClass {

      public  bool attribute;
      public  int attribute2;
      private static  struct attribute3;

      public function1( int parameter, bool parameter){
        return returnType;
      }

      private functionEvent(){
        attribute += 1;
      }
    }
  ```
  

### Media

Media in this document will have foot notes describing what the media is showing. Media can include images, videos of the project to assist in the understanding of this project.

Example:

  ![dotboxspawnemitter](https://github.com/user-attachments/assets/a0b89f3c-2c57-42c8-b502-7a0211c958d8)[^1]

  [^1]: Example of an image showing an Unreal Project taken from the [Unreal Documentation Webpage](https://dev.epicgames.com/documentation/en-us/unreal-engine/nodes-in-unreal-engine). 
  
</details>

<details>

  <summary>First Type: Button Based </summary>

  # First Type of Doors: Button Based

  ## Press to open

  These types of doors are opened by tapping a key button on the keyboard, there are a few methods that are being used.

  <img width="1554" height="871" alt="imagen" src="https://github.com/user-attachments/assets/8e9705ba-659d-4c11-8079-921a3fb3b6ce" /> [^2]

  [^2]: All door that can be opened with a button in the main level

  <summary>Player Character + Door Mechanic</summary>

  ### Player Character + Door Mechanic

  This method is specific due to the fact that the Key Pressed Event is in the Player Character Blueprint, and the door turns by moving the Z axis using a..... 

  In this case the "E" Key is used to open the door.

  The turning of the Z azis using this method is unique to this door, 

  <img width="1378" height="324" alt="imagen" src="https://github.com/user-attachments/assets/5e12fc9a-ee55-4e1e-8ab6-95bcf1c5b8fe" /> [^3]

  [^3]: BP_FirstPersonCharacter "E" Event in Unreal Engine 5
  

  ```

  public class BP_FirstPersonCharacter extends GameModeBase {

    public event E() { //The E key is used to open the door
      lineTraceChannel lineChannel = LineTraceByChannel(/*start*/ GetWorldLocation(FirstPersonCamera),
          /*end*/ (GetWorldLocation(firstPersonCamera) + (GetForwardVector(firstPersonCamera) * 3000.0)); //we need to view the line trace that the playes camera is using to see if they are looking at a door
      OnPressed() {
        if(lineChannel)){ //the line channel exists?
          if(ActorHasTag(lineChannel.hitChannel, "Door"){ //the line channel hit an actor with the door tag?
            BP_Door_Type_1 door = lineChannel.hitActor;
            door.OpenDoor();
          }
        }
      }
    }
  }
  ```

  <img width="1115" height="407" alt="imagen" src="https://github.com/user-attachments/assets/541bb4c6-0aac-4c61-8eb9-f8125d775e52" /> [^4]

  [^4]: Open Door Event from the Door_Type_1 blueprint in Unreal Engine 5

  <img width="1213" height="327" alt="imagen" src="https://github.com/user-attachments/assets/ca40fa27-3fb2-4194-8eee-c49408969d78" /> [^5]

  [^5]: Timeline for the OpenDoor Event, it reaches a Value of 1, after 7 seconds.

  ```

  public class Door_Type_1 extends Actor {
    public StaticMesh doorMesh;
    public StaticMesh doorOutMesh;


    public Timeline openDoorTimeline(){
      track doorLoad = [/*value*/[0, 1], /*time*/[0.0, 7.0]];
    }

    public event OpenDoorTimeline(){
      flipflop {
        A (opendDoor.play):
          SetRelativeRotation(doorMesh, /*x*/ 0.0, /*y*/ 0.0, /*z*/ Lerp(0.0, 0.0, openDoorTimeline.doorLoad));
        B (openDoor.reverse):
          SetRelativeRotation(doorMesh, /*x*/ 0.0, /*y*/ 0.0, /*z*/ Lerp(0.0, 0.0, openDoorTimeline.doorLoad));
      }
    }
  }
  
  ```

  <summary>Door Mechanic Only</summary>

  ### Door Mechanic Only

  This door has the Key Event in this case, the "F" Key inside the Door Actor, and the rotation of the door uses a different method which will be used for most doors moving forward, the difference is on how the z-axis of the door which uses a Make Rotator Function which sets the value of the z-Axis, depending if you are opening or closing the door. As well as adding the On Component Begin/End Overlap Events that trigger when the door's hitbox, overlaps with the player controller.
  
  <img width="982" height="536" alt="imagen" src="https://github.com/user-attachments/assets/37491c74-5e68-4b8b-8446-37e875cf9195" /> [^6]

  [^6]: Door_Type_4 Event Graph, with the Events "F", On Component Begin Overlap (Box) and On Component End Overlap (Box)

  ```

    public class Door_Type_4 extends Actor {
    public StaticMesh SMDoor;
    public StaticMesh doorOutMesh;


    public Timeline DoorSpeed(){
      track doorRot = [/*value*/[0, 90], /*time*/[0.0, 1.0]];
    }

    public event F(){
      flipflop {
        A (DoorSpeed.play):
          SetRelativeRotation(doorMesh, MakeRotator(0.0, 0.0, DoorSpeed.doorRot));
        B (DoorSpeed.reverse):
          SetRelativeRotation(doorMesh, MakeRotator(/*x*/ 0.0, /*y*/ 0.0, /*z*/ DoorSpeed.doorRot));
      }
    }

    public event OnComponentBeginOverlap(){
      EnableInput(self, GetPlayerController());
    }

    public event OnComponentEndOverlap(){
          DisableInput(self, GetPlayerController());
        }
  }
  
  ```

  <summary>Opening the door using a button at long distance</summary>

  ### Door with a Button at a long distance.

  This door has hitbox in which it is far away from the door itself, meaning that the hit box is away from the door model.

  The logic is the exact same as the previous door, except that the hitbox is away from the door, in the door hitbox, there is a simple cylinder to mark the place where the hitbox is so it can be interacted with.

  <img width="660" height="479" alt="imagen" src="https://github.com/user-attachments/assets/9d0efd01-2d61-46e8-9f2e-d722caef9dd9" /> [^7]

[^7]: Door_Type_5 Viewport showing the hitbox far from the door model

 <img width="982" height="536" alt="imagen" src="https://github.com/user-attachments/assets/37491c74-5e68-4b8b-8446-37e875cf9195" /> [^8]

  [^8]: Door_Type_ Event Graph, with the Events "F", On Component Begin Overlap (Box) and On Component End Overlap (Box)

  ```

    public class Door_Type_5 extends Actor {
    public StaticMesh SMDoor;
    public StaticMesh doorOutMesh;


    public Timeline DoorSpeed(){
      track doorRot = [/*value*/[0, 90], /*time*/[0.0, 1.0]];
    }

    public event F(){
      flipflop {
        A (DoorSpeed.play):
          SetRelativeRotation(doorMesh, MakeRotator(0.0, 0.0, DoorSpeed.doorRot));
        B (DoorSpeed.reverse):
          SetRelativeRotation(doorMesh, MakeRotator(/*x*/ 0.0, /*y*/ 0.0, /*z*/ DoorSpeed.doorRot));
      }
    }

    public event OnComponentBeginOverlap(){
      EnableInput(self, GetPlayerController());
    }

    public event OnComponentEndOverlap(){
          DisableInput(self, GetPlayerController());
        }
  }
  
  ```
  
</details>

<details>

  <summary>Second Type: Physics Based door</summary>

  # Second Type: Physics Based

  ## Just push

  These types of doors main way to be opened is to have a physics component that allows the player to move it. There are two ways in which the doors physics are being used.

  <summary>Physics Type A</summary>

  ### Physics Type A

  <summary>Physics Type B</summary>

  ### Physics Type B
  
</details>

<details>

  <summary>Third Type: Automatic Doors</summary>

  # Third Type: Automatic Doors

  ## Keeping Momentum

  There is only one type of door in this project, when the player reaches the door's hitbox, it start opening automatically, and closing once they leave.

  [Insert Door image]

  [Insert Door Component]

  [Insert Door Code]
  
</details>

<details>

  <summary>Fourth Type: Open with a Key</summary>

  # Fourth Type: Open with a Key

  ## Get the key, open the path.

  Another door type where there is only one type. There is an object type key, that once the player need to collect to be able to interact with the door.

  [Insert Door and Key Image]

  [Insert Door Component]

  [Insert Key Component]

  [Insert Player Component]

  [Insert Door code]

  [Insert Key code]

  [Insert player code]
  
</details>
