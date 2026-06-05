# API Reference Manual
## Medical Image-Based Disease Detection and Classification System

---

## 1. Overview

This document specifies the RESTful API endpoints for the **Medical Image-Based Disease Detection and Classification System**. 

- **Base URL:** `http://localhost:8000/`
- **Default Media Type:** `application/json`
- **Authentication Scheme:** HTTP Bearer token authorization.
  - To access protected routes, include the following header:
    `Authorization: Bearer <JWT_TOKEN>`

---

## 2. OpenAPI 3.0.3 Specification (YAML)

This YAML block defines the complete API contract. It can be copied directly into any Swagger UI editor to compile mock servers or client stubs.

```yaml
openapi: 3.0.3
info:
  title: Medical Image Disease Classification System API
  description: API for user authentication, DICOM image upload, deep learning disease detection, and report compilation.
  version: 1.0.0
servers:
  - url: http://localhost:8000
    description: Local Development Server
paths:
  /api/auth/login:
    post:
      summary: Authenticate User
      description: Validates clinical credentials and returns a session JWT.
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/LoginPayload'
      responses:
        '200':
          description: Login successful. Returns JWT token.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/LoginSuccess'
        '401':
          description: Invalid email or password.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

  /api/images/upload:
    post:
      summary: Upload DICOM scan
      description: Uploads a raw DICOM file, parses metadata headers, and stores cached visual PNG frames.
      security:
        - BearerAuth: []
      requestBody:
        required: true
        content:
          multipart/form-data:
            schema:
              type: object
              properties:
                file:
                  type: string
                  format: binary
                  description: DICOM file payload (max 100MB).
      responses:
        '201':
          description: Scan uploaded and parsed successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UploadSuccess'
        '400':
          description: Invalid file formatting or size limits exceeded.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
        '401':
          description: Missing or expired token.

  /api/predictions/{image_id}:
    get:
      summary: Get AI Inference Results
      description: Retrieves classification labels, confidence percentages, and coordinate bounding boxes.
      security:
        - BearerAuth: []
      parameters:
        - name: image_id
          in: path
          required: true
          description: Unique database Image ID.
          schema:
            type: integer
      responses:
        '200':
          description: Results retrieved successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/PredictionSuccess'
        '401':
          description: Missing or expired token.
        '404':
          description: Invalid image ID or inference scores not yet calculated.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

  /api/reports/export:
    post:
      summary: Compile & Lock PDF Report
      description: Finalizes clinical diagnosis notes, sign-offs the case, and exports a locked PDF report.
      security:
        - BearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ReportPayload'
      responses:
        '200':
          description: Report signed off and locked successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ReportSuccess'
        '401':
          description: Missing or expired token.
        '403':
          description: Access Forbidden. Only users with the "Doctor" role can sign off on reports.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

  /api/health:
    get:
      summary: System Health Check
      description: Monitors status of database, uvicorn server, and VRAM memory.
      responses:
        '200':
          description: Services operational.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/HealthStatus'

components:
  securitySchemes:
    BearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT

  schemas:
    LoginPayload:
      type: object
      required:
        - email
        - password
      properties:
        email:
          type: string
          format: email
          example: doctor_john@hospital.org
        password:
          type: string
          example: ClinicalPassword123

    LoginSuccess:
      type: object
      properties:
        token:
          type: string
          description: JWT session token.
        role:
          type: string
          enum: [Admin, Doctor, Radiologist]
        name:
          type: string
          example: Dr. John Doe

    UploadSuccess:
      type: object
      properties:
        image_id:
          type: integer
          example: 142
        patient_id:
          type: string
          example: P-90812
        patient_name:
          type: string
          example: Jane Miller
        png_url:
          type: string
          example: /static/preprocessed/142_view.png
        modality:
          type: string
          example: CT

    PredictionSuccess:
      type: object
      properties:
        image_id:
          type: integer
          example: 142
        disease_type:
          type: string
          example: Malignant Lung Lesion
        confidence_score:
          type: number
          format: float
          example: 0.9425
        bounding_boxes:
          type: array
          items:
            type: array
            items:
              type: number
              format: float
            example: [104.5, 45.0, 220.0, 185.5]
        analyzed_at:
          type: string
          format: date-time
          example: 2026-06-05T10:45:00Z

    ReportPayload:
      type: object
      required:
        - image_id
        - clinical_comments
      properties:
        image_id:
          type: integer
          example: 142
        clinical_comments:
          type: string
          example: Malignant lung lesion detected in right upper lobe. Recommend biopsy.

    ReportSuccess:
      type: object
      properties:
        report_id:
          type: integer
          example: 58
        pdf_url:
          type: string
          example: /static/reports/Report_142_Signed.pdf
        is_finalized:
          type: boolean
          example: true
        finalized_at:
          type: string
          format: date-time
          example: 2026-06-05T11:45:00Z

    HealthStatus:
      type: object
      properties:
        status:
          type: string
          example: healthy
        gpu_available:
          type: boolean
          example: true
        database_connected:
          type: boolean
          example: true

    ErrorResponse:
      type: object
      properties:
        error:
          type: string
          example: Detailed warning text.
```

---

## 3. Client cURL Examples

System administrators and developers can verify path routes using these sample commands:

### 3.1 Authentication cURL
```bash
curl -X POST http://localhost:8000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email": "doctor_john@hospital.org", "password": "ClinicalPassword123"}'
```

### 3.2 File Upload cURL
```bash
curl -X POST http://localhost:8000/api/images/upload \
  -H "Authorization: Bearer <TOKEN>" \
  -F "file=@/path/to/scan.dcm"
```

### 3.3 Get Prediction cURL
```bash
curl -X GET http://localhost:8000/api/predictions/142 \
  -H "Authorization: Bearer <TOKEN>"
```

### 3.4 Sign off & Lock cURL
```bash
curl -X POST http://localhost:8000/api/reports/export \
  -H "Authorization: Bearer <TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{"image_id": 142, "clinical_comments": "Verified."}'
```
