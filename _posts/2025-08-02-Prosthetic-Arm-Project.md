---
title: "EMG-Controlled Prosthetic Arm Design"
categories:
  - Project
tags:
  - EMG
  - Arduino
  - Prosthetics
  - Circuit Design
  - Signal Processing
date: 2025-08-02
---

# EMG-Controlled Prosthetic Arm: From Signal to Grip

As part of my BME 261 (Prototyping, Simulation and Design) course, my team developed an innovative low-cost prosthetic arm controlled by electromyographic (EMG) signals. This project challenged us to integrate mechanical design, electrical signal processing, and firmware development into a functional assistive device.

## Project Overview

<div style="text-align: center; margin: 30px 0;">
  <img src="/assets/Posts/Prosthetic-Arm/Gallery Walk Poster.png" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <p style="font-style: italic; margin-top: 15px; color: #666;">Research poster showcasing our prosthetic arm design and development process</p>
</div>

Our team of three biomedical engineering students set out to create a prosthetic hand that could interpret muscle contractions from the forearm and translate them into precise gripping motions. The device targets users who need basic functional support for workshop tasks like holding rulers, securing nails, or stabilizing materials while their other hand performs precision work.

<div style="text-align: center; margin: 30px 0;">
  <img src="/assets/Posts/Prosthetic-Arm/CAD Gripper Design.png" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <p style="font-style: italic; margin-top: 15px; color: #666;">CAD model showing the mechanical gripper design with gear system</p>
</div>

## The Challenge

Traditional prosthetic hands often lack the precision needed for delicate workshop tasks. Our project focused on the **Cybathlon Do-It-Yourself challenge**, which requires prosthetic devices to support active motion across multiple axes in confined spaces. We specifically targeted the precision holding aspect - enabling reliable grip and manipulation of small components like screws and nails.

### Design Constraints

- **Budget**: Maximum $50 CAD for the entire project
- **Manufacturing**: Limited access to specialized tools; relied on 3D printing and laser cutting
- **Signal Processing**: Arduino Uno's processing capabilities and 200Hz sampling rate
- **Integration**: Three subsystems (mechanical, electrical, firmware) had to work seamlessly together

## Technical Implementation

### Mechanical Subsystem

The mechanical design converts a single servo motor's rotation into coordinated finger-like pinching motion:

**Key Components:**
- Acrylic base plate with integrated gear system
- Two 24-tooth acrylic gears driving the gripping arms
- 12-tooth driver gear connected to servo motor
- 3D-printed motor housing and motion limiters
- Rubber band-enhanced grip surfaces for improved friction

**Design Philosophy:** Every component was chosen for its balance of lightweight construction, cost-effectiveness, and manufacturing simplicity. The gear ratios were carefully calculated to provide sufficient torque while maintaining precise control.

### Electrical Subsystem

The EMG signal processing pipeline required sophisticated analog conditioning:

**Signal Processing Chain:**
1. **Instrumentation Amplifier (AD623)**: Amplifies weak raw EMG signals (~100μV to 10mV) with large gain
2. **Multiple-Feedback Bandpass Filter**: Isolates 100-500Hz frequency range containing muscle activity
3. **Full-Wave Precision Rectifier**: Converts bipolar EMG signal to unipolar magnitude representation  
4. **Peak Detector**: Smooths signal with 5-second RC time constant for stable threshold detection

**Technical Challenges:** Operating with single 6V supply limited output swing. Used 2.5V reference voltage to bias signals within Arduino's 0-5V input range.

<div style="text-align: center; margin: 30px 0;">
  <img src="/assets/Posts/Prosthetic-Arm/EMG Filtering Signal.jpg" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <p style="font-style: italic; margin-top: 15px; color: #666;">EMG signal processing stages showing raw input and final envelope output</p>
</div>

### Firmware and Signal Classification

The Arduino-based control system implements intelligent muscle contraction classification:

**Activation Logic:**
- **Threshold Detection**: 3V activation threshold determined through experimental trials
- **Short Impulses** (100-800ms): Toggle grip direction
- **Long Impulses** (>800ms): Incremental 5° servo rotation every 200ms
- **Noise Rejection**: 200ms minimum duration prevents false triggers from arm movement

**Real-Time Performance:** System operates at 200Hz with minimal latency, providing responsive control that feels natural to users.

## Results and Testing

<div style="text-align: center; margin: 30px 0;">
  <img src="/assets/Posts/Prosthetic-Arm/Testing All Components.jpg" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <p style="font-style: italic; margin-top: 15px; color: #666;">Comprehensive testing setup with all subsystems</p>
</div>

Our prosthetic successfully demonstrated:

**Reliable object gripping** - Consistent grasp/release of small workshop items  
**Intuitive EMG control** - Users quickly adapted to muscle-based commands  
**Low-cost construction** - Final build under $50 budget  
**Modular design** - Easy assembly/disassembly for iterations

### Performance Metrics

- **Activation accuracy**: >95% correct classification of intended commands
- **Response time**: <100ms from muscle contraction to motor activation  
- **Grip strength**: Sufficient for holding screws, nails, and small tools
- **Battery life**: Several hours of continuous operation

## Technical Innovations

### EMG Signal Processing
Our frequency domain analysis of raw EMG data guided optimal bandpass filter design. We collected unfiltered EMG signals, performed FFT analysis, and validated our 100-500Hz passband effectively preserved muscle activity while attenuating 60Hz power line noise and motion artifacts.

### Adaptive Thresholding
Rather than using a fixed activation threshold, we experimentally determined optimal values by analyzing multiple users' EMG patterns. The 3V threshold with 200ms minimum duration struck the right balance between responsiveness and false trigger prevention.

### Mechanical Precision
Our gear system design prioritized precision over raw force. The 2:1 gear ratio (24-tooth driven, 12-tooth driver) provided fine control while maintaining sufficient torque for reliable gripping.

## Lessons Learned

**Technical Insights:**
- Analog signal conditioning is crucial for reliable EMG interpretation
- Mechanical tolerancing becomes critical in low-cost manufacturing
- Firmware classification logic must balance responsiveness with robustness

**Project Management:**
- Early prototyping revealed manufacturing constraints that influenced design decisions
- Interdisciplinary collaboration required clear interface definitions between subsystems
- Testing with actual users provided invaluable feedback for threshold optimization

## Future Improvements

For higher-fidelity iterations, we recommend:

**Mechanical Enhancements:**
- Steel gears to eliminate slippage issues
- Multi-articulated fingers with silicone joints
- Adjustable straps and padded contact points for comfort

**Control Improvements:**
- Multi-channel EMG for gesture classification
- Machine learning-based pattern recognition
- Wrist rotation and additional degrees of freedom

**User Experience:**
- Integrated electronics housing
- Haptic feedback for grip confirmation

## Conclusion

This project successfully demonstrated that sophisticated prosthetic control can be achieved within tight budget and timeline constraints. By combining careful analog signal processing, intelligent firmware classification, and precision mechanical design, we created a functional EMG-controlled prosthetic that addresses real user needs.

The experience reinforced the importance of interdisciplinary collaboration in biomedical engineering. Success required not just technical competency in each domain, but also careful attention to the interfaces between mechanical, electrical, and software systems.

Most importantly, this project highlighted the potential for low-cost assistive technologies to make a meaningful impact. With further refinement, devices like ours could provide affordable prosthetic solutions for users worldwide.

---