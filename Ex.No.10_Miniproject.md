# Ex.No: 10  Implementation of 2D/3D Car Racing game 
### REGISTER NUMBER : 212222040108
### AIM: 
To develop a car racing game in Unity 
### Algorithm:
```
1. Setup Your Scene
    Import or create your car model (with Rigidbody and Collider)
    Design a track/environment
    Set up a camera to follow the car
2. Script Car Controls
Key Features:
    Use Unity’s Rigidbody for physics-based movement
    Use Input.GetAxis("Vertical") for acceleration/braking
    Use Input.GetAxis("Horizontal") for steering
3. Basic Car Movement Logic
   Apply forward force for acceleration/braking
    Rotate car for steering
    Add drag/friction to slow down naturally
4. Collision Detection
   Unity’s Rigidbody with Colliders will handle collisions automatically
    Use OnCollisionEnter() to detect impacts and react accordingly
Collision Detection
1. Mountain Collision Check
If GreenCar hits the mountain:
Show “Blue Car Wins!”
Set game state to GameOver.
If BlueCar hits the mountain:
Show “Green Car Wins!”
Set game state to GameOver.
2. Head-On Collision Check
If GreenCar and BlueCar collide with each other (face to face):
Show “It's a Tie!”
Set game state to GameOver.
```  
### Program:
```
using UnityEngine;
using UnityEngine.UI;

public class CarController : MonoBehaviour
{
    public float acceleration = 800f;
    public float steering = 200f;
    public float maxSpeed = 100f;

    public Rigidbody rb;
    public Text speedText;
    public Text rpmText;

    private float moveInput;
    private float steerInput;

    void Start()
    {
        if (rb == null)
            rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        // Input
        moveInput = Input.GetAxis("Vertical");
        steerInput = Input.GetAxis("Horizontal");

        // Update UI
        float speed = rb.velocity.magnitude * 3.6f; // m/s to km/h
        float rpm = Mathf.Abs(moveInput) * 3000f;   // Simulated RPM
        if (speedText != null) speedText.text = Mathf.Round(speed) + " Km/h";
        if (rpmText != null) rpmText.text = Mathf.Round(rpm) + " RPM";
    }

    void FixedUpdate()
    {
        if (rb.velocity.magnitude < maxSpeed)
        {
            rb.AddForce(transform.forward * moveInput * acceleration * Time.fixedDeltaTime);
        }

        transform.Rotate(0f, steerInput * steering * Time.fixedDeltaTime, 0f);
    }
}

```

## Collision Handling:
```
void OnCollisionEnter(Collision collision)
{
    if (collision.gameObject.CompareTag("Mountain"))
    {
        if (this.CompareTag("GreenCar"))
            GameManager.Instance.EndGame("Blue Car Wins!");
        else if (this.CompareTag("BlueCar"))
            GameManager.Instance.EndGame("Green Car Wins!");
    }

    if (collision.gameObject.CompareTag("GreenCar") && this.CompareTag("BlueCar") ||
        collision.gameObject.CompareTag("BlueCar") && this.CompareTag("GreenCar"))
    {
        GameManager.Instance.EndGame("It's a Tie!");
    }
}
```
### Output:
![Screenshot 2025-05-20 142058](https://github.com/user-attachments/assets/7b834768-f7b9-45f6-aa92-3067ab282d3a)
![Screenshot 2025-05-20 142201](https://github.com/user-attachments/assets/5b8eab02-c41a-47dc-8654-ebaf9f3e511d)
![Screenshot 2025-05-20 142248](https://github.com/user-attachments/assets/2262ac12-2ff6-414c-b8c5-1b6a90f735e7)
![Screenshot 2025-05-20 142834](https://github.com/user-attachments/assets/4a987820-810f-45f9-b944-d9f64663c490)
![Screenshot 2025-05-20 142851](https://github.com/user-attachments/assets/71efbf53-0364-4eaf-a79e-a43f98fb0003)







### Result:
Thus the game was developed using Unity and adopted collision-based decision-making AI technology.
