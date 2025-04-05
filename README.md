# reflac

A Python script to recompress FLAC audio files in a specified directory using the FLAC command-line tool. It processes files in parallel with a configurable compression level and provides a progress bar with success/failure tracking.

## Features

- **Parallel Processing**: Utilizes 75% of available CPU threads for efficient re-encoding.
- **Configurable Compression**: Supports FLAC compression levels from 0 (fastest) to 8 (highest compression), defaulting to 5.
- **Progress Tracking**: Displays a real-time progress bar with percentage, processed files, and success/failure counts.
- **Error Reporting**: Lists detailed errors with full file paths for any failed re-encodings.
- **User Confirmation**: Prompts for confirmation before starting, showing the directory, file count, compression level, and thread count.
- **Cross-Platform**: Works on Windows, macOS, and Linux with proper path handling.

## Prerequisites

- **Python 3.6+**: Required to run the script.
- **FLAC**: The FLAC command-line tool must be installed and available in your system PATH.
  - On Windows: Download from [Xiph.org](https://xiph.org/flac/download.html).
  - On Linux: Install via your package manager (e.g., `sudo apt install flac` on Ubuntu).
- **Colorama**: Python library for colored terminal output (`pip install colorama`).

## Installation

1. Clone or download this repository:
   ```bash
   git clone https://github.com/rubic-codes/reflac.git
   cd reflac
   ```
2. Install the required Python dependency:
   ```bash
   pip install colorama
   ```
3. Ensure `flac` is installed and accessible:
   ```bash
   flac --version
   ```
   If this fails, install FLAC as per your operating system instructions above.

## Usage

Run the script from the command line with optional arguments:

### Basic Usage
Recompress FLAC files in the current directory with default compression level (5):
```bash
python reflac.py
```

### Specify Directory and Compression Level
Recompress FLAC files in a specific directory with a custom compression level (e.g., 8):
```bash
python reflac.py -d /path/to/music -c 8
```

### Command-Line Options
- `-d, --directory`: Directory to search for FLAC files (default: current directory).
- `-c, --compression`: Compression level from 0 to 8 (default: 5).

### Example Output
```
Searching for FLAC files in: /path/to/music
Located 20 FLAC files.
Directory scanned: /path/to/music
Files found: 20
Compression level: 5
Threads to use: 6

Start the re-encoding process? (Y/n): y

Processing with compression level 5 using 6 threads.
[##########          ]  50% (10/20) | Success: 10   | Failed: 0   
[##################################################] 100% (20/20) | Success: 19   | Failed: 1   

Recompression process finished.

Encountered the following issues:
----------------------------------------------------------------------
Failed to process /path/to/music/38 - appears (Armin van Buuren's Rising Star 12_ Instrumental mix).flac:
  ERROR initializing encoder
  init_status = FLAC__STREAM_ENCODER_INIT_STATUS_ENCODER_ERROR
  state = FLAC__STREAM_ENCODER_IO_ERROR
  An error occurred opening the output file; it is likely that the output
  directory does not exist or is not writable, the output file already exists and
  is not writeable, the disk is full or the file has a filename that exceeds the
  path length limit.
----------------------------------------------------------------------
```

## Notes

- **Thread Usage**: The script uses 75% of available CPU threads to balance performance and system responsiveness.
- **Error Handling**: If FLAC is not installed or files fail to process, detailed errors are shown with full paths.
- **Confirmation**: Press 'Y' or Enter to start; any other input aborts the process.

## Contributing

Feel free to submit issues or pull requests:
1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/your-feature`).
3. Commit your changes (`git commit -m "Add your feature"`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Open a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Built with Python and the `colorama` library for enhanced terminal output.
- Depends on the FLAC tool by Xiph.Org Foundation.
