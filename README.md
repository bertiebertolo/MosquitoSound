# Mosquito Electrophysiology Analysis

[![Work In Progress](https://img.shields.io/badge/status-work%20in%20progress-yellow.svg)](https://github.com/groupmosquito/MosquitoSound)
[![Python](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

> **⚠️ Note**: This repository is a work in progress and represents ongoing research and experimentation. Code, structure, and methodologies are subject to significant changes as the project evolves.

## Overview

This project analyzes electrophysiological recordings from mosquito auditory neurons in response to acoustic stimuli. The pipeline processes raw neural recordings from two mosquito species (*Culex* and *Aedes aegypti*) through signal processing, feature extraction, and deep learning models for classification and synthesis.

### Research Goals
- Extract and analyze neural response patterns from mosquito auditory nerve recordings
- Classify species-specific auditory responses using deep learning
- Generate synthetic neural responses using generative adversarial networks (GANs)
- Identify key acoustic features that drive neural activation

## Project Status

🚧 **Active Development** - This repository contains experimental code and exploratory analyses. Expect:
- Frequent updates and refactoring
- Changes to data processing pipelines
- Evolution of model architectures
- Code cleanup and documentation improvements

**Data Note**: Raw electrophysiology data has been removed for confidentiality. The notebooks demonstrate methodology and can be adapted to similar datasets.

## Pipeline Architecture

```
.smr files (Spike2) 
    ↓
WAV conversion (bandpass filtering)
    ↓
Feature extraction (spectrograms/MFCCs)
    ↓
Deep learning models (CNN autoencoder, GAN)
    ↓
Analysis & synthesis
```

## Notebooks

### Data Processing
- **`Sonogram_analysis.ipynb`** - Initial data exploration and sonogram generation from Spike2 files
- **`wav_analysis.ipynb`** - Converts .smr files to WAV format with bandpass filtering (0-1000 Hz)
- **`Converting to wav file.ipynb`** - Alternative conversion methods and Griffin-Lim reconstruction

### Feature Extraction & Modeling
- **`CNN_analysis.ipynb`** - Convolutional autoencoder for spectrogram feature extraction
- **`CNN_recpmstruction.ipynb`** - Autoencoder reconstruction experiments
- **`CNN_wav_analysis.ipynb`** - MFCC-based CNN classification experiments

### Generative Models
- **`4_MFCCGAN_mrh020615.ipynb`** - MelGAN-based architecture for audio synthesis from MFCCs

## Key Technologies

- **Signal Processing**: Neo (Spike2 file reading), SciPy (filtering), Librosa (audio features)
- **Deep Learning**: TensorFlow/Keras (autoencoders), PyTorch (GANs)
- **Data Analysis**: NumPy, Pandas, Scikit-learn
- **Visualization**: Matplotlib, Seaborn

## Technical Specifications

### Data Format
- **Source**: CED Spike2 electrophysiology recordings (.smr)
- **Sampling Rate**: 100,000 Hz
- **Species**: *Culex pipiens* and *Aedes aegypti*
- **Preprocessing**: Butterworth bandpass filter (0-1000 Hz, order 4)

### Model Architectures
- **CNN Autoencoder**: 128×128×3 RGB spectrograms → latent features
- **GAN**: Custom MelGAN variant with 36 MFCC coefficients
- **Training**: 80/20 train/test split with `random_state=42`

## Installation

```bash
# Clone repository
git clone https://github.com/yourusername/MosquitoSound.git
cd MosquitoSound

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install numpy pandas scipy scikit-learn
pip install librosa soundfile
pip install tensorflow torch torchvision
pip install neo matplotlib seaborn
pip install jupyter notebook
```

## Usage

**Note**: Since raw data is not included, these notebooks serve as methodology examples. To use with your own data:

1. Place Spike2 .smr files in `nerve_data_smr/{species}/`
2. Run `wav_analysis.ipynb` to convert to WAV format
3. Generate spectrograms/MFCCs using `CNN_analysis.ipynb` or `CNN_wav_analysis.ipynb`
4. Train models using the respective notebooks

## Directory Structure

```
MosquitoSound/
├── notebooks/
│   ├── CNN_analysis.ipynb
│   ├── wav_analysis.ipynb
│   └── ...
├── models/              # Saved model checkpoints (not tracked)
├── features/            # Extracted features (not tracked)
├── MRH-Baseline/        # GAN checkpoints (not tracked)

```

## Future Directions

- [ ] Implement cross-species classification
- [ ] Optimize GAN architecture for neural data
- [ ] Add comprehensive unit tests
- [ ] Create interactive visualization dashboard
- [ ] Document full experimental protocol
- [ ] Add pre-trained model weights (if publishable)

## Contributing

This is a research project in active development. Feedback, suggestions, and discussions are welcome through Issues.

## Citation

If you use this code or methodology in your research, please cite:

```
[Citation information to be added upon publication]
```

## License

MIT License 
## Contact

For questions or collaborations, please open an issue or contact albertothornton@outlook.com.

---

**Disclaimer**: This repository contains experimental research code. Methods and results are not peer-reviewed and should be validated before use in production or publication.
