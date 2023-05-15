# simple-unity-code
simple code for 3 animation states in unity



using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class animationa : MonoBehaviour
{
    private Animator anim;
    private bool isWalking = false;
    private bool isRunning = false; private void Start()
    {
        anim = GetComponent<Animator>();
    }
    private void Update()
    {
        float x = Input.GetAxis("Horizontal") * Time.deltaTime * 150.0f;
        transform.Rotate(0, x, 0); if (Input.GetKey(KeyCode.LeftShift) && Input.GetKey(KeyCode.W))
        {
            if (!isRunning)
            {
                isRunning = true;
                anim.Play("Running");
            }
            float z = Input.GetAxis("Vertical") * Time.deltaTime * 6.0f;
            transform.Translate(0, 0, z);
        }
        else if (Input.GetKey(KeyCode.W))
        {
            if (!isWalking && !isRunning)
            {
                isWalking = true;
                anim.Play("Walking");
            }
            float z = Input.GetAxis("Vertical") * Time.deltaTime * 3.0f;
            transform.Translate(0, 0, z);
        }
        else
        {
            if (isWalking || isRunning)
            {
                anim.Play("Standing Idle");
            }
            isWalking = false;
            isRunning = false;
        }
    }
}
