---
title: Audio File Manipulation Research
---

## SoX - Sound eXchange

Mixing multiple audio files into a single audio file is straightforward with sox.

SoX is available at http://sox.sourceforge.net, but in case you have qualms about going to SourceForge (as I do), I can send you the version for your machine. You can also install it via whatever package manager, in case whatever machine this ultimately ends up running on is a Linux machine.

### Combining multiple audio files

    sox -m audio_file_1.wav audio_file_2.wav {audio_file_n.wav} output_file.wav

will return an audio file ``output_file.wav`` the length of whichever ``audio_file_x.wav`` is longest, where all the input audio files are played simultaneously starting at time 0.

### Clipping an audio file

Syntax

    sox audio.wav newaudio.wav trim [SECOND TO START] [SECONDS DURATION]

so the command

    sox input_audio.wav output_audio.wav trim 8 10

saves ``input_audio.wav`` from seconds 8 to 18 as ``output_audio.wav``

### Output multiple files

By default, SoX writes to a single output file.

A new file is created after the completion of any effects listed before pseudo-effect ``newfile``. The files are automatically suffixed with a number, but this can be customized by placing ``%n`` in the file name where the number should be substituted. An optional number can be placed after the ``%`` to specify a minimum fixed width for the number.

Example:

Given an audio file 300 seconds in length, the command:

    sox -m file.wav outfile%3n.wav trim 0 50 : newfile : trim 0 50 : newfile : trim 0 50 : newfile : trim 0 50 : newfile : trim 0 50 : newfile : trim 0 50

will split ``file.wav`` into six files: ``outfile001.wav``, ``outfile002.wav``, ``outfile003.wav``, ``outfile004.wav``, ``outfile005.wav``, ``outfile006.wav``, each 50 seconds in length.

### But what are we trying to do again?

Pipes.

    (test piping example, add here)
