1. Create an AppState name "videoState" and set the data type to "Video Path" (notes the upper and lower case in the name)
---------------------------------------------------------------------------------------------------------------------------
2. create new custom action and Import that Package: universal_html: ^2.2.4 (Dont forget to hit the green reset button) 
---------------------------------------------------------------------------------------------------------------------------
3. add that code to the new cutsom action

import 'package:file_picker/file_picker.dart';
import 'package:universal_html/html.dart' as html;

Future<FFUploadedFile?> videoPreviewFinal() async {
  final result = await FilePicker.platform.pickFiles(type: FileType.video);

  if (result != null && result.files.isNotEmpty) {
    final videoFile = result.files.first;

    Uint8List? videoBytes = videoFile.bytes;
    String? url;

    if (videoBytes != null) {
      // ✅ Web: Convert Uint8List to Blob URL
      final blob = html.Blob([videoBytes]);
      url = html.Url.createObjectUrlFromBlob(blob);
    } else if (videoFile.path != null) {
      // ✅ Android & iOS: Use file path
      url = videoFile.path!;
    }

    // ✅ Create FFUploadFile object
    final FFUploadedFile ffUploadFile = FFUploadedFile(
      name: videoFile.name,
      bytes: videoBytes,
    );

    // ✅ Ensure url is not null before updating FFAppState
    if (url != null) {
      FFAppState().update(() {
        FFAppState().videoState = url!;
      });
    }

    return ffUploadFile;
  }

  return null; // Ensures function always returns a value
}
---------------------------------------------------------------------------------------------------------------------------
4. make the return value UploadedFile and tick the null box
---------------------------------------------------------------------------------------------------------------------------
5.
