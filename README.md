# FANUC iRVision System Implementation

**Author:** Dawson Burgess, Computer Science Department, University of Idaho, Moscow, ID, United States  
**Email:** [burg1648@vandals.uidaho.edu](mailto:burg1648@vandals.uidaho.edu)

## Overview

This repository contains the research paper and documentation for implementing the FANUC iRVision system on the CRX-10iA collaborative robot to detect and pick up large block dice. The project was conducted using the robot’s teaching pendant (TP) exclusively, without external APIs, focusing on vision-guided robotics for object recognition and manipulation.

### Key Features

- **Vision Setup**: Configured a robot-mounted iRVision camera with auto-calibration.
- **Process Design**: Developed a 2D single-view vision process to locate dice.
- **Robot Control**: Programmed TP code for precise pick-and-place operations.
- **Objective**: Achieved autonomous dice detection and handling in a controlled workspace.

## Project Structure

- **`FANUC_iRVision_System_Implementation.pdf`**: Research paper detailing setup, methods, and results.
- **`README.md`**: This file, providing an overview and instructions.

## Methodology

### iRVision Object Camera Setup

- **Camera Installation**: Mounted on the CRX-10iA near the end-of-arm tooling with optimized lighting.
- **Calibration**: Used "Robot-Generated Grid Calibration" with ~20 orbital positions (30+ minutes).
- **Training**: Captured dice images, masked pips for edge detection.

### Vision Process Setup

- **Type**: 2D Single-View Vision Process, storing data in Vision Register (VR[1]).
- **Offset Mode**: "Found Position" for direct Cartesian coordinates, avoiding fixed frame issues.
- **Tools**: Configured Snap Tool (200ms exposure) and GPM Locator Tool (60% score threshold).

### TP Program Implementation

- **Core Commands**: `VISION RUN_FIND`, `VISION GET_OFFSET`, and position register assignments.
- **Motion Handling**: Used `Wjnt` to manage wrist configuration and avoid "flipped" states.
- **Workflow**: Detects dice, moves to position, picks, and places at table center, looping until stopped.

## Results

- **Success**: The system reliably detects and picks dice, returning to a waiting position above the workspace.
- **Performance**: Consistent operation under controlled lighting, mimicking industrial pick-and-place tasks.

## Challenges and Limitations

- **Documentation**: Limited official resources; relied on FANUC iRVision manual and peer assistance.
- **Calibration**: Long process requiring uninterrupted button hold; prone to restart if errors occur.
- **Frames**: Initial confusion with robot motion and configuration settings (e.g., "flipped" states).

## Future Work

- Extend to multi-workspace detection (e.g., full table coverage).
- Explore Python API integration if camera access becomes available.
- Enhance with dynamic lighting adjustments for robustness.

## Installation and Usage

This project was implemented directly on the FANUC CRX-10iA teaching pendant, requiring no external software setup beyond the robot’s firmware. To replicate:

1. **Hardware**: FANUC CRX-10iA with iRVision camera module.
2. **Setup**: Follow the paper’s camera and vision process instructions.
3. **Program**: Input the TP code from Figure 11 in the paper.
4. **Run**: Execute on the TP, ensuring proper lighting and dice placement.

**Note**: No Python code is included, as the project avoids the API per constraints.

## License

This project is licensed under the [MIT License](LICENSE).

## Contact

For inquiries, contact Dawson Burgess at [burg1648@vandals.uidaho.edu](mailto:burg1648@vandals.uidaho.edu).

## Citation

If you use this project, please cite:
**Dawson Burgess. (2025). FANUC iRVision System Implementation. University of Idaho.**

## Acknowledgments

Special thanks to Jacob Friedberg for assistance with troubleshooting and resetting robot settings.
