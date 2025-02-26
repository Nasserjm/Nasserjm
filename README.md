import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Tap to Cash Prototype',
      home: HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Tap to Cash'),
      ),
      body: Center(
        child: ElevatedButton(
          child: Text('اضغط لتحويل الأموال'),
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => TransferScreen()),
            );
          },
        ),
      ),
    );
  }
}

class TransferScreen extends StatefulWidget {
  @override
  _TransferScreenState createState() => _TransferScreenState();
}

class _TransferScreenState extends State<TransferScreen> {
  final TextEditingController _amountController = TextEditingController();
  bool _isTransferring = false;
  String _message = '';

  void _startTransfer() async {
    setState(() {
      _isTransferring = true;
      _message = '';
    });

    // محاكاة عملية تحويل الأموال
    await Future.delayed(Duration(seconds: 2));

    setState(() {
      _isTransferring = false;
      _message = 'تم التحويل بنجاح!';
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('تحويل الأموال'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            TextField(
              controller: _amountController,
              keyboardType: TextInputType.number,
              decoration: InputDecoration(
                labelText: 'أدخل المبلغ',
                border: OutlineInputBorder(),
              ),
            ),
            SizedBox(height: 20),
            _isTransferring
                ? CircularProgressIndicator()
                : ElevatedButton(
                    onPressed: _startTransfer,
                    child: Text('تحويل'),
                  ),
            SizedBox(height: 20),
            Text(_message),
          ],
        ),
      ),
    );
  }
}
