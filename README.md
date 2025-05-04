# 9주차 플러터 연습 TIL And HomeWork
#### main.dart
<pre>
<code>
import 'package:flutter/material.dart';
import 'package:w9_w7ui123/page1.dart';
import 'package:w9_w7ui123/page2.dart';
import 'package:w9_w7ui123/page3.dart';

final imageitem = [
  'https://cdn.pixabay.com/photo/2019/11/25/16/15/sfari-4652364_1280.jpg',
  'https://cdn.pixabay.com/photo/2019/10/30/15/33/tajikistan-4589831_1280.jpg',
  'https://cdn.pixabay.com/photo/2018/11/12/18/44/thanksgiving-3811492_1280.jpg'
];

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: '복잡한 UI 작성',
      theme: ThemeData(

        colorScheme: ColorScheme.fromSeed(seedColor: Colors.black),
      ),
      home: const MyHomePage(),
      debugShowCheckedModeBanner: false,
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key});

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  var _index = 0;
  final _pages = [
    Page1(),
    Page2(),
    Page3(),
  ];



  @override
  Widget build(BuildContext context) {

    return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.white,
        title: 
        Text('복잡한 UI 페이지', 
        style:TextStyle(color:Colors.black)),
        centerTitle: true,

        actions: [
          IconButton(onPressed: () {}, 
          icon: Icon(Icons.add,color: Colors.black),
          ),
        ],
      ),
    
      body: _pages[_index],
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: _index,
          onTap: (index) {
          setState((){
            _index = index;
          });
  },
        items: [
        BottomNavigationBarItem(icon: Icon(Icons.home), label: '홈'),
        BottomNavigationBarItem(icon: Icon(Icons.assignment), label: '이용서비스'),
        BottomNavigationBarItem(icon: Icon(Icons.account_circle), label: '내 정보'),
      ]),
    );

  }
}

</code>
</pre>

<pre>
<code>
  import 'package:flutter/material.dart';
import 'package:carousel_slider/carousel_slider.dart';
import 'package:w9_w7ui123/main.dart';



class Page1 extends StatelessWidget{
  @override
  Widget build(BuildContext context){
    return ListView(
      children: <Widget>[
        _buildTop(),
        _buildMiddle(),
        _buildBottom(),
      ],
    );
  }

  Widget _buildTop(){
    return Padding(
      padding: const EdgeInsets.only(top: 20, bottom: 20),

    child: Column(
      children: [
        Row(
          mainAxisAlignment: MainAxisAlignment.spaceEvenly,
          children: [
            _buildCar('대리'),
            _buildCar('택시'),
            _buildCar('똑타'),
            _buildCar('자가용'),
          ],
        ),
        SizedBox(height: 20),
        Row(
          mainAxisAlignment: MainAxisAlignment.spaceEvenly,
          children: [
            _buildCar('아반떼'),
            _buildCar('소나타'),
            _buildCar('sm5'),
            _buildCar('제네시스'),
          ],
        ),
      ],
    )
    );
  }

  Widget _buildCar(String title) {
    return Column(
      children: [
        Icon(
          Icons.local_taxi,
          size: 40,
        ),
        Text(title)
      ],
    );
  }

    Widget _buildMiddle(){
    return CarouselSlider(
      options: CarouselOptions(
        height: 450,
        autoPlay: true,
      ),
      items: imageitem.map((url){
        return Builder(
          builder: (BuildContext context){
            return Container(
              width: MediaQuery.of(context).size.width,
              margin: EdgeInsets.symmetric(horizontal: 20),
              child: ClipRRect(
                borderRadius: BorderRadius.circular(8),
                child: Image.network(url, fit: BoxFit.cover),
              )
            );
          }
        );
      }).toList(),
      );
  }

    Widget _buildBottom(){
      final items = List.generate(10, (i){

    return ListTile(
      leading: Icon(Icons.notifications_none),
      title: Text('(${i+1}) [공지사항]'),
    );
  });

  return ListView(
    physics: NeverScrollableScrollPhysics(),
    shrinkWrap: true,
    children: items,
  );
  }
  }
</code>
      </pre>

과제 : 

값(데이터)과 값을 화면에 표현하는 로직을 구분하여 구현하는 것이 왜중요한가? : <br>
1. 유지보수 용이성 <br>
2. 코드의 재사용성 및 확장성  <br>
3. 테스트 용이성 <br>
4. 협업 효율 <br>
5. 코드 구조의 명확성 등<br>
결론적으로, 값과 화면 로직을 분리하는 것은 코드를 더 체계적으로 관리하고, 변경에 유연하게 대처하며, 여러 사람이 효율적으로 협력하여 품질 높은 소프트웨어를 개발하는 데 필수적인 과정이기 때문.

<br>
값과 화면 구성을 구분해서 화면 구성을 좀 더 효과적으로 전개할 방법은 ? : <br>
<br>
1. 데이터 정의 부분을 분리합니다.<br>
   Page1 위젯 외부(또는 별도의 데이터 파일)에 화면에 표시될 데이터를 리스트 등의 형태로 정의합니다. <br>
<br>
<예시>
</code>
// 예시: 별도의 데이터 파일 또는 Page1 클래스 외부
final List<String> carServiceTypes = ['대리', '택시', '똑타', '자가용'];
final List<String> carModels = ['아반떼', '소나타', 'sm5', '제네시스'];
// 이미지 URL 리스트도 마찬가지로 외부에 정의 (현재 main.dart에 있다고 가정)
// final List<String> imageitem = [...];

// 공지사항 목록도 데이터로 분리
final List<String> noticeItems = List.generate(10, (i) => '(${i+1}) [공지사항]');
</code>
  

