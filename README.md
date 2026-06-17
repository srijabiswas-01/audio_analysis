# audio_analysis
Modern AI and machine learning tools convert these sound waves into visual maps called spectrograms.

# Audio Source Separation & Analysis Pipeline

1. Install Dependencies
2. Import Libraries
3. Upload Audio
4. Validate Duration
5. Convert to WAV
6. Run Demucs Separation
7. Locate Output Folder Automatically
8. Create ZIP of Stems
9. Extract Metadata
10. Preview Audio Stems
11. Visualize Waveforms
12. Visualize Spectrograms
13. Visualize Pitch
14. Pitch Shift Vocals
15. Reconstruct Full Mix
16. Optional Interactive Controls


## Overall Project Description
This project implements an end-to-end audio processing pipeline in Google Colab using open-source Python libraries. The system uploads an audio file, validates its duration, converts it into a standard format, separates it into vocals, drums, bass, and other instruments using Demucs, performs audio analysis and visualization, enables vocal pitch modification, reconstructs the final remix, and exports the generated outputs and metadata for further processing or research.

## Part 1: Audio Upload, Pre-processing, and Source Separation
The first part initializes the environment by installing all required dependencies and importing the necessary libraries. It allows users to upload an audio file directly from Google Colab, validates that its duration does not exceed the configured limit, converts the audio into a standardized WAV format using FFmpeg, and performs source separation using Demucs. Finally, it automatically locates the generated stems and packages them into a ZIP archive for convenient access.

## Part 2: Metadata Extraction and Audio Visualization
The second part focuses on analysing the separated stems by extracting useful metadata such as duration, sampling rate, RMS energy, peak amplitude, file size, and estimated tempo. It also provides embedded audio playback for each component and visualizes the waveform, spectrogram, and frequency spectrum of every stem. The collected metadata is stored in a structured CSV file for documentation and future analysis.

## Part 3: Vocal Pitch Modification and Audio Reconstruction
The third part estimates the pitch contour of the separated stems and applies pitch shifting exclusively to the vocal track while preserving the instrumental components. After modifying the vocal frequency by a configurable number of semitones, it reconstructs the complete song by combining the shifted vocals with the drums, bass, and other stems. The final output is normalized to reduce clipping and saved as a new audio file.

## Part 4: Interactive Remixing and Export
The final part introduces interactive controls using widgets that allow users to dynamically adjust vocal pitch and independently control the gain of vocals, drums, bass, and other stems. Upon generating a remix, the system reconstructs and previews the updated audio in Colab. It also exports metadata reports and packages all generated files into a ZIP archive, creating a reproducible and user-friendly audio processing workflow.

## Library Documentation
### 1. google.colab.files
Purpose: Handles file uploads and downloads within the Google Colab environment.

Why it is used:
It enables users to upload audio files directly from their local machine into the notebook and optionally download processed outputs such as separated stems, metadata reports, and remixed audio files without requiring external storage services.

### 2. subprocess
Purpose: Executes external command-line programs from Python.

Why it is used:
The pipeline uses subprocess to invoke FFmpeg for audio conversion and Demucs for source separation. This approach integrates powerful external tools while allowing Python to automate their execution and monitor completion.

### 3. pathlib.Path
Purpose: Provides an object-oriented interface for filesystem paths.

Why it is used:
Path simplifies file and directory handling across operating systems, making it easier to detect output folders, construct file paths, iterate through generated stems, and perform file operations in a readable and portable manner.

### 4. shutil
Purpose: Performs high-level file operations.

Why it is used:
The library creates ZIP archives of separated stems and processed outputs, allowing users to conveniently download multiple generated files in a single compressed package.

### 5. os
Purpose: Interfaces with the operating system.

Why it is used:
It retrieves file names, sizes, and filesystem information required for metadata generation and report creation while supporting basic path-related operations.

### 6. numpy
Purpose: Efficient numerical computing library.

Why it is used:
NumPy performs mathematical operations on audio arrays, including RMS energy computation, peak amplitude detection, normalization, FFT calculations, and signal manipulation during remixing.

### 7. pandas
Purpose: Data manipulation and tabular analysis.

Why it is used:
Metadata collected from each separated stem is organized into structured DataFrames, allowing easy visualization, processing, and export to CSV format for documentation and research purposes.

### 8. librosa
Purpose: Comprehensive library for music and audio analysis.

Why it is used:
librosa serves as the core audio-processing library, providing audio loading, duration estimation, tempo detection, pitch estimation, Short-Time Fourier Transform (STFT), waveform analysis, and pitch-shifting functionality used throughout the pipeline.

### 9. librosa.display
Purpose: Visualization utilities for audio signals.

Why it is used:
It renders spectrograms and other audio-related plots, enabling users to visually inspect frequency content and temporal changes within the separated stems.

### 10. soundfile (sf)
Purpose: Reading and writing audio files.

Why it is used:
After pitch shifting and remixing, soundfile writes the processed NumPy arrays back into standard audio formats such as WAV while preserving sampling rate information.

### 11. matplotlib.pyplot
Purpose: Scientific plotting library.

Why it is used:
It generates static visualizations including pitch contours and spectrograms, making it easier to interpret audio characteristics and processing results.

### 12. plotly.graph_objects
Purpose: Interactive plotting framework.

Why it is used:
Plotly produces zoomable and interactive waveform and frequency spectrum plots, allowing users to explore audio signals in greater detail than static images.

### 13. mutagen
Purpose: Audio metadata handling library.

Why it is used:
Although optional in this workflow, mutagen can read embedded metadata from audio files such as tags and technical information, supporting richer file inspection and reporting.

### 14. IPython.display.Audio
Purpose: Embedded audio playback in notebooks.

Why it is used:
It creates playable audio widgets inside Google Colab, enabling users to instantly listen to separated stems, pitch-shifted vocals, and reconstructed remixes without downloading files.

### 15. IPython.display.display
Purpose: Displays rich notebook outputs.

Why it is used:
It renders tables, widgets, plots, and audio players interactively within Colab, improving the usability and presentation of analysis results.

### 16. ipywidgets
Purpose: Interactive graphical controls for Jupyter notebooks.

## Why it is used:
Widgets such as sliders and buttons allow users to adjust pitch shifts and stem gains dynamically, creating an intuitive interface for experimenting with remix parameters without modifying the source code.

## Why Demucs?
Demucs is a deep learning–based music source separation model trained to isolate components such as vocals, drums, bass, and accompaniment from mixed recordings. It was selected because it provides high-quality separation across many genres and languages, operates locally without requiring paid APIs, and integrates seamlessly into Python-based workflows for research and portfolio projects.

## Why FFmpeg?
FFmpeg is used to standardize uploaded audio into a consistent WAV format with a fixed sample rate and channel configuration. This preprocessing step ensures compatibility with downstream libraries such as Demucs and Librosa and improves reliability when handling diverse input formats including MP3, FLAC, M4A, AAC, and WAV.
