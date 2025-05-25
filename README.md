# baitaptuan2
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Phân loại độ tuổi',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const AgeCheckPage(),
    );
  }
}

class AgeCheckPage extends StatefulWidget {
  const AgeCheckPage({super.key});

  @override
  State<AgeCheckPage> createState() => _AgeCheckPageState();
}

class _AgeCheckPageState extends State<AgeCheckPage> {
  final TextEditingController _nameController = TextEditingController();
  final TextEditingController _ageController = TextEditingController();
  String _result = '';

  void _checkAge() {
    String name = _nameController.text.trim();
    int? age = int.tryParse(_ageController.text.trim());

    if (name.isEmpty || age == null) {
      setState(() {
        _result = 'Vui lòng nhập đầy đủ họ tên và tuổi hợp lệ.';
      });
      return;
    }

    String category;
    if (age > 65) {
      category = 'Người già';
    } else if (age >= 6) {
      category = 'Người lớn';
    } else if (age >= 2) {
      category = 'Trẻ em';
    } else {
      category = 'Em bé';
    }

    setState(() {
      _result = '$name thuộc nhóm: $category';
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('THỰC HÀNH 01')),
      body: Padding(
        padding: const EdgeInsets.all(20.0),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            TextField(
              controller: _nameController,
              decoration: const InputDecoration(labelText: 'Họ và tên'),
            ),
            TextField(
              controller: _ageController,
              keyboardType: TextInputType.number,
              decoration: const InputDecoration(labelText: 'Tuổi'),
            ),
            const SizedBox(height: 20),
            ElevatedButton(
              onPressed: _checkAge,
              child: const Text('Kiểm tra'),
            ),
            const SizedBox(height: 20),
            Text(
              _result,
              style: const TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
            ),
          ],
        ),
      ),
    );
  }
}
