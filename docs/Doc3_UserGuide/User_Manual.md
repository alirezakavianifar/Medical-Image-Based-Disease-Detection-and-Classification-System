# Clinical User Manual
## Medical Image-Based Disease Detection and Classification System

---

## 1. Introduction

Welcome to the **Medical Image-Based Disease Detection and Classification System**. This platform serves as an automated clinical decision support tool designed to assist radiologists and physicians by detecting pathological anomalies in medical scans (CT, MRI, X-Ray) using deep learning algorithms.

> [!IMPORTANT]
> **Clinical Advisory Note:**
> This system is designed as a secondary evaluation tool to assist diagnosis and should not replace primary review by qualified medical specialists.

---

## 2. Authentication & Session Security

To protect sensitive patient metadata and comply with health privacy regulations (HIPAA/GDPR), secure credential verification is enforced.

### 2.1 Login Procedure
1. Navigate to the login URL.
2. Enter your authorized clinical email address in the **Email** field.
3. Enter your password in the **Password** field.
4. Click the **Sign In** button.
5. Upon verification, you will be automatically redirected to the clinical dashboard view matching your account role (Admin, Doctor, or Radiologist).

### 2.2 Session Inactivity Timeout
To prevent unauthorized access to open workstations:
- The system monitors clinical activity (mouse movements, keystrokes).
- After **15 minutes of inactivity**, the active session token expires.
- A warning banner will display, and you will be redirected to the secure login screen.

### 2.3 Logout Procedure
- Click the **Log Out** button located in the lower left section of the sidebar navigation.
- The session token is cleared from the browser memory.

---

## 3. Medical Scan Uploading

Follow these steps to import new patient scans into the database cache:

1. Click on the **Upload Case** button in the left sidebar menu.
2. A file selection container will display.
3. You can either:
   - Click the container to open your local system file explorer and select a `.dcm` (DICOM) file.
   - Drag a `.dcm` scan file and drop it directly onto the dashed visual upload container.
4. The file will join the upload queue showing its name, file size, and upload progress:
   - Progress bar indicates the transfer speed.
   - Status tag displays *Uploading*, *Complete*, or *Failed*.

> [!WARNING]
> **File Constraints:**
> - Uploaded files must conform to the standard DICOM PS3 format.
> - Maximum file size per upload session is capped at **100MB**.

---

## 4. Reviewing AI Predictions on the Dashboard

Once upload is complete, the AI engine preprocesses the images and runs inference automatically. Select any patient from the navigation archive list to open the dashboard workspace:

```text
+------------------+----------------------------------+-----------------------+
|  Navigation      |          Image Canvas            |     AI Predictions    |
|  - Search cases  |                                  |  Label: Pneumonia     |
|  - Filter Modality|         +-----------------+      |  Confidence: 94.2%    |
|  - Patient List  |         |  Bounding Box   |      |  [==============----] |
|                  |         |  (overlay)      |      |                       |
|                  |         +-----------------+      |  Clinical Notes:      |
|                  |                                  |  [ Write comments... ]|
|                  |                                  |                       |
|  [Log Out]       |  [Contrast]  [Brightness]  [Zoom]|  [ Sign Off & Lock ]  |
+------------------+----------------------------------+-----------------------+
```

### 4.1 Left Sidebar (Case Archive)
- Use the **Search** input to look up patient records by Patient ID or Name.
- Use the modality dropdown list to filter cases (e.g. show only *CT* or *MRI* cases).
- Click on any Patient card to load the scan details into the center canvas viewer.

### 4.2 Center Viewport (Interactive Medical Canvas)
- Displays the preprocessed scan slice.
- Displays a translucent **bounding box outline** (or heatmap) drawn on the canvas, locating anomalous tissue.
- Use the sliders below the image to adjust image properties:
  - **Contrast:** Enhance details in low-contrast zones.
  - **Brightness:** Adjust overall luminance.
  - **Zoom:** Zoom in to inspect critical bounding box areas.

### 4.3 Right Panel (AI Diagnostics)
- **Classification Output:** Displays the predicted category label (e.g. *Normal*, *Benign Tumors*, *Malignant Lung Lesions*).
- **Confidence Rating:** Displays the model prediction probability (0% - 100%). A progress indicator highlights the statistical strength.

---

## 5. Case Verification & Report Exporting

This phase details how physicians sign off on diagnostic outcomes:

1. **Review Notes:** In the right panel input form, write clinical notes under the **Clinical Comments** header.
2. **Compile Report Draft:** Review the details. If changes are needed, edit the comments.
3. **Approve and Sign Off:**
   - Click the **Sign Off & Lock Case** button.
   - A verification pop-up will ask for confirmation.
   - *Note: Only verified Doctor roles have permissions to sign off.*
4. **Download PDF Report:**
   - Once signed, the case status changes to *Signed Off* and fields are locked.
   - Click **Download PDF Report** to download the locked file containing patient details, scan images with bounding box outlines, model predictions, and signed clinical comments.

---

## 6. Troubleshooting Guidelines

This section describes how to resolve common errors encountered during operation:

| Error Message / Issue | Probable Cause | Action Required |
| :--- | :--- | :--- |
| **"Uploaded file must be a valid DICOM document under 100MB"** | File has an incorrect extension, is corrupted, or exceeds the upload size limit. | Verify the file has a `.dcm` extension. Check the properties to confirm the file size is under 100MB. |
| **"Inference Timeout Error"** | Backend model inference took longer than the 5.0-second limit (e.g. due to server load or GPU issues). | Refresh the page and click "Analyze Image" again. If the issue persists, contact the system administrator to verify GPU VRAM availability. |
| **"Access Denied: Action requires Doctor role"** | A user authenticated with a Radiologist or Admin role tried to finalize and sign off on a report. | Confirm your account role. If you need sign-off permissions, contact the administrator to update your account privileges to "Doctor". |
| **Visual scan fails to load on dashboard** | Browser compatibility issue or PNG preprocessing crash. | Ensure you are using a supported browser (Chrome 110+, Safari 16+, Edge 110+). Clear browser cache and try again. |
