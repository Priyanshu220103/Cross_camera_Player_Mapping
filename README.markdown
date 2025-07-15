# Cross-Camera Player Mapping

## Overview
This project implements a cross-camera player tracking system that detects and matches players across two video feeds (broadcast and tacticam) using the YOLOv8 object detection model and ResNet18 for visual feature extraction. It processes videos to identify players, assigns global IDs based on visual features, and saves the player mappings to a CSV file (`player_mapping.csv`).

## Features
- **Player Detection**: Uses YOLOv8 to detect players, goalkeepers, referees, and balls in video frames.
- **Feature Extraction**: Extracts visual features from detected players using a pre-trained ResNet18 model.
- **Cross-Camera Matching**: Matches players across broadcast and tacticam videos based on visual feature similarity (cosine distance).
- **Output**: Generates a CSV file (`player_mapping.csv`) with player IDs, frame numbers, and bounding box coordinates for both camera views.

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/cross-camera-player-mapping.git
   ```
2. Navigate to the project directory:
   ```bash
   cd cross-camera-player-mapping
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Install PyTorch and Ultralytics YOLO:
   ```bash
   pip install torch torchvision ultralytics
   ```
5. Download the pre-trained YOLOv8 model (`best.pt`) and place it in the project root or specify its path in the code.

## Requirements
- Python 3.8+
- Libraries: `torch`, `torchvision`, `ultralytics`, `opencv-python`, `numpy`, `pandas`, `scipy`
- Pre-trained YOLOv8 model (`best.pt`)
- Input videos: `broadcast.mp4` and `tacticam.mp4`

## Usage
1. Place the input videos (`broadcast.mp4` and `tacticam.mp4`) in the project directory or update the paths in `main()`.
2. Run the Jupyter Notebook:
   ```bash
   jupyter notebook Cross_Camera_Player_Mapping.ipynb
   ```
3. Execute all cells to:
   - Detect players in both videos.
   - Extract and match visual features.
   - Save the mapping to `player_mapping.csv`.
4. The output CSV contains columns: `player_id`, `frame`, `broadcast_x`, `broadcast_y`, `broadcast_w`, `broadcast_h`, `tacticam_x`, `tacticam_y`, `tacticam_w`, `tacticam_h`.

## CSV Output
The generated `player_mapping.csv` file contains player tracking data with the following structure:
- **player_id**: Unique identifier for each player.
- **frame**: Video frame number.
- **broadcast_x/y/w/h**: Bounding box coordinates (center x, y, width, height) in the broadcast video.
- **tacticam_x/y/w/h**: Bounding box coordinates in the tacticam video.

Example:
```csv
player_id,frame,broadcast_x,broadcast_y,broadcast_w,broadcast_h,tacticam_x,tacticam_y,tacticam_w,tacticam_h
0,5,1598.256958,774.729675,85.261963,131.224731,1315.894775,850.463745,46.197632,77.162109
0,7,1681.445068,485.933441,62.173096,78.424622,896.524414,608.258667,49.063293,64.435364
...
```

## Project Structure
```
cross-camera-player-mapping/
├── data/                    # Input videos (broadcast.mp4, tacticam.mp4)
├── models/                  # YOLOv8 model (best.pt)
├── output/                  # Output CSV (player_mapping.csv)
├── Cross_Camera_Player_Mapping.ipynb  # Main Jupyter Notebook
├── requirements.txt          # Dependencies
└── README.md                # This file
```

## Notes
- The YOLOv8 model (`best.pt`) must be trained or obtained for player detection.
- Ensure input videos are synchronized and have compatible frame counts.
- Adjust the `feature_threshold` (default: 0.7) in `match_players()` for better matching accuracy if needed.
- The notebook filters players visible in both views using `both_views_df`.

## Contributing
1. Fork the repository.
2. Create a feature branch (`git checkout -b feature-branch`).
3. Commit changes (`git commit -m "Add new feature"`).
4. Push to the branch (`git push origin feature-branch`).
5. Open a Pull Request.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact
For questions or feedback, open an issue or contact [your-email@example.com](mailto:your-email@example.com).