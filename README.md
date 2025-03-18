---------------------------------------------------------------------------------------------------------------------------
1. create new custom action and Set the return type to "VideoPath" and Tick off the Nullable.
then define a new argument call "videoFile" set it to type "UploadedFile" (FFUploadedFile) and Tick off the Nullable.
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
5.a Go to your Home page add a Button widget and open the Action Flow Editor (Action tree),in the action tree add the 
"Upload/Save Media" action (Utilltles >> Upload Data >> Upload/Save Media),
and set the upload type to "Local Widget (Widget State)" then set the Media Source to "Gallery" for now, Tick on the "Allow Video" 
and for now Tick off the "Allow Photo".

b. 

 in the same action tree add new action and set it to the custom action we made (videoPreviewV2), set the "VideoFile" argument to the
"Uploaded Local File" from the First action we created, and give a name to the "Action Output Variable Name"

---------------------------------------------------------------------------------------------------------------------------
6. add a video player widget and set the video type to "NetWork" set the path to the Action Output you created.
now for the place holder the one that FlutterFlow give is not good is doing alot of lags for the video player widget
so what i recomend for now is to upload a random video to your supabase storage then copy the url from supabase and
use it as the place holder(Default Variable Value).
---------------------------------------------------------------------------------------------------------------------------
7. create a new button and upload the file to supabase like you usually will using the action out put as the file to upload.
---------------------------------------------------------------------------------------------------------------------------
