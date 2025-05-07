# Voice Translator App

A basic voice translation application created with MIT App Inventor. It enables translation between English and French using speech input and output.

## Overview

This app provides a user-friendly interface for quick voice translation. Speak your phrase, and the app will translate and speak it back in the selected target language.

## Features

* **Voice Input:** Uses the device's speech recognition to capture spoken phrases.
* **English to French Translation:** Translate spoken English into French.
* **French to English Translation:** Translate spoken French into English.
* **Text-to-Speech Output:** Speaks the translated text aloud.
* **Displays Text:** Shows both the recognized original text and the translated text.

## Requirements

To build and run this application, you will need:

* An account on the MIT App Inventor website (appinventor.mit.edu).
* A computer with internet access.
* An Android device or emulator with a working microphone and internet connection for speech recognition and translation services.
* A **Yandex Translate API Key**. You can obtain one from the Yandex Cloud console (some usage may require payment depending on volume). You will need to add this key to the `YandexTranslate` component in App Inventor.

## Building the Application

Refer to the `step-to-step_guide.md` file for detailed instructions on how to recreate this application in MIT App Inventor.

## How to Use

1.  Launch the application on your Android device.
2.  Ensure you have an active internet connection.
3.  Tap the **English to French** button if you want to speak English and get French translation.
4.  Tap the **French to English** button if you want to speak French and get English translation.
5.  When prompted by the speech recognition listener, speak the phrase you want to translate clearly into the microphone.
6.  The recognized text will appear, followed by the translated text, which will also be spoken aloud.

## Credits

This application was built using the MIT App Inventor platform (appinventor.mit.edu) and utilizes the Yandex Translate API, Speech Recognition, and Text-to-Speech components.
