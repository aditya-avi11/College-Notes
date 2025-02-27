
- Generative Adversial Networks.
- A class of machine learning models used in **computer vision** to generate new images that resemble real ones.
- GAN's architecture consists of 2 Neural Network : Generator & Discriminator.

![[Pasted image 20250204121700.png]]
![[Pasted image 20250204121725.png]]


## ==How GANs Work==

1. **Generator (G)**
    
    - The generator creates synthetic images from random noise.
    - Its goal is to generate images that are indistinguishable from real images.
2. **Discriminator (D)**
    
    - The discriminator is a classifier that distinguishes real images from fake (generated) ones.
    - It is trained to correctly classify real vs. generated images.
3. **Adversarial Training**
    
    - The generator tries to fool the discriminator by improving the quality of generated images.
    - The discriminator continuously improves its ability to detect fake images.
    - Over time, both networks improve until the generated images look real to the human eye.

<hr><hr>

## ==The Adversarial Training Process==

### Step 1: Training the Discriminator

- The Discriminator is trained with **real images** from the dataset, labeled as **real (1)**.
- It is also trained with **fake images** generated by the Generator, labeled as **fake (0)**.
- The Discriminator learns to improve its ability to distinguish between real and fake images.

### Step 2: Training the Generator

- The Generator creates **fake images** from random noise.
- These fake images are fed into the Discriminator.
- The Discriminator **predicts a probability** (real or fake).
- The Generator is updated to **minimize the Discriminator's ability to detect fake images**.

### Step 3: Adversarial Game (Minimax Optimization)

- The Generator and Discriminator are trained in a **zero-sum game**:
    - The **Generator improves** until the Discriminator can no longer differentiate real from fake images.
    - The **Discriminator improves** to correctly classify real vs. fake.
- This leads to an equilibrium where the Generator produces highly realistic images.


<hr><hr> 

## ==The Loss Functions Used in GANs==

![[Pasted image 20250204120213.png]]

### ==Breakdown of the Loss Functions==

1. **Discriminator Loss (Binary Cross-Entropy Loss)**

	![[Pasted image 20250204120341.png]]
    - The Discriminator wants to **maximize** its ability to classify real and fake images correctly.
    - It minimizes the log probability of misclassifying real and fake images.
2. **Generator Loss**
    
    ![[Pasted image 20250204120405.png]]
    - The Generator wants to **maximize** the Discriminator’s mistake.
    - ==It tries to **maximize** the probability that **D(G(z))** is close to 1 (i.e., the fake image is classified as real).==

<hr><hr>

## ==The Training Process==

### Step 1: Initialize GAN

- Randomly initialize both the **Generator (G)** and **Discriminator (D)**.

### Step 2: Train the Discriminator

- Take a batch of **real images** and label them as **1 (real)**.
- Take a batch of **fake images** generated by **G(z)** and label them as **0 (fake)**.
- Compute the **Discriminator loss** and update **θ_D**.

### Step 3: Train the Generator

- Sample a batch of random noise **z**.
- Generate fake images **G(z)**.
- Feed the fake images into the **Discriminator (D)**.
- Compute the **Generator loss** and update **θ_G** to fool the Discriminator.

### Step 4: Repeat Steps 2 & 3 Until Convergence

- Both networks continuously improve until the generated images are **indistinguishable from real ones**.

<hr><hr>

## ==Challenges in Training GANs==

Training GANs is difficult due to:

1. **Mode Collapse** – The Generator produces limited variations instead of diverse samples.
2. **Vanishing Gradients** – The Discriminator becomes too strong, making it hard for the Generator to improve.
3. **Training Instability** – GANs require careful tuning of hyperparameters and learning rates.
4. **Evaluation Difficulty** – There is no simple metric to measure GAN performance; metrics like **FID (Fréchet Inception Distance)** and **IS (Inception Score)** are commonly used.

<hr><hr>

## ==Variants of GANs==

Several improved GAN architectures address specific problems:

1. **DCGAN (Deep Convolutional GAN)** – Uses convolutional layers for better image generation.
2. **WGAN (Wasserstein GAN)** – Uses Wasserstein distance for better training stability.
3. **StyleGAN** – Generates highly realistic human faces with style-based latent space manipulation.
4. **CycleGAN** – Used for **image-to-image translation** without paired datasets.
5. **Pix2Pix** – Performs image translation tasks with a paired dataset.
6. **BigGAN** – Generates high-resolution images with better stability.

<hr><hr>

## ==Applications of GANs in Computer Vision==

- **Image Generation** – Creating high-resolution, photorealistic images.
- **Super-Resolution** – Enhancing image resolution (e.g., SRGAN).
- **Data Augmentation** – Generating synthetic data for training ML models.
- **Style Transfer** – Applying artistic styles to images (e.g., CycleGAN).
- **Medical Imaging** – Enhancing medical scans for better diagnosis.
- **Deepfake Technology** – Altering videos to swap faces or create realistic synthetic content.


<hr><hr>


