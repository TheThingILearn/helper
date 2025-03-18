---------------------------------------------------------------------------------------------------------------------------
1. create new custom action and Set the return type to "VideoPath" and Check off the Nullable.
then define a new argument call "videoFile" set it to type "UploadedFile" (FFUploadedFile) and check off the Nullable.
---------------------------------------------------------------------------------------------------------------------------
2. add that dependenie: universal_html: ^2.2.4 (Dont forget to hit the green reset button) 
---------------------------------------------------------------------------------------------------------------------------
3. add that code to the new cutsom action

```
// Automatic FlutterFlow imports
import '/backend/schema/structs/index.dart';
import '/backend/supabase/supabase.dart';
import '/flutter_flow/flutter_flow_theme.dart';
import '/flutter_flow/flutter_flow_util.dart';
import '/custom_code/actions/index.dart'; // Imports other custom actions
import '/flutter_flow/custom_functions.dart'; // Imports custom functions
import 'package:flutter/material.dart';
// Begin custom action code
// DO NOT REMOVE OR MODIFY THE CODE ABOVE!

import 'dart:io';

import 'package:universal_html/html.dart' as html;
import 'package:flutter/foundation.dart';

Future<String> videoPreviewV2(FFUploadedFile videoFile) async {
  Uint8List? videoBytes = videoFile.bytes;
  String? url;

  if (kIsWeb && videoBytes != null) {
    //Web - Convert Uint8List to Blob URL
    final blob = html.Blob([videoBytes]);
    url = html.Url.createObjectUrlFromBlob(blob);
  } else {
    //Mobile/Desktop - Save file locally and return the path
    final tempDir = Directory.systemTemp;
    final filePath = '${tempDir.path}/${videoFile.name}';
    final file = File(filePath);
    await file.writeAsBytes(videoBytes!);
    url = file.path;
  }

  return url;
}

// Set your action name, define your arguments and return parameter,
// and then add the boilerplate code using the green button on the right!e
```
---------------------------------------------------------------------------------------------------------------------------
4. Change the custom action name to "videoPreviewV2" save and check for errors
---------------------------------------------------------------------------------------------------------------------------
5. Go to your Home page add Button widget and open the Action Flow Editor (Action tree) add the "Upload/Save Media" action (Utilltles >> Upload Data >> Upload/Save Media)
set the upload type to "Local Widget (Widget State)" and the Media Source for now to Gallery, Checkon the "Allow Video" and for know
check off the 
---------------------------------------------------------------------------------------------------------------------------
6. go to your app HomePage and add a video player widget in the video type change/keep it to "NetWork"
in the path make a "conditional builder" and set the condetion to single condetion and make the first value
to the AppState you careated(videoState) and set the condetion to "Is Set" and press confirm. next make the "Then" value
To the AppState(videoState) and the else is where you will put the placeholder of the video
the deflut video - https://assets.mixkit.co/videos/preview/mixkit-forest-stream-in-the-sunlight-529-large.mp4
and hit confirm
---------------------------------------------------------------------------------------------------------------------------
7. Add a button to the home page and add on tap action, then use the cutsom code on the action block and set
an action out put to "videoFile"
---------------------------------------------------------------------------------------------------------------------------
8. create a new button and upload the file to supabase like you usually will using the action out put as the file to upload.
---------------------------------------------------------------------------------------------------------------------------
