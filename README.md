# 9주차 플러터 연습 TIL And HomeWork
#### main.dart
<pre>
<code>
  import 'package:flutter/material.dart';
import 'package:url_launcher/url_launcher.dart';
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

값(데이터)과 값을 화면에 표현하는 로직을 구분하여 구현하는 것이 왜중요한가? :
값과 화면 구성을 구분해서 화면 구성을 좀 더 효과적으로 전개할 방법은 ? : 
