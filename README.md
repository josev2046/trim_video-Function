## trim_video Function
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.15173478.svg)](https://doi.org/10.5281/zenodo.15173478)

This function uses `subprocess.run` to trim a video file using ffmpeg's `ffmpeg -i input.mp4 -ss start_time -to end_time -c copy output.mp4.`

![image](https://github.com/user-attachments/assets/29560939-8a66-4f26-814a-120d6a07c5fb)


### Function Signature

~~~```json
def trim_video(input_path: str, output_path: str, start_time: str, end_time: str) -> bool:
    """
    Trims a video file using ffmpeg.

    Args:
        input_path: Path to the input video file.
        output_path: Path to the output (trimmed) video file.
        start_time: Start time of the trim (e.g., "00:00:10", "10").
        end_time: End time of the trim (e.g., "00:00:20", "20").

    Returns:
        True if the trim was successful, False otherwise.
    """
~~~

### Description

The `trim_video` function constructs an `ffmpeg` command to extract a segment from a video. It then executes this command using `subprocess.run`. The function handles potential errors during the `ffmpeg` execution by catching the `subprocess.CalledProcessError` exception and providing informative error messages.

### Dependencies

`subprocess` (Python standard library)

### Arguments

* `input_path` (str): The file path of the video to be trimmed.
* `output_path` (str): The desired file path for the trimmed video output.
* `start_time` (str): A string representing the start time of the segment to extract. This can be in various `ffmpeg` time formats (e.g., "seconds", "HH:MM:SS").
* `end_time` (str): A string representing the end time of the segment to extract (same format as `start_time`).

### Returns

`bool`: Returns `True` if the `ffmpeg` command executes successfully, indicating a successful trim. Returns `False` if an error occurs during execution.

### Error Handling

The function handles errors by:

*  Catching the `subprocess.CalledProcessError` exception, which is raised if the `ffmpeg` command returns a non-zero exit code.
*  Printing the error message from `ffmpeg`'s standard error (`stderr`) to the console, providing insight into the `ffmpeg` failure.
*  Returning `False` to signal the failure to the calling code.

### Example Usage

~~~```python
input_video = "path/to/input.mp4"
output_segment = "path/to/output.mp4"
start = "00:00:05"
end = "00:00:15"

if trim_video(input_video, output_segment, start, end):
    print("Video trimmed successfully!")
    # Proceed with further processing
else:
    print("Video trimming failed.")
    # Handle the error
~~~

### Notes

* This function assumes that ffmpeg is installed and accessible in the system's PATH.
* The `start_time` and `end_time` arguments should be formatted according to ffmpeg's time specifications.
* Consider adding more robust input validation (e.g., checking file existence, time format validation) for production code.
