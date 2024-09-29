# Portfolio_app
import 'package:flutter/material.dart';
import 'package:google_fonts/google_fonts.dart';
import 'package:url_launcher/url_launcher.dart';

void main() => runApp(MyPortfolioApp());

class MyPortfolioApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'My Portfolio',
      theme: ThemeData(
        textTheme: GoogleFonts.poppinsTextTheme(),
        primarySwatch: Colors.blue,
      ),
      home: PortfolioHomePage(),
    );
  }
}

class PortfolioHomePage extends StatelessWidget {
  final String profilePicUrl =
      'https://example.com/your_profile_picture.png'; // Replace with your profile picture URL

  final List<String> skills = ['Flutter', 'Dart', 'Firebase', 'UI/UX'];

  final List<Map<String, String>> projects = [
    {
      'title': 'Currency Converter',
      'description': 'A description of your project.',
      'url': 'https://github.com/your_project_1'
    },
    {
      'title': 'Weather App',
      'description': 'A description of your project.',
      'url': 'https://github.com/your_project_2'
    },
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('My Portfolio'),
      ),
      body: SingleChildScrollView(
        padding: EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            // Profile Section
            Center(
              child: CircleAvatar(
                radius: 60.0,
                backgroundImage: AssetImage('Resources/Images/umar.JPG'),
              ),
            ),
            SizedBox(height: 20.0),
            Center(
              child: Text(
                '13-Umar Yameen',
                style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
              ),
            ),
            Center(
              child: Text(
                'Flutter Developer',
                style: TextStyle(fontSize: 18, color: Colors.grey),
              ),
            ),
            SizedBox(height: 30.0),

            // Skills Section
            Text(
              'Skills',
              style: TextStyle(fontSize: 22, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 10.0),
            Wrap(
              spacing: 8.0,
              children: skills
                  .map((skill) => Chip(
                        label: Text(skill),
                      ))
                  .toList(),
            ),
            SizedBox(height: 30.0),

            // Projects Section
            Text(
              'Projects',
              style: TextStyle(fontSize: 22, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 10.0),
            Column(
              children: projects
                  .map((project) => Card(
                        child: ListTile(
                          title: Text(project['title']!),
                          subtitle: Text(project['description']!),
                          trailing: IconButton(
                            icon: Icon(Icons.open_in_new),
                            onPressed: () async {
                              if (await canLaunch(project['url']!)) {
                                await launch(project['url']!);
                              }
                            },
                          ),
                        ),
                      ))
                  .toList(),
            ),
            SizedBox(height: 30.0),

            // Contact Section
            Text(
              'Contact',
              style: TextStyle(fontSize: 22, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 10.0),
            Row(
              children: [
                Icon(Icons.email),
                SizedBox(width: 10.0),
                Text('chauhadryumar@gmail.com'),
              ],
            ),
            SizedBox(height: 10.0),
            Row(
              children: [
                Icon(Icons.phone),
                SizedBox(width: 10.0),
                Text('03219619215'),
              ],
            ),
          ],
        ),
      ),
    );
  }
}
