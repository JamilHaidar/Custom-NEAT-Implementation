# Custom-NEAT-Implementation


My friend asked me if it was possible to create an AI where he can't create a dataset or have good input-output data.
The AI should be able to adapt to varying inputs too. There are many ways to do this. I suggested a simple NEAT (NeuroEvolution of Augmenting Topologies) implementation.

---

# Background
The NEAT approach has evolved through time and got more optimized and diverse. The original paper can be present [**here**](http://nn.cs.utexas.edu/downloads/papers/stanley.ec02.pdf).
For my simple demo, I created a simple implementation that doesn't cover species divergence. 
The demo is simple. There is a face of "Happy Jamil" that is being attacked by "Angry Jamils". 
The "Happy Jamil" is controlled by the mouse cursor or user touching the screen.
The "Angry Jamils" each have a Neural Network that takes in as input the angle from the direction they are facing to the center of the "Happy Jamil".

The output of each Neural Network dictates the angular velocity of the "Angry Jamil" while it constantly moves the direction it's facing.

The approach is simple. Create a simple Genetic Algorithm implementation. Instead of each individual having certain genes, their genes are Neural Networks.
The score function is the amount of time where direction of "Angry Jamil" is facing towards the "Happy Jamil" target.
During mutation, we loop over every weight and there are 4 ways it could mutate:
* Negate the weight
* Randomize the weight
* Scale the weight (grow)
* Scale the weight (shrink)

Every 15 seconds, the individuals are sorted according to their score. The top half is kept. The rest are re-initialized.

---

# The Code

Here is the code for the mutate function.

    public void mutate()
    {
        for (int i = 0; i < weights.Length; i++)

            for (int j = 0; j < weights[i].Length; j++)

                for (int k = 0; k < weights[i][j].Length; k++)
                {
                   
                    //mutate weight value 
                    float randomNumber = UnityEngine.Random.Range(0f, 100f);

                    if (randomNumber <= 2f)
                        weights[i][j][k] *= -1f;

                    else if (randomNumber <= 4f)

                        weights[i][j][k] = UnityEngine.Random.Range(-0.5f, 0.5f);

                    else if (randomNumber <= 6f)

                        weights[i][j][k] *= UnityEngine.Random.Range(0f, 1f) + 1f;

                    else if (randomNumber <= 8f)

                        weights[i][j][k] *= UnityEngine.Random.Range(0f, 1f);
                }
    }
---
# Final Notes

This project was actually my first NEAT implementation. It took me 4 hours to code since I had to look up certain concepts and tune the NN parameters.
I have included a compiled version of the demo for Windows and a .apk for Android.
To start the Windows version press the Spacebar. To start the Android version, double tap.


