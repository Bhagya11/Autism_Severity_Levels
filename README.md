# Autism_severity Levels
### **Step-by-Step Process for Severity Level Calculation, Gray Matter Extraction, and Comparison**  

This document outlines the **complete process** for calculating ASD severity levels, extracting gray matter intensity, and analyzing the relationship between gray matter and ASD severity.  

---

## **Step 1: Load and Inspect the Dataset**  

1. **Dataset Used:**  
   - The dataset **(NYU ABIDE Phenotypic Data)** contains **ADOS_TOTAL** and **DSM_IV_TR** columns, which help determine ASD severity.  

2. **Inspect Data:**  
   - Load the dataset and check for missing values.  
   - Filter for **only NYU subjects** (ensuring dataset consistency).  

---

## **Step 2: Calculate DSM-5 Severity Levels**  

We use **ADOS_TOTAL scores** to classify subjects based on the DSM-5 severity criteria:  

| **ADOS_TOTAL Score** | **DSM-5 Severity Level** |
|----------------------|-------------------------|
| 7–12                | Level 1 (Requiring support) |
| 13–20               | Level 2 (Substantial support) |
| 21+                 | Level 3 (Very substantial support) |
| TD (Typical Development) | Level 0 |

### **Severity Calculation Steps**  
- Extract **ADOS_TOTAL** and **DSM_IV_TR** columns.  
- Map each subject to a DSM-5 severity level based on ADOS_TOTAL.  
- Assign **TD (Typical Development) = Level 0** for control subjects.  
- Save the updated dataset with a **new "DSM_5_Severity" column**.  

---

## **Step 3: Extracting Gray Matter Intensity from MRI Scans**  

1. **Locate MRI Scans:**  
   - Each subject’s **T1-weighted MRI scan** is loaded from the **NYU dataset**.  
   - Handle both **.nii** and **.nii.gz** file formats.

2. **Preprocessing the MRI Data:**  
   - Convert to **grayscale**.  
   - Normalize intensity values **between 0 and 1**.  
   - Apply **smoothing (Full Width at Half Maximum = 2mm)**.  
   - Use **brain masking** to remove the skull.

3. **Gray Matter Segmentation:**  
   - Apply a **Gaussian Mixture Model (GMM) with 4 components** to classify tissues.  
   - Extract **gray matter region** using **Otsu’s thresholding**.  
   - Perform **morphological operations** (binary opening/closing) to refine segmentation.

4. **Extracting Mean Gray Matter Intensity:**  
   - Compute the **mean intensity** from the segmented **gray matter**.  
   - Store the extracted **GM_Intensity values** along with **Subject ID**.  

---

## **Step 4: Statistical Analysis - Comparing Gray Matter Intensity vs. Severity Levels**  

1. **Merge Severity Data with Gray Matter Intensity Data:**  
   - Match **subject IDs** from the two datasets.  
   - Create a final dataset with:  
     - **Subject ID**  
     - **DSM-5 Severity Level**  
     - **Mean Gray Matter Intensity**  

2. **Perform Kruskal-Wallis Test:**  
   - Used to check if **gray matter intensity differs significantly** across ASD severity levels.  
   - Null hypothesis: No significant difference across groups.  
   - Alternative hypothesis: At least one group differs significantly.  

---

## **Step 5: Visualization - Box Plot Analysis**  

1. **Generate a Box Plot:**  
   - **X-axis:** DSM-5 Severity Level (0 = TD, 1, 2, 3).  
   - **Y-axis:** Mean Gray Matter Intensity.  
   - Color-coded to show distribution across severity levels.

2. **Interpretation of the Box Plot:**  
   - **Higher severity (Level 3) shows significantly lower gray matter intensity.**  
   - **TD (Level 0) and Level 1 subjects have a broader intensity range.**  
   - **Level 2 shows a moderate gray matter intensity.**  
   - **Outliers suggest individual variability in gray matter reduction.**  

---

## **Final Conclusion Based on the Box Plot & Statistical Test**  

1. **Gray matter intensity significantly decreases with increasing ASD severity.**  
2. **Level 3 (Most severe ASD cases) exhibits the lowest gray matter intensity.**  
3. **Statistical analysis (Kruskal-Wallis test) confirms significant differences between severity levels (p < 0.05).**  
4. **TD and mild ASD cases (Level 1) have overlapping distributions, suggesting variability in gray matter loss.**  

---

## **Final Output Files**  
![image](https://github.com/user-attachments/assets/1e426f04-0ab0-406f-91cf-2776dca90f37)

✅ **Processed Dataset:**  
- Saved as `NYU_ABIDE_with_Severity1.csv` (includes DSM-5 severity levels).  

✅ **Gray Matter Analysis Results:**  
- **PNG images** of segmented gray matter saved for each subject.  
- **Box plot saved** as `GM_Intensity_Comparison.png`.  

✅ **Gray matter segmented png images**  

