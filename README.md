# Movement Script

## Name it "PlayerMovement"
## Copy & Paste it into C++


using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerMovement : MonoBehaviour
{
    public CharacterController controller;
 
    public float speed = 12f;
    public float gravity = -9.81f * 2;
    public float jumpHeight = 3f;
 
    public Transform groundCheck;
    public float groundDistance = 0.4f;
    public LayerMask groundMask;
 
    Vector3 velocity;
 
    bool isGrounded;
 
    // Update is called once per frame
    void Update()
    {
        //checking if we hit the ground to reset our falling velocity, otherwise we will fall faster the next time
        isGrounded = Physics.CheckSphere(groundCheck.position, groundDistance, groundMask);
 
        if (isGrounded && velocity.y < 0)
        {
            velocity.y = -2f;
        }
 
        float x = Input.GetAxis("Horizontal");
        float z = Input.GetAxis("Vertical");
 
        //right is the red Axis, foward is the blue axis
        Vector3 move = transform.right * x + transform.forward * z;
 
        controller.Move(move * speed * Time.deltaTime);
 
        //check if the player is on the ground so he can jump
        if (Input.GetButtonDown("Jump") && isGrounded)
        {
            //the equation for jumping
            velocity.y = Mathf.Sqrt(jumpHeight * -2f * gravity);
        }
 
        velocity.y += gravity * Time.deltaTime;
 
        controller.Move(velocity * Time.deltaTime);
    }
}

## After this, Go to file and click 'Save All'
## 'X' out and go to the 'Player' and drag the movement script into the component area.
## Click on 'Add Component' and search 'CharacterController'
## Drag the 'CharacterController' into the CharacterController Section on the Movement script.
## Create an 'Empty' in the Create section.
## Rename it "GroundCheck' and attach it to the 'Player' object
## Put the X, Y & Z Coordinates to 0, then drag it to the feet of the 'Player' object
## Drag the 'GroundCheck' on the GroundCheck section.
## Now, you should have a functional walking system for your unity character.

## If you need a bit more help / or confused, submit an issue.
