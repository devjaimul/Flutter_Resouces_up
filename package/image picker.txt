import 'dart:io';

import 'package:flutter/foundation.dart';
import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';

import '../utils/app_colors.dart';
import '../utils/text_style.dart';

class ImgPicker extends StatefulWidget {
  const ImgPicker({super.key});

  @override
  State<ImgPicker> createState() => _ImgPickerState();
}

class _ImgPickerState extends State<ImgPicker> {
  File? _image;
  final ImagePicker _picker = ImagePicker();

  @override
  Widget build(BuildContext context) {
    Future<void> getImage() async {
      final pickedFile = await _picker.pickImage(source: ImageSource.gallery);
      setState(() {
        if (pickedFile != null) {
          _image = File(pickedFile.path);
        } else {
          if (kDebugMode) {
            print('no img found');
          }
        }
      });
    }

    return Column(
      children: [
        CircleAvatar(
          radius: 100,
          backgroundImage: _image == null
              ? const NetworkImage('https://4.bp.blogspot.com/-7lKcs3VI8Kg/WtgJ__'
              '1RxaI/AAAAAAAAF9Q/6XFIxYxnGkspQc7-kvDMlzf-8cx0_khewCEwYBhgL/s1600/best%2Bprofile%2Bpics.png')
              : Image.file(_image!).image,
        ),
        const SizedBox(height: 20),
        SizedBox(
          width: double.infinity,
          child: ElevatedButton(
            onPressed: getImage,
            style: ElevatedButton.styleFrom(
              backgroundColor: AppColors.primaryColor,
              padding: const EdgeInsets.all(10),
            ),
            child: const HeadingTwo(data: 'Change Picture', color: Colors.white),
          ),
        ),
      ],
    );
  }
}
