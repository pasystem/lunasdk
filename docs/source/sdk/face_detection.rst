Face detection and landmarks
============================

Luna VL provides methods for faces detection on images and find landmarks on it.

Face detection
--------------

Detectors
~~~~~~~~~

There are 3 face detectors: *FACE_DET_V1, FACE_DET_V2, FACE_DET_V3*. *FaceDetV1* detector is more precise and
*FaceDetV2* works two times faster. *FaceDetV1* and *FaceDetV2* performance depends on number of faces on image and
image complexity. *FaceDetV3* performance depends only on target image resolution. *FACE_DET_V3* is the latest and most
precise detector. In terms of performance it is similar to *FaceDetV1* detector. *FaceDetV3*  may be slower then
*FaceDetV1* on images with one face and much more faster on images with many faces.


You should create a face detector using the method *createFaceDetector* of class *VLFaceEngine* for faces detection.
You should set detector type when creating detector. Once initialize detector can be using as many times as you like.

.. warning::

    We don’t recommend create often new detector because it is very slowly operation.

Redection
~~~~~~~~~

If there is only one image with a face bounding box on it, you can run the redetect method for a faster face detect
(face detection structure creation), with landmarks. Also, you can run redetect if the face bounding box belongs to
another image and a face shift was small. For example, you have frame sequence with the same face. You can detect face
on the first frame and redetect this face fast on the next frames.

Face alignment
--------------

Face alignment is the process of special key points (called "landmarks") detection on a face. FaceEngine does landmark
detection at the same time as the face detection since some of the landmarks are by products of that detection.


Landmarks5
~~~~~~~~~~

At the very minimum, just 5 landmarks are required: two for eyes, one for a nose tip and two for mouth corners. Using
these coordinates, one may warp the source photo image for use with all other FaceEngine
algorithms. All detector may provide 5 landmarks for each detection without additional computations.

*landmarks5* contains the following landmarks:

============            ==================
Array index             Landmark location
============            ==================
0                       Left eye center
------------            ------------------
1                       Right eye center
------------            ------------------
2                       Nose tip
------------            ------------------
3                       Left mouth corner
------------            ------------------
4                       Right mouth corner
============            ==================


Landmarks68
~~~~~~~~~~~

More advanced 68-points face alignment is also implemented. Use this when you need precise information about face and
its parts. The 68 landmarks require additional computation time, so don’t use it if you don’t need precise information
about a face. If you use 68 landmarks, 5 landmarks will be reassigned to more precise subset of 68 landmarks.


*landmarks68* contains the landmarks according to I-Bug 68-point annotation scheme.

.. image:: figure_68_markup.jpg

Examples
--------

.. literalinclude:: ../../../examples/sdk_examples/face_detection.py

.. literalinclude:: ../../../examples/sdk_examples/face_redetection.py

.. automodule:: lunavl.sdk.faceengine.facedetector
    :members:
