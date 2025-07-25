**deepfake detection tools**

triage - ExifTool, MediaInfo, FFmpeg
	`exiftool -a -G video_file.mp4`
	mediainfo - Extracts technical and tag data (codecs, frame rates, software used
	ffmpeg - inspect stream-level metadata
	`ffprobe -show_format -show_streams video.mp4`
	OR
	`ffprobe -v quiet -show_streams -show_format -print_format json video_file.mp4`
		
reverse search - InVID (extension)

deepfake detection - Deepware, DFDNet
	Deepware scanner ([website](https://scanner.deepware.ai/))  ([CLI](https://github.com/Hook35/deepfake-scanner))-   scans deepfake fingerprints
	DFDNet ([github](https://github.com/csxmli2016/DFDNet)) - facial reconstructions

manual inspection - Zoom frames, look for jitter, lip sync inconsistency, blinking rate, etc.