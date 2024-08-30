note: i know the cars its just example but it makes it easier for me to work with.

in that code we have table in supabase clled "car" and we query all the table.
in that table there is 2 column, one name cars_model and the other sale_status

that the code for that

![the supabase table](https://github.com/TheThingILearn/helper/blob/main/Screenshot_2024-08-30_21-55-37.png)

![the code it self table](https://github.com/TheThingILearn/helper/blob/main/Screenshot_2024-08-30_21-56-59.png)

![the code it self table](https://github.com/TheThingILearn/helper/blob/main/that%20the%20data%20table%20i%20will%20filter%20by%20in%20that%20example%20(1).png)


![the code it self table](https://github.com/TheThingILearn/helper/blob/main/that%20the%20data%20table%20i%20will%20filter%20by%20in%20that%20example%20(2).png
)

```
// Automatic FlutterFlow imports
import '/backend/supabase/supabase.dart';
import '/flutter_flow/flutter_flow_theme.dart';
import '/flutter_flow/flutter_flow_util.dart';
import '/custom_code/actions/index.dart'; // Imports other custom actions
import '/flutter_flow/custom_functions.dart'; // Imports custom functions
import 'package:flutter/material.dart';
// Begin custom action code
// DO NOT REMOVE OR MODIFY THE CODE ABOVE!

import 'package:supabase_flutter/supabase_flutter.dart';

Future<List<CarRow>> filters(String? carsmodel, String? salestatus) async {
  final query = Supabase.instance.client.from('car').select('*');
  {
    if (carsmodel != null && carsmodel.isNotEmpty)
      query.eq('cars_model', carsmodel);
    if (salestatus != null && salestatus.isNotEmpty)
      query.eq('sale_status', salestatus);
  }

  final response = await query.execute();

  final data = response.data as List<dynamic>;
  final car = data.map((item) => CarRow(item)).toList();
  return car;
}
// Set your action name, define your arguments and return parameter,
// and then add the boilerplate code using the green button on the right!
```



now follow that video https://www.youtube.com/watch?v=7eLJvJicC3E&t=90s

now when you get to the button part just 
