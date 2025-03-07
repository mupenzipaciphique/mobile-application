import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: PhoneHome(),
    );
  }
}

class PhoneHome extends StatefulWidget {
  @override
  _PhoneHomeState createState() => _PhoneHomeState();
}

class _PhoneHomeState extends State<PhoneHome> {
  int _selectedIndex = 0;

  // Function to refresh and display current time
  String getCurrentTime() {
    return DateTime.now().toString();
  }

  // Menu options
  static const List<Widget> _widgetOptions = <Widget>[
    SayHelloScreen(),
    ShowTimeScreen(),
    ExitScreen(),
  ];

  // Handle bottom navigation selection
  void _onItemTapped(int index) {
    setState(() {
      _selectedIndex = index;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Phone App Menu'),
        backgroundColor: Colors.blue,
      ),
      body: Center(
        child: _widgetOptions.elementAt(_selectedIndex),
      ),
      bottomNavigationBar: BottomNavigationBar(
        items: const <BottomNavigationBarItem>[
          BottomNavigationBarItem(
            icon: Icon(Icons.message),  // Fixed icon name here
            label: 'Say Hello',
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.access_time),
            label: 'Show Time',
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.exit_to_app),
            label: 'Exit',
          ),
        ],
        currentIndex: _selectedIndex,
        onTap: _onItemTapped,
      ),
    );
  }
}

// Say Hello Screen
class SayHelloScreen extends StatelessWidget {
  const SayHelloScreen({Key? key}) : super(key: key);  // Made constructor const

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Icon(Icons.access_alarm, size: 100, color: Colors.blue),
        SizedBox(height: 20),
        Text(
          'Hello, User! 👋',
          style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
        ),
      ],
    );
  }
}

// Show Time Screen
class ShowTimeScreen extends StatelessWidget {
  const ShowTimeScreen({Key? key}) : super(key: key);  // Made constructor const

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Icon(Icons.access_time, size: 100, color: Colors.blue),
        SizedBox(height: 20),
        Text(
          'Current Date & Time: ${DateTime.now()}',
          style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
        ),
      ],
    );
  }
}

// Exit Screen
class ExitScreen extends StatelessWidget {
  const ExitScreen({Key? key}) : super(key: key);  // Made constructor const

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Icon(Icons.exit_to_app, size: 100, color: Colors.red),
        SizedBox(height: 20),
        Text(
          'Goodbye! 👋',
          style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold, color: Colors.red),
        ),
        SizedBox(height: 20),
        ElevatedButton(
          onPressed: () {
            // Close the app (works on real devices)
            Navigator.pop(context);
          },
          child: Text('Exit App'),
        ),
      ],
    );
  }
}
