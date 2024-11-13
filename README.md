# Computer Vision-based Traffic Violation Detection System

**Student ID**: 1000129  
**Name**: Janisha Hota  
**School**: Delhi Public School, Bangalore North  
**Email**: janishahota@gmail.com  

---

## Introduction:
Computer vision is a field of artificial intelligence (AI) that uses machine learning and neural networks to teach computers and systems to derive meaningful information from digital images, videos and other visual inputs—and to make recommendations or take actions when they see defects or issues. (2) Nowadays, Computer vision is in great demand and used in different areas, including robotics, manufacturing, healthcare, etc. (3)

---

## Problem Statement:
Road Rules Are Not Suggestions – They’re Lifesavers. (5) Following traffic rules and safety guidelines is of the utmost importance to avoid life-threatening accidents from occurring. According to official statistics published by the Ministry of Road Transport and Highways (MoRTH), 153,972 persons were killed in road crashes in the year 2021 in India. This corresponds to 11.3 deaths per 100,000 population. (1) With enforced regulations and fines to discourage irresponsible driving, this rate will decrease. Due to the rise in private vehicles in India over the past few years due to the pandemic, the workload on the traffic police has greatly increased too. In case of any incidents or traffic rules violations, there should be repercussions for the perpetrator, to ensure safety and mindfulness on roads.

---

## Goal and Objective:
To create an AI Traffic violation detection model that can detect red light running, triples riding, using a phone while driving and helmet detection on a two-wheeler using computer vision and machine learning.

---

## Approach:
I will be following the traditional waterfall SDLC model, which consists of a top-down approach while following the stages of the Software Development Life Cycle (SDLC) (Clark, n.d.).

