## Data

### Input

ViameWeb takes two different kinds of clips, video file, and image sequences. Both kinds could be accompanied with a CSV file for annotation data.

### Output
The system saves to CSV file directly when the save button is pressed

## Architecture
VIAMEWeb has a typical girder + girder worker + docker architecture. Command-line executable VIAME and FFmpeg are built inside the worker docker image. See related docker scripts for detail

## Client
The client application is a standard [@vue/cli](https://cli.vuejs.org/) application. The video/image sequence playback and the timeline at the bottom are created meant to be composable and reusable. However, the ImageAnnotator and VideoAnnotator probably should inherit from the same base class as they share a lot of code base.

## Limitation
* The client app loads all annotations for a clip at once, which wouldn't scale when the clip is long or has many annotations. One possible solution is load annotations by chunk, this will need more logic in code and might need server-side help for anything that is needed such as the timeline.
* Reading and saving directly to CSV will have performance impact for longer clips and can't support chunk load or provide server side help for client functionality. 
* Currently, the upload need to upload each image separately via girder endpoint, which has a large overhead making uploading large image sequence slow