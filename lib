import 'package:flutter/material.dart';
import 'dart:async';

void main() => runApp(const MyCoolApp());

class MyCoolApp extends StatelessWidget {
  const MyCoolApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: '水動力 Pro',
      // 白天模式
      theme: ThemeData(
        brightness: Brightness.light,
        primarySwatch: Colors.blue,
      ),
      // 深色模式
      darkTheme: ThemeData(
        brightness: Brightness.dark,
        scaffoldBackgroundColor: const Color(0xFF121212),
        primarySwatch: Colors.indigo,
      ),
      themeMode: ThemeMode.system, // 跟隨系統切換黑白
      home: HydroDashPro(),
    );
  }
}

class HydroDashPro extends StatefulWidget {
  @override
  _HydroDashProState createState() => _HydroDashProState();
}

class _HydroDashProState extends State<HydroDashPro> {
  double waterLevel = 0.0; // 水位高度 (0.0 到 1.0)
  int goal = 2000;         // 目標 2000ml
  int current = 0;         // 目前喝水量

  @override
  void initState() {
    super.initState();
    // 設定定時器：每 30 分鐘提醒一次
    Timer.periodic(const Duration(minutes: 30), (timer) {
      _showReminder();
    });
  }

  void _showReminder() {
    // 檢查 context 是否還有效，避免頁面關閉後還跳彈窗
    if (!mounted) return;
    
    showDialog(
      context: context,
      builder: (context) => AlertDialog(
        title: const Text('💦 該喝水囉！動一動'), // 這裡之前漏掉了逗號
        content: const Text('為了保持運動表現，現在請喝一杯水。'),
        actions: [
          TextButton(
            onPressed: () => Navigator.pop(context),
            child: const Text('收到'),
          )
        ],
      ),
    );
  }

  void _addWater() {
    setState(() {
      if (current < goal) {
        current += 250;
        waterLevel = current / goal; // 計算百分比
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('水動力 Pro'), backgroundColor: Colors.blueAccent),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            // 水杯動畫區塊
            Container(
              width: 100,
              height: 200,
              decoration: BoxDecoration(
                border: Border.all(width: 3, color: Colors.grey),
                borderRadius: BorderRadius.circular(10), // 加一點點圓角比較像杯子
              ),
              child: Stack(
                alignment: Alignment.bottomCenter,
                children: [
                  // 藍色的水
                  AnimatedContainer(
                    duration: const Duration(milliseconds: 500),
                    width: 100,
                    height: 200 * waterLevel,
                    color: Colors.blue[300],
                  ),
                ],
              ),
            ),
            const SizedBox(height: 20),
            Text('$current / $goal ml', 
              style: const TextStyle(fontSize: 24, fontWeight: FontWeight.bold)),
            const SizedBox(height: 30),
            ElevatedButton(
              onPressed: _addWater,
              style: ElevatedButton.styleFrom(
                padding: const EdgeInsets.symmetric(horizontal: 30, vertical: 15),
              ),
              child: const Text('動一動喝杯水(250ML)')
            ),
          ],
        ),
      ),
    );
  }
}
