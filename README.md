# Jefferson

## Binaural Spatializer in OpenGL and CUDA

This project uses OpenGL to create a 3D visualization of two objects in space and then convolves audio using an HRTF to match the distance and angle of the two objects. It also utilizes parallel processing and the speed of a GPU. The project’s original purpose was to experiment with parallel processing and to see if CUDA can speed up real-time convolution, which I have not been able to solve yet. However, this result can be useful for VR/AR audio and being able to record audio whose source is being moved in 3D space.

Using libsndfile, this project takes in a 44.1k sample rate input file and reverb impulse response. If the input file is stereo, it is summed to mono using the formula R[i] = (L[i] + R[i]) / 2. If the reverb file is in stereo, the program terminates. Using cuFFT, it does convolution reverberation on the input file, and then stores that data into a buffer in the RAM and onto the disk as a file. I used thrust to calculate the RMS of both signals. Then, the program reads and stores 366 different HRTF impulse responses at various elevations and azimuths. The audio starts playing through PortAudio, and the graphical interface is then displayed to affect what is played.

A purple cartoon character indicates the listener, which remains is movable around the space. The green indicates the sound source which is stationary in the middle. Different keys listed below will move the sound source in the X, Y, and Z axes. The visualization can also be rotated by left clicking and dragging the visualization which helps to better visualize the 3D space. The user can also zoom in and out by clicking and dragging the right arrow key or by using the scroll wheel. The R key will reset back to the default perspective and position. My program also optionally writes the output to a sound file.

The cartoon character, which I’ve fondly named Jefferson, is available here as a [free]( https://free3d.com/3d-model/cartoon-character-47048.html) download. The letter J was created in Microsoft’s Paint 3D. I used Blender to combine, resize, scale, and export the character’s parts to a 3ds file, which I then imported into my program. 

## Tools list:
**OpenGL** - short for Open Graphics Library. It is an API/library in several programming languages to draw 2D and 3D images. It’s portable and it’s implemented primarily in each computer’s hardware.

**CUDA** - acronym for Compute Unified Device Architecture. It’s “a parallel computing platform and programming model developed by NVIDIA for general computing on graphical processing units (GPUs)” (Nvidia). It is a proprietary but free API in several different programming languages to speak directly to NVIDIA hardware and utilize parallel processing.

[General Knowledge](https://developer.nvidia.com/cuda-zone)

[Download link](https://developer.nvidia.com/cuda-zone)

[Documentation](https://docs.nvidia.com/cuda/)

**cuFFT** – NVIDIA CUDA Fast Fourier Transform library.

[General knowledge](https://developer.nvidia.com/cufft)

[Documentation](https://docs.nvidia.com/cuda/cufft/index.html)


**Thrust** – “Thrust is a C++ template library for CUDA based on the Standard Template Library (STL)” (Nvidia). It’s a library within CUDA that utilizes parallel processing for algorithms that already exist in C++’s standard library such as summing, reducing, and sorting.

[NVIDIA Documentation](https://docs.nvidia.com/cuda/thrust/index.html)

[GitHub Documentation](https://thrust.github.io/)

**HRTF** – acronym for Head Related Transfer Function. Several short audio filters depending on angle (azimuth) and elevation that can make a sound come from different locations in 3D space. The ones I used were the compact set from [MIT and KEMAR](http://sound.media.mit.edu/resources/KEMAR.html)

**PortAudio** - Portable audio library used to connect to the computer’s sound device

[Download link](http://www.portaudio.com/)

**Libsndfile** – Portable audio library used to read contents of wave files

[Download link](http://www.mega-nerd.com/libsndfile/)

**Blender** – Open source, free 3D creation suite

[Download link](https://blender.org/)

**3ds** – 3D Model file type importable/exportable by blender. I used [Damiano Vitulli’s](http://spacesimulator.net/tutorials/index.html) code to import 3ds files into my OpenGL program.

## Future Plans:
(in no particular order)  
-Incorporate more GPU Acceleration  
-Attempt to use NVIDIA's ray-tracing technology for audio  
-Include a waveform that passes through Jefferson's head  
-Be able to include more sound objects  
