# Flutter Animated Text

A flutter package which contains a collection of some cool and awesome text animations. Recommended package for text animations in Codemagic's Ebook, "Flutter libraries we love". Try out our live example app.

## Installing

1. Depend on it

Add this to your package's pubspec.yaml file:

   ```
   dependencies:
  animated_text_kit: ^4.2.2
   ```

2. Install it

You can install packages from the command line:

with pub:

   ```
   $ pub get
   ```

with Flutter:

   ```
   $ flutter pub get
   ```

3. Import it

Now in your Dart code, you can use:

   ```
   import 'package:animated_text_kit/animated_text_kit.dart';
   ```

## Usage

AnimatedTextKit is a Stateful Widget that produces text animations. Include it in your build method like:

   ```
   AnimatedTextKit(
  animatedTexts: [
    TypewriterAnimatedText(
      'Hello world!',
      textStyle: const TextStyle(
        fontSize: 32.0,
        fontWeight: FontWeight.bold,
      ),
      speed: const Duration(milliseconds: 2000),
    ),
  ],
  
  totalRepeatCount: 4,
  pause: const Duration(milliseconds: 1000),
  displayFullTextOnTap: true,
  stopPauseOnTap: true,
)
   ```

It has many configurable properties, including:

1. pause – the time of the pause between animation texts

2. displayFullTextOnTap – tapping the animation will rush it to completion

3. isRepeatingAnimation – controls whether the animation repeats

4. repeatForever – controls whether the animation repeats forever

5. totalRepeatCount – number of times the animation should repeat (when repeatForever is false)

There are also custom callbacks:

1. onTap – This is called when a user taps the animated text

2. onNext(int index, bool isLast) – This is called before the next text animation, after the previous one's pause

3. onNextBeforePause(int index, bool isLast) – This is called before the next text animation, before the previous one's pause

4. onFinished - This is called at the end, when the parameter isRepeatingAnimation is set to false

Note: You might come up with an issue that the text does not get updated with setState as shown here. The solution to this, is a key that changes based on the text. For reference, watch this video.

## New with Version 3

Version 3 refactored the code so that common animation controls were moved to AnimatedTextKit and all animations, except for TextLiquidFill, extend from AnimatedText. This saved hundreds of lines of duplicate code, increased consistency across animations, and makes it easier to create new animations.

It also makes the animations more flexible because multiple animations may now be easily combined. For example:

   ```
   AnimatedTextKit(
  animatedTexts: [
    FadeAnimatedText(
      'Fade First',
      textStyle: TextStyle(fontSize: 32.0, fontWeight: FontWeight.bold),
    ),
    ScaleAnimatedText(
      'Then Scale',
      textStyle: TextStyle(fontSize: 70.0, fontFamily: 'Canterbury'),
    ),
  ],
),
   ```

Using the legacy FadeAnimatedTextKit is equivalent to using AnimatedTextKit with FadeAnimatedText. An advantage of AnimatedTextKit is that the animatedTexts may be any subclass of AnimatedText, while using FadeAnimatedTextKit essentially restricts you to using just FadeAnimatedText.

Legacy AnimatedTextKit classes

Have you noticed that animation classes come in pairs? For example, there is FadeAnimatedText and FadeAnimatedTextKit. The significant refactoring with Version 3 split the original FadeAnimatedTextKit into FadeAnimatedText and a re-usable AnimatedTextKit, then FadeAnimatedTextKit was adjusted for backwards compatibility.

When introducing a new AnimationText subclass, you may wonder if you also need to also introduce an additional Kit class. The answer is NO. 🎉

Going forward, we are championing the adoption of the Version 3 approach, and have deprecated the legacy Kit classes. This will make creating new animations easier. We know it makes some legacy code more verbose, but the flexibility and simplicity is a conscious trade-off.

## Animations

Many animations are provided, but you can also create your own animations.

### Rotate

   ```
   Row(
  mainAxisSize: MainAxisSize.min,
  children: <Widget>[
    const SizedBox(width: 20.0, height: 100.0),
    const Text(
      'Be',
      style: TextStyle(fontSize: 43.0),
    ),
    const SizedBox(width: 20.0, height: 100.0),
    DefaultTextStyle(
      style: const TextStyle(
        fontSize: 40.0,
        fontFamily: 'Horizon',
      ),
      child: AnimatedTextKit(
        animatedTexts: [
          RotateAnimatedText('AWESOME'),
          RotateAnimatedText('OPTIMISTIC'),
          RotateAnimatedText('DIFFERENT'),
        ],
        onTap: () {
          print("Tap Event");
        },
      ),
    ),
  ],
);
```

Note: You can override transition height by setting the value of parameter transitionHeight for RotateAnimatedTextKit class.

### Fade

   ```
   return SizedBox(
  width: 250.0,
  child: DefaultTextStyle(
    style: const TextStyle(
      fontSize: 32.0,
      fontWeight: FontWeight.bold,
    ),
    child: AnimatedTextKit(
      animatedTexts: [
        FadeAnimatedText('do IT!'),
        FadeAnimatedText('do it RIGHT!!'),
        FadeAnimatedText('do it RIGHT NOW!!!'),
      ],
      onTap: () {
        print("Tap Event");
      },
    ),
  ),
);
   ```

### Typer

   ```
   return SizedBox(
  width: 250.0,
  child: DefaultTextStyle(
    style: const TextStyle(
      fontSize: 30.0,
      fontFamily: 'Bobbers',
    ),
    child: AnimatedTextKit(
      animatedTexts: [
        TyperAnimatedText('It is not enough to do your best,'),
        TyperAnimatedText('you must know what to do,'),
        TyperAnimatedText('and then do your best'),
        TyperAnimatedText('- W.Edwards Deming'),
      ],
      onTap: () {
        print("Tap Event");
      },
    ),
  ),
);
   ```


