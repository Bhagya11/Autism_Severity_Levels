# Autism_Subtype
### **Steps for Extracting Gray Matter (GM) from MRI Scans**  
Your script follows these steps to extract gray matter from MRI scans:  

#### **Step 1: Load the MRI NIfTI File**  
- Reads the `.nii` or `.nii.gz` file using `nibabel`.  
- Converts the image to a NumPy array for processing.  

#### **Step 2: Normalize Intensity Values**  
- Normalizes the intensity values to a 0-1 range for better contrast and processing.  

#### **Step 3: Apply Smoothing to Reduce Noise**  
- Uses a **2mm Gaussian kernel** (`smooth_img`) to reduce noise.  

#### **Step 4: Skull Stripping (Remove Non-Brain Areas)**  
- Computes a **brain mask** to remove non-brain regions.  
- Multiplies the brain mask with the image to retain only the brain.  

#### **Step 5: Gaussian Mixture Model (GMM) for Tissue Classification**  
- Uses **4 components** to classify different brain tissues:  
  - **CSF (Cerebrospinal Fluid)**  
  - **Gray Matter (GM)**  
  - **Deep GM (Subcortical structures like the thalamus)**  
  - **White Matter (WM)**  
- GMM assigns probability values to different tissues based on intensity distribution.  

#### **Step 6: Otsu’s Thresholding for Adaptive GM Selection**  
- **Otsu’s method** finds an optimal threshold to separate gray matter from other tissues.  
- Pixels **above the Otsu threshold** are classified as gray matter.  

#### **Step 7: Morphological Processing to Refine GM Mask**  
- **Binary Opening** removes small artifacts (noise).  
- **Binary Closing** fills small gaps in the GM mask.  
- The refined mask is applied to extract the final **gray matter volume**.  

#### **Step 8: Save the Middle Slice as PNG**  
- Extracts the **middle axial slice** of the gray matter volume.  
- Saves it as a `.png` file in a separate folder for each patient.  

### **Output Directory Structure**  
Each patient’s segmentation is saved in:  