1. **Planning**:  
   I first fine-tuned my idea. I surveyed to understand people's opinions on traffic violation detection and which violations they’ve witnessed occur frequently.  
   - Survey link: [Google Form Survey](https://forms.gle/ojh6PLXofioks5Te9)  
   - Survey responses:  
   I researched various current technological solutions for traffic violation detection, such as the e-Challan system in Karnataka, where violations are detected in real-time and fines are given to the vehicle’s registered owner. I decided to make a similar basic model for a few violations, based on the most occurring violations witnessed, which I obtained through my survey responses. They were red-light running, 2-wheeler Helmet detection and triples detection, and the usage of phones while driving.

2. **Defining**:  
   In this stage, I planned for what resources I would require, and how the app could be utilised. The resources required would be datasets for the following:  
   - Car (for red-light running)  
   - Motorcycle/2-wheeler (for triples detection and no helmet detection)  
   - Helmet/No Helmet (for no helmet detection)  
   - Traffic Light (for red-light running)  
   - Phone (for Phone usage while driving)  
   - Steering Wheel (for Phone usage while driving)  
   - People (for triples detection)

3. **Designing**:  
   In this stage, I turn my plan into a framework for the project. I have developed an ideal user experience storyboard.
   
   **[Storyboard made using canva.com]**

4. **Development/Building**:  
   I used Pycharm as the platform for creating the Python code.  
   **Libraries used**:  
   - Subprocess  
   - Yolo  
   - Matplotlib  
   - Cv2  
   - Numpy

   I started by splitting the code into separate parts based on the violation.  
   
   - **Red Light Running**:  
      - Loaded YOLOv8 model to detect “traffic light” and “car.”
      - Defined a vertical violation zone where car positions are checked.
      - Created a function to detect red traffic lights using HSV color space.
      - Processed each video frame with YOLO, filtered detections by confidence, and checked if a car in the violation zone coincided with a red light.
      - Drew bounding boxes on detected objects and the violation zone for clarity.
      - Calculated detection accuracy based on true and false positives and displayed frames with detected violations.

   - **Phone Usage while Driving**:  
      - Loaded two YOLO models: one for detecting cell phones and a custom model for detecting steering wheels.
      - Opened the video file and initialised counters for total frames and frames with both phone and wheel detected.
      - For each frame, I ran the phone model and the wheel model separately.
      - Checked if a detected object was a cell phone (green box) or a wheel (blue box) and drew bounding boxes with labels.
      - If both objects were detected, counted the frame and updated the highest confidence frame if the current confidence was greater.
      - Displayed each frame with bounding boxes in real-time.
      - After processing, the accuracy as the percentage of frames where both objects were detected.
      - Displayed the best frame (highest confidence) if a violation was detected.

   - **Helmet Detection on a 2-wheeler**:  
      - Load YOLOv8 model for detecting the "helmet" and "without helmet" classes.
      - Open video file, initialise a list to track violation frames and total frames.
      - Loop through video frames:
        - Run model inference on each frame.
        - Identify objects as "helmet" or "without helmet" based on detections.
        - For "without helmet":
          - Record frame and confidence score.
          - Draw red bounding box with label.
        - For "helmet":
          - Draw green bounding box with confidence score.
        - Display each frame with bounding boxes.
      - After processing, sort violation frames by confidence.
      - Display each top violation frame.

   - **Triples Detection**:  
      - Load YOLOv8 model and open the video file.
      - Initialize counters for frames, violations, and detections.
      - Loop through each frame, running YOLO on it to detect objects.
      - For each detection:
        - Check if the object is a two-wheeler or a person.
        - Store bounding box coordinates and draw them with color-coded labels.
      - For each detected two-wheeler:
        - Calculate distances to detected people.
        - If three or more people are within a certain distance, flag a violation and store the frame.
      - Calculate detection accuracy as average detections per frame.
      - Display each frame with bounding boxes and accuracy info.
      - Store and display frames where violations were detected.
      - Summarise results: total frames, violation count, and final detection accuracy.

   I then called all the codes in a single program, thus ensuring that the processing rate would be efficient.

5. **Testing and Deployment**:  
   Each violation detection model was tested independently to validate that the bounding boxes and violation conditions were functioning correctly. For example, I confirmed that the red-light-running detector accurately recognized cars crossing a designated boundary while the light was red, and similarly, that helmet and phone detection flagged violations accurately. The Accuracy rate for each of the models were:  
   - No Helmet Detection: 85%  
   - Phone Usage while driving: 74%  
   - Red-light running: 94%  
   - Triples Detection: 78.99%

---

## Limitations:
- **Model Accuracy in Varied Environments**: The YOLOv8 model may perform inconsistently in different lighting conditions, weather, or complex backgrounds. For example, poor lighting or rainy conditions may reduce detection accuracy for objects like helmets, traffic lights, or two-wheelers.
- **False Positives and False Negatives**: Despite a high confidence threshold, the model may occasionally misclassify objects, such as detecting non-helmet objects as helmets or failing to detect a person on a two-wheeler. This impacts the reliability of violation detection, leading to false alerts or missed violations.
- **Detection Speed and Real-time Processing**: Running YOLOv8 on video or real-time feeds may cause processing delays, especially on standard hardware, limiting its applicability for real-time enforcement or monitoring.

---

## Future Scope:
- **Real-time Optimization**: Improving model efficiency through model compression can enable real-time violation detection, making it feasible for live traffic monitoring and enforcement.
- **Integration with License Detection and Tracking**: With car license plate detection, we can track which vehicles have done a violation and send fines to the registered vehicle's owner.

---

## Results and Conclusion:
By developing this traffic violation model, I've had many key takeaways. By implementing the SDLC process, I've experienced what it's like to be in the shoes of a developer and learned firsthand how it might be as a profession in the future. I have also learned more about the real-life applications of computer vision and its implementation.

---

## References:
- https://tripc.iitd.ac.in/assets/publication/RSI_2023_web.pdf  
- https://www.ibm.com/topics/computer-vision  
- https://www.javatpoint.com/computer-vision-applications  
- Clark, H. (n.d.). *The Software Development Life Cycle (SDLC): 7 Phases and 5 Models*. The Product Manager. Retrieved January 15, 2024, from https://theproductmanager.com/topics/software-development-life-cycle/  
- https://infinitylearn.com/surge/english/slogans/slogans-on-traffic-rules/#:~:text=%E2%80%9CRoad%20Rules%20Are%20Not%20Suggestions,%2C%20Red%20Light%20for%20Risk
