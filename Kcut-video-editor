kcut-video-editor/
│
├── lib/
│   ├── main.dart
│   ├── screens/
│   │   ├── home.dart
│   │   ├── editor.dart
│   │   └── export.dart
│   ├── ads/admob.dart
│   └── video/ffmpeg_helper.dart
│
├── assets/
│   ├── music/
│   └── icons/
│
├── pubspec.yaml
└── android/
name: kcut
description: Fast Video Editor
version: 1.0.0+1

environment:
  sdk: ">=3.0.0 <4.0.0"

dependencies:
  flutter:
    sdk: flutter
  image_picker: ^1.0.7
  ffmpeg_kit_flutter: ^6.0.3
  google_mobile_ads: ^4.0.0
  path_provider: ^2.1.2
  import 'package:flutter/material.dart';
import 'screens/home.dart';
import 'package:google_mobile_ads/google_mobile_ads.dart';

void main() {
  WidgetsFlutterBinding.ensureInitialized();
  MobileAds.instance.initialize();
  runApp(const KCut());
}

class KCut extends StatelessWidget {
  const KCut({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'KCut',
      theme: ThemeData.dark(),
      home: const Home(),
    );
  }
}
final picker = ImagePicker();
final video = await picker.pickVideo(source: ImageSource.gallery);
import 'package:ffmpeg_kit_flutter/ffmpeg_kit.dart';

class FF {
  static Future<void> export720(String input, String output) async {
    await FFmpegKit.execute(
      "-i $input -vf scale=1280:720 -preset ultrafast $output"
    );
  }

  static String speed(double x) => "-filter:v setpts=${1/x}*PTS";
  static String volume(double v) => "-filter:a volume=$v";
}
import 'package:google_mobile_ads/google_mobile_ads.dart';

class Ads {
  static RewardedInterstitialAd? ad;

  static void load() {
    RewardedInterstitialAd.load(
      adUnitId: "ca-app-pub-3940256099942544/5354046379",
      request: const AdRequest(),
      rewardedInterstitialAdLoadCallback:
        RewardedInterstitialAdLoadCallback(
          onAdLoaded: (a) => ad = a,
          onAdFailedToLoad: (_) => ad = null,
        ),
    );
  }

  static void show(Function done) {
    if (ad != null) {
      ad!.show(onUserEarnedReward: (_, __) => done());
    } else {
      done();
    }
  }
}
Ads.show(() {
  FF.export720(input, output);
});
KCut does not collect personal data.
All videos are processed locally.
Ads are shown via Google AdMob.
