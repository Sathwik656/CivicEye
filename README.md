# **CivicEye: Traffic Violation Detection Software**

## **Introduction**
CivicEye is an innovative software designed to detect and monitor traffic violations using home-based CCTV cameras. It empowers users to identify common traffic rule violations, such as riding without helmets or triple riding, in real-time. The software integrates seamlessly with user-provided CCTV systems, processes violations locally, and sends critical data and evidence to a centralized database. Users can access detailed violation logs and reports via a dedicated website.

---

## **Objectives**
1. **Traffic Violation Detection:** Leverage AI-powered object detection (YOLOv3) to identify violations like "no helmet," "triple riding," and more.
2. **Automated Data Reporting:** Send violation data (images, timestamps, types) from the client’s system to a centralized database.
3. **Centralized Monitoring:** Allow users to view and manage detected violations via a web dashboard.
4. **Privacy and Efficiency:** Enable local processing on the client’s machine, ensuring data privacy and reducing server costs.
5. **Scalability:** Create a robust, user-friendly software that can be downloaded and run across different devices.

---

## **Key Features**
- **Real-Time Violation Detection:** Automatically detect and record traffic violations using the YOLOv3 object detection model.
- **Local Processing:** Run the detection software locally on the client’s machine, minimizing data transmission.
- **Automated Reporting:** Send violation evidence (photos and metadata) to a centralized database for storage and review.
- **Web Dashboard:** Provide a user-friendly website for viewing, searching, and filtering violations.
- **Customizable Configuration:** Users can easily configure the CCTV feed (RTSP URL) and software settings.

---

## **Software Workflow**
1. **User Setup:**
   - Download the software from the official GitHub repository.
   - Configure the CCTV feed by entering the RTSP URL in the provided `config.json` file.
   - Install dependencies using:
     ```bash
     pip install -r requirements.txt
     ```
   - Run the software using:
     ```bash
     python run_detection.py
     ```

2. **Violation Detection:**
   - The software streams the CCTV feed locally and processes video frames using YOLOv3.
   - Detected violations are logged, and images with bounding boxes are saved.

3. **Data Transmission:**
   - The software automatically sends violation data (timestamp, violation type, image) to a centralized server through a secure API.

4. **Centralized Monitoring:**
   - Users can log in to the web dashboard to view violation records, download reports, or review images.

---

## **Technical Specifications**
### **Development Requirements**
#### **Programming Language**
- **Python 3.8+**: Python is a versatile programming language with robust libraries for machine learning, computer vision, and web development. Version 3.8+ ensures compatibility with modern frameworks and libraries.

#### **Libraries**
1. **OpenCV**:
   - OpenCV is an open-source library used for real-time computer vision tasks.
   - In this project, it facilitates video streaming from CCTV cameras, frame extraction, and pre-processing for YOLOv3 input.
   - Example Usage:
     - Streaming a CCTV feed via RTSP.
     - Resizing frames for model input.
     - Displaying video feeds with bounding boxes.
     ```python
     import cv2
     cap = cv2.VideoCapture("rtsp://username:password@camera_ip:port")
     ret, frame = cap.read()
     cv2.imshow("Frame", frame)
     ```

2. **PyTorch**:
   - PyTorch is a machine learning framework used to implement and run YOLOv3.
   - It is used to load the pre-trained YOLOv3 model, process frames, and perform object detection.
   - Example Usage:
     - Loading YOLOv3 weights and configurations.
     - Running inference on video frames to detect objects.
     ```python
     import torch
     model = torch.hub.load('ultralytics/yolov5', 'yolov3')
     results = model(frame)
     ```

3. **Requests**:
   - Requests is a Python library for making HTTP requests.
   - It is used to send violation data (images and metadata) to the centralized server via REST APIs.
   - Example Usage:
     - Sending a POST request with violation details and images.
     ```python
     import requests
     data = {"violation_type": "No Helmet", "timestamp": "2025-02-15T10:30:00Z"}
     response = requests.post("https://your-server.com/api/violations", json=data)
     ```

4. **SQLite**:
   - SQLite is a lightweight, file-based database used for local storage of violation data.
   - It allows the software to temporarily store detected violations and metadata locally before sending them to the server.
   - Example Usage:
     - Creating a database to store violation logs.
     - Querying data for local analysis or debugging.
     ```python
     import sqlite3
     conn = sqlite3.connect("violations.db")
     cursor = conn.cursor()
     cursor.execute("CREATE TABLE IF NOT EXISTS Violations (id INTEGER PRIMARY KEY, timestamp TEXT, violation_type TEXT)")
     ```

### **Hardware Requirements**
#### For Clients:
- **Processor:** Intel i3 or higher
- **RAM:** 4GB (8GB recommended)
- **GPU:** Optional (YOLOv3-tiny can run on CPU)
- **Storage:** 20GB free disk space

#### For Centralized Server:
- **Processor:** 16-core CPU (e.g., Intel Xeon)
- **RAM:** 32GB
- **GPU:** NVIDIA Tesla T4 or equivalent
- **Storage:** 1TB SSD for video and metadata storage

---

## **Setup Instructions**
1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/CivicEye.git
   ```
2. Navigate to the project directory and install dependencies:
   ```bash
   cd roadwatch
   pip install -r requirements.txt
   ```
3. Update the `config.json` file with your CCTV RTSP URL and other preferences.
4. Start the detection software:
   ```bash
   python run_detection.py
   ```

---

## **API Endpoint**
- **POST /api/violations**
  - **Request Body:**
    ```json
    {
      "timestamp": "2025-02-15T10:30:00Z",
      "violation_type": "No Helmet",
      "client_id": "client_123",
      "image_data": "base64_encoded_image"
    }
    ```
  - **Response:**
    ```json
    {
      "status": "success",
      "message": "Violation data stored successfully."
    }
    ```

---

## **Web Dashboard**
1. **URL:** [https://CivicEye-dashboard.com](https://CivicEye-dashboard.com)
2. **Features:**
   - View detailed violation logs.
   - Filter by violation type, date, or client.
   - Download images and reports.

---

## **Future Enhancements**
1. Add support for more traffic violations (e.g., signal jumping, wrong-way driving).
2. Enable multi-language support for broader accessibility.
3. Implement live notification features (e.g., email or SMS alerts).
4. Optimize the YOLO model for Indian road conditions.

---

## **Support**
For issues or feature requests, please open a ticket in the [GitHub Issues](https://github.com/your-repo/CivicEye/issues) section or contact us at support@CivicEye.com.

