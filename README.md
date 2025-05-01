# Advanced License Plate Detection with Dehazing

A sophisticated license plate detection and recognition system that incorporates image dehazing, enhancement techniques, and OCR to accurately extract license plate information from challenging images.
Available for use on: https://license-plates.streamlit.app/

## Features

- **Advanced Image Preprocessing**: Incorporates CLAHE and Gaussian sharpening for image enhancement
- **Deep Learning Dehazing**: Custom UNet-based dehazing model for improving visibility in hazy conditions
- **Two-Stage Processing**: Attempts direct detection first, then falls back to enhanced processing if needed
- **License Plate Format Validation**: Intelligent text cleaning and format validation for Indian license plates
- **Interactive Web Interface**: Built with Streamlit for easy usage without technical knowledge

## Technical Stack

- **YOLOv8**: For license plate detection (using a custom-trained model)
- **PaddleOCR**: For text recognition from license plate images
- **PyTorch**: For the custom dehazing neural network
- **OpenCV**: For image processing and enhancement
- **Streamlit**: For the web interface
- **Concurrent Processing**: Utilizes asyncio and concurrent.futures for performance

## Installation

```bash
# Clone the repository
git clone https://github.com/TheFallen04/license_plate.git
cd license_plate

# Create a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

## Required Files

Make sure you have the following model files in your project directory:
- `best.pt`: YOLOv8 model trained for license plate detection
- `dehazing_unet.pth`: PyTorch model for image dehazing

## Usage

Run the Streamlit app:

```bash
streamlit run app.py
```

Then open your web browser and navigate to the displayed URL (typically http://localhost:8501).

## How It Works

1. **Upload Image**: User uploads an image containing a license plate
2. **First Pass Detection**: The system attempts to detect and read the license plate directly
3. **Enhancement (if needed)**: If detection fails, the system applies:
   - CLAHE for contrast enhancement
   - Gaussian sharpening for edge enhancement
   - Deep learning-based dehazing
4. **Second Pass Detection**: Detection and OCR are attempted again on the enhanced image
5. **Text Cleaning**: Detected text is cleaned and formatted to match standard license plate formats

## Dehazing Model Architecture

The system includes a custom UNet-based neural network for image dehazing:

- **Encoder-Decoder Architecture**: UNet-style network with skip connections
- **Residual Blocks**: For improved gradient flow and feature learning
- **Batch Normalization**: For training stability
- **LeakyReLU Activation**: For better gradient propagation

## License Plate Format Validation

The system is optimized for Indian license plate formats:
- Standard format: `XX00XX0000` (e.g., TN18D1866)
- With hyphens: `XX-00-X-0000` (e.g., TN-18-D-1866)

The system also implements intelligent correction for common OCR mistakes (e.g., '0' vs 'O').

## Requirements

```
streamlit>=1.24.0
opencv-python>=4.6.0
numpy>=1.23.0
torch>=1.12.0
torchvision>=0.13.0
pillow>=9.2.0
ultralytics>=8.0.0
paddleocr>=2.6.0
```



---

Created by [TheFallen04](https://github.com/TheFallen04), [Pranav](https://github.com/pranav-999)
