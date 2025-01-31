
# **Processing and Enhancement of Planetary Astrophotography Using Generative Adversarial Networks**

## **Authors**
- Diego Antonio Villalba González
- Arantxa Camil Junco Flores  
- Jonathan Alexis Hernández Cuevas

## **Abstract**

This project presents the development of a **Generative Adversarial Network (GAN)** combined with planetary image processing to enhance resolution, detail, and contrast from low-resolution and high-noise images.

We achieved **satisfactory results**, applicable to various **image processing fields**, such as **security cameras, medical imaging (ultrasounds), and astronomy**.

### **Example Results**

![Results on the Moon](/results/moon_result.jpeg)
![Results on the Moon](/results/moon2_result.jpeg)
![Results on Saturn](/results/saturn_result.jpeg)
![Results on Jupiter](/results/jupiter_result.png)

---

## **Introduction**

### **1.1 Astrophotography**

Astrophotography is a technique that combines **astrophysics and photography** to capture images of celestial objects. It has evolved from photographic plates to high-resolution digital cameras.

Technological advances have enabled **shorter exposure times**, **real-time image visualization**, and improved post-processing techniques. However, challenges such as **light pollution**, **digital noise**, and **tracking stability** of telescopes still impact image quality.

### **1.2 SRGANs (Super-Resolution GANs)**

SRGANs are a **type of deep learning model** that consists of two competing neural networks: **a generator and a discriminator**. The **generator** takes a **low-resolution image** and attempts to create a **high-resolution version**, while the **discriminator** learns to differentiate between real and generated images.

By competing against each other, both networks improve, resulting in **higher-quality image reconstruction**.

### **1.3 Problem Statement**

Planetary astrophotography is particularly challenging because:

- **Planets appear small and move quickly in the night sky.**
- **Atmospheric turbulence and motion blur** reduce image quality.
- **Typical photography resolution is limited by video capture quality.**

A common solution is **video stacking**, where multiple video frames are combined to reduce noise and improve detail. However, this method is still constrained by **video resolution limits**.

Our project **enhances planetary images** by applying **SRGANs**, allowing for **higher resolution and improved details** even when starting with low-quality sources.

---

## **Installation**

### **1. Clone the Repository**

```bash
git clone https://github.com/your_username/your_repo.git
cd your_repo
```
2. Create a Virtual Environment
```bash
python -m venv venv
source venv/bin/activate  # On Windows, use venv\\Scripts\\activate
```
3. Install Dependencies
```bash
pip install -r requirements.txt
```


## **Usage Instructions**

1. Prepare Your Data
	•	Place low-resolution planetary images in data/low_res/.
	•	If available, place high-resolution images in data/high_res/ for training.

2. Train the Model
```bash
python train.py --config configs/train_config.yaml
```

Modify the configuration file as needed for different datasets.

3. Generate Super-Resolution Images

Once trained, use the model to enhance new images:
```bash
python generate.py --input data/low_res/ --output results/high_res/
```

## **Contributing**

We welcome contributions!

1. **Fork the repository.**
2. **Create a new branch** (`git checkout -b feature-branch`).
3. **Make your changes.**
4. **Commit your changes** (`git commit -m 'Added feature X'`).
5. **Push to the branch** (`git push origin feature-branch`).
6. **Open a Pull Request.**

For major changes, please open an **issue first** to discuss them
## **License**

This project is licensed under the MIT License. See the LICENSE file for details.

## **References**

The main reference for this project is the following paper:

- **Ledig, C., Theis, L., Huszár, F., Caballero, J., Cunningham, A., Acosta, A., Aitken, A., Tejani, A., Totz, J., Wang, Z., & Shi, W. (2017).**  
  *Photo-Realistic Single Image Super-Resolution Using a Generative Adversarial Network.*  
  arXiv:1609.04802.  

For further details, you can access the original paper **[here](https://arxiv.org/abs/1609.04802)**.

Contact

For any questions or collaboration opportunities:
	•	Diego Villalba
	•	Email: diego.villalba@ciencias.unam.mx
	•	LinkedIn: Diego Antonio Villalba González
	•	GitHub: DiegoViillalba


