# Door Mechanic

## This Project is a collection of different type of doors with different mechanics for different uses

This project is meant to be a *learning and practical* execution of multiple doors types with different mechanics of interaction to open them for myself and a guide to others to implement something similar into their games/projects. The following project has these type of doors based on the following opening methods:

  1. Button-based doors
  2. Physics based doors
  3. Automatically opened based doors
  4. Doors opened with keys

This project can be viewed functioning in the following demo reel here: https://youtu.be/npkyZY1SgLA

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

  [Insert door screenshots here]

  <summary>Player Controller + Door Mechanic</summary>

  ### Player Controller + Door Mechanic

  This method is specific due to the fact that the Key Pressed Event is in the Player Controller Blueprint, and the door turns by moving the Z axis using a..... 

  In this case the "E" Key is used to open the door.

  The turning of the Z azis using this method is unique to this door, 

  [Insert Player COntroller Image here]

  [Insert Player Controller Code here]

  [Insert Door Blueprint here]

  [Insert Coor Blueprint Code here]

  Possible uses:

  Limitations:

  <summary>Door Mechanic Only</summary>

  This door has the Key Event in this case, the "F" Key inside the Door Actor, and the rotation of the door uses a different method
  
</details>
