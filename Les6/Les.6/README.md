# Les6.1 Oefening 6.1: Bouw mijn eigen mini-level

## Beschrijving
Ik heb een mini-level gemaakt waarin jij als speler (een capsule) munten moet verzamelen en alle punten in het spel moet behalen. Je kunt bewegen en ook springen.

## Wat ik heb in dit level toegepast van eerdere lessen?
-In mijn level heb ik van les1.2 Debug.Log() gebruik om berichten.te tonen.
#### Code (Coin)
```code
using UnityEngine;

public class Coin : MonoBehaviour
{
    public Vector3 rotateAmount;
    void Start()
    {
        Debug.Log("Hello Player! Welcome to the game!");
        Debug.Log("In this game you have to collect all the coins. Good luck!");
    }

    // Update is called once per frame
    void Update()
    {
        transform.Rotate(rotateAmount * Time.deltaTime);
    }

}      
```
-Van les2.1 heb ik een script toegepast dat automatisch draait.
#### Code (Coin draait)
```code
using UnityEngine;

public class Coin2 : MonoBehaviour
{
    public Vector3 rotateAmount;
   
    
    void Update()
    {
        transform.Rotate(rotateAmount * Time.deltaTime);
    }

}      
```
-Van les3.2 en les5.1 heb ik functies, argumenten en return types toegepast.
```code
using Unity.Profiling;
using Unity.VisualScripting;
using UnityEngine;

public class Player : MonoBehaviour
{
    private Rigidbody rb;
    public float jumpForce = 7f;
    public float moveSpeed = 5f;
    private bool isGrounded;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        float moveX = Input.GetAxis("Horizontal");
        float moveZ = Input.GetAxis("Vertical");
        Vector3 movement = new Vector3(moveX, 0f, moveZ) * moveSpeed;
        Vector3 newVelocity = new Vector3(movement.x, rb.linearVelocity.y, movement.z);
        rb.linearVelocity = newVelocity;

        if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
        }
    }
        void OnCollisionEnter(Collision collision)
        {
            if (collision.gameObject.CompareTag("Ground"))
            {
                isGrounded = true;
            }
        }
        void OnCollisonExit(Collision collision)
        {
            if (collision.gameObject.CompareTag("Ground"))
            {
                isGrounded = false;
            }
        }
    }
```
## Welke nieuwe feature heb ik toegevoegd?
-Ik heb Input.GetAxis toegevoegd.
#### Code (Third Person Camera)
```code
 UnityEngine;

public class ThirdPersonCamera : MonoBehaviour
{
    public Transform target;
    public float distance = 4f;
    public float height = 2f;
    public float rotationSpeed = 5f;

    private float currentX = 0f;
    private float currentY = 0f;
    public float minY = -20f;
    public float maxY = 60f;

    private void LateUpdate()
    {
        currentX += Input.GetAxis("Mouse X") * rotationSpeed;
        currentY -= Input.GetAxis("Mouse Y") * rotationSpeed;
        currentY = Mathf.Clamp(currentY, minY, maxY);

        Vector3 direction = new Vector3(0, 0, -distance);
        Quaternion rotation = Quaternion.Euler(currentY, currentX, 0);
        transform.position = target.position + rotation * direction + new Vector3(0, height, 0);

        transform.LookAt(target.position + Vector3.up * 1.5f);
    }
}
```
## Demo
![video](Les6.1.gif)







